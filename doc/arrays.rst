

Working with arrays
===================

In your code you will need arrays to hold data (floating point numbers,
integers, characters, logicals) and you need to allocate space for those.  You
can allocate this space statically or dynamically.  Below we will discuss
example of both.


Static arrays
-------------

Static allocation means that the array size is known at compile time. For
instance in the example below we specify an array where we can store 1000*3
double precision floating point coordinates for up to 1000 atoms:

.. code-block:: fortran

   integer, parameter :: MAX_NUM_ATOMS = 1000

   real(8) :: coordinates(MAX_NUM_ATOMS, 3)

There are at least two disadvantages of statically allocated arrays: First, if
we need to resize them, we need to recompile the code which is inconvenient.
The other disadvantage is that static arrays are always allocated, even if we
end up not using them during the calculation.

Therefore the recommendation is to not use static allocations unless the array
is small and known to "never" change.

It is also a bad idea to introduce static arrays "temporarily" for testing
because you are too lazy to allocate and deallocate dynamically.  Very often
you will forget to change them later and they remain "temporary" for years or
decades until someday somebody writes out of arrays bounds and all bets are
off.


Dynamic arrays
--------------

Write me ...


Passing arrays to functions/subroutines
---------------------------------------

Write me ...


Friendly advice
---------------

If you write a code that allocates possibly a lot of memory late in the (long)
calculation, plan your code for a dry-run option so that the code can be run
traversing all allocations and deallocations without doing actual computations.
This is very helpful in avoiding the otherwise extremely annoying experience of
a calculation that crashes after two weeks of runtime because the code fails to
allocate an array late in the calculation.
