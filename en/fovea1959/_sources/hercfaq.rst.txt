Frequently-Asked Questions
==========================

What is Hercules?
^^^^^^^^^^^^^^^^^

Hercules is a software implementation of the System/370, ESA/390 and
z/Architecture mainframe architectures. Hercules runs under Windows and
Linux, as well as under various other Unix or Unix-like systems on Intel
Pentium and other hardware platforms including Alpha, Sparc, and Mac.

So what exactly does that mean?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It means that your PC can emulate an IBM mainframe processor. The
mainframe can range from a System/360 to a z10 - running in "S/370"
mode, "ESA/390" mode, or "z/Architecture" mode.

Hercules executes S/370, ESA/390, and z/Architecture instructions and
channel programs. It emulates mainframe I/O devices by using PC devices.
For example, 3390 DASD devices are emulated by large files on your hard
disk, and local 3270 screens are emulated by tn3270 sessions. (Note: Not
all 370 and 390 features have been implemented in Hercules. See the list
of particulars later in this document. Also, certain non-standard
models, 360/20s, and the 360/67 virtual memory mode are not emulated.)

Hercules implements only the raw S/370, ESA/390, and z/Architecture
instruction set; it does not provide any operating system facilities.
This means that you need to provide an operating system or standalone
program which Hercules can load from an emulated disk or tape device.
You will have to write the operating system or standalone program
yourself, unless you can manage to obtain a license from IBM to run one
of their operating systems on your PC, or use IBM programs and operating
systems which have been placed in the public domain.

Is it functional enough to run production work?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Hercules has never claimed to be a production-capable system. It was
always meant to be a system programmer's toy. Having said that, it's now
become good enough to run a wide range of software without problems, and
there are reports that it has been used to run production work in some
parts of the world.

What are the licensing restrictions for Hercules?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Hercules is a copyright work which has been made generally available,
subject to the terms of the `Q Public License <herclic.html>`__. In
essence this allows free use and distribution of the program for
personal and commercial use. You may not distribute modified copies of
the program, but you may distribute your own patches along with the
program, provided that you also grant the maintainer permission to
include those patches in future versions of the program. You may not
copy any portion of the source code for use in any other program.

Hercules is *not*, repeat, *not* GPL software! The GNU General Public
License is a Unix/Linux software licensing agreement, which we, the
authors, will not participate in. We believe that the QPL, which has
been certified as compliant with the `Open Source
Definition <http://www.opensource.org>`__, provides the benefits and
protections of open source for both users and developers, without the
political baggage that has come to be associated with the GPL.

--------------

Can it run z/OS, z/VM, z/VSE?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes. Hercules is a software implementation of z/Architecture, and so it
is capable of running z/OS, z/VM, and z/VSE. Hercules also implements
ESA/390 (including SIE) and so it can run OS/390, VM/ESA, and VSE/ESA,
as well as older versions of these operating systems such as MVS/ESA,
MVS/XA, VM/SP, VSE/SP, etc.

**But** (and this is a big but), these operating systems are all IBM
Licensed Program Products, whose conditions of use generally restrict
their usage to specific IBM machine serial numbers. So you cannot just
copy these systems from work and run them on your PC.

What operating systems can I run legally?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most 3rd party operating systems like Linux/390, z/Linux and TELPAR are
covered under their own *free* license and can therefore run under
Hercules without any legal problems.

*OS/360* (PCP, MFT and MVT) is in the public domain, as far as we know.
The status of OSes for which IBM did not charge a license fee is
somewhat murky; these include *MVS* 3.8, *VM/370* release 6, and
*DOS/VS* release 34.

The legal status outside the USA, where something like public domain or
software without copyright doesn't exist, is "copyrighted software
provided at no charge". It is a known fact that vendors like *Amdahl*,
*Hitachi*, *Nixdorf* and others modified those operating systems, and
distributed them as their own OS for their own hardware, without asking
IBM for permission. But law had been changed over that time, so its not
clear if the same legal status applies in **your** country right now.

Rick Fochtman managed to obtain a letter from IBM that he is allowed to
distribute OS/360. Try to ask your salesdroid for a similar letter for
VM/370, MVS 3.8j or DOS/VS next time they want to sell you a major
upgrade.

OS/390, z/OS, and other ESA or z/Architecture operating systems are
definitely licensed to a particular machine. Therefore, in practice you
cannot run any classic ESA or z/Architecture operating system on your PC
unless you can obtain a license from IBM allowing you to do so. It is
believed that there are, however, four ways you could run z/OS, z/VM,
z/VSE, OS/390, VM/ESA, or VSE/ESA under Hercules using currently
available licenses:

#. Running under Linux on the Pentium processor of a P/390 which is
   licensed to run the OS.
#. Running under Linux/390 on a mainframe which is licensed to run the
   OS.
#. Running under the terms of a disaster recovery provision of the OS
   license (but I really don't recommend depending on Hercules to be
   your disaster recovery solution!).
#. Using the IBM OS/390 or z/OS DemoPkg, which is available only to IBM
   employees and IBM Business Partners.

What other programs will run under Hercules?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Any program which uses the S/370, ESA/390, or z/Architecture instruction
set, as implemented in Hercules. Some special utilities in the form of
standalone programs are known to run well. I can particularly recommend
Jan Jaeger's excellent standalone editor (ZZSA) which is included in the
Hercules distribution, or it can be downloaded from
http://www.cbttape.org/~jjaeger; I use it regularly to look at DASD
while debugging an OS installation, which is just what it's designed to
do. Note: ZZSA runs in ESA/390 mode. See Jan Jaeger's website for more
information and special logon procedures.

Where can I obtain OS/360 ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Rick Fochtman's OS/360 archive CD is now obtainable by download from
   https://cbttape.org/os360.htm.

#. At the cbttape site, you can download the OS/360 Y2K Starter package
   from ftp://cbttape.org/pub/OS360/OS360RICK1.zip, which contains a
   full featured MVT system on a 3330 image with some minimal
   documentation. The configuration is that of a 370/158 with 4
   megabytes of main storage, running OS/MVT Release 21.0. The same site
   also offers a MVTDBL volume and a *Builder* package for those who
   like to participate in OS/360 nucleus hacking.

   Please note that the previously mentioned cbttape OS/360 download
   link is an "ftp://" protocol link, and some web browsers (most
   notably Google Chrome) no longer support the "ftp://" protocol. If
   such is the case for you, you will need to use a proper FTP client to
   download the mentioned OS/360 .zip file.

#. Jay Maynard's "IBM Public Domain Software Collection" at
   http://www.ibiblio.org/jmaynard/ contains copies of the OS/360
   Release 21.8 distribution tapes.

Where can I obtain MVS 3.8 ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Original MVS 3.8 distribution as it was first used came from

-  ftp://ftp.cbttape.org/pub/cbttape/mvs38/

who advise using the mirrors at

-  ftp://ftp.ox.ac.uk/pub/linux/mvs38j/
-  http://source.rfc822.org/pub/mirror/hercules/mvs38j/
-  ftp://source.rfc822.org/pub/mirror/hercules/mvs38j/

Several people have generated a functional MVS system from this archive:

-  `Jay Moseley, CCP <http://www.jaymoseley.com/>`__
-  `Volker Bandke from BSP GmbH <http://www.bsp-gmbh.com/hercules/>`__
-  `Wolfgang Schäfer from Schäfernet <http://www.schaefernet.de/hercules/>`__

Where can I obtain VM/370 ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The VM/370 page at `cbttape.org <http://www.cbttape.org/vm6.htm>`__
contains download links for the Andy Norrie VM 4-pack system and the Bob
Abeles VM/370 R6 distribution.

Where can I obtain DOS/VS ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^

I've put the DOS/VS r34 install tape on my site. It'll expand to a 21 MB
AWSTAPE file, dosrel34.aws. You need the *Coverletter* to install it.
Read the relevant postings of the Hercules mailing list first, as the
install process is quite obscure.

You can grab those files at :

-  http://www.hercules-390.org/dosrel34.zip
-  http://www.hercules-390.org/dosrel34coverletter.pdf
-  http://open360.copyleft.de/DOS34/Installation.html

Where can I obtain Linux/390 ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The best starting point for information about Linux for S/390 and Linux
for zSeries is http://www.linuxvm.org/

Where can I find documentation?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The `Creating Hercules DASD <hercload.html>`__ document describes
various methods of creating and loading virtual DASD volumes.

I've produced a document describing how to build an OS/360 system on
Hercules, called "OS/360 on Hercules". It can be found at

-  `http://www.conmicro.com/hercos360/hercos360/ <http://www.conmicro.com/hercos360/>`__.

This will build an MVT system without TCAM/TSO, but with two 3270
consoles. You will need Malcolm Beattie's "Guide to Using 3270 Consoles
and Terminals for Hercules" with this MVT version.

-  http://www.clueful.co.uk/mbeattie/hercules/3270.html

The N.U.D.E guides can be found at :

-  http://www.kiyoinc.com/hercdoc.html.

| IBM provides only current documentation, ...
| but many things haven't changed since 1964 :

-  `IBM BookManager(r) BookServer
   Library <http://www.s390.ibm.com/bookmgr-cgi/bookmgr.cmd/LIBRARY>`__

--------------

What PC hardware do I need to run Hercules?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Classic IBM operating systems (OS/360, MVS 3.8, VM/370) are very light
by today's standards and will run satisfactorily on a 300Mhz Pentium
with as little as 32MB RAM.

Anything more up-to-date, such as Linux/390 or OS/390, requires much
more processing power. Hercules is CPU intensive, so you will want to
use the fastest processor you can get. A 2GHz Pentium, preferably with
hyperthreading, will probably provide acceptable performance for a light
workload. If you can afford a multiprocessor system, so much the better.
Hercules makes extensive use of multi-threading to overlap I/O with CPU
activity, and to dispatch multiple emulated CPU's in parallel.

For the latest 64-bit operating systems such as zLinux and z/OS, be
aware that there is a performance penalty when Hercules emulates
z/Architecture on a 32-bit processor such as the Pentium. If you are
serious about running 64-bit then you will probably want to build
Hercules for a 64-bit processor such as Alpha (DEC/Compaq/HP), or AMD64
(AMD Opteron, Athlon-64, Turion 64) together with a 64-bit version of
Linux or PPC (Power Mac G5) with OS X.

Hercules does not depend on the Pentium architecture. I've built and run
it successfully on a 500 MHz Alpha 21164, and others have run it on
SPARC and S/390 (!) Linux systems. One guy has even run OS/360 under
Hercules under Linux/390 under Hercules under Linux/390 under VM/ESA!
The prize for the world's smallest mainframe probably goes to Ivan
Warren, who claims to have run VM/370 under Hercules on an iPAQ 5450
handheld PDA.

You should provide enough RAM to accommodate your S/390 real storage
(main storage plus expanded storage) in addition to the normal
requirements of your PC's operating system. For maximum throughput, you
should set your main and expanded storage sizes high enough to eliminate
S/390 paging. S/390 storage is allocated out of your PC's virtual
storage.

You also need enough hard disk space to accommodate the emulated DASD. A
virtual "3330 model 1" disk drive will need about 100 megabytes of space
for emulation (a 3330-11 will need about 200 megabytes). A 3380 "single
density" model will need about 650MB, a 3390 model 2 needs about 2GB,
and a 3390 model 3 needs about 3GB. If you use the `compressed CKD DASD
feature <cckddasd.html>`__, these sizes will shrink dramatically,
usually to about 20 to 30 percent of the original size.

What sort of MIPS rate can I expect?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Thanks to the cumulative work of many individuals, including Valery
Pogonchenko, Juergen Dobrinski, Albert Louw, Gabor Hoffer, Jan Jaeger,
Paul Leisy, Clem Clarke, and Greg Smith, the performance of Hercules
today is vastly better than it was 5 years ago.

Even on a Celeron 300 you should see an execution speed of 1 to 2 MIPS,
which is enough to run OS/360 (MFT or MVT) or MVS 3.8 with a response
time better than that of a 3033 from the 1970's. It's also fast enough
to run VSE/ESA with an acceptable response time. On a more recent system
with a 2GHz Pentium processor, you may see the system peak at around 30
MIPS which is enough to run Linux/390 or z/OS with a light workload.

Performance on server class machines is now fairly respectable. For
example, on a dual-core Intel Xeon with hyperthreading (4 CPUs) running
at 3.46GHz, you might expect to see a sustained MIPS rate of 40 to 60
MIPS. A dual-processor quad-core Mac Pro (8 cores, 3 GHz) will sustain
over 150 MIPS. For anyone who is prepared to spend a considerable amount
of money on their Hercules system, there are reports that a sustained
300+ MIPS has been achieved on an Intel Core i7 processor running at
3.75GHz using all four cores plus hyperthreading (8 CPUs).

Typical I/O rates of around 50 EXCP/second are reported on average
hardware, with rates over 500/second achievable with hardware RAID.

What PC software do I need to run Hercules?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following software platforms are supported:

- Linux (kernel 2.4 or later)
- Windows Vista or greater (Windows 7 preferred)
- Mac OS X 10.3 or later
- Solaris 2.9 or later (Sparc or Intel)
- FreeBSD

You will also need tn3270 client software for the virtual 3270 console.
The tn3270 client can run on the same machine as Hercules, or on any
Unix or Windows box with a TCP/IP connection to the Hercules machine.

The supported and recommended tn3270 clients for Hercules are:

**x3270 for Unix**
   x3270 is included with most Linux distributions, or you can download
   it from http://x3270.bgp.nu/
**Vista tn3270 for Windows**
   Vista tn3270 can be obtained from
   `www.tombrennansoftware.com <http://www.tombrennansoftware.com>`__.
   The very modest license fee charged for this excellent 3270 emulator
   helps to support an independent software developer.
**Brown University tn3270 for Macintosh**
   Brown University tn3270 is freely available. You can download it from
   http://www.brown.edu/Facilities/CIS/tn3270/. There is one setting
   that must be changed to use this program with some operating systems,
   especially MVS 3.8: Open a connection to Hercules, but before IPLing
   the system, go to the Session->Features menu and set "Change embedded
   nulls to blanks" to "No". Click on "OK". Now, click on File->Save
   default settings... to make the setting permanent.

Other tn3270 clients, such as QWS3270, IBM Personal Communications,
Attachmate Extra, or Dynacomm Elite should also work in most cases, but
be aware that some tn3270 clients have bugs which make them unusable as
OS/360 or MVS consoles.

What software do I need to build Hercules on Linux and Unix?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To build Hercules for Linux and other Unix-like environments (including
Cygwin under Windows), you need to use the `gcc <http://gcc.gnu.org>`__
compiler, version 3.x or above. You will also need a full set of GNU
development tools, including recent versions of autoconf, automake,
flex, gawk, gcc, grep, m4, make, perl, and sed. Refer to the
util/bldlvlck file in the Hercules distribution for details.

What software do I need to build Hercules on Windows?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To build Hercules for the Windows native environment (without Cygwin),
you need to use the Microsoft C/C++ compiler (MSVC) version 15.x or
later (i.e. Visual Studio 2008 or greater). The 32-bit compiler and SDK
were packaged as Microsoft Visual C++ 2008 Express Edition at one point
in the past, but unfortunately Microsoft no longer offers it for
download from their web site.

Fish's `"Software Development
Laboratories" <http://www.softdevlabs.com>`__ web site however, has a
`"Hercules Windows Build
Instructions" <http://www.softdevlabs.com/hercules-msvc-build.html>`__
web page that contains download links that are still working should you
wish to use Visual Studio 2008 Express Edition.

The good news is Microsoft's latest offering of their `Visual
Studio <https://www.visualstudio.com/downloads/>`__ product comes with a
free "**Community Edition**" which *should* be able to successfully
build Hercules.

Which version of Visual Studio (Microsoft Visual C++) you use to build
Hercules with is largely unimportant as long as it works. More recent
versions may or may not provide better performance and may or may not
successfully build Hercules. The only way to know is to try.

Can Hercules be ported to run on other platforms?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

With the introduction of autotools, we do make efforts to ensure
Hercules builds and run on several different operating system platforms
(mostly Linux, Windows, MAC, Solaris, and FreeBSD right now), but we of
course simply cannot guarantee that it will run on every operating
system platform out there.

If you want to make Hercules run on AS/400, OS/2, or whatever, then by
all means go ahead. I welcome reports of any bugs or problems you find,
but I probably won't fix problems if it means introducing
platform-specific code, and I will not be able to test new releases
against other platforms. Folks who have gotten it compiled on the BSDs
report that the hardest part is removing the Linux-specific tape
support.

The Hercules code is not intended to be specific to Intel hardware, so
if you find any issues or faults related to running on other hardware
(SPARC, Alpha, PPC, ...) under Linux, then I'm likely to be receptive to
fixing that sort of problem. Issues related to Unix variants are less
likely to be fixed however.

--------------

How can I create a virtual DASD volume?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The `Creating Hercules DASD <hercload.html>`__ document describes
various methods of creating and loading virtual DASD volumes.

Can I read a tape which was created on a mainframe?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes, indirectly. The mainframe tape must be converted to AWSTAPE format
and then downloaded to your PC. The **tapeconv.jcl** file in the
Hercules directory contains a sample program which you can run under
OS/390 on your mainframe system. It reads a file from tape and converts
it to AWSTAPE format. Download the AWSTAPE file to your PC (making sure
to choose *binary* format for the download), and then add the downloaded
filename to the Hercules configuration file as a virtual tape device.
You will then be able to read the tape file from the virtual tape drive
located on your PC.

*Note: the "tapeconv" program will not correctly process input tapes
whose block size exceeds 32760!* One symptom of this may be the message
" ``ADRY011E I/O ERROR - DEVICE NOT ATTACHED.0000,NA,00...00,0000"``
when attempting to restore from tape originally created using the
default DF/DSS block size. The solution is to recreate the dump tape
with DCB=BLKSIZE=32760.

Can I attach a PC tape drive to Hercules?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes. Hercules can read and write tapes on SCSI drives. I have tested
this with 4mm DAT, QIC-1000, and 9-track drives.

Can I process mainframe tapes with Hercules?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes. It is possible to obtain 9-track open reel drives and 3480-type
cartridge drives which attach to the SCSI bus. Hercules makes these
appear to the operating system as channel-attached 3420 or 3480 devices,
making it possible to read and write real mainframe tapes.

Can I create Assembler programs without a mainframe?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes. If you want to write Assembler (BAL) programs to run on Hercules,
but you don't have access to a mainframe, then there are two interesting
products which you can run on your PC to assemble programs:

The "Tachyon 390 Cross Assembler" ( http://www.tachyonsoft.com/tachyon )
   With this assembler you can produce S/390-compatible object decks
   using your Linux or Windows PC. A high degree of HLASM compatibility,
   coupled with the ability to perform complex assemblies at lightning
   speed, make this a product which is well worth looking at. I have
   tried this assembler and it is truly amazing.
The "Dignus Systems/C Compiler" ( `http://www.dignus.com <http://www.dignus.com/>`__ )
   This is a C compiler which runs under Windows or Linux and generates
   mainframe assembler code which you can then assemble using the
   Tachyon assembler.

Sam Golob wrote a fascinating review of these two products in the
September 1999 issue of `NaSPA <http://www.naspa.com>`__ Technical
Support magazine.

--------------

What architectural features are implemented?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following features of **ESA/390** *have* been implemented:

-  24-bit and 31-bit addressing
-  370-XA Channel Subsystem
-  Access-List-Controlled Protection
-  Access Register Mode
-  Address-Limit Checking
-  BAKR/PC/PR/PT instructions
-  Binary Floating-Point instructions
-  Branch-Relative instructions
-  Branch and Save
-  Branch and Set Authority
-  Broadcasted Purging
-  Cancel I/O Facility
-  Channel Indirect Data Addressing
-  Channel Program Suspend/Resume
-  Checksum instruction
-  Commercial Instruction Set
-  Compare and Form Codeword and Update Tree instructions
-  Compare and Move Extended instructions
-  Compare Until Substring Equal
-  Compression
-  Concurrent Sense
-  Conditional Swapping
-  DAT-Enhancement Facility 1
-  Decimal Instructions
-  Dual Address Space
-  Dynamic Address Translation
-  Dynamic Reconfiguration
-  ETF2-Enhancement Facility
-  Expanded Storage
-  Extended TOD clock
-  Extended Translation Facility 1
-  Extended-Translation Facility 2
-  Fast Synchronous Data Mover Facility
-  Floating-Point-Support Extensions
-  Guest PER enhancement
-  Halfword-Immediate instructions
-  Hexadecimal Floating-Point Instructions
-  HFP-Multiply-and-Add/Subtract Facility
-  Home Space Mode
-  Incorrect-Length-Indication Suppression
-  Interlocked-Access Facility 2
-  Interpretive Execution (SIE)
-  Key-Controlled Protection
-  Linkage Stack
-  Logical Partition (LPAR) Support
-  Long-Displacement Facility
-  Low-Address Protection
-  LURA/STURA instructions
-  Message-Security-Assist Extension 1 Support
-  Message-Security-Assist Extension 2 Support
-  Message-Security Assist
-  MVCIN Move Inverse Instruction Support
-  Move Page (Facility 2)
-  Multiple Controlled Data Space (VM dataspaces)
-  MVCS/MVCP/MVCK/MVCSK/MVCDK instructions
-  MVS assists
-  N3 Instructions are installed
-  Operational Extensions: Console Integration
-  Page Protection
-  Perform Locked Operation
-  Private Space
-  Program Controlled Interruption (PCI)
-  Program Event Recording
-  Service-call-logical-processor (SCLP) facility
-  Set Address Space Control Fast
-  Square Root
-  Storage-Protection Override
-  Storage Key assist
-  Store-Facility-List-Extended Facility
-  Store System Information
-  String instructions
-  Subspace Group
-  Suppression on Protection with Virtual-Address enhancement
-  TB/TPROT instructions
-  TOD Clock, Clock Comparator, and CPU Timer
-  z/Architecture architectural mode is installed

The following features of **z/Architecture** *have* been implemented:

-  Access-Exception-Fetch/Store-Indication Facility
-  ASN-and-LX-Reuse Facility
-  BEAR-Enhancement Facility
-  CMPSC-Enhancement Facility
-  Compare-and-Swap-and-Store Facility 1
-  Compare-and-Swap-and-Store Facility 2
-  Conditional-Emergency-Signal and Sense-Running-Status Facility
-  Conditional-SSKE Facility
-  Configuration-Topology Facility
-  Constrained-Transactional-Execution Facility
-  DAT-Enhancement Facility 1
-  DAT-Enhancement Facility 2
-  Decimal-Floating-Point Facility
-  Decimal-Floating-Point Facility Has High Performance
-  Decimal-Floating-Point-Rounding Facility
-  Decimal-Floating-Point-Zoned-Conversion Facility
-  Decimal-Floating-Point-Packed-Conversion Facility
-  Distinct-Operands Facility
-  Enhanced-DAT Facility 1
-  Enhanced-Monitor Facility
-  ETF2-Enhancement Facility
-  ETF3-Enhancement Facility
-  Execute-Extensions Facility
-  Execution-Hint Facility
-  Extended-Immediate Facility
-  Extended-Translation Facility 1
-  Extended-Translation Facility 2
-  Extended-Translation Facility 3
-  Extract-CPU-Time Facility
-  Fast-BCR-Serialization Facility
-  Floating-Point-Extension Facility
-  Floating-Point-Support-Enhancement Facility
-  Floating-Point-Support-Sign-Handling Facility
-  FPR-GR-Transfer Facility
-  General-Instructions-Extension Facility
-  HFP-Multiply-and-Add/Subtract Facility
-  HFP-Unnormalized-Extensions Facility
-  High-Word Facility
-  IEEE-Exception-Simulation Facility
-  Integrated 3270 (SYSG) Console
-  Insert-Reference-Bits-Multiple Facility
-  Interlocked-Access Facility 1
-  Interlocked-Access Facility 2
-  IPTE-Range Facility
-  List-Directed Initial Program Load
-  Load-and-Trap Facility
-  Load-and-Zero-Rightmost-Byte Facility
-  Load-Program-Parameter Facility
-  Load/Store-on-Condition Facility 1
-  Load/Store-on-Condition Facility 2
-  Local-TLB-Clearing Facility
-  Logical Partition (LPAR) Support
-  Long-Displacement Facility
-  Long-Displacement Facility Has High Performance
-  Message-Security Assist
-  Message-Security-Assist Extension 1 Support
-  Message-Security-Assist Extension 2 Support
-  Message-Security-Assist Extension 3
-  Message-Security-Assist Extension 4
-  Miscellaneous-Instruction-Extensions Facility 1
-  Miscellaneous-Instruction-Extensions Facility 2
-  Miscellaneous-Instruction-Extensions Facility 3
-  Modified CCW Indirect Data Addressing (MIDAW) Facility
-  Move-with-Optional-Specifications Facility
-  Multiple-Subchannel-Set Facility
-  MVCIN Move Inverse Instruction Support
-  N3 Instructions are installed
-  Nonquiescing Key-Setting Facility
-  Parsing-Enhancement Facility
-  PER-3 Facility
-  PER Storage-Key-Alteration Facility
-  PER Zero-Address-Detection Facility
-  PFPO (Perform Floating-Point Operation) Facility
-  Population-Count Facility
-  Processor-Assist Facility
-  QDIO-Assist Support
-  QDIO Enhanced Buffer-State Management Support
-  QDIO Thin-Interrupts Support
-  QDIO Time-Delayed-Dispatching Support
-  Reset-Reference-Bits-Multiple Facility
-  Sense-Running-Status Facility
-  Store-Clock-Fast Facility
-  Store-Facility-List-Extended Facility
-  Store-Hypervisor-Information Facility
-  SVS Set Vector Summary Instruction Support
-  TOD-Clock-Steering Facility
-  Transactional-Execution Facility
-  z/Architecture architectural mode is installed
-  z/Architecture architectural mode is active

The following features of **z/Architecture** have *not* yet been
implemented:

-  CPU-Measurement Counter Facility
-  CPU-Measurement Sampling Facility
-  CZAM Facility (Configuration-z/Architecture-Architectural-Mode)
-  DEFLATE-Conversion Facility
-  Enhanced-DAT Facility 2
-  Enhanced-Sort Facility
-  Entropy-Encoding-Compression Facility
-  ESA/390-compatibility-Mode Facility
-  Extended-I/O-Measurement-Block Facility
-  Extended-I/O-Measurement-Word Facility
-  FCX-Bidirectional-Data-Transfer Facility
-  Fibre-Channel-Extensions (FCX) Facility
-  Guarded-Storage Facility
-  IDTE selective clearing when region-table invalidated
-  IDTE selective clearing when segment-table invalidated
-  Instruction-Execution-Protection Facility
-  Integrated ASCII (SYSA) Console
-  Message-Security-Assist Extension 5
-  Message-Security-Assist Extension 6
-  Message-Security-Assist Extension 7
-  Message-Security-Assist Extension 8
-  Message-Security-Assist Extension 9
-  Move-Page-and-Set-Key Facility
-  Multiple-Epoch Facility
-  Multithreading Facility
-  Neural-Network-Processing-Assist Facility
-  Order-Preserving-Compression Facility
-  Processor-Activity-Instrumentation Facility
-  Processor-Activity-Instrumentation Extension 1 Facility
-  Program-Directed IPL (*proper* Diagnose x'308' support)
-  Reset-DAT-Protection Facility
-  Restore-Subchannel Facility
-  Secure-Execution-Unpack Facility
-  Server-Time-Protocol Facility
-  Side-Effect-Access Facility
-  Storage-Key-Removal Facility
-  Store-CPU-Counter-Multiple Facility
-  Test-Pending-External-Interruption Facility
-  Ultravisor-Call Facility
-  Vector-Enhancements Facility 1
-  Vector-Enhancements Facility 2
-  Vector Packed-Decimal Facility
-  Vector-Packed-Decimal-Enhancement Facility 1
-  Vector-Packed-Decimal-Enhancement Facility 2
-  Warning-Track-Interruption Facility
-  z/Architecture Vector Facility

The following **standard** feature has *not* yet been implemented:

-  Clear I/O (full functionality for S/370)

The following **optional** features have been *partially* implemented:

-  Channel-Subsystem Call
-  VM/370 Assists (most but not all)

The following features are *not* yet implemented, either due to lack of
documentation, limited host system capability, or lack of supporting
hardware:

-  Asynchronous Data Mover Facility
-  Asynchronous Pageout Facility
-  Coupling Links
-  ESCON
-  Extended Sorting
-  External Time Reference (Sysplex Timer)
-  FICON
-  ICRF (Cryptography)
-  MIF (Multiple Image Facility)
-  Operational Extensions: Automatic Reconfiguration, Storage
   Reconfiguration, SCP-initiated Reset, Processor Availability
-  PR/SM
-  Program-Controlled re-IPL

Hercules is compliant with IBM's ALS-1, ALS-2 and ALS-3 architectural
level sets to the degree necessary to run all OS/390 versions through
2.10 and known versions of z/OS in both ARCHLVL 1 and ARCHLVL 2 mode,
and Linux and z/VM and z/VSE in both ESA/390 and z/Architecture mode.

--------------

Who are the Herculeans?
^^^^^^^^^^^^^^^^^^^^^^^

The following people are among those who have contributed to this
project, either as coders or as testers or both:

- `Roger Bowler <http://www.rogerbowler.fr/hercules.htm>`__ (original author)
- `Jay Maynard <http://en.wikipedia.org/wiki/Jay_Maynard>`__
- `Jan Jaeger <http://www.cbttape.org/~jjaeger>`__
- Butch Anton
- `Volker Bandke <http://www.bsp-gmbh.com/>`__
- David Barth
- `Malcolm Beattie <http://www.clueful.co.uk/mbeattie/>`__
- Mario Bezzi
- Florian Bilek
- Gordon Bonorchis
- Mike Cairns
- Chris Cheney
- `Marcin Cieslak <http://www.isoc.org.pl/user/3>`__
- `Clem Clarke <http://au.linkedin.com/in/clementclarke>`__
- `Vic Cross <http://veejoe.com.au/vic/index.htm>`__
- `Jacob Dekel <http://www.mvsdasd.org/about.html>`__
- Guy Desbiens
- Jacques Dilbert
- Juergen Dobrinski
- Fritz Elfert
- Neale Ferguson
- Tomas Fott
- Mike Frysinger
- Martin Gasparovic
- Mark Gaubatz
- Steve Gay
- Paolo Giacobbis
- Peter Glanzmann
- Roland Goetschi
- Graham Goodwin
- Paul Gorlinsky
- Harold Grovesteen
- John P. Hartmann
- Glen Herrmannsfeldt
- Brandon Hill
- Laddie Hanus
- Robert Hodge
- Gabor Hoffer
- Dan Horak
- Peter J. Jansen
- Soren Jorvang
- `Willem Konynenberg <http://konynenberg.com/>`__
- John Kozak
- Nobumichi Kozawa
- Peter Kuschnerus
- Paul Leisy
- Kevin Leonard
- `Bill Lewis <https://github.com/wrljet/>`__
- Albert Louw
- Peter Macdonald
- Lutz Mader
- Tomas Masek
- Rick McKelvy
- John McKown
- Dave Morton
- Christophe Nillon
- Mike Noel
- Andy Norrie
- Steve Orso
- Dutch Owen
- `Max H. Parke <http://www.lightlink.com/mhp/3705/>`__
- Gerd Petermann
- Reed H. Petty
- Jim Pierson
- Richard Pinion
- `Tim Pinkawa <http://www.timpinkawa.net/hercules>`__
- `Pasi Pirhonen <http://upi.iki.fi/>`__
- Valery Pogonchenko
- Bob Polmanter
- Andy Polyakov
- `Frans Pop <http://www.debian.org/News/2010/20100831>`__
- `Wolfhard Reimer <http://www.xing.com/profile/Wolfhard_Reimer>`__
- Emerson Santos
- `Jeff Savit <http://blogs.oracle.com/jsavit/>`__
- `Axel Schwarzer <http://de.linkedin.com/pub/axel-schwarzer/2/739/655>`__
- Paul Scott
- Daniel Seagraves
- Victor Shkamerda
- Ian Shorter
- `Greg Smith <http://www.linuxvm.org/community/gsmith.html>`__
- Enrico Sorichetti
- John Summerfield
- `Peter Sylvester <http://www.edelweb.fr/EdelStuff/Prospectus/sylvester.html>`__
- Mark Szlaga
- Adam Thornton
- Adrian Trenkwalder
- `"Fish" (David B. Trout) <http://www.softdevlabs.com>`__
- Ronen Tzur
- Bernard van der Helm
- Ard van der Leeuw
- Kris Van Hees
- Adam Vandenberg
- Kees Verruijt
- `Giuseppe Vitillaro <http://www.vitillaro.org/>`__
- `Ivan Warren <http://www.ivansoftware.com/>`__
- James Wekel
- `Juergen Winkelmann <https://www1.ethz.ch/id/people/allid_list/juergen>`__
- Bob Wood
- Ian Worthington
- Rod Zazubek
- Bjoern A. Zeeb
- `Matt Zimmerman <http://en.wikipedia.org/wiki/Matt_Zimmerman_(technologist)>`__

And thanks for support and encouragement from:

- Tim Alpaerts
- Bertus Bekker
- Giorgio de Nunzio
- `Rick Fochtman <http://articles.petoskeynews.com/2012-07-27/memorial-service_32894245>`__
- Alex Friis
- Sam Golob
- `Achim Haag <http://home.arcor.de/achim.haag//haagjobe.htm>`__
- `Cory Hamasaki <http://www.legacy.com/obituaries/washingtonpost/obituary.aspx?pid=143636886>`__
- Tony Harminc
- `Richard Higson <http://www.linuxvm.org/community/rhigson.html>`__
- `Jim Keohane <http://groups.yahoo.com/group/hercules-390/message/50662>`__
- Sam Knutson
- `Mike Ross <http://www.corestore.org/>`__
- Daniel Rudin
- `Rich Smrcina <http://www.linuxvm.org/community/rsmrcina.html>`__
- Henk Stegeman
- Mark S. Waterbury
 
If anyone feels they have been unfairly omitted from either of these
lists, please let us know.

--------------

Where can I obtain technical support?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please see our :ref:`techsupp` web page.
