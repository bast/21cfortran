

Working with arrays
===================

In your code you will need arrays to hold data (floating point numbers,
integers, characters, logicals) and you need to allocate space for those. You
can allocate this space statically or dynamically. Below we will discuss
examples of both.


Static arrays
-------------

Static allocation means that the array size is known at compile time. For
instance in the example below we specify an array where we can store 1000*3
double precision floating point coordinates for up to 1000 atoms:

.. code-block:: fortran

   integer, parameter :: MAX_NUM_ATOMS = 1000

   real(8) :: coordinates(MAX_NUM_ATOMS, 3)

Other examples:

.. code-block:: fortran

   ! a static array holding 200 floating points
   real(8) :: array1(200)

   ! a static 2-dimensional array holding 81 integers
   integer :: array2(9, 9)

   ! a static array holding 401 logicals indexed from 0 to 400
   logical :: array3(0:400)

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

.. code-block:: fortran

   ! you:    we will never need more than 10000 here
   ! future: wrong, one day you will
   integer :: myarray(10000)


Dynamic arrays
--------------

Write me ...


Custom dynamic allocation schemes
---------------------------------

In the good old Fortran 77 days dynamic allocation was not possible but it was
nevertheless needed. One way out was to statically or dynamically (using
another language) allocate a big block of memory and to subdivide it and to
"allocate" and "deallocate" manually during the calculation.  Such a custom
dynamic allocation is present in a number of legacy codes.  One problem of this
is that out of bounds bugs can be difficult to detect because they cannot be
detected by the compiler or tools designed to detect such bugs. This is because
for the compiler and the tools such out of bounds access bugs can appear as
regular in-bounds reads and writes.  The other disadvantage is that code that
uses custom dynamic allocation schemes becomes less modular (because the big
chunk of memory is often carried around through many levels of routine calls)
and less portable (because you cannot reuse a routine which depends on a custom
solution that another code may not provide).


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
