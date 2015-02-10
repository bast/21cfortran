

Getting started
===============


Before you start
----------------

Fortran is a compiled language so we will need a compiler.
It will be useful to install GFortran and CMake.

On Debian-like distributions::

  $ sudo apt-get install gfortran cmake

GFortran and CMake are free. It is no problem to use a Fortran compiler
provided by another vendor instead of GFortran (Intel, PGI, Cray, XL).


Compiling a hello world program
-------------------------------

The classic hello world program to get us started:

.. literalinclude:: code/hello.F90
    :language: fortran

Copy-paste it to your editor and save it as ``hello.F90``.
You can compile it with (example GFortran)::

  $ gfortran hello.F90 -o hello.x

Then run the code with::

  $ ./hello.x

  hello world

Exciting times. Now we can begin.


Building portable Fortran code with CMake
-----------------------------------------

Write me ...


Fixed or free form
------------------

Write me ...
