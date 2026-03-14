<a id="SECTION000142000000000000000"></a>
## Automatic determination of Kerker's factor

<a id="886"></a>
If the keyword 'scf.Kerker.factor' is not given in your input file,
OpenMX Ver. 3.9 automatically estimates a proper value of Kerker's factor $\alpha $ by the following
equation:

| $\displaystyle \alpha = \frac{0.5}{\vert {\bf b}_{\rm min}\vert^2}\left(4\frac{Dq}{Aq}+1.0\right)$ |  |  |  |
| --- | --- | --- | --- |

with

| $\displaystyle Aq = \frac{1}{3}\left(\vert {\bf b}_1 \vert^2 + \vert {\bf b}_2 \vert^2 + \vert {\bf b}_3 \vert^2\right),$ |  |  |  |
| --- | --- | --- | --- |

| $\displaystyle Dq = \frac{1}{3}\sum_{i<j}\left\vert\vert {\bf b}_i \vert^2- \vert {\bf b}_j \vert^2\right\vert,$ |  |  |  |
| --- | --- | --- | --- |

where
${\bf b}_i (i=1,2,3)$ is a reciprocal vector, and
${\bf b}_{\rm min}$ is the smallest vector
among {**b**}. The equation takes account of the dependency of $\alpha $ on the size and anisotropy
of the system. From a series of numerical calculations it is found that the estimated value works
well in most cases.

---
