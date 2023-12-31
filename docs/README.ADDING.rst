Adding New Source Files to Hercules
===================================

Adding new files to the Hercules emulator project would certainly seem
like a simple straightforward thing. Unfortunately there are some
additional details which far too many Hercules developers frequently
overlook *(including myself sometimes!)*.

This document attempts to describe these oversights and should be used
as internal reference documentation that all Hercules developers should
review on occasion.

Adding new files to the repository is only the *first* (and most
important) step in the process. But the other steps, which too many
developers tend to forget about, are just as important.

Those additional steps (which many developers tend to overlook) fall
into two major areas:

1. *Updating the* **build files** *so that the new files are included in
   the build process.*
2. *Adding the files to the* **Visual Studio project files** *(user
   interface).*

Repository
----------

Adding a new source file to our git repository is a simple and
straightforward process so I won’t bother going into any detail. If you
don’t already know how to add new files to the git repository, then you
probably have no business being a Hercules developer!

Build Files
-----------

After adding the new source file to the repository you need to update
one of the ``Makefile.am`` files (non-Windows) **and** one or more of
the ``msvc.makefile.includes`` files (Windows). Which makefile or
msvc.makefile.includes file you need to update depends on what type of
file you are adding.

The easiest way to determine which Makefile (or msvc.makefile.includes
file) that you need to update *(as well as the change you need to make
to it)*, is to simply do a ``grep`` for the filename of a *similar* file
that already exists in Hercules.

For example, if you are adding a new .c source file pertaining to
instruction emulation ``hengine.dll``, you might do a grep for
``general1`` *(without the extension!)* and make your change to all of
the same files in the same manner. If you are adding a new html file,
you might do your grep for ``hercconf``, etc.

*Linux:*
^^^^^^^^

If you are adding a new **``.c`` source file**, you need to update the
project’s main (primary) ``Makefile.am`` file in the root directory of
the repository:

-  ```Makefile.am`` <https://github.com/SDL-Hercules-390/hyperion/blob/master/Makefile.am>`__

If you are adding a new **runtest** test file to the ``tests``
subdirectory, you need to update the ``Makefile.am`` file in *that*
directory:

-  ```tests/Makefile.am`` <https://github.com/SDL-Hercules-390/hyperion/blob/master/tests/Makefile.am>`__

If you are adding a new ``.html`` documentation **webpage** to the
``html`` subdirectory, then you need to add your new file to *that*
subdirectory’s ``Makefile.am`` file:

-  ```html/Makefile.am`` <https://github.com/SDL-Hercules-390/hyperion/blob/master/html/Makefile.am>`__

*MSVC:*
^^^^^^^

If you are adding a new ``.c`` source file, you first need to determine
which “module” (DLL) that file is a part of. The collection of object
code pertaining to each of our modules (shared libraries or DLLs) is
controlled via the ``OBJ_CODE.msvc``, ``MODULES.msvc`` and
``MOD_RULES2.msvc`` makefile fragments in the ``msvc.makefile.includes``
directory:

-  ```OBJ_CODE.msvc`` <https://github.com/SDL-Hercules-390/hyperion/blob/master/msvc.makefile.includes/OBJ_CODE.msvc>`__
   (maybe, depending on what type of file you are adding)
-  ```MODULES.msvc`` <https://github.com/SDL-Hercules-390/hyperion/blob/master/msvc.makefile.includes/MODULES.msvc>`__
   (maybe, depending on what type of file you are adding)
-  ```MOD_RULES2.msvc`` <https://github.com/SDL-Hercules-390/hyperion/blob/master/msvc.makefile.includes/MOD_RULES2.msvc>`__
   (maybe, depending on what type of file you are adding)

If you are adding a new **runtest** test file to the ``tests``
subdirectory, you do *not* need to update any build file. You only need
to update one of the **Visual Studio project files** as discussed in the
“Visual Studio” section just below.

If you are adding a new ``.html`` documentation **webpage** to the
``html`` subdirectory, then once again, you *only* need to update one of
the **Visual Studio project files** as discussed in the next section
immediately below.

Visual Studio
-------------

As part of the process of adding a new file to Hercules, it is also
important to add that file to the following Visual Studio project files:

-  `Hercules_VS2008.vcproj <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2008.vcproj>`__

-  `Hercules_VS2015.vcxproj <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2015.vcxproj>`__

-  `Hercules_VS2015.vcxproj.filters <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2015.vcxproj.filters>`__

-  `Hercules_VS2017.vcxproj <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2017.vcxproj>`__

-  `Hercules_VS2017.vcxproj.filters <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2017.vcxproj.filters>`__

-  `Hercules_VS2019.vcxproj <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2019.vcxproj>`__

-  `Hercules_VS2019.vcxproj.filters <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2019.vcxproj.filters>`__

-  `Hercules_VS2022.vcxproj <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2022.vcxproj>`__

-  `Hercules_VS2022.vcxproj.filters <https://github.com/SDL-Hercules-390/hyperion/blob/master/Hercules_VS2022.vcxproj.filters>`__

The change that you need to make to each of the above files should
hopefully be obvious, and you should follow the same format that already
exists.

   **NOTE:** *  The changes that need to be made to the above Visual
   Studio 2015, 2017, 2019 and 2022 project files are all exactly
   identical. The easiest way to make your changes is to first change
   the two 2015 files first, and then simply copy those exact same
   changes over into the same 2017, 2019 and 2022 files. Please also
   note that the VS2008 project file is an exception to the rule. Its
   format is completely different, so be sure to make your changes in
   the right place.*

The easiest way to determine how to make your change is to simply search
for the filename of a *similar* file that already exists in Hercules.

Example commits:
~~~~~~~~~~~~~~~~

Here are some sample commits so you can see the changes that need to be
made when adding a new file to Hercules:

-  `New “cckdmap”
   utility <https://github.com/SDL-Hercules-390/hyperion/commit/ae0313a371fd5c7189dcba4939700a0d3692e007>`__

-  `Add TCPIP (X’75’) instruction; see README.TCPIP for
   details. <https://github.com/SDL-Hercules-390/hyperion/commit/7714b835ebcc8ceeb0a8bd473f7694d2e427b1f8>`__

But again, the perhaps easiest way is to simple make the same changes
that were made when a *similar* type file was added in the past.

--------------

Please let me know if there is anything I can do to explain the above
process more clearly for you.

I know it seems somewhat complicated, but it’s not.

**You basically just need to remember to:**

-  Add the file to the correct autoconf ``Makefile.am`` file
-  Add the file to the correct MSVC makefile fragment
   *(``OBJ_CODE.msvc`` etc)*
-  Add the file to all of the Visual Studio project files
   (``Hercules_VS2008.vcproj``, ``Hercules_VS2015.vcxproj``,
   ``Hercules_VS2015.vcxproj.filters``, etc)

And the easiest way to do that is, like I said, by doing it just like
others have done it previously. Do a grep for a similar type file and
review the files and the changes that were made when that file was
added.

**“Fish”** *(David B. Trout)     October 5, 2010*
