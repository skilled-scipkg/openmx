<a id="SECTION000690000000000000000"></a>
# Calling OpenMX as library or computational engine

Note: I (Ozaki) had misunderstood how MPI_Comm_spawn works
at the moment of the release of OpenMX Ver. 3.9 (Dec. 3, 2019).
So, a part of the desctription below is not correct.
Please use the capability at your own risk.

OpenMX can be utilized as library or computational engine from your program using MPI_Comm_spawn.
You may mpirun your program and may want to call OpenMX with different input files from the program
in different MPI groups at the same time. In such cases the functionality may be useful.
Let us illustrate the functionality by introducing 'example_mpi_spawn.c' which is stored in the directory 'source'.
The code 'example_mpi_spawn.c' can be compiled as

```text

  % make example_mpi_spawn
```

Then, you may obtain the executable file of 'example_mpi_spawn' in the directory 'work'.
Please move to the directory 'work' and perform as

```text

  % mpirun -np 24 -machinefile machine0 --oversubscribe ./example_mpi_spawn
```

Setting the number of MPI processes, the machinefile, and the parameters may be changed depending on
your computational environment. In some enviroment, you may need to attach '-oversubscribe' as option for mpirun
in order to access the full physical cores on your machine.
In the test calculation, the MPI processes of 24 are divided to three groups, each of which
consists of 8 MPI processes, and in each group having 8 MPI processes OpenMX runs with an input file: 'Methane.dat', 'C60.dat',
or 'Fe2.dat'. Starting from the example code as shown below, you may be able to develop a host program which calls OpenMX
as child process. In the code 'Make_Comm_Worlds' creates three MPI communicaition groups, and 'MPI_Comm_spawn' calls OpenMX
with one of the input files as argument. Note that OpenMX called by 'MPI_Comm_spawn' will not display most of standard output
but write them in 'System.Name.std' to avoid appearence of too much information as standard output
in such a case that OpenMX is multiply called by 'MPI_Comm_spawn' at the same time.

```text

/**********************************************************************                                                                   
                                                                                                                                          
  example_mpi_spawn.c:                                                                                                                    
                                                                                                                                          
  An example of calling OpenMX as library by MPI_Comm_spawn, where                                                                        
  a given MPI processes are grouped to three new MPI communication                                                                        
  groups and OpenMX runs with an input file: 'Methane.dat', 'C60.dat',                                                                
  or 'Fe2.dat' in each MPI group.                                                                                                        
                                                                                                                                          
  Log of example_mpi_spawn.c:                                                                                                             
                                                                                                                                          
     25/Sep./2019  Released by Taisuke Ozaki                                                                                              
                                                                                                                                          
***********************************************************************/

#include "mpi.h"
#include <stdio.h>
#include <stdlib.h>

void Make_Comm_Worlds(
   MPI_Comm MPI_Curret_Comm_WD,
   int myid0,
   int numprocs0,
   int Num_Comm_World,
   int *myworld1,
   MPI_Comm *MPI_CommWD,     /* size: Num_Comm_World */
   int *NPROCS1_ID,          /* size: numprocs0 */
   int *Comm_World1,         /* size: numprocs0 */
   int *NPROCS1_WD,          /* size: Num_Comm_World */
   int *Comm_World_StartID   /* size: Num_Comm_World */
   );

int main(int argc, char *argv[])
{
  int i,j;
  int numprocs0,myid0,ID0;
  int numprocs1,myid1;
  int num;
  int Num_Comm_World1;
  int myworld1;
  int *NPROCS1_ID,*NPROCS1_WD;
  int *Comm_World1;
  int *Comm_World_StartID;
  MPI_Comm *MPI_CommWD;
  MPI_Comm comm;
  MPI_Comm *intercomm;

  MPI_Init(&argc,&argv);
  MPI_Comm_size(MPI_COMM_WORLD,&numprocs0);
  MPI_Comm_rank(MPI_COMM_WORLD,&myid0);

  /* set Num_Comm_World1 */

  Num_Comm_World1 = 3;

  /* allocation of arrays */

  NPROCS1_ID = (int*)malloc(sizeof(int)*numprocs0);
  Comm_World1 = (int*)malloc(sizeof(int)*numprocs0);
  NPROCS1_WD = (int*)malloc(sizeof(int)*Num_Comm_World1);
  Comm_World_StartID = (int*)malloc(sizeof(int)*Num_Comm_World1);
  MPI_CommWD = (MPI_Comm*)malloc(sizeof(MPI_Comm)*Num_Comm_World1);
  intercomm = (MPI_Comm*)malloc(sizeof(MPI_Comm)*Num_Comm_World1);

  /* Make_Comm_Worlds */

  Make_Comm_Worlds(MPI_COMM_WORLD, myid0, numprocs0, Num_Comm_World1, 
                   &myworld1, MPI_CommWD,
                   NPROCS1_ID, Comm_World1, NPROCS1_WD, Comm_World_StartID);

  /* get numprocs1 and myid1 */

  MPI_Comm_size(MPI_CommWD[myworld1],&numprocs1);
  MPI_Comm_rank(MPI_CommWD[myworld1],&myid1);

  /*                                                                                                                                      
  printf("numprocs0=%2d myid0=%2d myworld1=%2d numprocs1=%2d myid1=%2d\n",                                                                
          numprocs0,myid0,myworld1,numprocs1,myid1);                                                                                      
  */

  /* MPI_Comm_spawn */

  char command[] = "./openmx";
  char **argvin;
  char *inputfiles[] = { "Methane.dat", "C60.dat", "Fe2.dat" };

  argvin=(char **)malloc(2 * sizeof(char *));
  argvin[0] = inputfiles[myworld1];
  argvin[1] = NULL;

  MPI_Comm_spawn( command, argvin, numprocs1, MPI_INFO_NULL, 0,
                  MPI_CommWD[myworld1], &intercomm[myworld1], MPI_ERRCODES_IGNORE );

  /* MPI_Barrier */

  MPI_Barrier(MPI_COMM_WORLD);

  /* freeing of arrays */

  free(NPROCS1_ID);
  free(Comm_World1);
  free(NPROCS1_WD);
  free(Comm_World_StartID);
  free(MPI_CommWD);
  free(intercomm);

  /* MPI_Finalize() */

  fflush(stdout);
  MPI_Finalize();

  return 0;
}

void Make_Comm_Worlds(
   MPI_Comm MPI_Curret_Comm_WD,
   int myid0,
   int numprocs0,
   int Num_Comm_World,
   int *myworld1,
   MPI_Comm *MPI_CommWD,     /* size: Num_Comm_World */
   int *NPROCS1_ID,          /* size: numprocs0 */
   int *Comm_World1,         /* size: numprocs0 */
   int *NPROCS1_WD,          /* size: Num_Comm_World */
   int *Comm_World_StartID   /* size: Num_Comm_World */
   )
{
  int i,j,is,ie;
  int ID0;
  int numprocs1,myid1;
  int num;
  double avnum;
  int *new_ranks;
  MPI_Group new_group,old_group;

.....

}
```
