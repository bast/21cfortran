

Static arrays
=============


Static allocation means that the array size
is known at compile time. For instance in the example
below we specify an array where we can store 1000*3
double precision floating point coordinates for up
to 1000 atoms:

.. code-block:: fortran

   integer, parameter :: MAX_NUM_ATOMS = 1000

   real(8) :: coordinates(MAX_NUM_ATOMS, 3)
