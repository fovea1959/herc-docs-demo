Creating DASD
=============

Using pre-built DASD images
---------------------------

IBM distributes pre-built OS/390 and z/OS systems on two different
CD-ROM packages:

   **The OS/390 and z/OS Application Development CD (ADCD)**

   available only to members of IBM PartnerWorld for Developers, and

   **The OS/390 and z/OS DemoPkg**

   available only to IBM employees and qualified IBM Business Partners.

Both of these packages contain pre-built DASD image files which simply
need to be unzipped onto your hard drive. The unzipped images can be
directly read by Hercules. Be aware, however, that you cannot use the
ADCD images because the PartnerWorld scheme requires you to purchase or
lease an IBM approved machine in order to obtain the ADCD, and the
software on the ADCD is licensed for use only on the machine that it was
shipped with. See IBM's "`Enterprise server
solutions <http://www.ibm.com/servers/enable/site/zinfo/adcd.html>`__"
web page for more information.

If you want Hercules to be an approved machine so that you can use the
ADCD, then I suggest you lobby **IBM Developer Relations** at the
address given on their web page. Different rules apply to the OS/390 and
z/OS DemoPkg CD which is available only to IBM employees and business
partners. If you fall into this category then you probably know what the
rules are. I don't.  :-(

--------------

Creating, formatting, and loading DASD volumes
----------------------------------------------

--------------

Creating an empty DASD volume
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The dasdinit or dasdinit64 utility must first be run from the Unix shell
prompt to create a file containing an empty DASD volume. If you are
going to be creating `compressed dasd images <cckddasd.html>`__, it is
recommended that you use the new *dasdinit64* utility as it is able to
create `CCKD64 format <hercrnot.html#CCKD64>`__ dasd images which are
highly advantageous over the old 32-bit CCKD images that plain dasdinit
creates.

| The format of the command is:

::

       Usage: dasdinit64 [-options] filename devtype[-model] [volser] [size]
       Builds an empty dasd image file
       options:

         -z        build compressed dasd image file using zlib
         -bz2      build compressed dasd image file using bzip2
         -0        build compressed dasd image file with no compression
         -lfs      build a large (uncompressed) dasd file (if supported)
         -a        build dasd image file that includes alternate cylinders
                   (option ignored if size is manually specified)
         -r        build 'raw' dasd image file
                   (no VOL1 or IPL track)
         -b        make wait PSW in IPL1 record a BC-mode PSW
                   (default is EC-mode PSW)
         -m        enable wait PSW in IPL1 record for machine checks
                   (default is disabled for machine checks)
         -linux    null track images will look like Linux dasdfmt'ed images
                   (3390 device type only)

         filename  name of dasd image file to be created
         devtype   CKD: 2305, 2311, 2314, 3330, 3340, 3350, 3375, 3380, 3390, 9345
                   FBA: 0671, 3310, 3370, 9313, 9332, 9335, 9336

         model     device model (implies size) (opt)
         volser    volume serial number (1-6 characters)
                   (specified only if '-r' option not used)
         size      number of CKD cylinders or 512-byte FBA sectors
                   (required if model not specified else optional)

| 
| Note that the defaults for the wait PSW written to the IPL1 record
  have changed from earlier releases of Hercules. In the past, the wait
  PSW created by dasdinit was a BC-mode PSW enabled for machine check
  interrupts. The current default for the wait PSW is EC-mode, disabled
  for machine checks. To obtain the earlier behavior, run dasdinit with
  the "-b" and "-m" flags.

The current list of device types and models supported is:

::


                 CKD DEVICES

                                  alt
           devtype-model    cyls  cyls

           2311              [*]
           2311-1            200   2

           2314              [*]
           2314-1            200   3

           3330              [*]
           3330-1            404   7
           3330-2            808   7
           3330-11           808   7

           3340              [*]
           3340-1            348   1
           3340-35           348   1
           3340-2            696   2
           3340-70           696   2

           3350              [*]
           3350-1            555   5

           3375              [*]
           3375-1            959   1

           3380              [*]
           3380-1            885   1
           3380-A            885   1
           3380-B            885   1
           3380-D            885   1
           3380-J            885   1
           3380-2           1770   2
           3380-E           1770   2
           3380-3           2655   3
           3380-K           2655   3
           EMC3380K+        3339   3
           EMC3380K++       3993   3

           3390              [*]
           3390-1           1113   1
           3390-2           2226   1
           3390-3           3339   1
           3390-9          10017   3
           3390-27         32760   3
           3390-54         65520   3

           9345              [*]
           9345-1           1440   0
           9345-2           2156   0


                FBA DEVICES

           devtype-model  blocks

           3310              [*]
           3310-1         125664

           3370              [*]
           3370-Al        558000
           3370-B1        558000
           3370-A2        712752
           3370-B2        712752

           9313              [*]
           9313-1         246240

           9332              [*]
           9332-200       360036
           9332-400       360036
           9332-600       554800

           9335              [*]
           9335-1         804714

           9336              [*]
           9336-10        920115
           9336-20       1672881
           9336-25       1672881

           0671-08        513072
           0671           574560
           0671-04        624456

       [*] size may be specified else size defaults to the first listed model.

Volumes exceeding 2GB
^^^^^^^^^^^^^^^^^^^^^

For regular (uncompressed) CKD volumes which exceed 2GB in size (such as
the 3390-3 and larger models) -- *and for which the -lfs parameter was
not specified* -- the DASDINIT / DASDINIT64 program creates multiple
files by appending the characters **\_1**, **\_2**, **\_3** etc. to the
file name specified on the command line. These characters are inserted
before the first dot (**.**) after the last slash (**/**). If there is
no dot, then the characters are appended to the end of the name. Each
file contains a whole number of cylinders. Hercules CKD support
recognizes the files as belonging to a single logical volume. Specify
the full name of just the first file in the Hercules configuration file
(e.g. "*filename*\ \_1").

*If the -lfs option is specified however*, then the output file is a
single large file which can be as large as your system supports.

The DASDINIT / DASDINIT64 program cannot create FBA volumes exceeding
2GB unless the **-lfs** parameter is specified and *large file size* is
supported on your platform..

Examples
^^^^^^^^

To create a 3330 model 1 CKD volume consisting of 404 cylinders (plus 7
alternate cylinders too) with volume serial number WORK01 in a file
called **work01.151:**

::

       dasdinit64 -a work01.151 3330-1 work01

To create a compressed 3350 CKD volume consisting of 560 cylinders (555
cylinders plus the 5 alternate cylinders) with volume serial number
SYSRES in a file called **dosvs34.24f:**

::

       dasdinit64 -a -bz2 dosvs34.24f 3350-1 sysres

To create a 3370 FBA volume with only 100000 sectors (instead of the
usual 558000 sectors) with volume serial number WORK02 in a file called
**mini.work02.140:**

::

       dasdinit64 mini.work02.140 3370 work02 100000

To create a 3390 model 3 (triple density) CKD volume of 3339 cylinders
with volume serial number WORK03:

::

       dasdinit64 triple.a88 3390-3 work03

Because this volume exceeds 2GB, DASDINIT / DASDINIT64 will create two
files with **triple_1.a88 containing cylinders 0-2518 and triple_2.a88
containing cylinders 2519-3339. However, if you instead specify the
``-lfs`` option:**

::

       dasdinit64 -lfs triple.a88 3390-3 work03

then DASDINIT /DASDINIT64 will create a single file **triple.a88**
containing all the cylinders. Your platform must support *large file
sizes* to specify the **-lfs** option.

Formatting the empty DASD volume
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After creating a DASD volume you can format it with a program such as
standalone IBCDASDI or ICKDSF.

Here is an example of the IBCDASDI control statements required to
initialize a 3330 volume:

::

       WORK01 JOB  'INITIALIZE 3330 WORK VOLUME'
              MSG   TODEV=1052,TOADDR=009
              DADEF TODEV=3330,TOADDR=151,IPL=NO,VOLID=WORK01,BYPASS=YES
              VLD   NEWVOLID=WORK01,OWNERID=HERCULES
              VTOCD STRTADR=1,EXTENT=5
              END

To run IBCDASDI, place the above statements in a file called
**init3330.txt** and start Hercules in S/370 mode with a configuration
file containing these statements:

::

       CPUSERIAL  001234
       CPUMODEL   3145
       MAINSIZE   2
       CNSLPORT   1052
       ARCHLVL    S/370

       0009   1052
       000A   1442    ibcdasdi.rdr
       000C   1442    init3330.txt
       0151   3330    work01.151

After IPLing from card reader device 00A, connect a telnet client to
port 1052, and press enter. At the IBCDASDI prompt, enter the command:

::

       input=1442 00c

Loading the new DASD volume
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Next, you need to create a full volume dump file of your chosen
*mainframe* dasd volume (converting it to AWSTAPE format) by using the
**tapeconv.jcl** job in the Hercules source directory. You would run
this JCL on your *mainframe*.

The resulting AWSTAPE mainframe file can then be downloaded in binary
format to your PC where Hercules is running, where it can then be
defined as a Hercules virtual tape drive in your Hercules configuration
file.

A standalone program could then be IPLed on Hercules to restore the
volume image from the virtual tape onto the formatted Hercules DASD
volume.

--------------

Building a DASD volume from unloaded PDS files
----------------------------------------------

dasdload / dasdload64
~~~~~~~~~~~~~~~~~~~~~

The dasdload program can be run from the Unix shell prompt to create a
new DASD image file and load it with data from unloaded PDS files.

The format of the dasdload / dasdload64 command is:

::

  dasdload   [options] ctlfile outfile [msglevel [maxdblk maxttr maxdscb]]
  dasdload64 [options] ctlfile outfile [msglevel [maxdblk maxttr maxdscb]]|        

where *[options]* can be:

-z            Build compressed dasd image file using zlib.
-bz2          Build compressed dasd image file using bzip2.
-0            Build compressed dasd image file with no compression.
-a            Build dasd image file that includes alternate cylinders.
-b            For a volume without IPL text, make the wait PSW written to the IPL1 record a BC-mode PSW. The default is to make the wait PSW an EC-mode PSW.
-m            For a volume without IPL text, make the wait PSW written to the IPL1 record enabled for machine checks. The default is to make the wait PSW disabled for machine checks.
- ctlfile       is the name of the control file which specifies the datasets that are to be loaded onto the newly-created volume
- outfile       is the name of the DASD image file to be created
- msglevel      is an optional number from 0 to 5 (default is 1) which controls the level of detail of the messages issued during the load.
- maxdblk       is the optional maximum number of DBLK table entries or 0 to use the default
- maxttr        is the optional maximum number of TTR table entries or 0 to use the default
- maxdscb       is the optional maximum number of DSCB table entries or 0 to use the default


| command --option1 value1 \\
|         --option2 value2 \\
|         --option3 value3


- ``--option1``: value1
- ``--option2``: value2
- ``--option3``: value3




**Note** that dasdload's default for the wait PSW written to the IPL1
record *have changed from earlier releases of Hercules*. In the past,
the wait PSW created by dasdload on volumes without IPL text was a
BC-mode PSW enabled for machine check interrupts. The current default
for the wait PSW is EC-mode, disabled for machine checks. To obtain the
earlier behavior, run dasdload with the "-b" and "-m" flags.

Control file
^^^^^^^^^^^^

The control file required by the dasdload /dasdload64 program is an
ASCII text file consisting of a *volume statement* followed by one
*dataset statement* for each dataset to be created.

The format of the volume statement is:

       
*``volser devtype``*\ ``[-``\ *``model``*\ ``] [``\ *``cyls``*\ ``[``\ *``ipltext``*\ ``] ]``

where:

   *``volser``*
      is the volume serial number for the newly-created volume
   *``devtype``*
      is the emulated device type (2311, 2314, 3330, 3340, 3350, 3375,
      3380, or 3390) for the new volume. FBA device types are not
      supported by the dasdload / dasdload64 program. Model may be
      specified like `dasdinit / dasdinit64 <#models>`__ above.
   *``cyls``*
      is the size of the new volume in cylinders. If *``cyls``* is coded
      as ``*`` or as ``0`` or is omitted, then the default size for the
      device type and model is used.
   *``ipltext``*
      is an optional parameter specifying the name of a file containing
      the IPL text which will be written to the volume. The file must be
      in the form of an object deck containing fixed length 80-byte
      EBCDIC records in the same format as expected by IBCDASDI or
      ICKDSF.

The format of a dataset statement is:

       
*``dsname method units pri sec dir dsorg recfm lrecl blksize keylen``*

where:

   *``dsname``*
      is the dataset name
   *``method``*
      is the dataset loading method which can be one of the following:

      ``XMIT``\ *``filename``*
         the dataset is loaded from an unloaded PDS created by the TSO
         XMIT command
      ``SEQ``\ *``filename``*
         the sequential dataset is loaded from a **binary** file.
         ascii/ebcdic translation is not currently supported. Also, the
         dsorg must either be *PS* or *DA* and recfm must either be *F*
         or *FB*.
      ``EMPTY``
         the dataset is initialized with an end of file record (if DSORG
         is PS) or an empty PDS directory (if DSORG is PO)
      ``DIP``
         the dataset is initialized with a LOGREC header record
      ``CVOL``
         the dataset is initialized as an OS SYSCTLG containing the
         minimum entries needed to IPL an OS/360 system
      ``VTOC``
         specifies the size and location of the VTOC. A dataset name
         must be coded on this statement, although it is not used. If no
         VTOC statement is present, the VTOC will be placed after the
         last dataset on the volume and the size of the VTOC will be the
         minimum number of tracks necessary.
   *``units``*
      is the space allocation units: ``TRK`` or ``CYL``.
   *``pri``*
      is the space allocation primary quantity
   *``sec``*
      is the space allocation secondary quantity
   *``dir``*
      is the number of directory blocks
   *``dsorg``*
      is the dataset organization: ``PS``, ``PO``, ``DA``, or ``IS``,
   *``recfm``*
      is the record format: ``F``, ``FB``, ``FBS``, ``V``, ``VB``,
      ``VBS``, or ``U``.
   *``lrecl``*
      is the logical record length
   *``blksize``*
      is the block size
   *``keylen``*
      is the key length

All parameters except dsname and method are optional. Defaults of zero
are supplied for DCB parameters. For datasets loaded with the XMIT
method, the DCB parameters are taken from the unloaded PDS, and the
minimum space allocation required to load the dataset is used unless a
larger quantity is specified. If space allocation is omitted, the
default is TRK 1 0 0. If CYL is specified without any primary quantity
then the default space allocation is 1 cylinder or the minimum number of
cylinders required to load the dataset, whichever is larger.

Example 1:
^^^^^^^^^^

To create a 2314 volume in a file called **sysres.230** using the
control file **sysres.plf** with message level 2:

::

       dasdload64 sysres.plf sysres.230 2

An example control file is shown below:

::

       #
       # Pack layout file for MFT system residence volume
       #
       sysres 2314 * ieaipl00.rdr
       sys1.parmlib    xmit    /cdrom/os360/reslibs/parmlib.xmi
       sys1.imagelib   xmit    /cdrom/os360/reslibs/imagelib.xmi
       sysctlg         cvol    trk 1 0 0       ps f 256 256 8
       sysvtoc         vtoc    trk 5
       sys1.logrec     dip     trk 1 0 0
       sys1.nucleus    xmit    /cdrom/os360/reslibs/nucleus.xmi cyl
       sys1.svclib     xmit    /cdrom/os360/reslibs/svclib.xmi cyl
       sys1.sysjobqe   empty   cyl 2 0 0       da f 176 176 0
       sys1.dump       empty   cyl 10 0 0      ps u 0 3625 0

Example 2:
^^^^^^^^^^

To create a compressed 3390-3 volume in a file called **linux.500**
containing a bootable linux system for linux/390 installation using the
control file **linux.prm**:

::

       dasdload64 -z linux.prm linux.500

An example control file is shown below:

::

       #
       #   Build a bootable linux disk
       #
       #   [Note: the dataset names (sys1.linux...) are hard-coded in
       #    linuxipl.obj and cannot be changed without rebuilding it]
       #
       linux  3390-3 * linuxipl.obj
       sys1.linux.parmfile    SEQ images/redhat.prm trk   1 0 0 ps fb 1024 1024
       sys1.linux.tapeipl.ikr SEQ images/kernel.img trk 200 0 0 ps fb 1024 1024
       sys1.linux.initrd      SEQ images/initrd.img trk 200 0 0 ps fb 1024 1024

Fixing the XCTL tables in SVCLIB
--------------------------------

DASDISUP:   IEHIOSUP
~~~~~~~~~~~~~~~~~~~~

On an OS/360 system, the Open/Close/EOV modules in SYS1.SVCLIB have XCTL
tables embedded within them. These tables contain TTRs pointing to other
modules, and these TTRs need to be adjusted after loading SVCLIB to
DASD. OS/360 provides a program called IEHIOSUP to perform this
function, but the catch-22 situation is that you can't run IEHIOSUP
until you have the system up and running, and you can't IPL until you
have fixed the XCTL tables!

To solve this dilemma, Hercules provides a program called dasdisup which
can be run from the Unix command line after running dasdload /
dasdload64.

The format of the dasdisup command is:

        ``dasdisup``\ *``outfile [sf=shadow-file-name]``*

where

   *``outfile``*
      is the name of the DASD image file to be updated
   *``shadow-file-name``*
      (optional) is the name of the associated shadow file as specified
      in the Hercules config file

**Note:** *do not use this procedure except on OS/360 IPL volumes! Other
operating systems do not have XCTL tables!*

--------------

Other DASD utilities
--------------------

These programs can be used to extract data from CKD DASD images by means
of commands issued at the Unix shell prompt.

DASDLS:   List datasets on volume
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DASDLS, written by Malcolm Beattie and enhanced by others, is a command
to let you list the names of the datasets contained in disk images.

The command format is:

        ``dasdls [-option [-option ... ]] ckdfile [sf=sfile] [...]``

where *ckdfile* is the name of a Unix file containing a CKD volume and
*sfile* (optional) is the name of the associated shadow file.

*-option* can be:

   *``-hdr``*
      show column headers
   *``-dsnl [=n]``*
      restrict dsname width
   *``-info``*
      show F1 info
   *``-caldt``*
      calendar date format
   *``-refdt``*
      show last-reference date
   *``-expdt``*
      show expiry date
   *``-yroffs [=n]``*
      year offset

**Note:** Multiple images can be processed in the same run, but options
must be specified ahead of each image.

DASDCAT:   Display PDS members
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DASDCAT, written by Malcolm Beattie, is a command to let you read
datasets from disk images.

The command format is:

       
``dasdcat -i``\ *``ckdfile [sf=shadow-file-name] dsname1 dsname2 ...``*\ ``-i``\ *``ckdfile2 dsname10 ...``*

where *ckdfile* is the name of a Unix file containing a CKD volume,
*shadow-file-name* (optional) is the name of the associated shadow file,
and *dsname* can be a plain (non-partitioned) dataset name (which is
currently not handled) or of the form *pdsname*/*memname* where
*memname* can be:

-  **PDS member name** (automatically uppercased), optionally followed
   by ":" and flags "a" or "c".

   -  "c" means (c)ard images and turns a PDS members with a block size
      that's a multiple of 80 into multiple newline separated lines of
      72 characters with EBCDIC converted to ASCII and with sequence
      numbers chopped off.
   -  "a" means (a)sciify the member (but don't chop off sequence
      numbers or do the card image thing).

-  **?** (don't forget to quote it to avoid the shell globbing it) to
   list the names of all PDS members instead of outputting their
   contents.
-  **\*** (again, quote it or backwhack it to avoid it being a glob) to
   output all members of the PDS instead of just a named one. This can
   optionally be followed with colon-then-flags, as above. Each member
   is preceded with a line "> Member: memname" and, if the "c" for
   card-images flags is used, each line of the members' contents is
   preceded with "\| " to guarantee it can be distinguished from
   contents.

.. _examples-1:

Examples:
^^^^^^^^^

::

       % dasdcat -i mvtres.350 sf= mvtres_1.350 'sys1.parmlib/?'

       ieabld00
       ieaige00
       ieaigg00
       ieaigg01
       iearsv00
       ikjprm00
       lnklst00
       presres
       smfdeflt

       % dasdcat -i mvtres.350 sys1.parmlib/smfdeflt:c

        OPT=2, SYSTEM,JOB AND STEP DATA COLLECTION
        EXT=YES, USER EXITS ARE TO BE TAKEN
        JWT=15, MAXIMUM CONTINUOUS WAIT TIME IS 15 MINS.PER STEP
        BUF=400, A MINIMUM 400 BYTE BUFFER IS DEFINED
        SID=6A, SYSTEM ID IS 6A
        MDL=65, MODEL IS MOD 65
        OPI=YES, PERMIT OPERATOR INTERVENTION
        MAN=ALL, RECORD USER AND SYSTEM RECORDS
        PRM=(,282,NL) SYS1.MAN ALLOCATED TO NON-LABELED TAPE

       % dasdcat -i mvtres.350 sys1.help/\*:c

       > Member ACCOUNT
       | )S SUBCOMMANDS -
       | ADD/A,CHANGE/C,DELETE/D,LIST/L,LISTIDS/LISTI,HELP/H,END
       | )F FUNCTION -
       | THE ACCOUNT COMMAND PROCESSOR INVOKES THE CONVERSATIONAL PROGRAMS
       ...
       > Member ALLOC
       | )F FUNCTION -
       | THE ALLOCATE COMMAND DYNAMICALLY DEFINES AND ALLOCATES A DATA SET
       | WITH OR WITHOUT AN ATTRIBUTE LIST OF DCB PARAMETERS
       | )X SYNTAX -
       | ALLOCATE DATASET('DSNAME'/*) FILE('DDNAME')
       ...

DASDPDSU:   Unload PDS members
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DASDPDSU is a command which unloads PDS members from a disk image and
copies each member to a file *memname*.mac in the current working
directory.

The command format is:

       
``dasdpdsu``\ *``ckdfile [sf=shadow-file-name] pdsname``*\ ``[ASCII] [odir]``

where *ckdfile* is the name of a file containing a CKD volume,
*shadow-file-name* (optional) is the name of the associated shadow file,
and *pdsname* is the name of a PDS on that volume. If the optional
**ASCII** keyword is specified, the members will be unloaded as ASCII
variable length text files. Otherwise the members are unloaded as fixed
length EBCDIC binary files. The optional *odir* parameter is the name of
the directory where the output files should be placed. Otherwise if not
specified they are created in the current directory.

--------------

If you have a question about Hercules, see the `Hercules
Frequently-Asked Questions <hercfaq.html>`__ page.

--------------
