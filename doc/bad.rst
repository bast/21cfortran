

Bad practices
=============


Common blocks
-------------


implicit.h
----------

Whenever you see this:

.. code-block:: fortran

   #include "implicit.h"

or this:

.. code-block:: fortran

   implicit real(8) (a-h,o-z)

or any ``implicit`` statement that is not ``implicit none``, then run. With the
implicit statement you can infer the type (in the above case ``real(8)`` from
the first character of a variable or parameter.  In other words ``implicit
real(8) (a-h,o-z)`` means that we do not have to explicitly declare
variables/parameters and all variables/parameters starting with i-n will be
implicitly integers and all others implicitly double precision numbers.

This may sound like a good idea but is one of the greatest evils of the
language. The reason for this is that you will very easily introduce typos
which are difficult to detect.  This may lead to undefined behavior.  The other
problem is that ``implicit`` in combination with common blocks leaves you
completely in the blind about where variables are defined and which common
blocks are used or unused.

Avoid the ``implicit`` statement at any cost and always use ``implicit none``
which forces you to declare all variables.  Generations of programmers and your
future self will thank you.


SIXLTR variables
----------------

In the good old days six character variables were the norm and a limitation.
Today they are not.

Try to guess the meaning of the following variables:

.. code-block:: fortran

   NWNABA, DIPDER, TSTINP, FCKDDR, GSQUAD, MSDIDI, SUPMAT

Exactly. We have no idea. In the 21st century there is no reason
to not use self-explaining variable names. The six character limitation
is long gone.


Fixed-form
----------


Large static arrays
-------------------


Long subroutines
----------------

If a subroutine does not fit into your laptop terminal screen, then it is too
long. Divide and conquer.


Functional programming features
-------------------------------


Elemental functions
-------------------


Pure functions
--------------


