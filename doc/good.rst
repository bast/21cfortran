

Good practices
==============


Version control
---------------


implicit none
-------------


Implementation hiding
---------------------


Module names match file names
-----------------------------

Consider you have a module called ``some_functionality``:

.. code-block:: fortran

   module some_functionality

   contains

      ...

   end module

In this case it is good practice to also call the file either
some_functionality.f90 or some_functionality.F90 (for the suffix see next
section).

The reason is that if you see a compilation or linking problem in a specific
module you know immediately where to find it.  It is frustrating to work with
projects where the module names do not match file names.

For the same reason it is good practice to use only one module per file instead
of packing several modules into one file. The latter is possible but confusing.
Be an organized programmer and keep modules separate.


File suffix
-----------


Explicitly list all data and methods used from a module
-------------------------------------------------------

Citing from the Zen of Python:
"Namespaces are one honking great idea -- let's do more of those!"

Namespaces are one honking great idea in Fortran, too.

Therefore the explicit use statement

.. code-block:: fortran

   use some_module, only: function1, subroutine1, subroutine2

is better than the general statement

.. code-block:: fortran

   use some_module

for three reasons: 1) the explicit use statement with "only" pollutes the
namespace less, 2) the reader of this file can find out from which module
functions, subroutines, and variables are imported, and 3) it makes it easy to
identify symbols which are not used after a refactoring round.


Good comments
-------------


Object-oriented programming features
------------------------------------


Private and public methods and data
-----------------------------------
