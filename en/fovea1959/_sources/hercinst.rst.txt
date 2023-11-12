Building and Installing
=======================

Building from source - Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Download the `source code .ZIP
   file <https://github.com/sdl-hercules-390/hyperion/archive/master.zip>`__
   from Github, or even better, `clone the
   repository <https://github.com/sdl-hercules-390/hyperion>`__\ **.**
   (Note: building from the source code .zip file is *strongly
   discouraged*. Instead, it is *highly recommended* that you clone the
   git repository and build from that instead.)

   ::

          git clone  https://github.com/SDL-Hercules-390/hyperion.git  <directory-name>

   | **Note:** *By downloading the .zip file (or cloning the repostiory)
     you agree to the terms of the* `Q Public
     Licence <herclic.html>`__\ *.*

#. Hercules for Windows is built using the Microsoft Visual C (MSVC)
   compiler. Refer to file
   `README.WIN64 <https://github.com/sdl-hercules-390/hyperion/blob/master/readme/README.WIN64.md>`__
   for details. Note: Fish also has updated VS2015/VS2017 instructions
   on his `MSVC Hercules Build
   Instructions <http://www.softdevlabs.com/hercules-vs2015-build.html>`__
   web page.

#. Be sure to read the `Release
   Notes <https://sdl-hercules-390.github.io/html/hercrnot.html>`__ with
   every new release, which contains important late-breaking information
   about each new release.

Windows pre-built binaries:
~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Download one of the `pre-built
   binaries <http://www.softdevlabs.com/hyperion.html#prebuilt>`__ from
   `SoftDevLabs <http://www.softdevlabs.com>`__.
#. (Optional) You might also want to install Fish's `Hercules GUI for
   Windows <http://www.softdevlabs.com/hercgui>`__.

Building from source - Mac OS X
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Important - Not Recently Tested. May be obsolete.**

#. Install **Xcode** from the `App
   Store <http://itunes.apple.com/app/xcode/id497799835>`__.
#. Install **Homebrew** using the procedure described at http://brew.sh/
#. Use these commands to install pre-requisite software:
   ``brew install gnu-sed``
#. Proceed with *Building from source - Linux and macOS* below.

Building from source - Linux and macOS (High Sierra and newer)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Important: Please read everything before doing anything. Don't be
bashful about asking for help.**

| **Important:** You must use at least version 6.2.0 of the gcc compiler
  and associated glibc2 library. Refer to the `Hercules Frequently-Asked
  Questions <hercfaq.html#3.04>`__ page for required compiler and other
  software levels.

#. Download the `source code .ZIP
   file <https://github.com/sdl-hercules-390/hyperion/archive/master.zip>`__
   from Github, or even better, `clone the
   repository <https://github.com/sdl-hercules-390/hyperion>`__\ **.**
   (Note: building from the source code .zip file is *strongly
   discouraged*. Instead, it is *highly recommended* that you clone the
   git repository and build from that instead. This allows the exact
   version of the source code to be determined, which is very helpful
   should a problem need to be diagnosed.)

   ::

          git clone  https://github.com/SDL-Hercules-390/hyperion.git  <directory-name>

   | **Note:** *By downloading the .zip file (or cloning the repostiory)
     you agree to the terms of the* `Q Public
     Licence <herclic.html>`__\ *.*

#. Be sure to read the `Release
   Notes <https://sdl-hercules-390.github.io/html/hercrnot.html>`__ with
   every new release, which contains important late-breaking information
   about each new release.

#. Install the required packages appropriate for your system.

   -  Debian / Ubuntu / Mint / etc

      | ``sudo apt-get -y install git wget time``
      | ``sudo apt-get -y install build-essential cmake flex gawk m4 autoconf automake libtool-bin libltdl-dev``
      | ``sudo apt-get -y install libbz2-dev zlib1g-dev``
      | ``sudo apt-get -y install libcap2-bin``

      *Note: For Regina REXX to run the included tests:*

      ``sudo apt-get -y install libregina3-dev``

   -  Elbrus Linux (similar to Debian)
     
      | ``sudo apt-get -y install git wget time``
      | ``sudo apt-get -y install build-essential cmake flex gawk m4 autoconf automake libtool``
      | ``sudo apt-get -y install bzip2 zlib``
      | ``sudo apt-get -y install libcap``

   -  Arch / Manjaro

      | ``sudo pacman -S --needed --noconfirm git wget``
      | ``sudo pacman -S --needed --noconfirm base-devel make cmake flex gawk m4 autoconf automake``
      | ``sudo pacman -S --needed --noconfirm bzip2 zlib``

   -  Fedora

      | ``sudo dnf -y install git wget``
      | ``sudo dnf -y install gcc make cmake flex gawk m4 autoconf automake libtool-ltdl-devel``
      | ``sudo dnf -y install bzip2-devel zlib-devel``

   -  CentOS / AlmaLinux / Rocky Linux 8+ / Red Hat RHEL 9

      | ``sudo yum -y install git wget time``
      | ``sudo yum -y install gcc make cmake flex gawk m4 autoconf automake libtool-ltdl-devel``
      | ``sudo yum -y install bzip2-devel zlib-devel``

      *Note: On CentOS 9, the following command is required* **before**
      *installing the packages:*

      ``sudo yum config-manager --set-enabled crb``

      | *Note: On Red Hat RHEL 9, the following command is required*
        **before** *installing the packages:*
      | (refer
        `here <https://www.redhat.com/sysadmin/install-epel-linux>`__
        for more information)

      ``sudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms``

   -  CentOS 7

      | ``sudo yum -y install git wget``
      | ``sudo yum -y install gcc make flex gawk m4 autoconf automake libtool-ltdl-devel``
      | ``sudo yum -y install bzip2-devel zlib-devel``

      *Note: On CentOS 7, there is no package for CMAKE 3.x, it must be
      built from source.*

   -  openSUSE (15.1+)

      | ``sudo zypper install -y git``
      | ``sudo zypper install -y -t pattern devel_basis autoconf automake cmake flex gawk m4 libtool``
      | ``sudo zypper install -y -t pattern bzip2 libz1 zlib-devel``
      | ``sudo zypper install -y libcap-progs``

   -  Apple Darwin (macOS High Sierra, Mojave, Catalina, Big Sur, etc.)
      with Homebrew

      | ``xcode-select --install``
      | ``/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"``

      | brew install wget gsed
      | brew install cmake autoconf automake libtool

      *Note: So configure/make will find ltdl.h and libltdl:*

      | ``export CFLAGS="$CFLAGS -I$(find $(brew --cellar libtool) -type d -name "include" | sort -n | tail -n 1)"``
      | ``export LDFLAGS="$LDFLAGS -L$(find $(brew --cellar libtool) -type d -name "lib" | sort -n | tail -n 1)"``

      *And include these options to configure:*

      | ``--disable-getoptwrapper``
      | ``--without-included-ltdl``

   -  Apple Darwin (macOS Big Sur) with MacPorts

      Information on installing MacPorts may be found
      `here <https://guide.macports.org/chunked/installing.macports.html>`__.

      | ``sudo port install wget gsed``
      | ``sudo port install cmake autoconf automake libtool``

      *Note: So configure/make will find ltdl.h and libltdl:*

      ``export CFLAGS=-I/opt/local/include LDFLAGS=-L/opt/local/lib``

   -  FreeBSD

      | ``sudo pkg install -y bash git wget``
      | ``sudo pkg install -y gmake autoconf automake cmake flex gawk m4 libltdl``
      | ``sudo pkg install -y bzip2``

      *Note: Bash is required by parts of the build apparatus.*

      *Note: So configure/make will find ltdl.h and libltdl:*

      ``export CFLAGS=-I/usr/local/include LDFLAGS=-L/usr/local/lib``

   -  OpenBSD is not currently supported

#. Verify you have all of the correct versions of the more important
   packages installed:

   ``./util/bldlvlck``

   Please note that SDL Hyperion comes pre-delivered with an already
   pre-generated ``./configure`` script, so doing a ``./autogen.sh`` is
   not necessary and is in fact now strongly discouraged. An autogen
   would only be necessary if you were to manually make some changes to
   the Hercules default ``Makefile.am`` and/or ``configure.ac`` files
   (which under normal circumstances you should never need to do).

#. Download and build all **External Packages**, if needed:
   Hercules links with several pre-built "External Package" static link
   libraries that have been pre-built for you and come distributed with
   Hercules (i.e. they are a part of the Hercules repository).
   Currently all of the external package static link libraries for the
   Intel x86 (32-bit) and x64 (64-bit) architectures for both Windows
   and Linux for both normal optimized Release builds as well as
   unoptimized Debug builds are already provided as part of the
   distribution. Thus to build Hercules you should not need to do
   anything special. Simply build Hercules just as you normally would.
   In some unusual situations however, you MIGHT need to rebuild ALL
   existing external packages for your particular system. Exactly what
   those situations are and what causes them to occur is unclear, but
   one thing is certain: it will never hurt to build all of the external
   packages anyway just to be safe.
   If you wish to modify or debug any of the external packages
   themselves (or need to build a non-Intel x86/x64 architecture build
   of Hercules however, such as arm, mips, ppc, sparc, xscale, etc),
   then you will need to manually build each of the external packages
   first in order to create the static link libraries that Hercules will
   need to link with, before you can then build Hercules.
   For more detailed External Package build information please refer to
   the
   `README.EXTPKG <https://github.com/sdl-hercules-390/hyperion/blob/master/readme/README.EXTPKG.md>`__
   document.

#. Configure Hercules for your system:

   ``./configure``

   By default, the configure script will attempt to guess appropriate
   compiler optimization flags for your system. If its guesses turn out
   to be wrong, you can either specify your own optimization flags with
   ``--enable-optimization=FLAGS`` (*preferred*) or else as a last
   resort disable all optimization by passing the
   ``--disable-optimization`` option instead (**not** *recommended*).
   For additional configuration options, run:
   ``./configure --help=short``.

   For Apple macOS, these additional configure switches are recommended:

   | ``--disable-getoptwrapper``
   | ``--without-included-ltdl``

#. Build the executables:

   ``make``

#. (Optional) Install the programs:

   | ``sudo make install``

   This is an optional step because once Hercules is built, you should
   be able to run Hercules directly from the Hercules build directory
   itself without needing to install anything beforehand. But if you
   want to officially install it somewhere, then by all means do so.

   It should be mentioned however, that if you do decide to run directly
   out of the build directory, you should first set the 'cap_sys_nice'
   capabilities on the Hercules executables and start Hercules as root.
   This will allow Hercules to properly set the priorities of its
   internal threads:

   ::

      sudo setcap 'cap_sys_nice=eip' ./hercules
      sudo setcap 'cap_sys_nice=eip' ./herclin
      sudo setcap 'cap_net_admin+ep' ./hercifc

   You *don't* need to do this if you do ``sudo make install`` however
   since the makefile does this for you. You only need to do this when
   you decide to *not* install the results of the build and run directly
   out of the build directory instead.
