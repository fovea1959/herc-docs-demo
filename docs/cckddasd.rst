Compressed Dasd Emulation
=========================

--------------

Contents
--------

-  `Introduction <#introduction>`__
-  `Shadow Files <#shadowfiles>`__
-  `File Structure <#filestructure>`__
-  `How It Works <#howitworks>`__
-  `Tuning options <#cckdcommand>`__
-  `Utilities <#utilities>`__

--------------

Introduction
------------

Using compressed DASD files can significantly reduce the host system
file space required for emulated DASD files and possibly provide a
performance gain as well because less physical I/O occurs.

Using compressed DASD files also has other advantages too, such as
allowing you to use `shadow files <#shadowfiles>`__.

Both **CKD** (Count-Key-Data) and **FBA** (Fixed-Block-Architecture)
emulation files can be compressed.

In regular (or uncompressed) files, each CKD track or FBA block occupies
a specific spot in the emulation file. The offset of the track or block
in the file can be directly calculated knowing the track or block number
and the maximum size of the track or block. In compressed files, each
track image or group of blocks may be compressed by
`zlib <http://www.zlib.net/>`__ or `bzip2 <http://www.bzip.org/>`__, and
only occupies the space neccessary for the compressed data. The offset
of a compressed track or block is obtained by performing a two-table
lookup. The lookup tables themselves reside in the emulation file.

Because FBA blocks are 512 bytes in length, and that being a rather
small number, FBA blocks are thus grouped into **block groups**. Each
block group contains 120 FBA blocks (60K).

Whenever a track or block group is written to a compressed file, it is
written either to an existing free space within the file or at the end
of the file, the lookup tables are then updated, and then the space the
track or block group previously occupied is freed. The location of a
track or block group in the file can change many times.

In the event of a failure (for example, Hercules crash, operating system
crash or power failure), the compressed emulation file on the host's
physical disk may be out of sync if the host operating system defers
physical writes to the file system containing the emulation file.
However, several methods have evolved to greatly reduce the chance of
this occurring as well as the amount of data loss that can occur after
these kinds of events, so the chance of actual data loss is relatively
small.

A compressed dasd image file may occupy only 20% of the disk space
required by an uncompressed file. In other words, you may be able to
have 5 times more emulated volumes on your system by using compressed
DASD files than by using uncompressed dasds. Compressed files are
slightly more sensitive to failures and data corruption however, but due
to their design and careful implementation, the chance of this actually
occuring is relatively small.

Compressed DASD images are created via the
`dasdinit64 <hercload.html#dasdinit>`__ utility.

--------------

Shadow Files
------------

Shadow files are only supported for compressed dasd images.

A compressed CKD or FBA dasd can have more than one physical file. These
additional files are called *shadow files*. Shadow files are designed to
be used as a kind of *"snapshot"*, where a new shadow file can be
created on demand. An emulated dasd is represented by a *base* file and
0 or more shadow files. All files are opened *read-only* except for the
*current* file, which is opened *read-write*.

Shadow files are specified by the **sf=**\ *shadow-file-name* parameter
on the device statement for the compressed DASD device.

Please note that the specified shadow filename does *not* have to
actually exist. The *shadow-file-name* operand of the **sf=** parameter
is simply a **filename template** that will be used to name the shadow
file whenever a shadow file is to be created. Shadow files do not
actually get created until you specifically create them via the
``sf+xxxx`` (or ``sf+*``) command, or automatically
**(**\ ```*`` <#autoshadow>`__\ **)** by marking either the base dasd
image file or an existing shadow file as read-only. Please refer to the
discussion of the **sf** command in the next section further below for
more information.

The **shadow file name** should have spot where the shadow file number
will be set. This is either the character immediately preceding the
filename extension or the last character of the file name itself if
there is no extension.

| For example, the following device statement:

::

       0001  2311  AAAAAA.model-x.ext   sf=AAAAAA_Shadow_0.model-x.ext

will cause a shadow file with the following name to be created:

::

                                           AAAAAA_Shadow_0.model-1.ext

whereas the following *slightly different device statement*:

::

       0002  2311  BBBBBB.model-x.ext   sf=BBBBBB.model-x_Shadow_0.ext

will cause a shadow file with the following name to be created:

::

                                           BBBBBB.model-x_Shadow_1.ext

*Notice the placement of the shadow file number* in the above two
examples: it is always immediately before the *last* period of the
filename. In earlier versions of Hercules the shadow file number was
erroneously placed immediately before the *first* period of the filename
instead of the last period. In newer versions of Hyperion this has been
corrected to place the number immediately before the *last* period, as
it was originally intended.

The Advantage of Shadow Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A shadow file contains all the changes made to the emulated dasd since
it was created, until the next shadow file is created. The moment of the
shadow file's creation can be thought of as a *"snapshot"* of the
current emulated dasd as it existed at that point in time, because if
the shadow file is later removed, then the emulated dasd reverts back to
the state it was in at the moment the snapshot was taken.

Using shadow files, you can keep the base file on a read-only device
such as cdrom, or change the base file attributes to read-only, ensuring
that this file can never be corrupted.

With the use of shadow files you can reconfigure your guest without
worrying about whether the new settings might render your guest
unusable. Simply create a new shadow file *before* you do your
reconfiguration. If something goes wrong, simply exit Hercules and then
delete that set of shadow files. You'll be right back to where you were
*before* you made your changes! Then you can simply try again. Once you
are satisfied that your changes are good, you can then do a "``sf-*``"
backwards merge (see further below) to "commit" your changes.

There can be up to 8 shadow files in use at any time for an emulated
dasd device. The base file is designated file\ **[0]** and the shadow
files are file\ **[1]** to file\ **[8]**. The *highest* numbered file in
use at a given time is the *current* file, where all writes will occur.
Track reads start with the *current* file and proceeds downward until a
file is found that actually contains the track image.

Hercules console commands are provided to add a new shadow file, remove
the current shadow file (with or without backward merge), compress the
current shadow file, and display the shadow file status and statistics:

   +-----------------+-----------------+-----------------+-----------------+
   |                 |                 |                 |                 |
   +-----------------+-----------------+-----------------+-----------------+
   | **sfd**         | unit            |                 | Display shadow  |
   |                 |                 |                 | file status and |
   |                 |                 |                 | statistics      |
   +-----------------+-----------------+-----------------+-----------------+
   | **sfc**         | unit            |                 | Compress the    |
   |                 |                 |                 | current file    |
   +-----------------+-----------------+-----------------+-----------------+
   | **sf+**         | unit            |                 | Create a new    |
   |                 |                 |                 | shadow file     |
   |                 |                 |                 | **(**\          |
   |                 |                 |                 | ```*`` <#autosh |
   |                 |                 |                 | adow>`__\ **)** |
   +-----------------+-----------------+-----------------+-----------------+
   |                 |                 |                 |                 |
   +-----------------+-----------------+-----------------+-----------------+
   | **sf-**         | unit            | merge           | Remove a shadow |
   |                 |                 | *nomerge        | file.           |
   |                 |                 | force     *     | If *merge* is   |
   |                 |                 |                 | specified or    |
   |                 |                 |                 | defaulted, then |
   |                 |                 |                 | the contents of |
   |                 |                 |                 | the current     |
   |                 |                 |                 | file is merged  |
   |                 |                 |                 | into the        |
   |                 |                 |                 | previous file,  |
   |                 |                 |                 | the current     |
   |                 |                 |                 | file is         |
   |                 |                 |                 | removed, and    |
   |                 |                 |                 | the previous    |
   |                 |                 |                 | file becomes    |
   |                 |                 |                 | the current     |
   |                 |                 |                 | file. The       |
   |                 |                 |                 | previous file   |
   |                 |                 |                 | must be able to |
   |                 |                 |                 | be opened       |
   |                 |                 |                 | read-write. If  |
   |                 |                 |                 | *nomerge* is    |
   |                 |                 |                 | specified then  |
   |                 |                 |                 | the contents of |
   |                 |                 |                 | the current     |
   |                 |                 |                 | file is         |
   |                 |                 |                 | discarded and   |
   |                 |                 |                 | the previous    |
   |                 |                 |                 | file becomes    |
   |                 |                 |                 | the current     |
   |                 |                 |                 | file. However,  |
   |                 |                 |                 | if the previous |
   |                 |                 |                 | file is         |
   |                 |                 |                 | read-only, then |
   |                 |                 |                 | a new shadow    |
   |                 |                 |                 | file is created |
   |                 |                 |                 | (re-added) and  |
   |                 |                 |                 | that becomes    |
   |                 |                 |                 | the current     |
   |                 |                 |                 | file. The       |
   |                 |                 |                 | *force* option  |
   |                 |                 |                 | is required     |
   |                 |                 |                 | when doing a    |
   |                 |                 |                 | merge to the    |
   |                 |                 |                 | base file and   |
   |                 |                 |                 | the base file   |
   |                 |                 |                 | is read-only    |
   |                 |                 |                 | because the     |
   |                 |                 |                 | *ro* option was |
   |                 |                 |                 | specified on    |
   |                 |                 |                 | the device      |
   |                 |                 |                 | config          |
   |                 |                 |                 | statement.      |
   +-----------------+-----------------+-----------------+-----------------+
   |                 |                 |                 |                 |
   +-----------------+-----------------+-----------------+-----------------+
   | **sfk**         | unit            | level           | Perform the     |
   |                 |                 |                 | **chkdsk**      |
   |                 |                 |                 | function on the |
   |                 |                 |                 | current file.   |
   |                 |                 |                 | Level is a      |
   |                 |                 |                 | number from -1  |
   |                 |                 |                 | ... 4, with the |
   |                 |                 |                 | default level   |
   |                 |                 |                 | being **2**:    |
   |                 |                 |                 |      -1         |
   |                 |                 |                 | devhdr,         |
   |                 |                 |                 | cdevhdr, L1     |
   |                 |                 |                 | table.          |
   |                 |                 |                 |       0         |
   |                 |                 |                 | devhdr,         |
   |                 |                 |                 | cdevhdr, L1     |
   |                 |                 |                 | table, L2       |
   |                 |                 |                 | tables.         |
   |                 |                 |                 |       1         |
   |                 |                 |                 | devhdr,         |
   |                 |                 |                 | cdevhdr, L1     |
   |                 |                 |                 | table, L2       |
   |                 |                 |                 | tables, free    |
   |                 |                 |                 | spaces.         |
   |                 |                 |                 |       **2**     |
   |                 |                 |                 |   devhdr,       |
   |                 |                 |                 | cdevhdr, L1     |
   |                 |                 |                 | table, L2       |
   |                 |                 |                 | tables, free    |
   |                 |                 |                 | spaces,         |
   |                 |                 |                 | trkhdrs.        |
   |                 |                 |                 |  *(default)*    |
   |                 |                 |                 |       3         |
   |                 |                 |                 | devhdr,         |
   |                 |                 |                 | cdevhdr, L1     |
   |                 |                 |                 | table, L2       |
   |                 |                 |                 | tables, free    |
   |                 |                 |                 | spaces,         |
   |                 |                 |                 | trkimgs.        |
   |                 |                 |                 |       4         |
   |                 |                 |                 | devhdr,         |
   |                 |                 |                 | cdevhdr, build  |
   |                 |                 |                 | everything else |
   |                 |                 |                 | from recovery.  |
   +-----------------+-----------------+-----------------+-----------------+

   *Note*: You can use '**``*``**' in place of 'unit' in any of the
   above commands to apply the command to *all* compressed dasd.
   (``sf+*``,\ ``sf-*``,\ ``sfc*``,\ ``sfk*``,\ ``sfd*``)

   **(``*``)** In addition to the **sf+** command, shadow files can also
   be created *automatically* whenever the base dasd image and all of
   its existing shadow files (if any) are marked as read-only. When
   Hercules opens a compressed dasd image file with a ``sf=`` option, it
   automatically looks for and opens whatever existing shadow files
   there may be, with the highest numbered shadow file being the one
   where all writes will occur. If the highest numbered shadow file is
   also marked as a read-only file too, then a new shadow file is
   automatically created and used instead.

--------------

Compressed DASD File Structure
------------------------------

A compressed DASD file has 6 types of spaces, a *device header*, a
*compressed device header*, a *primary lookup table*, *secondary lookup
tables*, track or block group *images*, and *free spaces*. The first 3
types (*device header, compressed device header, primary lookup table*)
only occur once, in order, at the very beginning of the file. The rest
of the file is occupied by the other 3 space types.

**It is also important to note** *that, except for the actual track or
block group images space types, all numeric fields in each of the above
space types are always kept in LITTLE endian format and are
automatically converted to host format as needed before being used. This
is the complete opposite of the way emulated guest storage is maintained
(which is always in big endian format).*

The very first 512 bytes of a compressed DASD file is the **device
header**. The device header contains an "eye-catcher" that identifies
the file type (32-bit or 64-bit CKD or FBA and base or shadow). The
original CCKD design used 32-bit file offset values thus limiting file
sizes to only 4GB or less.

The newer 64-bit design however, uses 64-bit offset values, thereby
allowing compressed dasd image files to grow up to the theoretical
maximum of 18,000,000 TB (18,000,000,000 GB). The *actual* maximum file
size however, is limited by both the operating system and the format of
whatever file system you are using. On Windows, using NTFS for example,
the maximum file size is limited to only 16 TB (16,000 GB).

      Device-id
      Dasd image type
       
         
      CKD_P370
          Normal *(uncompressed)* CKD dasd image
      CKD_C370
          Compressed CKD dasd image
      CKD_S370
          Compressed CKD dasd Shadow file
      n/a\*
          Normal *(uncompressed)* FBA\ **\*\*** dasd image
      FBA_C370
          Compressed FBA dasd image
      FBA_S370
          Compressed FBA dasd Shadow file
       
         
      CKD_P064
          Normal *(uncompressed)* CKD64 dasd image
      CKD_C064
          Compressed CKD64 dasd image
      CKD_S064
          Compressed CKD64 dasd Shadow file
      n/a\*
          Normal *(uncompressed)* FBA64\ **\*\*** dasd image
      FBA_C064
          Compressed FBA64 dasd image
      FBA_S064
          Compressed FBA64 dasd Shadow file

   *(\*)  Normal (uncompressed) FBA/FBA64 dasd image files do not have
   device headers. The first 512 bytes of a normal (uncompressed)
   FBA/FBA64 dasd image file is the actual first sector of the emulated
   FBA dasd device itself.*

   *(\*\*)  Normal (uncompressed) FBA64 dasd image files are exactly
   identical to normal (uncompressed) FBA dasd image files. There is
   absolutely no distinction between the two types. Their formats are
   exactly identical.*

| 
| The device type and file size information is specified in this header
  and, except for the eye-catcher (or device-id), this header is
  identical for both compressed CCKD/CCKD64 and compressed CFBA/CFBA64
  images as well as for uncompressed CKD/CKD64 images. As mentioned just
  above however, it is *not* used for uncompressed FBA/FBA64 images.

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| V |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| H |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| R |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| " |   |   |   |   |   |   |   | d |   |   |   | d |   |   |   |
| * |   |   |   |   |   |   |   | h |   |   |   | h |   |   |   |
| * |   |   |   |   |   |   |   | _ |   |   |   | _ |   |   |   |
| C |   |   |   |   |   |   |   | h |   |   |   | t |   |   |   |
| K |   |   |   |   |   |   |   | e |   |   |   | r |   |   |   |
| D |   |   |   |   |   |   |   | a |   |   |   | k |   |   |   |
| _ |   |   |   |   |   |   |   | d |   |   |   | s |   |   |   |
| C |   |   |   |   |   |   |   | s |   |   |   | i |   |   |   |
| 3 |   |   |   |   |   |   |   |   |   |   |   | z |   |   |   |
| 7 |   |   |   |   |   |   |   |   |   |   |   | e |   |   |   |
| 0 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| " |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| ( |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| v |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| i |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| c |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| - |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| i |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| o |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| " |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| y |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| - |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| c |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| a |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| t |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| c |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| h |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| " |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| ) |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| d | d | d |   | d |   |   |   |   |   |   |   |   |   |   |   |
| h | h | h |   | h |   |   |   |   |   |   |   |   |   |   |   |
| _ | _ | _ |   | _ |   |   |   |   |   |   |   |   |   |   |   |
| d | f | h |   | s |   |   |   |   |   |   |   |   |   |   |   |
| e | i | i |   | e |   |   |   |   |   |   |   |   |   |   |   |
| v | l | g |   | r |   |   |   |   |   |   |   |   |   |   |   |
| t | e | h |   | i |   |   |   |   |   |   |   |   |   |   |   |
| y | s | c |   | a |   |   |   |   |   |   |   |   |   |   |   |
| p | e | y |   | l |   |   |   |   |   |   |   |   |   |   |   |
|   | q | l |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| v |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

The *dh_heads*, *dh_trksize* and *dh_highcyl* values, being numeric, are
always kept in little endian format.

The next 512 bytes contains the **compressed device header**.

The compressed device header contains file usage information, such as
the amount of free space in the file.

Note that even though this control block is labeled "CCKD_DEVHDR" (or
"CCKD64_DEVHDR" for 64-bit images), it actually applies to (is used for)
compressed FBA images (CFBA/CFBA64) too, as well as for compressed CKD
images (CCKD/CCKD64).

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| V |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| H |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| R |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| c |   |   | c | n |   |   |   | n |   |   |   | c |   |   |   |
| d |   |   | d | u |   |   |   | u |   |   |   | d |   |   |   |
| h |   |   | h | m |   |   |   | m |   |   |   | h |   |   |   |
| _ |   |   | _ | _ |   |   |   | _ |   |   |   | _ |   |   |   |
| v |   |   | o | L |   |   |   | L |   |   |   | s |   |   |   |
| r |   |   | p | 1 |   |   |   | 2 |   |   |   | i |   |   |   |
| m |   |   | t | t |   |   |   | t |   |   |   | z |   |   |   |
|   |   |   | s | a |   |   |   | a |   |   |   | e |   |   |   |
|   |   |   |   | b |   |   |   | b |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| c |   |   |   | f |   |   |   | f |   |   |   | f |   |   |   |
| d |   |   |   | r |   |   |   | r |   |   |   | r |   |   |   |
| h |   |   |   | e |   |   |   | e |   |   |   | e |   |   |   |
| _ |   |   |   | e |   |   |   | e |   |   |   | e |   |   |   |
| u |   |   |   | _ |   |   |   | _ |   |   |   | _ |   |   |   |
| s |   |   |   | o |   |   |   | t |   |   |   | l |   |   |   |
| e |   |   |   | f |   |   |   | o |   |   |   | a |   |   |   |
| d |   |   |   | f |   |   |   | t |   |   |   | r |   |   |   |
|   |   |   |   |   |   |   |   | a |   |   |   | g |   |   |   |
|   |   |   |   |   |   |   |   | l |   |   |   | e |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   | s |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   | t |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| f |   |   |   | f |   |   |   | c |   |   |   | c | c | c |   |
| r |   |   |   | r |   |   |   | d |   |   |   | d | m | m |   |
| e |   |   |   | e |   |   |   | h |   |   |   | h | p | p |   |
| e |   |   |   | e |   |   |   | _ |   |   |   | _ | _ | _ |   |
| _ |   |   |   | _ |   |   |   | c |   |   |   | n | a | p |   |
| n |   |   |   | i |   |   |   | y |   |   |   | u | l | a |   |
| u |   |   |   | m |   |   |   | l |   |   |   | l | g | r |   |
| m |   |   |   | b |   |   |   | s |   |   |   | l | o | m |   |
|   |   |   |   | e |   |   |   |   |   |   |   | f |   |   |   |
|   |   |   |   | d |   |   |   |   |   |   |   | m |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   | t |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| v |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

| 

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| V |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| H |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| R |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| c |   |   | c | n |   |   |   | n |   |   |   | c |   |   |   |
| d |   |   | d | u |   |   |   | u |   |   |   | d |   |   |   |
| h |   |   | h | m |   |   |   | m |   |   |   | h |   |   |   |
| _ |   |   | _ | _ |   |   |   | _ |   |   |   | _ |   |   |   |
| v |   |   | o | L |   |   |   | L |   |   |   | c |   |   |   |
| r |   |   | p | 1 |   |   |   | 2 |   |   |   | y |   |   |   |
| m |   |   | t | t |   |   |   | t |   |   |   | l |   |   |   |
|   |   |   | s | a |   |   |   | a |   |   |   | s |   |   |   |
|   |   |   |   | b |   |   |   | b |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| c |   |   |   |   |   |   |   | c |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   | d |   |   |   |   |   |   |   |
| h |   |   |   |   |   |   |   | h |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| i |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| z |   |   |   |   |   |   |   | e |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   | d |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| f |   |   |   |   |   |   |   | f |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   | r |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   | e |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   | e |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   |   |   |   |   |   |   |
| o |   |   |   |   |   |   |   | t |   |   |   |   |   |   |   |
| f |   |   |   |   |   |   |   | o |   |   |   |   |   |   |   |
| f |   |   |   |   |   |   |   | t |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | a |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | l |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| f |   |   |   |   |   |   |   | f |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   | r |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   | e |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   | e |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   |   |   |   |   |   |   |
| l |   |   |   |   |   |   |   | n |   |   |   |   |   |   |   |
| a |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   | m |   |   |   |   |   |   |   |
| g |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| t |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| f |   |   |   |   |   |   |   | c | c | c |   | r |   |   |   |
| r |   |   |   |   |   |   |   | d | m | m |   | e |   |   |   |
| e |   |   |   |   |   |   |   | h | p | p |   | s |   |   |   |
| e |   |   |   |   |   |   |   | _ | _ | _ |   | e |   |   |   |
| _ |   |   |   |   |   |   |   | n | a | p |   | r |   |   |   |
| i |   |   |   |   |   |   |   | u | l | a |   | v |   |   |   |
| m |   |   |   |   |   |   |   | l | g | r |   | e |   |   |   |
| b |   |   |   |   |   |   |   | l | o | m |   | d |   |   |   |
| e |   |   |   |   |   |   |   | f |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   | m |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | t |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| v |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| e |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

The *num_L1tab*, *num_L2tab*, *cdh_cyls*, *cdh_size*, *cdh_used*,
*free_off*, *free_total*, *free_largest*, *free_num*, *free_imbed*, and
*cmp_parm* values, being numeric, are always kept in little endian
format.

| 
| After the compressed device header is the **primary lookup table**
  (also called the Level 1 table or *L1tab*.) Each 4 byte unsigned entry
  in the *L1tab* (8 byte unsigned entry for CCKD64) contains the file
  offset of a *secondary lookup table* (or *level 2 table* or *L2tab*).

The track or block group number being accessed divided by 256 gives the
index into the *L1tab*. That is, each L1tab entry (*CCKD_L1ENT* or
*CCKD64_L1ENT*) represents 256 tracks or block groups. The number of
entries in the *L1tab* is dependent on the size of the emulated device.

Because each Level 1 table entry (CCKD_L1ENT or CCKD64_L1ENT) is a
numeric value, they are of course always kept in little endian format.

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| A |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| C |   |   |   | C |   |   |   | C |   |   |   | C |   |   |   |
| C |   |   |   | C |   |   |   | C |   |   |   | C |   |   |   |
| K |   |   |   | K |   |   |   | K |   |   |   | K |   |   |   |
| D |   |   |   | D |   |   |   | D |   |   |   | D |   |   |   |
| _ |   |   |   | _ |   |   |   | _ |   |   |   | _ |   |   |   |
| L |   |   |   | L |   |   |   | L |   |   |   | L |   |   |   |
| 1 |   |   |   | 1 |   |   |   | 1 |   |   |   | 1 |   |   |   |
| E |   |   |   | E |   |   |   | E |   |   |   | E |   |   |   |
| N |   |   |   | N |   |   |   | N |   |   |   | N |   |   |   |
| T |   |   |   | T |   |   |   | T |   |   |   | T |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   | L |   |   |   | L |   |   |   | L |   |   |   |
| 1 |   |   |   | 1 |   |   |   | 1 |   |   |   | 1 |   |   |   |
| \ |   |   |   | \ |   |   |   | \ |   |   |   | \ |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   | : |   |   |   | : |   |   |   | : |   |   |   |
| s |   |   |   | s |   |   |   | s |   |   |   | s |   |   |   |
| u |   |   |   | u |   |   |   | u |   |   |   | u |   |   |   |
| b |   |   |   | b |   |   |   | b |   |   |   | b |   |   |   |
| : |   |   |   | : |   |   |   | : |   |   |   | : |   |   |   |
| ` |   |   |   | ` |   |   |   | ` |   |   |   | ` |   |   |   |
| 0 |   |   |   | 1 |   |   |   | 2 |   |   |   | 3 |   |   |   |
| ` |   |   |   | ` |   |   |   | ` |   |   |   | ` |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   | L |   |   |   | L |   |   |   | L |   |   |   |
| 1 |   |   |   | 1 |   |   |   | 1 |   |   |   | 1 |   |   |   |
| \ |   |   |   | \ |   |   |   | \ |   |   |   | \ |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   | : |   |   |   | : |   |   |   | : |   |   |   |
| s |   |   |   | s |   |   |   | s |   |   |   | s |   |   |   |
| u |   |   |   | u |   |   |   | u |   |   |   | u |   |   |   |
| b |   |   |   | b |   |   |   | b |   |   |   | b |   |   |   |
| : |   |   |   | : |   |   |   | : |   |   |   | : |   |   |   |
| ` |   |   |   | ` |   |   |   | ` |   |   |   | ` |   |   |   |
| 4 |   |   |   | 5 |   |   |   | 6 |   |   |   | 7 |   |   |   |
| ` |   |   |   | ` |   |   |   | ` |   |   |   | ` |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   | L |   |   |   | L |   |   |   | L |   |   |   |
| 1 |   |   |   | 1 |   |   |   | 1 |   |   |   | 1 |   |   |   |
| \ |   |   |   | \ |   |   |   | \ |   |   |   | \ |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   | : |   |   |   | : |   |   |   | : |   |   |   |
| s |   |   |   | s |   |   |   | s |   |   |   | s |   |   |   |
| u |   |   |   | u |   |   |   | u |   |   |   | u |   |   |   |
| b |   |   |   | b |   |   |   | b |   |   |   | b |   |   |   |
| : |   |   |   | : |   |   |   | : |   |   |   | : |   |   |   |
| ` |   |   |   | ` |   |   |   | ` |   |   |   | ` |   |   |   |
| n |   |   |   | n |   |   |   | n |   |   |   | n |   |   |   |
| - |   |   |   | - |   |   |   | - |   |   |   | - |   |   |   |
| 4 |   |   |   | 3 |   |   |   | 2 |   |   |   | 1 |   |   |   |
| ` |   |   |   | ` |   |   |   | ` |   |   |   | ` |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

| 

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| A |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| C |   |   |   |   |   |   |   | C |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   | C |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   | K |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   | D |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   | 6 |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   | 4 |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   | E |   |   |   |   |   |   |   |
| N |   |   |   |   |   |   |   | N |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   | T |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | \ |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| u |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
| 0 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | \ |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| u |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 3 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | \ |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| u |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   | 5 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | \ |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| u |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   | 7 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | \ |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| u |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
| n |   |   |   |   |   |   |   | n |   |   |   |   |   |   |   |
| - |   |   |   |   |   |   |   | - |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   | 3 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | \ |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| s |   |   |   |   |   |   |   | s |   |   |   |   |   |   |   |
| u |   |   |   |   |   |   |   | u |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| : |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
| n |   |   |   |   |   |   |   | n |   |   |   |   |   |   |   |
| - |   |   |   |   |   |   |   | - |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

| 
| Following the primary lookup table (*L1tab*), in no particular order,
  are: **secondary lookup tables** (*L2tabs*), *track or block group
  images*, and *free spaces*.

Each **secondary lookup table** (or *L2tab*), contains 256 eight byte
entries (256 sixteen byte entries for CCKD64). The entry is indexed by
the remainder of the track or block group number divided by 256.

Each L2 entry contains an unsigned 4 byte *offset* (unsigned 8 byte
*offset* for CCKD64) to the **track or block group image** (*L2_trkoff*
= file offset to where the track image or block group begins), an
unsigned 2 byte track or block group *length* (the actual amount of data
contained on the track or in the block group) and an unsigned 2 byte
*size* of the track or block group image (i.e. how much space is
actually available for use at that particular file offset).

The length is the amount of available space currently being consumed by
the track or block group image, and the size is the amount of space
actually available. The size of course may be greater than the length to
prevent short free spaces from accumulating in the file.

Because each field in the Level 2 table (*L2_trkoff*, *L2_len* and
*L2_size*) is a numeric value, they are of course always kept in little
endian format.

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| A |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| C |   |   |   |   |   |   |   | C |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   | C |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   | K |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   | D |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   | L |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 2 |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   | E |   |   |   |   |   |   |   |
| N |   |   |   |   |   |   |   | N |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   | T |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   | L |   | L |   | L |   |   |   | L |   | L |   |
| 2 |   |   |   | 2 |   | 2 |   | 2 |   |   |   | 2 |   | 2 |   |
| _ |   |   |   | _ |   | _ |   | _ |   |   |   | _ |   | _ |   |
| t |   |   |   | l |   | s |   | t |   |   |   | l |   | s |   |
| r |   |   |   | e |   | i |   | r |   |   |   | e |   | i |   |
| k |   |   |   | n |   | z |   | k |   |   |   | n |   | z |   |
| o |   |   |   | \ |   | e |   | o |   |   |   | \ |   | e |   |
| f |   |   |   |   |   | \ |   | f |   |   |   |   |   | \ |   |
| f |   |   |   | : |   |   |   | f |   |   |   | : |   |   |   |
| \ |   |   |   | s |   | : |   | \ |   |   |   | s |   | : |   |
|   |   |   |   | u |   | s |   |   |   |   |   | u |   | s |   |
| : |   |   |   | b |   | u |   | : |   |   |   | b |   | u |   |
| s |   |   |   | : |   | b |   | s |   |   |   | : |   | b |   |
| u |   |   |   | ` |   | : |   | u |   |   |   | ` |   | : |   |
| b |   |   |   | 0 |   | ` |   | b |   |   |   | 1 |   | ` |   |
| : |   |   |   | ` |   | 0 |   | : |   |   |   | ` |   | 1 |   |
| ` |   |   |   |   |   | ` |   | ` |   |   |   |   |   | ` |   |
| 0 |   |   |   |   |   |   |   | 1 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   | L |   | L |   | L |   |   |   | L |   | L |   |
| 2 |   |   |   | 2 |   | 2 |   | 2 |   |   |   | 2 |   | 2 |   |
| _ |   |   |   | _ |   | _ |   | _ |   |   |   | _ |   | _ |   |
| t |   |   |   | l |   | s |   | t |   |   |   | l |   | s |   |
| r |   |   |   | e |   | i |   | r |   |   |   | e |   | i |   |
| k |   |   |   | n |   | z |   | k |   |   |   | n |   | z |   |
| o |   |   |   | \ |   | e |   | o |   |   |   | \ |   | e |   |
| f |   |   |   |   |   | \ |   | f |   |   |   |   |   | \ |   |
| f |   |   |   | : |   |   |   | f |   |   |   | : |   |   |   |
| \ |   |   |   | s |   | : |   | \ |   |   |   | s |   | : |   |
|   |   |   |   | u |   | s |   |   |   |   |   | u |   | s |   |
| : |   |   |   | b |   | u |   | : |   |   |   | b |   | u |   |
| s |   |   |   | : |   | b |   | s |   |   |   | : |   | b |   |
| u |   |   |   | ` |   | : |   | u |   |   |   | ` |   | : |   |
| b |   |   |   | 2 |   | ` |   | b |   |   |   | 2 |   | ` |   |
| : |   |   |   | 5 |   | 2 |   | : |   |   |   | 5 |   | 2 |   |
| ` |   |   |   | 4 |   | 5 |   | ` |   |   |   | 5 |   | 5 |   |
| 2 |   |   |   | ` |   | 4 |   | 2 |   |   |   | ` |   | 5 |   |
| 5 |   |   |   |   |   | ` |   | 5 |   |   |   |   |   | ` |   |
| 4 |   |   |   |   |   |   |   | 5 |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | ` |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

| 

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| A |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| N |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| T |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   | L |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 2 |   | 2 |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   | _ |   |   |   |   |   |
| t |   |   |   |   |   |   |   | l |   | s |   |   |   |   |   |
| r |   |   |   |   |   |   |   | e |   | i |   |   |   |   |   |
| k |   |   |   |   |   |   |   | n |   | z |   |   |   |   |   |
| o |   |   |   |   |   |   |   | \ |   | e |   |   |   |   |   |
| f |   |   |   |   |   |   |   |   |   | \ |   |   |   |   |   |
| f |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | s |   | : |   |   |   |   |   |
|   |   |   |   |   |   |   |   | u |   | s |   |   |   |   |   |
| : |   |   |   |   |   |   |   | b |   | u |   |   |   |   |   |
| s |   |   |   |   |   |   |   | : |   | b |   |   |   |   |   |
| u |   |   |   |   |   |   |   | ` |   | : |   |   |   |   |   |
| b |   |   |   |   |   |   |   | 0 |   | ` |   |   |   |   |   |
| : |   |   |   |   |   |   |   | ` |   | 0 |   |   |   |   |   |
| ` |   |   |   |   |   |   |   |   |   | ` |   |   |   |   |   |
| 0 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   | L |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 2 |   | 2 |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   | _ |   |   |   |   |   |
| t |   |   |   |   |   |   |   | l |   | s |   |   |   |   |   |
| r |   |   |   |   |   |   |   | e |   | i |   |   |   |   |   |
| k |   |   |   |   |   |   |   | n |   | z |   |   |   |   |   |
| o |   |   |   |   |   |   |   | \ |   | e |   |   |   |   |   |
| f |   |   |   |   |   |   |   |   |   | \ |   |   |   |   |   |
| f |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | s |   | : |   |   |   |   |   |
|   |   |   |   |   |   |   |   | u |   | s |   |   |   |   |   |
| : |   |   |   |   |   |   |   | b |   | u |   |   |   |   |   |
| s |   |   |   |   |   |   |   | : |   | b |   |   |   |   |   |
| u |   |   |   |   |   |   |   | ` |   | : |   |   |   |   |   |
| b |   |   |   |   |   |   |   | 1 |   | ` |   |   |   |   |   |
| : |   |   |   |   |   |   |   | ` |   | 1 |   |   |   |   |   |
| ` |   |   |   |   |   |   |   |   |   | ` |   |   |   |   |   |
| 1 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| * |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   | L |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 2 |   | 2 |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   | _ |   |   |   |   |   |
| t |   |   |   |   |   |   |   | l |   | s |   |   |   |   |   |
| r |   |   |   |   |   |   |   | e |   | i |   |   |   |   |   |
| k |   |   |   |   |   |   |   | n |   | z |   |   |   |   |   |
| o |   |   |   |   |   |   |   | \ |   | e |   |   |   |   |   |
| f |   |   |   |   |   |   |   |   |   | \ |   |   |   |   |   |
| f |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | s |   | : |   |   |   |   |   |
|   |   |   |   |   |   |   |   | u |   | s |   |   |   |   |   |
| : |   |   |   |   |   |   |   | b |   | u |   |   |   |   |   |
| s |   |   |   |   |   |   |   | : |   | b |   |   |   |   |   |
| u |   |   |   |   |   |   |   | ` |   | : |   |   |   |   |   |
| b |   |   |   |   |   |   |   | 2 |   | ` |   |   |   |   |   |
| : |   |   |   |   |   |   |   | 5 |   | 2 |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | 4 |   | 5 |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | ` |   | 4 |   |   |   |   |   |
| 5 |   |   |   |   |   |   |   |   |   | ` |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| L |   |   |   |   |   |   |   | L |   | L |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | 2 |   | 2 |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   | _ |   |   |   |   |   |
| t |   |   |   |   |   |   |   | l |   | s |   |   |   |   |   |
| r |   |   |   |   |   |   |   | e |   | i |   |   |   |   |   |
| k |   |   |   |   |   |   |   | n |   | z |   |   |   |   |   |
| o |   |   |   |   |   |   |   | \ |   | e |   |   |   |   |   |
| f |   |   |   |   |   |   |   |   |   | \ |   |   |   |   |   |
| f |   |   |   |   |   |   |   | : |   |   |   |   |   |   |   |
| \ |   |   |   |   |   |   |   | s |   | : |   |   |   |   |   |
|   |   |   |   |   |   |   |   | u |   | s |   |   |   |   |   |
| : |   |   |   |   |   |   |   | b |   | u |   |   |   |   |   |
| s |   |   |   |   |   |   |   | : |   | b |   |   |   |   |   |
| u |   |   |   |   |   |   |   | ` |   | : |   |   |   |   |   |
| b |   |   |   |   |   |   |   | 2 |   | ` |   |   |   |   |   |
| : |   |   |   |   |   |   |   | 5 |   | 2 |   |   |   |   |   |
| ` |   |   |   |   |   |   |   | 5 |   | 5 |   |   |   |   |   |
| 2 |   |   |   |   |   |   |   | ` |   | 5 |   |   |   |   |   |
| 5 |   |   |   |   |   |   |   |   |   | ` |   |   |   |   |   |
| 5 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| ` |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

| 
| A **track image** or **block group image** contains two fields: a
  5-byte *header* and a variable amount of data that may or may not be
  compressed. The length field in the secondary lookup table entry
  (*L2_len* field shown just above) includes the length of both the
  5-byte header as well as the track or block group data.

The 5-byte *track or block group header* contains a 1 byte compression
indicator and 4 bytes that identify the track or block group. The format
of the identifier depends on whether the emulated device is CKD or FBA:

CKD Track Header

0

1

2

3

4

cmp

CC

HH

For **CKD**, the 2 byte CC is the cylinder number of the track image and
the HH is the head number. These numbers are stored in *big-endian* byte
order. When the compression indicator byte is zero the 5 byte header is
identical to the *Home Address* (or *HA*) for the track image.

The data --- which may or may not be compressed --- begins with the *R0*
count and ends with the *end-of-track* marker, which is a count field
containing ``FFFFFFFFFFFFFFFF`` (eight hex x'FF's). The Home Address
plus the uncompressed track data comprise the track image.

====================== ======== = = =
FBA Block Group Header              
====================== ======== = = =
0                      1        2 3 4
cmp                    nnnnnnnn     
====================== ======== = = =

For **FBA**, the 4 byte nnnnnnnn is the *big-endian* sector number of
the block group (i.e. the sector or block number of the first block in
the group). The block group data (the individual sectors in the block
group) --- which may or may not be compressed (depending on the *cmp*
flag) --- follows immediately after the block group header.

There is of course no end-of-track marker at the end of an FBA block
group. (FBA devices do not have tracks.)

Please note that, while the *FBA Block Group Header* is the first part
of the block group, it is *not* part of the compressed image. Only the
sectors themselves (which immediately follow the *Block Group Header*)
are actually compressed. FBA devices do not have Track Headers (Home
Addresses). The *FBA Block Group Header* should be considered an
internal structure and is never exposed to the guest.

The **cmp** compression indicator byte contains the value 0, 1 or 2. Any
other value is invalid:

0

   Data is uncompressed

1

   Data is compressed using zlib

2

   Data is compressed using bzip2

3...255

   (invalid)

| 
| **free space blocks** which are *not* part of the *initial free space
  chain table*, contain a 4 byte *offset* (8 bytes for CCKD64) to the
  *next* free space, a 4 byte (or 8 byte) *length* of the free space
  (which includes both the offset and length fields) and zero or more
  bytes of undefined data.

The format of free space blocks which *are* part of the *initial free
space chain table* (used only during initialization of the internally
maintained free space chain) are formatted *slightly differently*. (see
further below)

The contents of the actual free space *data* is entirely unpredictable,
and can be anything from previous track data to previously used
secondary lookup tables, etc. From the programmer's point of view it is
meaningless. It is just unpredictable/undefined file space.

The *fb_offnxt* and *fb_len* values, being numeric, are always kept in
little endian format:

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| F |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| R |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | 8 |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | . |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | . |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | . |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| f |   |   |   | f |   |   |   | d |   |   |   |   |   |   |   |
| b |   |   |   | b |   |   |   | a |   |   |   |   |   |   |   |
| _ |   |   |   | _ |   |   |   | t |   |   |   |   |   |   |   |
| o |   |   |   | l |   |   |   | a |   |   |   |   |   |   |   |
| f |   |   |   | e |   |   |   |   |   |   |   |   |   |   |   |
| f |   |   |   | n |   |   |   | . |   |   |   |   |   |   |   |
| n |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| x |   |   |   |   |   |   |   | . |   |   |   |   |   |   |   |
| t |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | . |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| a |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| t |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| a |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

| 

+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| C |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| D |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 6 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 4 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| F |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| R |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| E |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| B |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| L |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| K |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| f |   |   |   |   |   |   |   | f |   |   |   |   |   |   |   |
| b |   |   |   |   |   |   |   | b |   |   |   |   |   |   |   |
| _ |   |   |   |   |   |   |   | _ |   |   |   |   |   |   |   |
| o |   |   |   |   |   |   |   | l |   |   |   |   |   |   |   |
| f |   |   |   |   |   |   |   | e |   |   |   |   |   |   |   |
| f |   |   |   |   |   |   |   | n |   |   |   |   |   |   |   |
| n |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| x |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| t |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| d |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| a |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| t |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| a |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| . |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

The compressed device header's `free_off <#cdevhdr>`__ field contains
the file offset to either the first actual free space block (which then
contains the offset to the next free space block, etc), or else the file
offset to a "new" format *initial free space chain table*, explained
further below.

The minimum length of a free space is 8 bytes (16 bytes for CCKD64). The
free space chain is ordered by file offset and no two free spaces are
adjacent. The chain is terminated when a free space block has zero
offset to the next free space.

Each free space block in the chain (or the entire "new" format *initial
free space chain table*) is read when the file is first opened for
read-write, and are written only when the file is closed. The free space
chain itself however, is maintained internally in storage while the file
is opened and the system is running.

The compressed device header `free_off <#cdevhdr>`__ field contains
either the offset to the first free space block in the chain, or else to
a "new" format *initial free space chain table*. The compressed device
header `free_num <#cdevhdr>`__ field contains the count of the total
number of free spaces there are in the chain.

Whenever a dasd image file is closed, a "new" format *initial free space
chain table* is written out to the first available free space block that
is large enough to hold the entire table (or to the end of the file if a
large enough free space block was not found).

The "new" format *initial free space chain table* allows quick
initialization of the internal in-storage free space chain since each
individual free space block does not need to read from disk. Instead,
the location and size of *all* available free spaces are read in *all at
once* from the initial free space chain table that was written out when
the file was closed.

The "new" format **initial free space chain table** is a table of
(contiguous series of) **slightly modified free space blocks**, wherein
the first block in the chain is a dummy block containing the 8-byte
literal "**FREE_BLK**" in ASCII, and where the remaining blocks in the
table are identical in format to the above documented **free space
block** layout, *with the following important exceptions:*

#. The *fb_offnxt* field does *not* contain the file offset to the
   *next* free space, but rather instead contains the file offset of the
   *current* free space.
#. The *fb_len* field is itself accurate regarding the size (length) of
   the free space at that offset, but the free space blocks in the table
   themselves do not contain any actual free space *data*. That is to
   say, each free space block in the table is exactly 8 bytes in size
   (or 16 bytes for CCKD64).

The number of free space blocks in the table is *one more* than the
compressed device header `free_num <#cdevhdr>`__ field to account for
the first dummy block containing the "FREE_BLK" literal.

--------------

How It Works
------------

Reading
~~~~~~~

A track or block group image is read while executing a channel program
or by the *readahead* thread. An image has to be read before it is
updated or written to. An image may be *cached*. If an image is cached,
then the channel program may complete *synchronously*. This means that
if all the data a channel program accesses is cached and Hercules does
not have to perform physical I/O, then the channel program runs
synchronously within the SSCH or SIO instruction in the *CPU* thread.
All DASD channel programs are started synchronously. If a CCW in the
channel program requires physical I/O then the channel program is
interrupted and restarted at that CCW *asynchronously* in a *device I/O*
thread.

All compressed devices share a common cache; the devices can be a
mixture of FBA and/or CKD device types. Each cache entry contains a
pointer to a 64K buffer containing an uncompressed track or block group
image. If the track or block group image being read is not found in the
cache, then the oldest (or *least recently used* or *LRU*) entry that is
not *busy* is *stolen*. A cache entry is busy if it is being read, or
last accessed by an *active* channel program, or updated but not yet
written, or being written. If no cache entries are available then the
read must enter a *cache wait*. When images are detected to be accessed
sequentially then the readahead thread(s) may be signalled to read
following sequential images.

Writing
~~~~~~~

When a cache entry is updated or written to, a bit is turned on
indicating the cache entry has been updated. When a *cache wait* occurs,
or (more likely) during space recovery, a cache *flush* is performed.
When the cache is flushed, if any entries have the updated bit on, then
the writer thread(s) are signalled. The writer thread selects the oldest
cache entry with the updated bit on, compresses the image, and writes it
to the file. The new image is written to a new space in the file and
then the space previously occupied by the image is freed. In certain
circumstances, the image may be written under *stress*. A stress write
occurs when a reading thread is in a *cache wait* or when a high
percentage of cache entries are pending write. In this circumstance, the
compression parameters are relaxed to reduce the CPU requirements. An
image written under stress is likely to take up more space than the same
image written not under stress. The writer thread(s) run 1 nicer than
the CPU thread(s); compression is a CPU intensive activity.

Space Recovery
~~~~~~~~~~~~~~

Space recovery is also called, somewhat inaccurately, garbage
collection. The primary function of the space recovery thread, or
garbage collector, is to keep the emulated compressed DASD files as
small as possible. After all, that is the reason for using compressed
DASD files in the first place.

When a track or block group image is written, it is written to a new
location in the file. It is either written to an existing free space
within the file or to the end of the file, increasing the size of the
file. The space previously occupied by the image is freed, but it is not
immediately available for space allocation requests. Instead, it is
*pending* free space. It is assigned a *pending value* (typically 2)
that is decremented each space recovery cycle (typically every 10
seconds). When the pending value reaches 0 then the space is available
for allocation. This increases the chance that a track or block group
image can be recovered in the event of a failure.

The space recovery routine relocates track or block group images towards
the beginning of the file, causing free space to move towards the end of
the file. When a free space reaches the end of the file, it 'falls off',
that is, the file size is reduced.

Simply put, the space recovery routine first selects a space after a
sufficiently large *non-pending* free space. It then reads and writes
consecutive spaces using the normal cckd read and write routines. The
space read will become *pending* free space and will hopefully be
written to a *non-pending* free space occurring earlier in the file.
Sometimes it is necessary to write the space later in the file to
increase free space size earlier in the file. Left to itself, the space
recovery routine will eventually remove all free space from the file.
However, it is not intended to be a replacement for the ``cckdcomp``
utility; rather, the intent is to provide sufficient free space to
prevent excessive file growth.

Another function performed by space recovery is to relocate *L2*
(secondary lookup) tables towards the beginning of the file. This
simplifies *chkdsk* recovery and enables the chkdsk function to complete
more quickly during initialization.

Interestingly however, this is actually *not recommended*, as it tends
to make accessing track data *slower*, not faster. Instead, L2 tables
should be kept as close as possible to the actual track data they point
to. Enabling automatic garbage collection is therefore *not recommended*
and is thus the reason it is disabled by default starting with Hercules
4.5.

Starting with Hercules 4.5, CCKD will (if `gsmsgs <#gcmsgs>`__\ =1)
report the current garbage state (fragmentation state) of each dasd
image at startup so you can know which images you should perform manual
defragmentation for.

--------------

Runtime tuning options
----------------------

The **cckd** command and initialization statement can be used to affect
cckd processing. The **CCKD** initialization statement is specified as a
Hercules configuration file statement and supports the same options as
the **cckd** command explained below.

**Syntax:**

**cckd**

**help**

Display cckd help

**cckd**

**stats**

Display current cckd statistics

**cckd**

**opts**

Display current cckd options

**cckd**

opt=value

Set a cckd option.  Multiple options may be specified,

 

 

separated by a comma with no intervening blanks:

 

 

 

**comp=**\ n

  Compression to be used

 

**compparm=**\ n

  Compression parameter to be used

 

**debug=**\ n

  Turn CCW tracing debug messages on or off

 

**freepend=**\ n

  Set the free pending value

 

**fsync=**\ n

  Turn fsync on or off

 

**gcint=**\ n

  Garbage collector interval

 

**gcmsgs=**\ n

  Garbage collector messages

 

**gcparm=**\ n

  Garbage collector parameter

 

**gcstart=**\ n

  Start garbage collector

 

**linuxnull=**\ n

  Check for null linux tracks

 

**nosfd=**\ n

  Turn off stats report at close

 

**nostress=**\ n

  Turn stress writes on or off

 

**ra=**\ n

  Number of readahead threads

 

**raq=**\ n

  Readahead queue size

 

**rat=**\ n

  Number of tracks to readahead

 

**trace=**\ n

  Number of trace table entries

 

**wr=**\ n

  Number of writer threads

| 
| **Options:**

**comp=**\ n

 

| Compression type:

| **-1** Default
| **  0** None
| **  1** zlib
| **  2** bzip2

| Override the compression used for all cckd files. -1 (default) means
  don't override the compression.

**compparm=**\ n

 

| Compression parameter. A value between -1 and 9. -1 means use the
  default parameter. A higher value generally means more compression at
  the expense of cpu and/or storage.

**debug=**\ n

 

Enables or disables debug tracing. When enabled, additional CCKD trace
messages are displayed when CCW tracing is enabled for a CCKD dasd
device.

The default is **0** (disable CCKD trace mesages).

| You can specify **0** (disable debug tracing) or **1** (enable debug
  tracing).

**freepend=**\ n

 

Specifies the *free pending* value for freed space. When a track or
block group image is written the space it previously occupied is freed.
This space will not be available for future allocations until *n*
garbage collection intervals have completed. In the event of a
catastrophic failure, previously written track or block group images
should be recoverable if the current image has not yet been written to
the physical disk. By default the value is set to **-1**. This means
that if *fsync* is specified then the value is 1 otherwise it is 2. If 0
is specified then freed space is immediately available for new
allocations.

The default is **-1**.

| You can specify a number between **-1** and **4**.

**fsync=**\ n

 

Enables or disables *fsync*. When fsync is enabled, then the disk
emulation file is synchronized with the physical hard disk at the end of
a garbage collection interval (however, no more often than 5 seconds).
This means that if *freepend* is non-zero then if a catastrophic error
occurs then the emulated disks *should* be recovered coherently.
However, fsync may cause performance degradation depending on the host
operating system and/or the host operating system level.

The default is **0** (fsync disabled).

| You can specify **0** (disable fsync) or **1** (enable fsync).

**gcint=**\ n

 

Number of seconds the garbage collector thread waits during an interval.
At the end of an interval, the garbage collector performs space
recovery, flushes the cache, and optionally *fsync*\ s the emulation
file. (However, the file will not be *fsync*\ ed unless at least 5
seconds have elapsed since the last *fsync*).

The default *(as of Hercules version 4.5)* is **0**, meaning automatic
garbage collection is disabled.

You can specify a number between **0** and **60**. A value of 0 disables
the default automatic behavior of the garbage collector, converting it
to manual on-demand mode instead. When in manual mode, the garbage
collector will only run by specific demand via the 'gcstart' option, and
once started, will only run through one garbage collection cycle and
then exit, requiring you to manually start it again when desired. In
automatic mode (gcint > 0), the garbage collector will start itself
automatically and remain idle (but still running) between each garbage
collection cycle, automatically starting the next cycle every 'gcint'
seconds.

| It is recommended that this parameter remain set to its default value
  of 0 in order to prevent the garbage collector from running
  automatically. Rather, it is highly recommended that you manually
  defragment your dasd images yourself before starting Hercules, via
  either ``cckdcomp`` or ``cckdcomp64`` (*not recommended*) or
  `convto64 <https://github.com/SDL-Hercules-390/hyperion/blob/master/readme/README.CCKD64.md>`__
  instead (*recommended*).

**gcmsgs=**\ n

 

Set to 1 to display garbage collector messages.

| Set to **0** (the default) to suppress garbage collector messages.
  Garbage collector messages are issued (if enabled) during each garbage
  collection cycle as well as during startup to report the current
  garbage state of each image.

**gcparm=**\ n

 

A value affecting the amount of data moved during the garbage
collector's space recovery routine. The garbage collector determines an
amount of space to move based on the ratio of free space to used space
in an emulation file, and on the number of free spaces in the file. (The
garbage collector wants to reduce the free space to used space ratio and
the number of free spaces).

The value is logarithmic; a value of 8 means moving 2\ :sup:`8` the
selected value, while a negative value similarly decreases the amount to
be moved. Normally, 256K will be moved for a file in an interval.
Specifying a value of +8 can increase the amount to 64M. At least 64K
will always be moved. Interestingly, specifying a large value (such as
+8) may not increase the garbage collection efficiency correspondingly.

The default is **0**.

| You can specify any number between **-8** and **+8**.

**gcstart=**\ n

 

If set to 1 then space recovery will become active on any emulated disks
that have free space. Normally space recovery will ignore emulated disks
until they have been updated.

| The default is **0**.

**linuxnull=**\ n

 

If set to 1 then tracks written to 3390 cckd volumes that were
initialized with the *-linux* option will be checked if they are null
(that is, if all 12 4096 byte user records contain zeroes). This is used
by the dasdcopy utility.

| The default is **0**.

**nosfd=**\ n

 

If set to 1 the shadow file status and statistics report will not be
displayed when the device is closed.

| The default is **0**, meaning the shadow file status and statistics
  report will be displayed like normal when the device is closed.

**nostress=**\ n

 

Indicates whether *stress* writes will occur or not. A track or block
group may be written under stress when a high percentage of the cache is
pending write or when a device I/O thread is waiting for a cache entry.
When a stressed write occurs, the compression algorithm and/or
compression parm may be relaxed, resulting in faster compression but at
the expense of a slightly larger compressed image.

If *nostress* is set to one, then a stressed situation is ignored. You
would typically set this value to one when you want create the smallest
emulation file possible in exchange for a possible performance
degradation.

The default is **0**.

| You can specify **0** (enable stressed writes) or **1** (disable
  stressed writes).

**ra=**\ n

 

Number of readahead threads. When sequential track or block group access
is detected, some number (*rat=*) of tracks or block groups are queued
(*raq=*) to be read by one of the readahead threads.

The default is **2**.

| You can specify a number between **1** and **9**.

**raq=**\ n

 

Size of the readahead queue. When sequential track or block group access
is detected, some number (*rat=* ) of tracks or block groups are queued
in the readahead queue.

The default is **4**.

| You can specify a number between **0** and **16** (a value of zero
  disables readahead).

**rat=**\ n

 

Number of tracks or block groups to read ahead when sequential access
has been detected.

The default is **2**.

| You can specify a number between **0** and **16** (a value of zero
  disables readahead).

**trace=**\ n

 

Number of cckd trace entries. You would normally specify a non-zero
value when debugging or capturing a problem in cckd code. When the
problem occurs, you should enter the **k** Hercules console command
which will print the trace table entries.

The default is **64**.

| You can specify a number between **0** and **200000**. Each entry
  represents 128 bytes. Normally, for debugging, I use 100000.

**wr=**\ n

 

Number of writer threads. When the cache is *flushed* updated cache
entries are marked write pending and a writer thread is signalled. The
writer thread compresses the track or block group and writes the
compressed image to the emulation file. A writer thread is cpu-intensive
while compressing the track or block group and I/O-intensive while
writing the compressed image. The writer thread runs one *nicer* than
the CPU thread(s).

The default is **2**.

| You can specify a number between **1** and **9**.

--------------

Utilities
---------

+------------------+--------------------------------------------------+
| **ckd2cckd  **   |                                                  |
+------------------+--------------------------------------------------+
| **cckd2ckd  **   |                                                  |
+------------------+--------------------------------------------------+
| **fba2cfba  **   |                                                  |
+------------------+--------------------------------------------------+
| **cfba2fba  **   |                                                  |
+------------------+--------------------------------------------------+
| **ckd2cckd64  ** |                                                  |
+------------------+--------------------------------------------------+
| **cckd642ckd  ** |                                                  |
+------------------+--------------------------------------------------+
| **fba2cfba64  ** |                                                  |
+------------------+--------------------------------------------------+
| **cfba642fba  ** |                                                  |
+------------------+--------------------------------------------------+
|                  | These utilities are deprecated. Use the below    |
|                  | **dasdcopy** / **dasdcopy64** utility instead.   |
+------------------+--------------------------------------------------+

| 

+-----------------------------------+-----------------------------------+
| **dasdcopy  **                    | *[-options] ifile [sf=sfile]      |
|                                   | ofile*                            |
+-----------------------------------+-----------------------------------+
| **dasdcopy64  **                  | *[-options] ifile [sf=sfile]      |
|                                   | ofile*                            |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | Copy / convert dasd image files   |
|                                   | from one type to another.         |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | +--------------+--------------+   |
|                                   | | **-q  **     | quiet mode   |   |
|                                   | |              | (don't       |   |
|                                   | |              | display      |   |
|                                   | |              | status)      |   |
|                                   | +--------------+--------------+   |
|                                   | | **-r  **     | replace the  |   |
|                                   | |              | output file  |   |
|                                   | |              | if it exists |   |
|                                   | +--------------+--------------+   |
|                                   | | **-z  **     | compress     |   |
|                                   | |              | using zlib   |   |
|                                   | |              | (default)    |   |
|                                   | +--------------+--------------+   |
|                                   | | **-bz2  **   | compress     |   |
|                                   | |              | using bzip2  |   |
|                                   | +--------------+--------------+   |
|                                   | | **-0  **     | don't        |   |
|                                   | |              | compress     |   |
|                                   | |              | output       |   |
|                                   | +--------------+--------------+   |
|                                   | | **-blks n    | size of      |   |
|                                   | |  **          | output fba   |   |
|                                   | |              | file         |   |
|                                   | +--------------+--------------+   |
|                                   | | **-cyls n    | size of      |   |
|                                   | |  **          | output ckd   |   |
|                                   | |              | file         |   |
|                                   | +--------------+--------------+   |
|                                   | | **-a  **     | output ckd   |   |
|                                   | |              | file will    |   |
|                                   | |              | have alt     |   |
|                                   | |              | cyls         |   |
|                                   | +--------------+--------------+   |
|                                   | | **-lfs  **   | create       |   |
|                                   | |              | single large |   |
|                                   | |              | output file  |   |
|                                   | +--------------+--------------+   |
|                                   | | **-o type    | output file  |   |
|                                   | |  **          | type: CKD,   |   |
|                                   | |              | CCKD, FBA,   |   |
|                                   | |              | CFBA.        |   |
|                                   | |              | *(dasdcopy/  |   |
|                                   | |              | dasdcopy64)* |   |
|                                   | |              | output file  |   |
|                                   | |              | type: CKD64, |   |
|                                   | |              | CCKD64,      |   |
|                                   | |              | FBA64,       |   |
|                                   | |              | CFBA64.      |   |
|                                   | |              | *(           |   |
|                                   | |              | dasdcopy64)* |   |
|                                   | +--------------+--------------+   |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | **Note:** *Any shadow file        |
|                                   | specified as input is merged into |
|                                   | the output,*                      |
+-----------------------------------+-----------------------------------+
|                                   | *rendering the input shadow file  |
|                                   | obsolete once the copy            |
|                                   | completes.*                       |
+-----------------------------------+-----------------------------------+

| 

+-----------------------------------+-----------------------------------+
| **cckdcdsk  **                    | *[-v] [-f] [-ro] [-level]         |
|                                   | filename1 [filename2 ...]*        |
+-----------------------------------+-----------------------------------+
| **cckdcdsk64  **                  | *[-v] [-f] [-ro] [-level]         |
|                                   | filename1 [filename2 ...]*        |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | Check the integrity and repair /  |
|                                   | recover one or more damaged       |
|                                   | compressed files.                 |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | +--------------+--------------+   |
|                                   | | **-v  **     | Display      |   |
|                                   | |              | version and  |   |
|                                   | |              | exit.        |   |
|                                   | +--------------+--------------+   |
|                                   | | **-f  **     | Perform      |   |
|                                   | |              | check even   |   |
|                                   | |              | if the       |   |
|                                   | |              | *OPENED* bit |   |
|                                   | |              | is on.       |   |
|                                   | +--------------+--------------+   |
|                                   | | **-ro  **    | Open the     |   |
|                                   | |              | file(s)      |   |
|                                   | |              | *read-only*. |   |
|                                   | |              | The file     |   |
|                                   | |              | will not be  |   |
|                                   | |              | repaired.    |   |
|                                   | +--------------+--------------+   |
|                                   | | **-level  ** | A number     |   |
|                                   | |              | from 0 .. 4  |   |
|                                   | |              | indicating   |   |
|                                   | |              | the level of |   |
|                                   | |              | checking /   |   |
|                                   | |              | recovery:    |   |
|                                   | |              | **0**        |   |
|                                   | |              | Minimal      |   |
|                                   | |              | checking     |   |
|                                   | |              | (default):   |   |
|                                   | |              | hdr, chdr,   |   |
|                                   | |              | l1, l2       |   |
|                                   | |              | **1**        |   |
|                                   | |              | Normal       |   |
|                                   | |              | checking:    |   |
|                                   | |              | hdr, chdr,   |   |
|                                   | |              | l1, l2, free |   |
|                                   | |              | spaces.      |   |
|                                   | |              | **2**        |   |
|                                   | |              | Extra        |   |
|                                   | |              | checking:    |   |
|                                   | |              | hdr, chdr,   |   |
|                                   | |              | l1, l2, free |   |
|                                   | |              | spaces,      |   |
|                                   | |              | track hdrs.  |   |
|                                   | |              | **3**        |   |
|                                   | |              | Maximal      |   |
|                                   | |              | checking:    |   |
|                                   | |              | hdr, chdr,   |   |
|                                   | |              | l1, l2, free |   |
|                                   | |              | spaces,      |   |
|                                   | |              | track hdrs,  |   |
|                                   | |              | track data.  |   |
|                                   | |              | **4**        |   |
|                                   | |              | Recover      |   |
|                                   | |              | everything   |   |
|                                   | |              | (without     |   |
|                                   | |              | using any    |   |
|                                   | |              | metadata).   |   |
|                                   | +--------------+--------------+   |
+-----------------------------------+-----------------------------------+

| 

+-----------------------------------+-----------------------------------+
| **cckdcomp  **                    | *[-v] [-f] [-level] filename1     |
|                                   | [filename2 ...]*                  |
+-----------------------------------+-----------------------------------+
| **cckdcomp64  **                  | *[-v] [-f] [-level] filename1     |
|                                   | [filename2 ...]*                  |
+-----------------------------------+-----------------------------------+
|                                   | Remove all free space from a      |
|                                   | compressed file or files.         |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | +--------------+--------------+   |
|                                   | | **-v  **     | Display      |   |
|                                   | |              | version and  |   |
|                                   | |              | exit.        |   |
|                                   | +--------------+--------------+   |
|                                   | | **-f  **     | Perform      |   |
|                                   | |              | compress     |   |
|                                   | |              | even if the  |   |
|                                   | |              | *OPENED* bit |   |
|                                   | |              | is on.       |   |
|                                   | +--------------+--------------+   |
|                                   | | **-level  ** | A number 0   |   |
|                                   | |              | .. 4         |   |
|                                   | |              | indicating   |   |
|                                   | |              | the cckdcdsk |   |
|                                   | |              | level.       |   |
|                                   | +--------------+--------------+   |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | **NOTE:** *Use of the cckdcomp64  |
|                                   | utility is discouraged. It is     |
|                                   | recommended that you use          |
|                                   | the*\ `convt                      |
|                                   | o64 <https://github.com/SDL-Hercu |
|                                   | les-390/hyperion/blob/master/read |
|                                   | me/README.CCKD64.md>`__\ *utility |
|                                   | instead, as it is both faster and |
|                                   | much safer than cckdcomp64. If    |
|                                   | you are still using 32-bit CCKD,  |
|                                   | it is hightly recommended that    |
|                                   | you convert all of your Hercules  |
|                                   | dasds to the                      |
|                                   | new*\ `CC                         |
|                                   | KD64 <https://github.com/SDL-Herc |
|                                   | ules-390/hyperion/blob/master/rea |
|                                   | dme/README.CCKD64.md>`__\ *format |
|                                   | instead.*                         |
+-----------------------------------+-----------------------------------+

| 

+-----------------------------------+-----------------------------------+
| **cckdswap  **                    | *[-v] [-f] [-level] filename1     |
|                                   | [filename2 ...]*                  |
+-----------------------------------+-----------------------------------+
| **cckdswap64  **                  | *[-v] [-f] [-level] filename1     |
|                                   | [filename2 ...]*                  |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | Change the *endianness* or        |
|                                   | *byte-order* of a compressed file |
|                                   | or files                          |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
|                                   | +--------------+--------------+   |
|                                   | | **-v  **     | Display      |   |
|                                   | |              | version and  |   |
|                                   | |              | exit.        |   |
|                                   | +--------------+--------------+   |
|                                   | | **-f  **     | Perform swap |   |
|                                   | |              | even if the  |   |
|                                   | |              | *OPENED* bit |   |
|                                   | |              | is on.       |   |
|                                   | +--------------+--------------+   |
|                                   | | **-level  ** | A number 0   |   |
|                                   | |              | .. 4         |   |
|                                   | |              | indicating   |   |
|                                   | |              | the cckdcdsk |   |
|                                   | |              | level.       |   |
|                                   | +--------------+--------------+   |
+-----------------------------------+-----------------------------------+

--------------

|back|

.. |back| image:: images/back.gif
   :target: ##
