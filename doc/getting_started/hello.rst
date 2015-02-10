

Compiling a hello world program
===============================

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
