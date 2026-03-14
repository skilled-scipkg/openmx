<a id="SECTION000508000000000000000"></a>
## Other tips

It would be better to provide atomic coordinates for bulk
systems in Ang or AU instead of FRAC, since the atomic position
tends to be translated in FRAC to keep the fractional coordinate within 0 to 1.
The translation tends to generate a confusing movie in the visualization
of the result.

Only three routines are added to implement the NEB functionality.
They are 'neb.c', 'neb_run.c', and 'neb_check.c'.
The main routine is 'neb.c'. It may be easy to implement related
methods in 'neb.c'.

---
