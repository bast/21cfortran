

Working with arrays
===================

Sooner or later in your code you will need arrays to hold data (floating point
numbers, integers, characters, logicals) and you need to allocate space for
those. You can allocate this space statically or dynamically. Below we will
discuss examples of both.


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

   ! a static array holding 200 double precision numbers
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
decades until someday somebody writes out of array bounds and this is then
no fun.

.. code-block:: fortran

   ! you:    we will "never" need more than 10000 here
   ! future: wrong, one day you will
   integer :: myarray(10000)


Dynamic arrays
--------------

Dynamic is typically better than static, with one exception: if statically
allocating program runs out of memory, it crashes immediately.  A dynamically
allocating program can run ouf of memory late which can be frustrating (see
below).

This is how it works:

.. code-block:: fortran

   ! allocatable 1-dimensional double precision array
   real(8), allocatable :: myarray1(:)

   ! allocatable 2-dimensional integer array
   integer, allocatable :: myarray2(:, :)

   ! here we allocate both
   allocate(myarray1(1000))
   allocate(myarray2(500, 500))

   ! in between we do some work ...

   ! here we deallocate both
   deallocate(myarray1)
   deallocate(myarray2)


Custom dynamic allocation schemes
---------------------------------

In the good old Fortran 77 days dynamic allocation was not possible but it was
nevertheless needed. One way out was to statically or dynamically (using
another language) allocate a big block of memory at the beginning of the
calculation and to manage the memory block during the calculation by
subdividing it and to "allocate" and "deallocate" with custom functions. Such a
custom dynamic allocation is present in a number of legacy codes. One problem
with this is that out of bounds memory access bugs can be difficult to detect
because they cannot be detected by the compiler or tools typically designed to
detect such bugs. This is because for the compiler and the tools such out of
bounds access bugs can appear as regular in-bounds reads and writes because
they all can happen within the one big block of memory. The other disadvantage
is that code that uses custom dynamic allocation schemes becomes less modular
(because the big chunk of memory is often carried around through many levels of
routine calls) and less portable (because you cannot reuse a routine which
depends on a custom solution that another code may not provide).


Passing arrays to functions/subroutines
---------------------------------------

Write me ...


Friendly advice
---------------

If you write a code that allocates possibly a lot of memory late in a possibly
long calculation, plan your code for a memory dry-run option so that the code
can be run traversing all allocations and deallocations without doing actual
computations.  This is very helpful in avoiding the otherwise extremely
annoying experience of seeing a calculation crash after two weeks of runtime
because the code fails to allocate an array late in the calculation.
