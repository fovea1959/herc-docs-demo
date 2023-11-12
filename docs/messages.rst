##################
Messages and Codes
##################

Version 4 Release 00
First Edition, November 21, 2015
HEMC040000- 00

Preface
=======

Edition information
-------------------

This edition applies to the Hercules S/370, ESA/390 and z/Architecture
Emulator Release 4.00.0 and to all subsequent versions, releases and
modifications until otherwise indicated in new editions. Make sure you
are using the correct edition for the level of software you are using.

What this book is about
---------------------------

This book describes all messages and codes of the Hercules Emulator. For
guidance in operating or debugging Hercules, for a general overview or
for guidance in installation of the product, additional manuals are
available. Please see Chapter “Related Publications” for more
information on these manuals. Please note that some information can be
found in more than one manual. This redundancy is not intended to
unnecessarily expand the manuals but should help to find all necessary
information in one place.

Who should read this book
-------------------------

This book is mainly intended for people who are responsible for
operating the Hercules Emulator. It serves as a starting point for
resolving errors in the Hercules environment.

What you need to know to understand this book
---------------------------------------------

To understand this book you should be somewhat familiar with the
Microsoft Windows and/or Linux ope- rating systems. You should also be
familiar with the installation and operation of the Hercules Emulator
itself. Last but not least you should be familiar with the hardware and
software of IBM mainframe environments and their underlying ideas and
concepts, as Hercules emulates IBM mainframe hardware.

How to use this book
--------------------

This book is designed as a reference book for all messages and codes of
the Hercules Emulator and related products. It is not intended to be
read chapter by chapter.

Revision Notice
---------------

Hercules Release: Version 4 Release 00 Modification 0 Publication
Number: HEMC0 40000 SoftCopy Name: HerculesMessagesandCodes Revision
Number: HEMC040000- 00 Date: November 21, 2015

Readers Comments
--------------------

If you like or dislike anything about this book please send an email to
the address below. Feel free to comment on any errors or lack of
clarity. Please limit your comments on the information in this specific
book and also include the “Revision Notice” just above. Thank you for
your help.

Send your comments by email to the Hercules-390 discussion group:
hercules-390@yahoogroups.com

Legal Advice
------------

Hercules implements only the raw S/370, ESA/390, and z/Architecture
instruction set, it does not provide any operating system facilities.
This means that you need to provide an operating system or standalone
program which Hercules can load from an emulated disk or tape device.
You will have to write the operating system or standalone program
yourself, unless you possess a license from IBM to run one of their
operating systems on your PC, or use IBM programs and operating systems
which have been placed in the public domain.

NOTE: It is YOUR responsibility to comply with the terms of the license
for the operating system you intend to run on the Hercules Emulator.

Trademarks
----------

The following is a list of trademark acknowledgements and copyright
notices of product and company names mentioned in this book. Other
product and company names in this book, which are not listed below may
be the trademarks or registered trademarks of their respective owners.

-  IBM, System/370, ESA/390, z/Architecture, MVS, OS/390, z/OS, VM,
   VM/ESA, z/VM, VSE, VSE/ESA, z/VSE are trademarks or registered
   trademarks of International Business Machines Corporation (IBM).
-  Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows
   Server 2008, Visual C++ Toolkit, Visual C++ Express are trademarks of
   Microsoft Corporation.
-  Linux is a trademark owned by Linus Torvalds. The Linux Mark
   Institute is the exclusive licensor of the Linux trademark on behalf
   of its owner Linus Torvalds.
-  WinPcap is copyrighted by NetGroup, Politecnico di Torino (Italy).
-  Cygwin is copyrighted by Red Hat, Inc.
-  Vista tn3270 is copyrighted by Tom Brennan Software.
-  Pentium, XEON are trademarks or registered trademarks of Intel
   Corporation.
-  Athlon, Opteron are trademarks or registered trademarks of Advanced
   Micro Devices (AMD), Inc.
-  Xmit Manager is copyrighted by Neal Johnston-Ward.
-  FLEX-ES is a registered trademark of Fundamental Software, Inc.

Acknowledgements
----------------

The Hercules manuals would not have been possible without the assistance
of many people and I would like to thank all those who helped me. In
particular I would like to thank:

-  The Hercules developers for their documentation on various websites
   from which I derived a great deal of information.
-  Roger Bowler and Fish for proof-reading the manuals.
-  Loris Degoianni for allowing me to use parts of the original WinPcap
   documentation.
-  Tom Brennan for allowing me to use parts of his Vista tn3270
   documentation.
-  My colleagues for working with early previews of the documentation,
   beginning with just a few pages.
-  Mike Cairns for reviewing and editing the manuals.
-  Robert Allan for providing the “Linux Installation” part.
-  Lutz Mader for providing the “Mac OS X Installation” part.

If anyone feels they have been forgotten on this list please let me
know. Peter Glanzmann

Summary of changes
=====================

Version 4, First Edition (HEMC040000-00)
----------------------------------------

This section describes briefly the various changes that have been made
in the “Messages and Codes” manual related to the previous edition. The
most significant changes made in this edition of the manual are the
following:

-  Chapter 2 (Related Publications): New manual “Operations and
   Utilities Guide” added.
-  Chapter 3 (Summary of changes) added.
-  Chapter 4 (Introduction): New section “Message Standardization”
   added.
-  Chapter 4 (Introduction): New section “Message Format (Hercules
   V4.00)” added.
-  Chapter 4 (Introduction): New section “Component List (Hercules
   V4.00)” added.
-  Chapter 4 (Introduction): New section “Debug Option” added.
-  Part I: New Messages added. Not all messages are documented yet.
-  Appendix A. Message Index (New → Old) added.
-  Appendix B. Message Index (Old → New) added.
-  Appendix C. Links: List of links updated.

Introduction
============

Overview
--------

This Chapter gives an introduction to the messages and codes of the
Hercules Emulator and related tools, as well as the messages written
from the various standalone utility programs.

Locations
---------

All messages are written to the Hercules console (native console as well
as the Hercules Windows GUI / Hercules Studio) and to the Hercules log
file, if a log file is specified in the startup command.

Message Standardization
-----------------------

Hercules version 4.00 introduces the message standardization. With this
major rework of the message processing it is ensured that messages are
issued in a consistent way throughout the various Hercules functions. It
is also ensured that message numbers can not be assigned twice. Due to
this change in the message processing it may be necessary for users to
review existing HAO (Hercules Automated Operator) rules and self written
scripts. Message indices in the appendices of this manual which show the
relationship between old and new message identifiers will reduce the
amount of work that has to be invested in these tasks. The cross
reference tables can be found later on in this book.

Message Format (Hercules V3.07)
-----------------------------------

Up to Hercules version 3.07 all Hercules-issued messages had the
following format:

H H C m m n n n s text

The following table explains the various parts of the old message
format:

Part Explanation

HHC HHC is the message prefix for Hercules. All Hercules messages will
have this prefix.

mm “mm” be found in section specifies the component4.6. that issued the
message. A detailed list of all components can

nnn “nnn” specifies the message number. This number is assigned more or
less sequentially.

s “s” is the message severity. Details can be found in section 4.8.

text “text” is the actual message text.

Table 1: Message Format until Hercules V3.

Message Format (Hercules V4.00)
-------------------------------

Beginning with Hercules version 4.00 all Hercules-issued messages have
the following format:

H H C n n n n n s text

The following table explains the various parts of the new message
format:

Part Explanation

HHC HHC is the message prefix for Hercules. All Hercules messages will
have this prefix.

nnnnn “nnnnn” specifies the message number. This number is assigned more
or less sequentially.

s “s” is the message severity. Details can be found in section 4.8.

text “text” is the actual message text.

Table 2: Message Format since Hercules V4.

Component List (Hercules V3.07)
-------------------------------

The following table presents all the Hercules component prefixes from
the old message format, along with a short description of the issuing
component.

Prefix Component

AO Hercules Automatic Operator

CA Communication Adapter Emulation

CF Configuration File Processing

CP CPU Emulation

CT Channel-to-Channel Adapter Emulation

CU CCKD Utilities

DA DASD Emulation (CKD, CCKD and FBA)

DC DASDCOPY Utility

DG Dyngui.DLL

DI DASDINIT Utility

DL DASDLOAD Utility

Prefix Component

DS DASDISUP Utility

DT DASDCAT Utility

DU DASD Utilities Common Functions

HD Hercules Dynamic Loader

HE HETINIT Utility

HG HETGET Utility

HM HETMAP Utility

HT HTTP Server

HU HETUPD Utility

IF Network Interface Configuration Handler (hercifc)

IN Hercules Initialization

LC LCS Emulation

LG System Log Functions

PN Hercules Control Panel Command Messages

PR Printer Emulation

PU Card Punch Emulation

RD Card Reader Emulation

SD Socket Devices Common Functions

TA Tape Device Emulation

TC TAPECOPY Utility

TE Terminal Emulation

TM TAPEMAP Utility

TS TAPESPLT Utility

TT TOD Clock and Timer Services

TU TUN / TAP Driver Support

VM VM / CP Emulation Facility

Table 3: Hercules Component List (V3.07)
----------------------------------------

Component List (Hercules V4.00)
-------------------------------

The following table presents all the Hercules components and the
assigned messages ranges.

Message Range Component

HHC00000s - HHC00099s General Messages

HHC00100s - HHC00199s General Messages

HHC00200s - HHC00299s Tape Device Emulation

HHC00300s - HHC00399s DASD Device Emulation (CCKD)

HHC00400s - HHC00499s DASD Device Emulation (CKD)

HHC00500s - HHC00599s DASD Device Emulation (FBA)

HHC00600s - HHC00699s DASD Device Emulation (SCE)

HHC00700s - HHC00799s Shared Device Server

HHC00800s - HHC00899s CPU Emulation

HHC00900s - HHC00999s CTC Adapter Emulation

HHC01000s - HHC01099s Communication Adapter Emulation

HHC01100s - HHC01199s Printer Emulation

HHC01200s - HHC01299s Card Punch Emulation / Card Reader Emulation

HHC01300s - HHC01399s Channel-to-Channel Adapter Emulation

HHC01400s - HHC01499s Hercules Initialization and Shutdown

HHC01500s - HHC01599s Dynamic Loader

HHC01600s - HHC01699s Panel Communication

HHC01700s - HHC01799s ECPS:VM Support

HHC01800s - HHC01899s HTTP Server

HHC01900s - HHC01999s Diagnose Calls

HHC02000s - HHC02099s Suspend / Resume Processing

HHC02100s - HHC02199s System Logger

HHC02200s - HHC02299s Command Processing

HHC02300s - HHC02399s IEEE Component

HHC02400s - HHC02499s DASD Utilities

HHC02500s - HHC02599s DASD Utilities

HHC02600s - HHC02699s Various Utilities

HHC02700s - HHC02799s Tape Utilities

HHC04100s - HHC04199s Windows Specific Components

HHC17000s - HHC17099s Query Commands

HHC90000s - HHC90999s Debug Messages

Table 4: Hercules Component List (V4.00)
----------------------------------------

Message Severity
----------------

The following table shows the different message severities, issued by
the Hercules Emulator.

::

   Code Meaning
   S Severe error message. This type of error causes immediate termination of Hercules.

::

   E Error continue message. The function being executed did not execute correctly but Herculesrunning. should

::

   W Warning message. Not necessarily an error but something to take note of and possibly correct.
   I Information message. General messages that do not require any further action.
   A Action message. Hercules needs input, you need to do something.
   D Debug message.

Table 5: Message Severity
-------------------------

Debug Option
------------

If DEBUG is defined, either by a “#define debug” statement or by
“configure –enable-debug” and OPTION_DEBUG_MESSAGES is enabled in
“featall.h” then all messages will be prefixed by “sourcefile.c:lineno”
where sourcefile is the name of the C source file and lineno is the line
number where the message has been issued.

Example: hsccmd.c 2597 HHC02204I Value ‘message level’ set to ‘debug’

Debug messages can also be switched on by issuing the panel command
“MSGLEVEL DEBUG”.

Message Examples
----------------

The following figure shows some Hercules messages. Although these
messages are from a real IPL, please note that they are not complete i.e
some messages have been deleted. The messages are shown just as an
example of how messages look, especially the variable parts of messages.

HHC01413I Hercules version 4.0. HHC01414I (c) Copyright 1999-2010 by
Roger Bowler, Jan Jaeger, and others HHC01415I Built on Feb 07 2011 at
05:30: HHC01416I Build information: HHC01417I Windows (MSVC) build for
AMD HHC01417I Modes: S/370 ESA/390 z/Arch HHC01417I Max CPU Engines: 8
HHC01417I Using fthreads Threading Model HHC01417I Using FishIO
HHC01417I Dynamic loading support HHC01417I Using shared libraries
HHC01417I HTTP Server support HHC01417I No SIGABEND handler HHC01417I
Regular Expressions support HHC01417I Automatic Operator support
HHC01417I Machine dependent assists: cmpxchg1 cmpxchg4 cmpxchg HHC01417I
Running on GOOFY Windows-6.1.7600. NT , Intel(R) x64 MP= HHC01508I HDL:
loadable module directory is ‘D:/Hercules/’ HHC00150I Crypto module
loaded (c) Copyright 2003-2010 by Bernard van der Helm HHC00151I
Activated facility: ‘Message Security Assist’ HHC00151I Activated
facility: ‘Message Security Assist Extension 1, 2, 3 and 4’ HHC00100I
Thread id 00001204, prio 15, name ‘Processor CP00’ started HHC00100I
Thread id 000012B8, prio 0, name ‘Timer’ started HHC00811I Processor
CP00: architecture mode ‘z/Arch’ HHC02203I auto_scsi_mount: NO HHC01474I
Using ‘internal’ codepage conversion table ‘DEFAULT’ HHC00827I Processor
CP00: engine 00 type 0 set: ‘CP’ HHC00827I Processor CP01: engine 01
type 0 set: ‘CP’ HHC00827I Processor CP02: engine 02 type 0 set: ‘CP’
HHC00827I Processor CP03: engine 03 type 0 set: ‘CP’ HHC01802I HTTP
server using root directory D:/Hercules/html/ HHC01807I HTTP server
signaled to start HHC01435I Config file
‘D:/MVS/CONF/MVS_V38J_V400.CONF’: will ignore include errors HHC00100I
Thread id 0000116C, prio 0, name ‘HTTP server’ started HHC01437I Config
file[39] ‘D:/MVS/CONF/MVS.CONF’ HHC01802I HTTP server using root
directory D:/Hercules/html/ HHC01803I HTTP server waiting for requests
on port 80 HHC02204I logopts set to TIMESTAMP HHC00100I Thread id
00001230, prio 0, name ‘Processor CP01’ started HHC00811I Processor
CP01: architecture mode ‘S/370’ HHC00100I Thread id 00001194, prio 0,
name ‘Processor CP02’ started HHC00811I Processor CP02: architecture
mode ‘S/370’ HHC00100I Thread id 00001180, prio 0, name ‘Processor CP03’
started HHC00811I Processor CP03: architecture mode ‘S/370’ HHC00100I
Thread id 00001034, prio 0, name ‘Shared device server 0.1’ started
HHC00737I Shared: waiting for shared device requests on port 3990
HHC01042I 0:000E COMM: device bound to socket ‘192.168.0.101:14031’
HHC00100I Thread id 0000038C, prio 0, name ‘Socket device listener’
started HHC01042I 0:000F COMM: device bound to socket
‘192.168.0.101:14032’ HHC00100I Thread id 00000D40, prio 0, name
‘Console connection’ started HHC01024I Waiting for console connections
on port 3270 . . .

. . . HHC00013I Herc command: ‘exit’ HHC01420I Begin Hercules shutdown
HHC01423I Calling termination routines HHC01500I HDL: begin shutdown
sequence HHC01501I HDL: calling ‘term_sockdev’ HHC00101I Thread id
0000038C, prio 0, name ‘Socket device listener’ ended HHC01502I HDL:
calling ‘term_sockdev’ complete HHC01501I HDL: calling
‘shared_device_manager_shutdown’ HHC00101I Thread id 000002A8, prio 0,
name ‘Hercules Automatic Operator’ ended HHC01502I HDL: calling
‘shared_device_manager_shutdown’ complete HHC01501I HDL: calling
‘http_shutdown’ HHC00101I Thread id 0000116C, prio 0, name ‘HTTP server’
ended HHC01502I HDL: calling ‘http_shutdown’ complete HHC01501I HDL:
calling ‘release_config’ HHC00101I Thread id 00001204, prio -15, name
‘Processor CP00’ ended HHC00101I Thread id 00001230, prio 0, name
‘Processor CP01’ ended HHC00101I Thread id 00001194, prio 0, name
‘Processor CP02’ ended HHC00101I Thread id 00001180, prio 0, name
‘Processor CP03’ ended HHC01465I 0:000C device detached HHC00101I Thread
id 000012B8, prio -20, name ‘Timer’ ended HHC01465I 0:000D device
detached HHC01465I 0:000E device detached HHC01465I 0:000F device
detached HHC01465I 0:030E device detached HHC01465I 0:0010 device
detached HHC01465I 0:0011 device detached HHC01465I 0:00C0 device
detached HHC01465I 0:00C1 device detached HHC01465I 0:00C2 device
detached HHC01465I 0:00C3 device detached HHC01465I 0:00C4 device
detached . . . HHC00101I Thread id 00000D40, prio 0, name ‘Console
connection’ ended HHC00101I Thread id 00000484, prio 0, name ‘Read-ahead
thread-1’ ended HHC00101I Thread id 00000B60, prio 0, name ‘Read-ahead
thread-2’ ended HHC00101I Thread id 000008A8, prio 0, name ‘Garbage
collector’ ended HHC00101I Thread id 00001118, prio 0, name ‘Writer
thread-2’ ended HHC00101I Thread id 00000C10, prio 0, name ‘Writer
thread-1’ ended HHC01465I 0:034B device detached HHC01465I 0:0480 device
detached HHC01465I 0:0481 device detached HHC01465I 0:0E20 device
detached HHC01427I Main storage released HHC01427I Expanded storage
released HHC01422I Configuration released HHC01502I HDL: calling
‘release_config’ complete HHC01501I HDL: calling ‘hdl_term’ HHC01512I
HDL: begin termination sequence HHC01513I HDL: calling module cleanup
routine ‘dyngui’ HHC01514I HDL: module cleanup routine ‘dyngui’ complete
HHC01513I HDL: calling module cleanup routine ‘*Hercules’ HHC01514I HDL:
module cleanup routine ’*\ Hercules’ complete HHC01515I HDL: termination
sequence complete HHC01502I HDL: calling ‘hdl_term’ complete HHC01501I
HDL: calling ‘logger_term’

Figure 1: Sample Messages

Part I: New Messages
--------------------


HHC00001s – HHC00069s (General)
===============================

HHC00001I
---------

HHC00001I is not yet documented

Explanation …

Severity …

Action …

HHC00002E
---------

HHC000 02 E is not yet documented

Explanation …

Severity …

Action …

HHC00003E
---------

HHC00003E is not yet documented

Explanation …

Severity …

Action …

HHC00004I
---------

HHC00004I is not yet documented

Explanation …

Severity …

Action …

HHC00005W
---------

HHC00005W is not yet documented

Explanation …

Severity …

Action …

HHC00006I
---------

HHC00006I is not yet documented

Explanation …

Severity …

Action …

HHC00007I
---------

HHC00007I is not yet documented

Explanation …

Severity …

Action …

HHC00008I
---------

HHC00008I is not yet documented

Explanation …

Severity …

Action …

HHC00009I
---------

HHC00009I is not yet documented

Explanation …

Severity …

Action …

HHC00010A
---------

HHC00010A is not yet documented

Explanation …

Severity …

Action …

HHC00011E
---------

HHC00011E is not yet documented

Explanation …

Severity …

Action …

HHC00012W
---------

HHC00012W is not yet documented

Explanation …

Severity …

Action …

HHC00013I
---------

HHC00013I Herc command: ‘cmd’

Explanation Console command ‘cmd’ has been issued at the Hercules
console. See also message HHC01603I.

Severity Information.

Action None. This is an informational message.

HHC00014E
---------

HHC00014E is not yet documented

Explanation …

Severity …

Action …

HHC00015E
---------

HHC00015E is not yet documented

Explanation …

Severity …

Action …

HHC00016E
---------

HHC00016E is not yet documented

Explanation …

Severity …

Action …

HHC00017I
---------

HHC00017I is not yet documented

Explanation …

Severity …

Action …

HHC00018I
---------

HHC00018I Hercules is running in elevated mode

Explanation Hercules is running in elevated mode on a Windows system
(with administrative rights).

Severity Information.

Action None. This is an informational message.

HHC00018W
---------

HHC00018W Hercules is not running in elevated mode

Explanation Hercules is not running in elevated mode on a Windows system
(without administrative rights).

Severity Warning.

Action If you need administrative rights for Hercules (e.g. for
CTCI-WIN) then restart Hercules from a command prompt started as
administrator. If no administrative rights are necessary then you can
savely ignore this message.

HHC00069I
---------

HHC00069I is not yet documented

Explanation …

Severity …

Action …

HHC00070s – HHC00099s (Hercules Automatic Operator)
===================================================

HHC00070E
---------

HHC00070E Unknown hao command, valid commands are: hao tgt : define
target rule (pattern) to react on hao cmd : define command for
previously defined rule hao list : list all rules/commands or only at
index hao del : delete the rule at index hao clear : delete all rules
(stops automatic operator)

Explanation The entered HAO command is unknown to the Hercules Automatic
Operator.

Severity Error.

Action Enter a valid HAO command from the list of message HHC00070E.

HHC00071E
---------

HHC00071E The ‘command’ was not added because table is full; table size
is nn

Explanation The rule (target and command) could not be added to the HAO
table because the table is already full. The value nn displays the
current table size.

Severity Error.

Action To add another rule either delete an existing rule to free a
table entry or rebuild Hercules with an in- creased table size (“#define
HAO_MAXRULE nn” in file hao.c).

HHC00072E
---------

HHC00072E The command ‘cmd’ given, but the command ‘tgt’ was expected
HHC00072E The command ‘tgt’ given, but the command ‘cmd’ was expected

Explanation

HAO entries must be defined in the correct order. To define a rule,
first a “HAO TGT target” command must be given, followed immediately by
a “HAO CMD command”. These error messages will appear in case of an
incorrect order of the HAO commands or in case of two subsequent “HAO
TGT” or two sub- sequent “HAO CMD” commands:

-  In case of the first error message a “HAO CMD command” has been
   entered but a “HAO TGT target” command has been expected. This can be
   the case if two “HAO CMD” commands have been entered immediately one
   after the other or an initial HAO TGT target was missing.
-  In case of the second error message the command “HAO TGT target” has
   been entered, but a “HAO CMD command” has been expected. This can be
   the case if two “HAO TGT target” com- mands have been entered
   immediately one after the other.

Severity Error.

Action Reenter the correct HAO command which is a “HAO TGT target” in
case of the first error message and a “HAO CMD command” in case of the
second error message.

HHC00073E
---------

HHC00073E Empty ‘target’ specified HHC00073E Empty ‘command’ specified

Explanation There was either an empty “HAO TGT” or an empty “HAO CMD”
command specified. The first case (HAO TGT) indicates a missing target
rule (pattern) to react on, the second case indicates a missing command
for a previously defined rule.

Severity Error.

Action Reenter the given HAO command with a valid target rule (“HAO TGT
target”) or a valid command (“HAO CMD command”).

HHC00074E
---------

HHC00074E The target was not added because a duplicate was found in the
table at nn

Explanation A “HAO TGT target” command has been entered but there is
already a rule in the table at index nn that has the same target rule
defined. The target rule could not be added to the table.

Severity Error.

Action

Use the “HAO LIST” command (without the index argument) to get a list of
all defined HAO rules and find the rule with the target from the
previous “HAO TGT target” command. If the command assigned to that
target rule is already what is supposed to have then no more actions are
necessary at this point. If the command assigned to that target rule is
not what is supposed to have then first delete the corres- ponding rule
with a “HAO DEL nn” command. After deleting the rule redefine it with a
new pair of “HAO TGT” and “HAO CMD” commands.

HHC00075E
---------

HHC00075E is not yet documented

Explanation …

Severity …

Action …

HHC00076E
---------

HHC00076E The ‘command’ was not added because it causes a loop with the
‘target’ at index nn HHC00076E The ‘target’ was not added because it
causes a loop with the ‘command’ at index nn

Explanation A HAO rule could not been defined because it causes a loop
with another already defined rule at table index nn.

Severity Error.

Action Check the rule you just wanted to define against the rule at
table index nn for any inconsistencies. Then try to redefine the rule.
Use the “HAO LIST nn” command to display the rule that is mentioned in
the error message.

HHC00077I
---------

HHC00077I The ‘func’ was placed at index nn

Explanation A new defined target rule (func = ‘target’) or a new defined
command (func = ‘command’) was placed at table index number nn.

Severity Information.

Action None. This is an informational message.

HHC00078E
---------

HHC00078E The command was not added because it may cause dead locks

Explanation A “HAO CMD cmd” command has been entered but command cmd
could not be added to the table be- cause it may cause deadlocks within
the HAO processing.

Severity Error.

Action Reenter the “HAO CMD” command with a valid command for the target
rule.

HHC00079E
---------

HHC00079E No rule defined at index nn

Explanation A “HAO LIST nn” command has been entered but there is no
target rule defined at this index. The entry at index nn is empty.

Severity Error.

Action Use the “HAO LIST” command (without the index argument) to get a
list of all defined HAO rules.

HHC00080I
---------

HHC00080I All HAO rules are cleared

Explanation All defined rules for the Hercules Automatic Operator have
been cleared and HAO is stopped. This is the response to a “HAO CLEAR”
command. The message is followed by one or more HHC00088I messages and a
HHC00082I message.

Severity Information.

Action None. This is an informational message.

HHC00081I
---------

HHC00081I Match at index nn, executing command ‘cmd’

Explanation A HAO rule has fired. There was a match at index number nn
in the table of defined HAO rules and the command cmd has been excuted.

Severity Information.

Action None. This is an informational message.

HHC00082I
---------

HHC00082I nn rule(s) displayed:

Explanation This message displays the number of rules (nn) that have
been displayed in response to a “HAO LIST” command. The messages is
preceeded by message HHC00087I and one or more (nn) messages HHC00088I.

Severity Information.

Action None. This is an informational message.

HHC00083E
---------

HHC00083E The command ‘del’ was given without a valid index

Explanation A “HAO DEL” command has been entered without a valid index
number. The entry could not be deleted.

Severity Error.

Action Reenter the delete command with an index in the valid range
between 0 and nn (“HAO DEL nn”). Enter a “HAO LIST” command first, if
necessary, to get the list of used entries.

HHC00084E
---------

HHC00084E Invalid index; index must be between 0 and nn

Explanation A HAO command has been entered with an index that is outside
the valid range. The index must be in the valid range between 0 and nn.

Severity Error.

Action Reenter the previous command with an index in the valid range
between 0 and nn. Enter a “HAO LIST” command first, if necessary, to get
the list of used entries.

HHC00085E
---------

HHC00085E Rule at index nn not deleted, already empty

Explanation The rule (target and command) an index nn has not been
deleted. The table entry is already empty.

Severity Error.

Action Use the “HAO LIST” command to get a list of all defined HAO
rules. Check all listed entries to find the one you want to delete and
retry the “HAO DEL” command with the correct index.

HHC00086I
---------

HHC00086I Rule at index nn successfully deleted

Explanation The rule (target and command) at table index number nn has
been deleted.

Severity Information.

Action None. This is an informational message.

HHC00087I
---------

HHC00087I The defined Hercules Automatic Operator rule(s) are:

Explanation This message shows all defined rules for the Hercules
Automatic Operator. It is following a “HAO LIST” command.

Severity Information.

Action None. This is an informational message.

HHC00088I
---------

HHC00088I Index nn: target ‘target’ -> command ‘cmd’

Explanation This message displays the target rule ‘target’ and its
corresponding command ‘cmd’ that are defined at index nn of the table.

Severity Information.

Action None. This is an informational message.

HHC00089E
---------

HHC00089E There are no HAO rules defined

Explanation A “HAO LIST” command has been entered but there are no rules
defined. The table is empty.

Severity Error.

Action Define a HAO rule before using the “HAO LIST” command.

HHC00100s – HHC00199s (General)
===============================

HHC00100I
---------

HHC00100I Thread id nnnnnnnn, prio nn, name ‘threadname’ started

Explanation The thread with the name ‘threadname’ has been started under
the id nnnnnnnn with priority nn.

Severity Information.

Action None. This is an informational message.

HHC00101I
---------

HHC00101I Thread id nnnnnnnn, prio nn, name ‘threadname’ ended

Explanation The thread with the name ‘threadname’ running under the id
nnnnnnnn with priority nn has been ended.

Severity Information.

Action None. This is an informational message.

HHC00102E
---------

HHC00102E Error in function create_thread(): threadname

Explanation The thread with the name ‘threadname’ could not be created.

Severity Error.

Action See any additional messages for further details of the failure.

HHC00103I
---------

HHC00103I is not yet documented

Explanation …

Severity …

Action …

HHC00105E
---------

HHC00105E is not yet documented

Explanation …

Severity …

Action …

HHC00130W
---------

HHC00130W is not yet documented

Explanation …

Severity …

Action …

HHC00131A
---------

HHC00131A is not yet documented

Explanation …

Severity …

Action …

HHC00135E
---------

HHC00135E is not yet documented

Explanation …

Severity …

Action …

HHC00136E
---------

HHC00136E is not yet documented

Explanation …

Severity …

Action …

HHC00137E
---------

HHC00137E is not yet documented

Explanation …

Severity …

Action …

HHC00138E
---------

HHC00138E is not yet documented

Explanation …

Severity …

Action …

HHC00139E
---------

HHC00139E is not yet documented

Explanation …

Severity …

Action …

HHC00140E
---------

HHC00140E is not yet documented

Explanation …

Severity …

Action …

HHC00141E
---------

HHC00141E is not yet documented

Explanation …

Severity …

Action …

HHC00142E
---------

HHC00142E is not yet documented

Explanation …

Severity …

Action …

HHC00143E
---------

HHC00143E is not yet documented

Explanation …

Severity …

Action …

HHC00144E
---------

HHC00144E is not yet documented

Explanation …

Severity …

Action …

HHC00145E
---------

HHC00145E is not yet documented

Explanation …

Severity …

Action …

HHC00146I
---------

HHC00146I is not yet documented

Explanation …

Severity …

Action …

HHC00147I
---------

HHC00147I is not yet documented

Explanation …

Severity …

Action …

HHC00148I
---------

HHC00148I is not yet documented

Explanation …

Severity …

Action …

HHC00149I
---------

HHC00149I is not yet documented

Explanation …

Severity …

Action …

HHC00150I
---------

HHC00150I modname module loaded [info]

Explanation Hercules has loaded the module modname. This message can
provide additional information about the loaded module in the optional
info field.

Severity Information.

Action None. This is an informational message.

HHC00151I
---------

HHC00151I is not yet documented

Explanation …

Severity …

Action …

HHC00152E
---------

HHC00152E is not yet documented

Explanation …

Severity …

Action …

HHC00153E
---------

HHC00153E is not yet documented

Explanation …

Severity …

Action …

HHC00154E
---------

HHC00154E is not yet documented

Explanation …

Severity …

Action …

HHC00160I
---------

HHC00160I is not yet documented

Explanation …

Severity …

Action …

HHC00161E
---------

HHC00161E is not yet documented

Explanation …

Severity …

Action …

HHC00200s – HHC00299s (Tape Device Emulation)
=============================================

HHC00201I
---------

HHC00201I is not yet documented

Explanation …

Severity …

Action …

HHC00202E
---------

HHC00202E is not yet documented

Explanation …

Severity …

Action …

HHC00203E
---------

HHC00203E is not yet documented

Explanation …

Severity …

Action …

HHC00204E
---------

HHC00204E is not yet documented

Explanation …

Severity …

Action …

HHC00205E
---------

HHC00205E is not yet documented

Explanation …

Severity …

Action …

HHC00206E
---------

HHC00206E is not yet documented

Explanation …

Severity …

Action …

HHC00207E
---------

HHC00207E is not yet documented

Explanation …

Severity …

Action …

HHC00208I
---------

HHC00208I is not yet documented

Explanation …

Severity …

Action …

HHC00209I
---------

HHC00209I is not yet documented

Explanation …

Severity …

Action …

HHC00210I
---------

HHC00210I is not yet documented

Explanation …

Severity …

Action …

HHC00211I
---------

HHC00211I is not yet documented

Explanation …

Severity …

Action …

HHC00212E
---------

HHC00212E is not yet documented

Explanation …

Severity …

Action …

HHC00213E
---------

HHC00213E is not yet documented

Explanation …

Severity …

Action …

HHC00214E
---------

HHC00214E is not yet documented

Explanation …

Severity …

Action …

HHC00215I
---------

HHC00215I is not yet documented

Explanation …

Severity …

Action …

HHC00216I
---------

HHC00216I is not yet documented

Explanation …

Severity …

Action …

HHC00217I
---------

HHC00217I is not yet documented

Explanation …

Severity …

Action …

HHC00218I
---------

HHC00218I is not yet documented

Explanation …

Severity …

Action …

HHC00219I
---------

HHC00219I is not yet documented

Explanation …

Severity …

Action …

HHC00220W
---------

HHC00220W is not yet documented

Explanation …

Severity …

Action …

HHC00221I
---------

HHC00221I is not yet documented

Explanation …

Severity …

Action …

HHC00222I
---------

HHC00222I is not yet documented

Explanation …

Severity …

Action …

HHC00223E
---------

HHC00223E is not yet documented

Explanation …

Severity …

Action …

HHC00224I
---------

HHC00224I is not yet documented

Explanation …

Severity …

Action …

HHC00225E
---------

HHC00225E is not yet documented

Explanation …

Severity …

Action …

HHC00226I
---------

HHC00226I is not yet documented

Explanation …

Severity …

Action …

HHC00227I
---------

HHC00227I is not yet documented

Explanation …

Severity …

Action …

HHC00228I
---------

HHC00228I is not yet documented

Explanation …

Severity …

Action …

HHC00229I
---------

HHC00229I is not yet documented

Explanation …

Severity …

Action …

HHC00235I
---------

HHC00235I is not yet documented

Explanation …

Severity …

Action …

HHC00243W
---------

HHC00243W is not yet documented

Explanation …

Severity …

Action …

HHC00300s – HHC00399s (DASD Device Emulation (CCKD))
====================================================

HHC00300E
---------

HHC00300E is not yet documented

Explanation …

Severity …

Action …

HHC00301E
---------

HHC00301E is not yet documented

Explanation …

Severity …

Action …

HHC00302E
---------

HHC00302E is not yet documented

Explanation …

Severity …

Action …

HHC00303E
---------

HHC00303E is not yet documented

Explanation …

Severity …

Action …

HHC00304E
---------

HHC00304E is not yet documented

Explanation …

Severity …

Action …

HHC00305E
---------

HHC00305E is not yet documented

Explanation …

Severity …

Action …

HHC00306E
---------

HHC00306E is not yet documented

Explanation …

Severity …

Action …

HHC00307E
---------

HHC00307E is not yet documented

Explanation …

Severity …

Action …

HHC00308E
---------

HHC00308E is not yet documented

Explanation …

Severity …

Action …

HHC00309E
---------

HHC00309E is not yet documented

Explanation …

Severity …

Action …

HHC00310E
---------

HHC00310E is not yet documented

Explanation …

Severity …

Action …

HHC00311E
---------

HHC00311E is not yet documented

Explanation …

Severity …

Action …

HHC00312E
---------

HHC00312E is not yet documented

Explanation …

Severity …

Action …

HHC00313E
---------

HHC0033E1 is not yet documented

Explanation …

Severity …

Action …

HHC00314E
---------

HHC00314E is not yet documented

Explanation …

Severity …

Action …

HHC00315I
---------

HHC00315I is not yet documented

Explanation …

Severity …

Action …

HHC00316I
---------

HHC00316I is not yet documented

Explanation …

Severity …

Action …

HHC00317E
---------

HHC00317E is not yet documented

Explanation …

Severity …

Action …

HHC00318W
---------

HHC00318W is not yet documented

Explanation …

Severity …

Action …

HHC00319E
---------

HHC00319E is not yet documented

Explanation …

Severity …

Action …

HHC00320I
---------

HHC00320I is not yet documented

Explanation …

Severity …

Action …

HHC00321I
---------

HHC00321I is not yet documented

Explanation …

Severity …

Action …

HHC00322W
---------

HHC00322W is not yet documented

Explanation …

Severity …

Action …

HHC00323E
---------

HHC00323E is not yet documented

Explanation …

Severity …

Action …

HHC00324E
---------

HHC00324E is not yet documented

Explanation …

Severity …

Action …

HHC00325I
---------

HHC00325I is not yet documented

Explanation …

Severity …

Action …

HHC00326E
---------

HHC00326E is not yet documented

Explanation …

Severity …

Action …

HHC00327E
---------

HHC00327E is not yet documented

Explanation …

Severity …

Action …

HHC00328I
---------

HHC00328I is not yet documented

Explanation …

Severity …

Action …

HHC00329W
---------

HHC00329W is not yet documented

Explanation …

Severity …

Action …

HHC00330I
---------

HHC00330I is not yet documented

Explanation …

Severity …

Action …

HHC00331W
---------

HHC00331W is not yet documented

Explanation …

Severity …

Action …

HHC00332I
---------

HHC00332I is not yet documented

Explanation …

Severity …

Action …

HHC00333I
---------

HHC00333I is not yet documented

Explanation …

Severity …

Action …

HHC00334I
---------

HHC00334I is not yet documented

Explanation …

Severity …

Action …

HHC00335I
---------

HHC00335I is not yet documented

Explanation …

Severity …

Action …

HHC00336I
---------

HHC00336I is not yet documented

Explanation …

Severity …

Action …

HHC00337I
---------

HHC00337I is not yet documented

Explanation …

Severity …

Action …

HHC00338I
---------

HHC00338I is not yet documented

Explanation …

Severity …

Action …

HHC00339I
---------

HHC00339I is not yet documented

Explanation …

Severity …

Action …

HHC00340I
---------

HHC00340I is not yet documented

Explanation …

Severity …

Action …

HHC00341I
---------

HHC00341I is not yet documented

Explanation …

Severity …

Action …

HHC00342E
---------

HHC00342E is not yet documented

Explanation …

Severity …

Action …

HHC00343E
---------

HHC00343E is not yet documented

Explanation …

Severity …

Action …

HHC00344E
---------

HHC00344E is not yet documented

Explanation …

Severity …

Action …

HHC00345I
---------

HHC0 03 45I is not yet documented

Explanation …

Severity …

Action …

HHC00346I
---------

HHC00346I is not yet documented

Explanation …

Severity …

Action …

HHC00347I
---------

HHC00347I is not yet documented

Explanation …

Severity …

Action …

HHC00348E
---------

HHC00348E is not yet documented

Explanation …

Severity …

Action …

HHC00349E
---------

HHC00349E is not yet documented

Explanation …

Severity …

Action …

HHC00352E
---------

HHC0 0352 E is not yet documented

Explanation …

Severity …

Action …

HHC00353E
---------

HHC00353E is not yet documented

Explanation …

Severity …

Action …

HHC00354E
---------

HHC00354E is not yet documented

Explanation …

Severity …

Action …

HHC00355E
---------

HHC00355E is not yet documented

Explanation …

Severity …

Action …

HHC00356E
---------

HHC00356E is not yet documented

Explanation …

Severity …

Action …

HHC00357I
---------

HHC00357I is not yet documented

Explanation …

Severity …

Action …

HHC00358I
---------

HHC00358I is not yet documented

Explanation …

Severity …

Action …

HHC00359I
---------

HHC00359I is not yet documented

Explanation …

Severity …

Action …

HHC00360I
---------

HHC00360I is not yet documented

Explanation …

Severity …

Action …

HHC00361E
---------

HHC00361E is not yet documented

Explanation …

Severity …

Action …

HHC00362E
---------

HHC00362E is not yet documented

Explanation …

Severity …

Action …

HHC00363W
---------

HHC00363W is not yet documented

Explanation …

Severity …

Action …

HHC00364W
---------

HHC00364W is not yet documented

Explanation …

Severity …

Action …

HHC00365W
---------

HHC00365W is not yet documented

Explanation …

Severity …

Action …

HHC00366W
---------

HHC00366W is not yet documented

Explanation …

Severity …

Action …

HHC00367W
---------

HHC00367W is not yet documented

Explanation …

Severity …

Action …

HHC00368W
---------

HHC00368W is not yet documented

Explanation …

Severity …

Action …

HHC00369W
---------

HHC00369W is not yet documented

Explanation …

Severity …

Action …

HHC00370W
---------

HHC00370W is not yet documented

Explanation …

Severity …

Action …

HHC00371W
---------

HHC00371W is not yet documented

Explanation …

Severity …

Action …

HHC00372I
---------

HHC00372I is not yet documented

Explanation …

Severity …

Action …

HHC00373I
---------

HHC00373I is not yet documented

Explanation …

Severity …

Action …

HHC00374E
---------

HHC00374E is not yet documented

Explanation …

Severity …

Action …

HHC00375W
---------

HHC00375W is not yet documented

Explanation …

Severity …

Action …

HHC00376W
---------

HHC00376W is not yet documented

Explanation …

Severity …

Action …

HHC00377I
---------

HHC00377I is not yet documented

Explanation …

Severity …

Action …

HHC00378E
---------

HHC00378E is not yet documented

Explanation …

Severity …

Action …

HHC00396I
---------

HHC00396I is not yet documented

Explanation …

Severity …

Action …

HHC00397I
---------

HHC00397I is not yet documented

Explanation …

Severity …

Action …

HHC00398I
---------

HHC00398I is not yet documented

Explanation …

Severity …

Action …

HHC00399I
---------

HHC00399I is not yet documented

Explanation …

Severity …

Action …

HHC00400s – HHC00499s (DASD Device Emulation (CKD))
===================================================

HHC00400E
---------

HHC00400E is not yet documented

Explanation …

Severity …

Action …

HHC00401E
---------

HHC00401E is not yet documented

Explanation …

Severity …

Action …

HHC00402E
---------

HHC00402E is not yet documented

Explanation …

Severity …

Action …

HHC00403I
---------

HHC00403I is not yet documented

Explanation …

Severity …

Action …

HHC00404E
---------

HHC00404E is not yet documented

Explanation …

Severity …

Action …

HHC00405E
---------

HHC00405E is not yet documented

Explanation …

Severity …

Action …

HHC00406E
---------

HHC00406E is not yet documented

Explanation …

Severity …

Action …

HHC00407E
---------

HHC00407E is not yet documented

Explanation …

Severity …

Action …

HHC00408E
---------

HHC00408E is not yet documented

Explanation …

Severity …

Action …

HHC00409I
---------

HHC00409I is not yet documented

Explanation …

Severity …

Action …

HHC00410E
---------

HHC00410E is not yet documented

Explanation …

Severity …

Action …

HHC00411E
---------

HHC00411E is not yet documented

Explanation …

Severity …

Action …

HHC00412E
---------

HHC00412E is not yet documented

Explanation …

Severity …

Action …

HHC00413E
---------

HHC00413E is not yet documented

Explanation …

Severity …

Action …

HHC00414I
---------

HHC00414I is not yet documented

Explanation …

Severity …

Action …

HHC00415E
---------

HHC00415E is not yet documented

Explanation …

Severity …

Action …

HHC00416E
---------

HHC00416E is not yet documented

Explanation …

Severity …

Action …

HHC00417I
---------

HHC00417I is not yet documented

Explanation …

Severity …

Action …

HHC00418E
---------

HHC00418E is not yet documented

Explanation …

Severity …

Action …

HHC00419E
---------

HHC00419E is not yet documented

Explanation …

Severity …

Action …

HHC00420E
---------

HHC00420E is not yet documented

Explanation …

Severity …

Action …

HHC00421E
---------

HHC00421E is not yet documented

Explanation …

Severity …

Action …

HHC00422E
---------

HHC00422E is not yet documented

Explanation …

Severity …

Action …

HHC00423I
---------

HHC00423I is not yet documented

Explanation …

Severity …

Action …

HHC00424I
---------

HHC00424I is not yet documented

Explanation …

Severity …

Action …

HHC00425I
---------

HHC00425I is not yet documented

Explanation …

Severity …

Action …

HHC00426I
---------

HHC00426I is not yet documented

Explanation …

Severity …

Action …

HHC00427I
---------

HHC00427I is not yet documented

Explanation …

Severity …

Action …

HHC00428I
---------

HHC00428I is not yet documented

Explanation …

Severity …

Action …

HHC00429I
---------

HHC00429I is not yet documented

Explanation …

Severity …

Action …

HHC00430I
---------

HHC00430I is not yet documented

Explanation …

Severity …

Action …

HHC00431I
---------

HHC00431I is not yet documented

Explanation …

Severity …

Action …

HHC00432E
---------

HHC00432E is not yet documented

Explanation …

Severity …

Action …

HHC00433I
---------

HHC00433I is not yet documented

Explanation …

Severity …

Action …

HHC00434I
---------

HHC00434I is not yet documented

Explanation …

Severity …

Action …

HHC00435I
---------

HHC00435I is not yet documented

Explanation …

Severity …

Action …

HHC00436I
---------

HHC00436I is not yet documented

Explanation …

Severity …

Action …

HHC00437I
---------

HHC00437I is not yet documented

Explanation …

Severity …

Action …

HHC00438I
---------

HHC00438I is not yet documented

Explanation …

Severity …

Action …

HHC00439I
---------

HHC00439I is not yet documented

Explanation …

Severity …

Action …

HHC00440I
---------

HHC00440I is not yet documented

Explanation …

Severity …

Action …

HHC00441I
---------

HHC00441I is not yet documented

Explanation …

Severity …

Action …

HHC00442I
---------

HHC00442I is not yet documented

Explanation …

Severity …

Action …

HHC00443E
---------

HHC00443E is not yet documented

Explanation …

Severity …

Action …

HHC00445I
---------

HHC00445I is not yet documented

Explanation …

Severity …

Action …

HHC00446E
---------

HHC00446E is not yet documented

Explanation …

Severity …

Action …

HHC00447I
---------

HHC00447I is not yet documented

Explanation …

Severity …

Action …

HHC00448E
---------

HHC00448E is not yet documented

Explanation …

Severity …

Action …

HHC00449I
---------

HHC00449I is not yet documented

Explanation …

Severity …

Action …

HHC00450E
---------

HHC00450E is not yet documented

Explanation …

Severity …

Action …

HHC00451E
---------

HHC00451E is not yet documented

Explanation …

Severity …

Action …

HHC00452E
---------

HHC00452E is not yet documented

Explanation …

Severity …

Action …

HHC00453I
---------

HHC00453I is not yet documented

Explanation …

Severity …

Action …

HHC00454I
---------

HHC00454I is not yet documented

Explanation …

Severity …

Action …

HHC00455E
---------

HHC00455E is not yet documented

Explanation …

Severity …

Action …

HHC00456I
---------

HHC00456I is not yet documented

Explanation …

Severity …

Action …

HHC00457I
---------

HHC00457I is not yet documented

Explanation …

Severity …

Action …

HHC00458E
---------

HHC00458E is not yet documented

Explanation …

Severity …

Action …

HHC00459I
---------

HHC00459I is not yet documented

Explanation …

Severity …

Action …

HHC00460I
---------

HHC00460I is not yet documented

Explanation …

Severity …

Action …

HHC00461E
---------

HHC00461E is not yet documented

Explanation …

Severity …

Action …

HHC00462I
---------

HHC00462I is not yet documented

Explanation …

Severity …

Action …

HHC00463I
---------

HHC00463I is not yet documented

Explanation …

Severity …

Action …

HHC00464E
---------

HHC00464E is not yet documented

Explanation …

Severity …

Action …

HHC00465I
---------

HHC00465I is not yet documented

Explanation …

Severity …

Action …

HHC00466I
---------

HHC00466I is not yet documented

Explanation …

Severity …

Action …

HHC00467I
---------

HHC00467I is not yet documented

Explanation …

Severity …

Action …

HHC00468I
---------

HHC00468I is not yet documented

Explanation …

Severity …

Action …

HHC00500s – HHC00599s (DASD Device Emulation (FBA))
===================================================

HHC00500E
---------

HHC00500E is not yet documented

Explanation …

Severity …

Action …

HHC00501E
---------

HHC00501E is not yet documented

Explanation …

Severity …

Action …

HHC00502E
---------

HHC0052E0 is not yet documented

Explanation …

Severity …

Action …

HHC00503E
---------

HHC00503E is not yet documented

Explanation …

Severity …

Action …

HHC00504I
---------

HHC00504I is not yet documented

Explanation …

Severity …

Action …

HHC00505E
---------

HHC00505E is not yet documented

Explanation …

Severity …

Action …

HHC00506E
---------

HHC00506E is not yet documented

Explanation …

Severity …

Action …

HHC00507I
---------

HHC00507I is not yet documented

Explanation …

Severity …

Action …

HHC00508E
---------

HHC00508E is not yet documented

Explanation …

Severity …

Action …

HHC00509E
---------

HHC00509E is not yet documented

Explanation …

Severity …

Action …

HHC00510E
---------

HHC00510E is not yet documented

Explanation …

Severity …

Action …

HHC00511E
---------

HHC00511E is not yet documented

Explanation …

Severity …

Action …

HHC00512E
---------

HHC00512E is not yet documented

Explanation …

Severity …

Action …

HHC00513E
---------

HHC00513E is not yet documented

Explanation …

Severity …

Action …

HHC00514E
---------

HHC00514E is not yet documented

Explanation …

Severity …

Action …

HHC00515E
---------

HHC00515E is not yet documented

Explanation …

Severity …

Action …

HHC00516I
---------

HHC00516I is not yet documented

Explanation …

Severity …

Action …

HHC00517I
---------

HHC00517I is not yet documented

Explanation …

Severity …

Action …

HHC00 518 I
---------~~

HHC00518I is not yet documented

Explanation …

Severity …

Action …

HHC00519I
---------

HHC00519I is not yet documented

Explanation …

Severity …

Action …

HHC00520I
---------

HHC00520I is not yet documented

Explanation …

Severity …

Action …

HHC00521I
---------

HHC00521I is not yet documented

Explanation …

Severity …

Action …

HHC00600s – HHC00699s (DASD Device Emulation (SCE))
===================================================

HHC00600E
---------

HHC00600E is not yet documented

Explanation …

Severity …

Action …

HHC00601E
---------

HHC00601E is not yet documented

Explanation …

Severity …

Action …

HHC00602E
---------

HHC00602E is not yet documented

Explanation …

Severity …

Action …

HHC00603W
---------

HHC00603W is not yet documented

Explanation …

Severity …

Action …

HHC00604E
---------

HHC00604E is not yet documented

Explanation …

Severity …

Action …

HHC00605E
---------

HHC00605E is not yet documented

Explanation …

Severity …

Action …

HHC00700s – HHC00799s (Shared Device Server)
============================================

HHC00700S
---------

HHC00700S is not yet documented

Explanation …

Severity …

Action …

HHC00701W
---------

HHC00701W is not yet documented

Explanation …

Severity …

Action …

HHC00702S
---------

HHC00702S is not yet documented

Explanation …

Severity …

Action …

HHC00703S
---------

HHC00703S is not yet documented

Explanation …

Severity …

Action …

HHC00704S
---------

HHC00704S is not yet documented

Explanation …

Severity …

Action …

HHC00705S
---------

HHC00705S is not yet documented

Explanation …

Severity …

Action …

HHC00706S
---------

HHC00706S is not yet documented

Explanation …

Severity …

Action …

HHC00707S
---------

HHC00707S is not yet documented

Explanation …

Severity …

Action …

HHC00708I
---------

HHC00708I is not yet documented

Explanation …

Severity …

Action …

HHC00709S
---------

HHC00709S is not yet documented

Explanation …

Severity …

Action …

HHC00710S
---------

HHC00710S is not yet documented

Explanation …

Severity …

Action …

HHC00711S
---------

HHC00711S is not yet documented

Explanation …

Severity …

Action …

HHC00712I
---------

HHC00712I is not yet documented

Explanation …

Severity …

Action …

HHC00713E
---------

HHC00713E is not yet documented

Explanation …

Severity …

Action …

HHC00714E
---------

HHC00714E is not yet documented

Explanation …

Severity …

Action …

HHC00715E
---------

HHC00715E is not yet documented

Explanation …

Severity …

Action …

HHC00716E
---------

HHC00716E is not yet documented

Explanation …

Severity …

Action …

HHC00717E
---------

HHC00717E is not yet documented

Explanation …

Severity …

Action …

HHC00718E
---------

HHC00718E is not yet documented

Explanation …

Severity …

Action …

HHC00719E
---------

HHC00719E is not yet documented

Explanation …

Severity …

Action …

HHC00720E
---------

HHC00720E is not yet documented

Explanation …

Severity …

Action …

HHC00721I
---------

HHC00721I is not yet documented

Explanation …

Severity …

Action …

HHC00722E
---------

HHC00722E is not yet documented

Explanation …

Severity …

Action …

HHC00723E
---------

HHC00723E is not yet documented

Explanation …

Severity …

Action …

HHC00724E
---------

HHC00724E is not yet documented

Explanation …

Severity …

Action …

HHC00725E
---------

HHC00725E is not yet documented

Explanation …

Severity …

Action …

HHC00726E
---------

HHC0 0726 E is not yet documented

Explanation …

Severity …

Action …

HHC00727E
---------

HHC0 0727 E is not yet documented

Explanation …

Severity …

Action …

HHC00728E
---------

HHC0 0728 E is not yet documented

Explanation …

Severity …

Action …

HHC00729E
---------

HHC0 0729 E is not yet documented

Explanation …

Severity …

Action …

HHC00730W
---------

HHC0 07 30W is not yet documented

Explanation …

Severity …

Action …

HHC00731I
---------

HHC00731I is not yet documented

Explanation …

Severity …

Action …

HHC00732E
---------

HHC00732E is not yet documented

Explanation …

Severity …

Action …

HHC00733I
---------

HHC00733I is not yet documented

Explanation …

Severity …

Action …

HHC00734E
---------

HHC00734E is not yet documented

Explanation …

Severity …

Action …

HHC00735E
---------

HHC00735E is not yet documented

Explanation …

Severity …

Action …

HHC00736W
---------

HHC00736W is not yet documented

Explanation …

Severity …

Action …

HHC00737I
---------

HHC00737I is not yet documented

Explanation …

Severity …

Action …

HHC00738E
---------

HHC00738E is not yet documented

Explanation …

Severity …

Action …

HHC00739E
---------

HHC00739E is not yet documented

Explanation …

Severity …

Action …

HHC00740E
---------

HHC00740E is not yet documented

Explanation …

Severity …

Action …

HHC00741E
---------

HHC00741E is not yet documented

Explanation …

Severity …

Action …

HHC00742E
---------

HHC00742E is not yet documented

Explanation …

Severity …

Action …

HHC00743I
---------

HHC00743I is not yet documented

Explanation …

Severity …

Action …

HHC00800s – HHC00899s (CPU Emulation)
=====================================

HHC00800I
---------

HHC00800I is not yet documented

Explanation …

Severity …

Action …

HHC00801I
---------

HHC00801I is not yet documented

Explanation …

Severity …

Action …

HHC00802I
---------

HHC00802I is not yet documented

Explanation …

Severity …

Action …

HHC00803I
---------

HHC00803I is not yet documented

Explanation …

Severity …

Action …

HHC00804I
---------

HHC00804I is not yet documented

Explanation …

Severity …

Action …

HHC00805I
---------

HHC00805I is not yet documented

Explanation …

Severity …

Action …

HHC00806I
---------

HHC00806I is not yet documented

Explanation …

Severity …

Action …

HHC00807I
---------

HHC00807I is not yet documented

Explanation …

Severity …

Action …

HHC00808I
---------

HHC00808I is not yet documented

Explanation …

Severity …

Action …

HHC00809I
---------

HHC00809I is not yet documented

Explanation …

Severity …

Action …

HHC00810E
---------

HHC00810E Processor nn: ipl failed: device dev not found

Explanation An attempt has been made to IPL CPU number nn from device
dev, but the IPL failed because there is no device dev attached to the
system. IPL processing is terminated. The target processor remains in
the ma- nual state.

Severity Error.

Action Reissue the IPL command specifying a device that is attached to
the system.

HHC00811I
---------

HHC00811I is not yet documented

Explanation …

Severity …

Action …

HHC00812I
---------

HHC00812I is not yet documented

Explanation …

Severity …

Action …

HHC00813E
---------

HHC00813E is not yet documented

Explanation …

Severity …

Action …

HHC00814I
---------

HHC00814I is not yet documented

Explanation …

Severity …

Action …

HHC00815I
---------

HHC00815I is not yet documented

Explanation …

Severity …

Action …

HHC00816W
---------

HHC00816W is not yet documented

Explanation …

Severity …

Action …

HHC00817I
---------

HHC00817I is not yet documented

Explanation …

Severity …

Action …

HHC00818E
---------

HHC00818E is not yet documented

Explanation …

Severity …

Action …

HHC00819I
---------

HHC00819I is not yet documented

Explanation …

Severity …

Action …

HHC00820I
---------

HHC00820I is not yet documented

Explanation …

Severity …

Action …

HHC00821I
---------

HHC00821I is not yet documented

Explanation …

Severity …

Action …

HHC00822I
---------

HHC00822I is not yet documented

Explanation …

Severity …

Action …

HHC00823I
---------

HHC00823I is not yet documented

Explanation …

Severity …

Action …

HHC00824I
---------

HHC00824I is not yet documented

Explanation …

Severity …

Action …

HHC00825E
---------

HHC00825E is not yet documented

Explanation …

Severity …

Action …

HHC00826E
---------

HHC00826E is not yet documented

Explanation …

Severity …

Action …

HHC00827I
---------

HHC00827I is not yet documented

Explanation …

Severity …

Action …

HHC00828E
---------

HHC00828E Processor nn: ipl failed: architecture mode mode, csw status
cswstat, sense sense

Explanation An attempt has been made to ipl CPU number nn, but the IPL
failed because of an I/O error on the IPL device. In the message text,
mode is the system architecture mode, cswstat is the CSW status returned
from the IPL I/O operation, and sense is the sense information returned
by the IPL device. Note that an attempt to IPL while the system is set
to z/Architecture mode will cause the architecture mode to be reset to
ESA/390 at the start of IPL processing, and message HHC00828E will
reflect that change.

Severity Error.

Action Correct the cause of the IPL device I/O problem and reissue the
IPL command.

HHC00832I
---------

HHC00832I is not yet documented

Explanation …

Severity …

Action …

HHC00834I
---------

HHC0 08 34I is not yet documented

Explanation …

Severity …

Action …

HHC00838I
---------

HHC00838I is not yet documented

Explanation …

Severity …

Action …

HHC00839E
---------

HHC00839E Processor nn: ipl failed: architecture mode mode, invalid ipl
psw psw

Explanation An attempt has been made to IPL CPU number nn, but the IPL
failed because of an error loading the initial PSW from the IPL device.
A common cause of IPL PSW errors is bits within the PSW set incon-
sistently, or a mismatch between the PSW bit settings and the system
architecture mode. In particular, this message will be produced if an
attempt is made to IPL with the architecture mode set to z/Architecture
or ESA/390 and the IPL PSW loaded from the target device is a BC-mode
PSW. Note that an attempt to IPL while the system is set to
z/Architecture mode will cause the architecture mode to be reset to
ESA/390 at the start of the IPL processing, and message HHC0839E will
reflect that change. IPL processing is terminated. The target processor
remains in the manual state and the load indicatorremains on.

Severity Error.

Action Correct the IPL device initial PSW to set PSW bit values
consistently, or change the system architecture mode to one that allows
the IPL device initial PSW to be used, or IPL from a different device.

HHC00840I
---------

HHC00840I is not yet documented

Explanation …

Severity …

Action …

HHC00841I
---------

HHC00841I is not yet documented

Explanation …

Severity …

Action …

HHC00842I
---------

HHC00842I is not yet documented

Explanation …

Severity …

Action …

HHC00843I
---------

HHC00843I is not yet documented

Explanation …

Severity …

Action …

HHC00844I
---------

HHC00844I is not yet documented

Explanation …

Severity …

Action …

HHC00845I
---------

HHC00845I is not yet documented

Explanation …

Severity …

Action …

HHC00846I
---------

HHC00846I is not yet documented

Explanation …

Severity …

Action …

HHC00850I
---------

HHC0 0850 I is not yet documented

Explanation …

Severity …

Action …

HHC00851I
---------

HHC00851I is not yet documented

Explanation …

Severity …

Action …

HHC00852I
---------

HHC00852I is not yet documented

Explanation …

Severity …

Action …

HHC00853I
---------

HHC00853I is not yet documented

Explanation …

Severity …

Action …

HHC00854I
---------

HHC00854I is not yet documented

Explanation …

Severity …

Action …

HHC00855I
---------

HHC00855I is not yet documented

Explanation …

Severity …

Action …

HHC00856I
---------

HHC00856I is not yet documented

Explanation …

Severity …

Action …

HHC00857I
---------

HHC00857I is not yet documented

Explanation …

Severity …

Action …

HHC00858I
---------

HHC00858I is not yet documented

Explanation …

Severity …

Action …

HHC00859I
---------

HHC00859I is not yet documented

Explanation …

Severity …

Action …

HHC00860I
---------

HHC00860I is not yet documented

Explanation …

Severity …

Action …

HHC00861I
---------

HHC00861I is not yet documented

Explanation …

Severity …

Action …

HHC00862I
---------

HHC00862I is not yet documented

Explanation …

Severity …

Action …

HHC00863I
---------

HHC00863I is not yet documented

Explanation …

Severity …

Action …

HHC00864I
---------

HHC00864I is not yet documented

Explanation …

Severity …

Action …

HHC00865I
---------

HHC00865I is not yet documented

Explanation …

Severity …

Action …

HHC00866I
---------

HHC00866I is not yet documented

Explanation …

Severity …

Action …

HHC00867I
---------

HHC00867I is not yet documented

Explanation …

Severity …

Action …

HHC00868I
---------

HHC00868I is not yet documented

Explanation …

Severity …

Action …

HHC00869I
---------

HHC00869I is not yet documented

Explanation …

Severity …

Action …

HHC00870I
---------

HHC00870I is not yet documented

Explanation …

Severity …

Action …

HHC00871I
---------

HHC00871I is not yet documented

Explanation …

Severity …

Action …

HHC00872I
---------

HHC00872I is not yet documented

Explanation …

Severity …

Action …

HHC00873I
---------

HHC00873I is not yet documented

Explanation …

Severity …

Action …

HHC00874I
---------

HHC00874I is not yet documented

Explanation …

Severity …

Action …

HHC00875I
---------

HHC00875I is not yet documented

Explanation …

Severity …

Action …

HHC00876I
---------

HHC00876I is not yet documented

Explanation …

Severity …

Action …

HHC00877I
---------

HHC00877I is not yet documented

Explanation …

Severity …

Action …

HHC00880I
---------

HHC00880I is not yet documented

Explanation …

Severity …

Action …

HHC00881I
---------

HHC00881I is not yet documented

Explanation …

Severity …

Action …

HHC00882I
---------

HHC00882I is not yet documented

Explanation …

Severity …

Action …

HHC00890I
---------

HHC00890I is not yet documented

Explanation …

Severity …

Action …

HHC00891E
---------

HHC00891E is not yet documented

Explanation …

Severity …

Action …

HHC00892E
---------

HHC00892E is not yet documented

Explanation …

Severity …

Action …

HHC00893E
---------

HHC00893E is not yet documented

Explanation …

Severity …

Action …

HHC00895E
---------

HHC00895E is not yet documented

Explanation …

Severity …

Action …

HHC00896E
---------

HHC00896E is not yet documented

Explanation …

Severity …

Action …

HHC00898I
---------

HHC00898I is not yet documented

Explanation …

Severity …

Action …

HHC00900s – HHC00999s (CTC Adapter Emulation)
=============================================

HHC00900E
---------

HHC00900E is not yet documented

Explanation …

Severity …

Action …

HHC00901I
---------

HHC00901I is not yet documented

Explanation …

Severity …

Action …

HHC00902W
---------

HHC00902W is not yet documented

Explanation …

Severity …

Action …

HHC00904I
---------

HHC00904I is not yet documented

Explanation …

Severity …

Action …

HHC00905I
---------

HHC00905I is not yet documented

Explanation …

Severity …

Action …

HHC00906E
---------

HHC00906E is not yet documented

Explanation …

Severity …

Action …

HHC00907I
---------

HHC00907I is not yet documented

Explanation …

Severity …

Action …

HHC00908E
---------

HHC00908E is not yet documented

Explanation …

Severity …

Action …

HHC00909E
---------

HHC00909E is not yet documented

Explanation …

Severity …

Action …

HHC00910I
---------

HHC00910I is not yet documented

Explanation …

Severity …

Action …

HHC00911E
---------

HHC00911E is not yet documented

Explanation …

Severity …

Action …

HHC00912E
---------

HHC00912E is not yet documented

Explanation …

Severity …

Action …

HHC00913I
---------

HHC00913I is not yet documented

Explanation …

Severity …

Action …

HHC00914W
---------

HHC00914W is not yet documented

Explanation …

Severity …

Action …

HHC00915E
---------

HHC00915E is not yet documented

Explanation …

Severity …

Action …

HHC00916E
---------

HHC00916E is not yet documented

Explanation …

Severity …

Action …

HHC00918E
---------

HHC00918E is not yet documented

Explanation …

Severity …

Action …

HHC00920E
---------

HHC00920E is not yet documented

Explanation …

Severity …

Action …

HHC00921I
---------

HHC00921I is not yet documented

Explanation …

Severity …

Action …

HHC00922I
---------

HHC00922I is not yet documented

Explanation …

Severity …

Action …

HHC00933I
---------

HHC00933I is not yet documented

Explanation …

Severity …

Action …

HHC00934I
---------

HHC00934I is not yet documented

Explanation …

Severity …

Action …

HHC00936E
---------

HHC00936E is not yet documented

Explanation …

Severity …

Action …

HHC00937E
---------

HHC00937E is not yet documented

Explanation …

Severity …

Action …

HHC00938I
---------

HHC00938I is not yet documented

Explanation …

Severity …

Action …

HHC00939W
---------

HHC00939W is not yet documented

Explanation …

Severity …

Action …

HHC00940E
---------

HHC00940E is not yet documented

Explanation …

Severity …

Action …

HHC00941E
---------

HHC00941E is not yet documented

Explanation …

Severity …

Action …

HHC00942I
---------

HHC00942I is not yet documented

Explanation …

Severity …

Action …

HHC00943W
---------

HHC00943W is not yet documented

Explanation …

Severity …

Action …

HHC00944E
---------

HHC00944E is not yet documented

Explanation …

Severity …

Action …

HHC00945I
---------

HHC00945I is not yet documented

Explanation …

Severity …

Action …

HHC00946I
---------

HHC00946I is not yet documented

Explanation …

Severity …

Action …

HHC00947I
---------

HHC00947I is not yet documented

Explanation …

Severity …

Action …

HHC00948I
---------

HHC00948I is not yet documented

Explanation …

Severity …

Action …

HHC00949I
---------

HHC00949I is not yet documented

Explanation …

Severity …

Action …

HHC00950I
---------

HHC00950I is not yet documented

Explanation …

Severity …

Action …

HHC00951I
---------

HHC00951I is not yet documented

Explanation …

Severity …

Action …

HHC00952I
---------

HHC00952I is not yet documented

Explanation …

Severity …

Action …

HHC00953W
---------

HHC00953W is not yet documented

Explanation …

Severity …

Action …

HHC00954E
---------

HHC00954E is not yet documented

Explanation …

Severity …

Action …

HHC00955E
---------

HHC00955E is not yet documented

Explanation …

Severity …

Action …

HHC00956E
---------

HHC00956E is not yet documented

Explanation …

Severity …

Action …

HHC00957E
---------

HHC00957E is not yet documented

Explanation …

Severity …

Action …

HHC00958E
---------

HHC00958E is not yet documented

Explanation …

Severity …

Action …

HHC00959E
---------

HHC00959E is not yet documented

Explanation …

Severity …

Action …

HHC00960E
---------

HHC00960E is not yet documented

Explanation …

Severity …

Action …

HHC00961E
---------

HHC00961E is not yet documented

Explanation …

Severity …

Action …

HHC00962E
---------

HHC00962E is not yet documented

Explanation …

Severity …

Action …

HHC00963E
---------

HHC00963E is not yet documented

Explanation …

Severity …

Action …

HHC00964I
---------

HHC00964I is not yet documented

Explanation …

Severity …

Action …

HHC00970E
---------

HHC00970E is not yet documented

Explanation …

Severity …

Action …

HHC00971I
---------

HHC00971I is not yet documented

Explanation …

Severity …

Action …

HHC00972I
---------

HHC00972I is not yet documented

Explanation …

Severity …

Action …

HHC00973E
---------

HHC00973E is not yet documented

Explanation …

Severity …

Action …

HHC00974E
---------

HHC00974E is not yet documented

Explanation …

Severity …

Action …

HHC00975E
---------

HHC00975E is not yet documented

Explanation …

Severity …

Action …

HHC00976E
---------

HHC00960E is not yet documented

Explanation …

Severity …

Action …

HHC01000s – HHC01099s (Communication Adapter Emulation)
=======================================================

HHC01000E
---------

HHC01000E is not yet documented

Explanation …

Severity …

Action …

HHC01001I
---------

HHC01001I is not yet documented

Explanation …

Severity …

Action …

HHC01002E
---------

HHC01002E is not yet documented

Explanation …

Severity …

Action …

HHC01003W
---------

HHC01003W is not yet documented

Explanation …

Severity …

Action …

HHC01004I
---------

HHC01004I is not yet documented

Explanation …

Severity …

Action …

HHC01005W
---------

HHC01005W is not yet documented

Explanation …

Severity …

Action …

HHC01006I
---------

HHC01006I is not yet documented

Explanation …

Severity …

Action …

HHC01007E
---------

HHC01007E is not yet documented

Explanation …

Severity …

Action …

HHC01008E
---------

HHC01008E is not yet documented

Explanation …

Severity …

Action …

HHC01009W
---------

HHC01009W is not yet documented

Explanation …

Severity …

Action …

HHC01010I
---------

HHC01010I is not yet documented

Explanation …

Severity …

Action …

HHC01011I
---------

HHC01011I is not yet documented

Explanation …

Severity …

Action …

HHC01012E
---------

HHC01012E is not yet documented

Explanation …

Severity …

Action …

HHC01013E
---------

HHC01013E is not yet documented

Explanation …

Severity …

Action …

HHC01014I
---------

HHC01014I is not yet documented

Explanation …

Severity …

Action …

HHC01015E
---------

HHC01015E is not yet documented

Explanation …

Severity …

Action …

HHC01016I
---------

HHC01016I is not yet documented

Explanation …

Severity …

Action …

HHC01017E
---------

HHC0 1017 E is not yet documented

Explanation …

Severity …

Action …

HHC01018I
---------

HHC01018I devaddr COMM: client ipaddr devtype devtype: connected

Explanation The client at IP address ipaddr has connected to Hercules as
a devtype device at device address devaddr and is now available.

Severity Information.

Action None. This is an informational message.

HHC01019E
---------

HHC0 1019 E is not yet documented

Explanation …

Severity …

Action …

HHC01020E
---------

HHC0 10 20E is not yet documented

Explanation …

Severity …

Action …

HHC01022I
---------

HHC01022I devaddr COMM: client ipaddr devtype devtype: connection closed
by client

Explanation The client with devtype devtype at IP address ipaddr that
was connected to the 3270 console at device address devaddr has closed
the connection. The device is no longer available for use.

Severity Information.

Action None. This is an informational message.

HHC01023W
---------

HHC01023W Waiting for port port to become free for console connections

Explanation

The thread that handles connection requests from console devices is
waiting for the TCP port denoted by port to become available for use.

Severity Warning.

Action If this message persists, some other program has control of the
TCP port listed. Determine the program involved and terminate it.

HHC01024I
---------

HHC01024I Waiting for console connections on port port.

Explanation Hercules is ready to accept console connections on port
port.

Severity Information.

Action None. This is an informational message.

HHC01025E
---------

HHC01025E is not yet documented

Explanation …

Severity …

Action …

HHC01026A
---------

HHC01026A is not yet documented

Explanation …

Severity …

Action …

HHC01027I
---------

HHC01027I is not yet documented

Explanation …

Severity …

Action …

HHC01028E
---------

HHC01028E is not yet documented

Explanation …

Severity …

Action …

HHC01029E
---------

HHC01029E is not yet documented

Explanation …

Severity …

Action …

HHC01030I
---------

HHC01030I is not yet documented

Explanation …

Severity …

Action …

HHC01031I
---------

HHC01031I is not yet documented

Explanation …

Severity …

Action …

HHC01032E
---------

HHC01032E is not yet documented

Explanation …

Severity …

Action …

HHC01033E
---------

HHC01033E is not yet documented

Explanation …

Severity …

Action …

HHC01034E
---------

HHC01034E is not yet documented

Explanation …

Severity …

Action …

HHC01035E
---------

HHC01035E is not yet documented

Explanation …

Severity …

Action …

HHC01036E
---------

HHC01036E is not yet documented

Explanation …

Severity …

Action …

HHC01037E
---------

HHC01037E is not yet documented

Explanation …

Severity …

Action …

HHC01038E
---------

HHC01038E is not yet documented

Explanation …

Severity …

Action …

HHC01039E
---------

HHC01039E is not yet documented

Explanation …

Severity …

Action …

HHC01040I
---------

HHC01040I is not yet documented

Explanation …

Severity …

Action …

HHC01041E
---------

HHC01041E is not yet documented

Explanation …

Severity …

Action …

HHC01042I
---------

HHC01042I is not yet documented

Explanation …

Severity …

Action …

HHC01043E
---------

HHC01043E is not yet documented

Explanation …

Severity …

Action …

HHC01044I
---------

HHC01044I is not yet documented

Explanation …

Severity …

Action …

HHC01045E
---------

HHC01045E is not yet documented

Explanation …

Severity …

Action …

HHC01046I
---------

HHC01046I is not yet documented

Explanation …

Severity …

Action …

HHC01047I
---------

HHC01047I is not yet documented

Explanation …

Severity …

Action …

HHC01048D
---------

HHC01048D is not yet documented

Explanation …

Severity …

Action …

HHC01049D
---------

HHC01049D is not yet documented

Explanation …

Severity …

Action …

HHC01050D
---------

HHC01050D is not yet documented

Explanation …

Severity …

Action …

HHC01051D
---------

HHC01051D is not yet documented

Explanation …

Severity …

Action …

HHC01052D
---------

HHC01052D is not yet documented

Explanation …

Severity …

Action …

HHC01053D
---------

HHC01053D is not yet documented

Explanation …

Severity …

Action …

HHC01054D
---------

HHC01054D is not yet documented

Explanation …

Severity …

Action …

HHC01055D
---------

HHC01055D is not yet documented

Explanation …

Severity …

Action …

HHC01056D
---------

HHC01056D is not yet documented

Explanation …

Severity …

Action …

HHC01057D
---------

HHC01057D is not yet documented

Explanation …

Severity …

Action …

HHC01058D
---------

HHC01058D is not yet documented

Explanation …

Severity …

Action …

HHC01059D
---------

HHC01059D is not yet documented

Explanation …

Severity …

Action …

HHC01060D
---------

HHC01060D is not yet documented

Explanation …

Severity …

Action …

HHC01061D
---------

HHC01061D is not yet documented

Explanation …

Severity …

Action …

HHC01062D
---------

HHC01062D is not yet documented

Explanation …

Severity …

Action …

HHC01063D
---------

HHC01063D is not yet documented

Explanation …

Severity …

Action …

HHC01064D
---------

HHC01064D is not yet documented

Explanation …

Severity …

Action …

HHC01065D
---------

HHC01065D is not yet documented

Explanation …

Severity …

Action …

HHC01066D
---------

HHC01066D is not yet documented

Explanation …

Severity …

Action …

HHC01067D
---------

HHC01067D is not yet documented

Explanation …

Severity …

Action …

HHC01068D
---------

HHC01068D is not yet documented

Explanation …

Severity …

Action …

HHC01069D
---------

HHC01069D is not yet documented

Explanation …

Severity …

Action …

HHC01070D
---------

HHC01070D is not yet documented

Explanation …

Severity …

Action …

HHC01071D
---------

HHC01071D is not yet documented

Explanation …

Severity …

Action …

HHC01072D
---------

HHC01072D is not yet documented

Explanation …

Severity …

Action …

HHC01073I
---------

HHC01073I is not yet documented

Explanation …

Severity …

Action …

HHC01074D
---------

HHC01074D is not yet documented

Explanation …

Severity …

Action …

HHC01075D
---------

HHC01075D is not yet documented

Explanation …

Severity …

Action …

HHC01076D
---------

HHC01076D is not yet documented

Explanation …

Severity …

Action …

HHC01077D
---------

HHC01077D is not yet documented

Explanation …

Severity …

Action …

HHC01078D
---------

HHC01078D is not yet documented

Explanation …

Severity …

Action …

HHC01079D
---------

HHC01079D is not yet documented

Explanation …

Severity …

Action …

HHC01080D
---------

HHC01080D is not yet documented

Explanation …

Severity …

Action …

HHC01081D
---------

HHC01081D is not yet documented

Explanation …

Severity …

Action …

HHC01082D
---------

HHC01082D is not yet documented

Explanation …

Severity …

Action …

HHC01083D
---------

HHC01083D is not yet documented

Explanation …

Severity …

Action …

HHC01084D
---------

HHC01084D is not yet documented

Explanation …

Severity …

Action …

HHC01090D
---------

HHC01090D is not yet documented

Explanation …

Severity …

Action …

HHC01091D
---------

HHC01091D is not yet documented

Explanation …

Severity …

Action …

HHC01100s – HHC01199s (Printer Emulation)
=========================================

HHC01100I
---------

HHC01100I is not yet documented

Explanation …

Severity …

Action …

HHC01101E
---------

HHC01101E is not yet documented

Explanation …

Severity …

Action …

HHC01102E
---------

HHC01102E is not yet documented

Explanation …

Severity …

Action …

HHC01103E
---------

HHC01103E is not yet documented

Explanation …

Severity …

Action …

HHC01104E
---------

HHC01104E is not yet documented

Explanation …

Severity …

Action …

HHC01105E
---------

HHC01105E is not yet documented

Explanation …

Severity …

Action …

HHC01106I
---------

HHC01106I is not yet documented

Explanation …

Severity …

Action …

HHC01107I
---------

HHC01107I is not yet documented

Explanation …

Severity …

Action …

HHC01108E
---------

HHC01108E is not yet documented

Explanation …

Severity …

Action …

HHC01200s – HHC01299s (Card Punch / Card Reader Emulation)
==========================================================

HHC01200E
---------

HHC01200E is not yet documented

Explanation …

Severity …

Action …

HHC01201E
---------

HHC01201E is not yet documented

Explanation …

Severity …

Action …

HHC01202E
---------

HHC01202E is not yet documented

Explanation …

Severity …

Action …

HHC01203E
---------

HHC01203E is not yet documented

Explanation …

Severity …

Action …

HHC01204I
---------

HHC01204I is not yet documented

Explanation …

Severity …

Action …

HHC01205W
---------

HHC01205W is not yet documented

Explanation …

Severity …

Action …

HHC01206I
---------

HHC01206I is not yet documented

Explanation …

Severity …

Action …

HHC01207E
---------

HHC01207E is not yet documented

Explanation …

Severity …

Action …

HHC01208E
---------

HHC01208E is not yet documented

Explanation …

Severity …

Action …

HHC01209E
---------

HHC01209E is not yet documented

Explanation …

Severity …

Action …

HHC01300s – HHC01399s (Channel-to-Channel Adapter Emulation)
============================================================

HHC0 1300 I
---------~~

HHC01300I is not yet documented

Explanation …

Severity …

Action …

HHC01301I
---------

HHC01301I is not yet documented

Explanation …

Severity …

Action …

HHC01302I
---------

HHC01302I is not yet documented

Explanation …

Severity …

Action …

HHC01303I
---------

HHC01303I is not yet documented

Explanation …

Severity …

Action …

HHC01304I
---------

HHC01304I is not yet documented

Explanation …

Severity …

Action …

HHC01305I
---------

HHC01305I is not yet documented

Explanation …

Severity …

Action …

HHC01306I
---------

HHC01306I is not yet documented

Explanation …

Severity …

Action …

HHC01307I
---------

HHC01307I is not yet documented

Explanation …

Severity …

Action …

HHC01308I
---------

HHC01308I is not yet documented

Explanation …

Severity …

Action …

HHC01309I
---------

HHC01300I is not yet documented

Explanation …

Severity …

Action …

HHC01310I
---------

HHC01310I is not yet documented

Explanation …

Severity …

Action …

HHC01311I
---------

HHC01311I is not yet documented

Explanation …

Severity …

Action …

HHC01312I
---------

HHC01312I is not yet documented

Explanation …

Severity …

Action …

HHC01313I
---------

HHC01313I is not yet documented

Explanation …

Severity …

Action …

HHC01314I
---------

HHC01314I is not yet documented

Explanation …

Severity …

Action …

HHC01315I
---------

HHC01315I is not yet documented

Explanation …

Severity …

Action …

HHC01316I
---------

HHC01316I is not yet documented

Explanation …

Severity …

Action …

HHC01317I
---------

HHC01317I is not yet documented

Explanation …

Severity …

Action …

HHC01318I
---------

HHC01318I is not yet documented

Explanation …

Severity …

Action …

HHC01319I
---------

HHC01319I is not yet documented

Explanation …

Severity …

Action …

HHC01329I
---------

HHC01329I is not yet documented

Explanation …

Severity …

Action …

HHC01330I
---------

HHC01330I is not yet documented

Explanation …

Severity …

Action …

HHC01332I
---------

HHC01332I is not yet documented

Explanation …

Severity …

Action …

HHC01333I
---------

HHC01333I is not yet documented

Explanation …

Severity …

Action …

HHC01334I
---------

HHC01334I is not yet documented

Explanation …

Severity …

Action …

HHC01335I
---------

HHC01335I is not yet documented

Explanation …

Severity …

Action …

HHC01350E
---------

HHC01350E is not yet documented

Explanation …

Severity …

Action …

HHC01351E
---------

HHC01351E is not yet documented

Explanation …

Severity …

Action …

HHC01352T
---------

HHC01352T is not yet documented

Explanation …

Severity …

Action …

HHC01353W
---------

HHC01353W is not yet documented

Explanation …

Severity …

Action …

HHC01400s – HHC01499s (Hercules Initialization and Shutdown)
============================================================

HHC01400I
---------

HHC01400I is not yet documented

Explanation …

Severity …

Action …

HHC01401I
---------

HHC01401I is not yet documented

Explanation …

Severity …

Action …

HHC01402I
---------

HHC01402I is not yet documented

Explanation …

Severity …

Action …

HHC01403W
---------

HHC01403W is not yet documented

Explanation …

Severity …

Action …

HHC01404S
---------

HHC01404S is not yet documented

Explanation …

Severity …

Action …

HHC01405E
---------

HHC01405E is not yet documented

Explanation …

Severity …

Action …

HHC01406W
---------

HHC01406W is not yet documented

Explanation …

Severity …

Action …

HHC01407S
---------

HHC01407S is not yet documented

Explanation …

Severity …

Action …

HHC01408S
---------

HHC01408S is not yet documented

Explanation …

Severity …

Action …

HHC01409S
---------

HHC01409S is not yet documented

Explanation …

Severity …

Action …

HHC01410S
---------

HHC01410S is not yet documented

Explanation …

Severity …

Action …

HHC01411E
---------

HHC01411E is not yet documented

Explanation …

Severity …

Action …

HHC01412I
---------

HHC01412I Hercules terminated

Explanation Hercules has finished the shutdown procedure and has
terminated.

Severity Information.

Action

None.

HHC01413I
---------

HHC01413I Hercules version v.rr.m HHC01413I Hercules version v.rr.m-git
-xxxx-xxxxxxxx

Explanation This message displays the version of Hercules thast is
currently running. For productive, stable versions the message shows the
version, release and modification level in the form v.rr.m. Snaphots
from the de- velopers repository additionally show the commit level in
the form git-xxxx-xxxxxxxx.

Severity Information.

Action None.

HHC01414I
---------

HHC01414I (c) Copyright 1999-yyyy by Roger Bowler, Jan Jaeger, and
others

Explanation This message displays the copyright statement, where yyyy is
the current year of the build of Hercules.

Severity Information.

Action None.

HHC01415I
---------

HHC01415I Built on Mon dd yyyy at hh:mm:ss

Explanation This message shows when the running Hercules build was
compiled. Mon is the abbreviated month, dd is the day, yyyy is the year
and hh:mm:ss is the timestamp of the build.

Severity Information.

Action

None.

HHC01416I
---------

HHC01416I Build information:

Explanation This is the title for the build information. This message is
followed by several HHC01416I messages showing detailed build
information.

Severity Information.

Action None.

HHC01417I
---------

HHC01417I is not yet documented

Explanation …

Severity …

Action …

HHC01418E
---------

HHC01418E is not yet documented

Explanation …

Severity …

Action …

HHC01419E
---------

HHC01419E is not yet documented

Explanation …

Severity …

Action …

HHC01420I
---------

HHC01420I Begin Hercules shutdown

Explanation Hercules is starting shutting down because an “EXIT” or
“QUIT” console command has been issued.

Severity Information.

Action None.

HHC01422I
---------

HHC01422I Configuration released

Explanation The configuration that has been in use has been released.
This message is issued during shutdown of Hercules.

Severity Information.

Action None.

HHC01423I
---------

HHC01423I Calling termination routines

Explanation During shutdown Hercules is calling the termination
routines.

Severity Information.

Action None.

HHC01424I
---------

HHC01424I All termination routines complete

Explanation During shutdown of Hercules all termination routines have
been finished.

Severity Information.

Action None.

HHC01425I
---------

HHC01425I Hercules shutdown complete

Explanation Hercules has been completed the shutdown procedure.

Severity Information.

Action None.

HHC01426I
---------

HHC01426I Shutdown initiated

Explanation The Hercules shutdown has been initiated. This message is
issued due to an “EXIT” or “QUIT” console command that has been given.

Severity Information.

Action None.

HHC01427I
---------

HHC01427I type storage released

Explanation During shutdown of Hercules the allocated storage has been
released. The storage type is either “Main” or “Expanded”.

Severity Information.

Action None.

HHC01430S
---------

HHC01430S is not yet documented

Explanation …

Severity …

Action …

HHC01431I
---------

HHC01431I is not yet documented

Explanation …

Severity …

Action …

HHC01432S
---------

HHC01432S is not yet documented

Explanation …

Severity …

Action …

HHC01433S
---------

HHC01433S is not yet documented

Explanation …

Severity …

Action …

HHC01435I
---------

HHC01435I is not yet documented

Explanation …

Severity …

Action …

HHC01436S
---------

HHC01436S is not yet documented

Explanation …

Severity …

Action …

HHC01437I
---------

HHC01437I is not yet documented

Explanation …

Severity …

Action …

HHC01438W
---------

HHC01438W is not yet documented

Explanation …

Severity …

Action …

HHC01439S
---------

HHC0 1439 S is not yet documented

Explanation …

Severity …

Action …

HHC01441E
---------

HHC0 14 41E is not yet documented

Explanation …

Severity …

Action …

HHC01443S
---------

HHC0 14 43S is not yet documented

Explanation …

Severity …

Action …

HHC01447I
---------

HHC01447I is not yet documented

Explanation …

Severity …

Action …

HHC01448S
---------

HHC01448S is not yet documented

Explanation …

Severity …

Action …

HHC01451E
---------

HHC01451E is not yet documented

Explanation …

Severity …

Action …

HHC01452W
---------

HHC01452W is not yet documented

Explanation …

Severity …

Action …

HHC01453S
---------

HHC01453S is not yet documented

Explanation …

Severity …

Action …

HHC01454S
---------

HHC01454S is not yet documented

Explanation …

Severity …

Action …

HHC01455E
---------

HHC01455E is not yet documented

Explanation …

Severity …

Action …

HHC01456E
---------

HHC01456E is not yet documented

Explanation …

Severity …

Action …

HHC01457E
---------

HHC01457E is not yet documented

Explanation …

Severity …

Action …

HHC01458W
---------

HHC01458W is not yet documented

Explanation …

Severity …

Action …

HHC01459I
---------

HHC01459I is not yet documented

Explanation …

Severity …

Action …

HHC01460E
---------

HHC01460E is not yet documented

Explanation …

Severity …

Action …

HHC01461E
---------

HHC01461E is not yet documented

Explanation …

Severity …

Action …

HHC01462E
---------

HHC01462E is not yet documented

Explanation …

Severity …

Action …

HHC01463E
---------

HHC01463E is not yet documented

Explanation …

Severity …

Action …

HHC01464E
---------

HHC01464E is not yet documented

Explanation …

Severity …

Action …

HHC01465I
---------

HHC01465I is not yet documented

Explanation …

Severity …

Action …

HHC01466E
---------

HHC01466E is not yet documented

Explanation …

Severity …

Action …

HHC01467E
---------

HHC01467E is not yet documented

Explanation …

Severity …

Action …

HHC01468E
---------

HHC01468E is not yet documented

Explanation …

Severity …

Action …

HHC01469E
---------

HHC01469E is not yet documented

Explanation …

Severity …

Action …

HHC01470E
---------

HHC01470E is not yet documented

Explanation …

Severity …

Action …

HHC01471E
---------

HHC01471E is not yet documented

Explanation …

Severity …

Action …

HHC01472E
---------

HHC01472E is not yet documented

Explanation …

Severity …

Action …

HHC01473E
---------

HHC01473E is not yet documented

Explanation …

Severity …

Action …

HHC01474I
---------

HHC01474I is not yet documented

Explanation …

Severity …

Action …

HHC01475E
---------

HHC01475E is not yet documented

Explanation …

Severity …

Action …

HHC01476I
---------

HHC01476I is not yet documented

Explanation …

Severity …

Action …

HHC01477W
---------

HHC01477W is not yet documented

Explanation …

Severity …

Action …

HHC01478I
---------

HHC01478I is not yet documented

Explanation …

Severity …

Action …

HHC01479I
---------

HHC01479I is not yet documented

Explanation …

Severity …

Action …

HHC01480E
---------

HHC0 14 80E is not yet documented

Explanation …

Severity …

Action …

HHC01481I
---------

HHC01481I is not yet documented

Explanation …

Severity …

Action …

HHC01482I
---------

HHC01482I is not yet documented

Explanation …

Severity …

Action …

HHC01483E
---------

HHC01483E is not yet documented

Explanation …

Severity …

Action …

HHC01484I
---------

HHC01484I is not yet documented

Explanation …

Severity …

Action …

HHC01485I
---------

HHC01485I is not yet documented

Explanation …

Severity …

Action …

HHC01486I
---------

HHC01486I is not yet documented

Explanation …

Severity …

Action …

HHC01487I
---------

HHC01487I is not yet documented

Explanation …

Severity …

Action …

HHC01488I
---------

HHC01488I is not yet documented

Explanation …

Severity …

Action …

HHC01489E
---------

HHC01489E is not yet documented

Explanation …

Severity …

Action …

HHC01490I
---------

HHC01490I is not yet documented

Explanation …

Severity …

Action …

HHC01491I
---------

HHC01491I is not yet documented

Explanation …

Severity …

Action …

HHC01492I
---------

HHC01492I is not yet documented

Explanation …

Severity …

Action …

HHC01493I
---------

HHC01493I is not yet documented

Explanation …

Severity …

Action …

HHC01500s – HHC01599s (Dynamic Loader)
======================================

HHC01500I
---------

HHC01500I is not yet documented

Explanation …

Severity …

Action …

HHC01501I
---------

HHC01501I is not yet documented

Explanation …

Severity …

Action …

HHC01502I
---------

HHC01502I is not yet documented

Explanation …

Severity …

Action …

HHC01504I
---------

HHC01504I is not yet documented

Explanation …

Severity …

Action …

HHC01505E
---------

HHC01505E is not yet documented

Explanation …

Severity …

Action …

HHC01506W
---------

HHC01506W is not yet documented

Explanation …

Severity …

Action …

HHC01507W
---------

HHC01507W is not yet documented

Explanation …

Severity …

Action …

HHC01508I
---------

HHC01508I is not yet documented

Explanation …

Severity …

Action …

HHC01509I
---------

HHC01509I is not yet documented

Explanation …

Severity …

Action …

HHC01510I
---------

HHC01510I is not yet documented

Explanation …

Severity …

Action …

HHC01511S
---------

HHC01511S is not yet documented

Explanation …

Severity …

Action …

HHC01512I
---------

HHC01512I is not yet documented

Explanation …

Severity …

Action …

HHC01513I
---------

HHC01513I is not yet documented

Explanation …

Severity …

Action …

HHC01514I
---------

HHC01514I is not yet documented

Explanation …

Severity …

Action …

HHC01515I
---------

HHC01515I is not yet documented

Explanation …

Severity …

Action …

HHC01516E
---------

HHC01516E is not yet documented

Explanation …

Severity …

Action …

HHC01517E
---------

HHC01517E is not yet documented

Explanation …

Severity …

Action …

HHC01518E
---------

HHC0 15 18E is not yet documented

Explanation …

Severity …

Action …

HHC01519E
---------

HHC01519E is not yet documented

Explanation …

Severity …

Action …

HHC01520E
---------

HHC01520E is not yet documented

Explanation …

Severity …

Action …

HHC01521E
---------

HHC01521E is not yet documented

Explanation …

Severity …

Action …

HHC01522E
---------

HHC01522E is not yet documented

Explanation …

Severity …

Action …

HHC01523E
---------

HHC0 1523 E is not yet documented

Explanation …

Severity …

Action …

HHC01524E
---------

HHC01524E is not yet documented

Explanation …

Severity …

Action …

HHC01525E
---------

HHC01525E is not yet documented

Explanation …

Severity …

Action …

HHC01526I
---------

HHC01526I is not yet documented

Explanation …

Severity …

Action …

HHC01527I
---------

HHC01527I is not yet documented

Explanation …

Severity …

Action …

HHC01528I
---------

HHC01528I is not yet documented

Explanation …

Severity …

Action …

HHC01529I
---------

HHC01529I is not yet documented

Explanation …

Severity …

Action …

HHC01530E
---------

HHC01530E is not yet documented

Explanation …

Severity …

Action …

HHC01531I
---------

HHC01531I is not yet documented

Explanation …

Severity …

Action …

HHC01532I
---------

HHC01532I is not yet documented

Explanation …

Severity …

Action …

HHC01533I
---------

HHC01533I is not yet documented

Explanation …

Severity …

Action …

HHC01534I
---------

HHC01534I is not yet documented

Explanation …

Severity …

Action …

HHC01535I
---------

HHC01535I is not yet documented

Explanation …

Severity …

Action …

HHC01540E
---------

HHC01540E is not yet documented

Explanation …

Severity …

Action …

HHC01541I
---------

HHC01541I HDL: dyngui.dll initiated

Explanation The dyngui loadable module was successfully loaded and
initiated.

Severity Information.

Action None. This is an informational message.

HHC01542I
---------

HHC01542I HDL: dyngui.dll terminated

Explanation The dyngui loadable module was successfully terminated.

Severity Information.

Action None. This is an informational message.

HHC01600s – HHC01699s (Panel Communication)
===========================================

HHC01600E
---------

HHC01600E is not yet documented

Explanation …

Severity …

Action …

HHC01602I
---------

HHC01602I is not yet documented

Explanation …

Severity …

Action …

HHC01603I
---------

HHC01603I cmd

Explanation Console command ‘cmd’ has been issued at the Herculese
console. See also Message HHC00013I.

Severity Information.

Action None. This is an informational message.

HHC01604I
---------

HHC01604I is not yet documented

Explanation …

Severity …

Action …

HHC01605E
---------

HHC01605E is not yet documented

Explanation …

Severity …

Action …

HHC01606I
---------

HHC01606I is not yet documented

Explanation …

Severity …

Action …

HHC01607I
---------

HHC01607I is not yet documented

Explanation …

Severity …

Action …

HHC01608W
---------

HHC01608W is not yet documented

Explanation …

Severity …

Action …

HHC01609E
---------

HHC01609E is not yet documented

Explanation …

Severity …

Action …

HHC01610I
---------

HHC01610I is not yet documented

Explanation …

Severity …

Action …

HHC01700s – HHC01799s (ECPS:VM Support)
=======================================

HHC01700W
---------

HHC01700W is not yet documented

Explanation …

Severity …

Action …

HHC01701I
---------

HHC01701I is not yet documented

Explanation …

Severity …

Action …

HHC01702I
---------

HHC01702I is not yet documented

Explanation …

Severity …

Action …

HHC01703I
---------

HHC01703I is not yet documented

Explanation …

Severity …

Action …

HHC01704I
---------

HHC01704I is not yet documented

Explanation …

Severity …

Action …

HHC01705I
---------

HHC01705I is not yet documented

Explanation …

Severity …

Action …

HHC01706I
---------

HHC01706I is not yet documented

Explanation …

Severity …

Action …

HHC01707I
---------

HHC01707I ECPS:VM {VM \| CP} ASSIST feature xxxxxxxx {Disabled \|
Enabled}

Explanation This message is indicating that the ECPS:VM ASSIST feature
‘feature’ of type VM or CP has been either disabled or enabled.

Severity Information.

Action None. This is an informational message.

HHC01708I
---------

HHC01708I All ECPS:VM {VM \| CP} ASSIST features {Disabled \| Enabled}

Explanation This message is indicating that all ECPS:VM ASSIST features
of type VM or CP have been either disabled or enabled.

Severity Information.

Action None. This is an informational message.

HHC01709I
---------

HHC01709I is not yet documented

Explanation …

Severity …

Action …

HHC01710I
---------

HHC01710I is not yet documented

Explanation …

Severity …

Action …

HHC01711I
---------

HHC01711I is not yet documented

Explanation …

Severity …

Action …

HHC01712I
---------

HHC01712I is not yet documented

Explanation …

Severity …

Action …

HHC01713I
---------

HHC01713I is not yet documented

Explanation …

Severity …

Action …

HHC01714I
---------

HHC01714I is not yet documented

Explanation …

Severity …

Action …

HHC01715W
---------

HHC01715W is not yet documented

Explanation …

Severity …

Action …

HHC01716I
---------

HHC01716I is not yet documented

Explanation …

Severity …

Action …

HHC01717I
---------

HHC01717I is not yet documented

Explanation …

Severity …

Action …

HHC01718E
---------

HHC01718E is not yet documented

Explanation …

Severity …

Action …

HHC01719I
---------

HHC01719I ECPS:VM Command processor invoked

Explanation The ECPS:VM command processor has been invoked.

Severity Information.

Action None. This is an informational message.

HHC01720E
---------

HHC01720E is not yet documented

Explanation …

Severity …

Action …

HHC01721E
---------

HHC01721E is not yet documented

Explanation …

Severity …

Action …

HHC01722I
---------

HHC01722I ECPS:VM Command processor complete

Explanation The ECPS:VM command processor has been completed.

Severity Information.

Action None. This is an informational message.

HHC01723W
---------

HHC01723W is not yet documented

Explanation …

Severity …

Action …

24. HHC01800s – HHC01899s (HTTP Server)
------------------------------------------------

HHC01800E
---------

HHC01800E is not yet documented

Explanation …

Severity …

Action …

HHC01801E
---------

HHC01801E is not yet documented

Explanation …

Severity …

Action …

HHC01802I
---------

HHC01802I HTTP server using root directory path

Explanation The Hercules HTTP server is using ‘path’ as the root
directory.

Severity Information.

Action None. This is an informational message.

HHC01803I
---------

HHC01803I is not yet documented

Explanation …

Severity …

Action …

HHC01804W
---------

HHC01804W is not yet documented

Explanation …

Severity …

Action …

HHC01805I
---------

HHC01805I is not yet documented

Explanation …

Severity …

Action …

HHC01806W
---------

HHC01806W is not yet documented

Explanation …

Severity …

Action …

HHC01807I
---------

HHC01807I is not yet documented

Explanation …

Severity …

Action …

HHC01808I
---------

HHC01808I is not yet documented

Explanation …

Severity …

Action …

HHC01809I
---------

HHC01809I is not yet documented

Explanation …

Severity …

Action …

HHC01810I
---------

HHC01810I is not yet documented

Explanation …

Severity …

Action …

HHC01811I
---------

HHC01811I is not yet documented

Explanation …

Severity …

Action …

HHC01812E
---------

HHC01812E is not yet documented

Explanation …

Severity …

Action …

HHC01814E
---------

HHC01814E is not yet documented

Explanation …

Severity …

Action …

HHC01815E
---------

HHC01815E is not yet documented

Explanation …

Severity …

Action …

HHC01900s – HHC01999s (Diagnose Calls)
======================================

HHC01900I
---------

HHC0 19 00I is not yet documented

Explanation …

Severity …

Action …

HHC01901I
---------

HHC01901I is not yet documented

Explanation …

Severity …

Action …

HHC01902I
---------

HHC01902I is not yet documented

Explanation …

Severity …

Action …

HHC01905I
---------

HHC01905I is not yet documented

Explanation …

Severity …

Action …

HHC01906I
---------

HHC01906I is not yet documented

Explanation …

Severity …

Action …

HHC01907I
---------

HHC01907I is not yet documented

Explanation …

Severity …

Action …

HHC01908E
---------

HHC01908E is not yet documented

Explanation …

Severity …

Action …

HHC01909I
---------

HHC01909I is not yet documented

Explanation …

Severity …

Action …

HHC01920I
---------

HHC01920I is not yet documented

Explanation …

Severity …

Action …

HHC01921I
---------

HHC01920I is not yet documented

Explanation …

Severity …

Action …

HHC01922I
---------

HHC01922I is not yet documented

Explanation …

Severity …

Action …

HHC01923I
---------

HHC01923I is not yet documented

Explanation …

Severity …

Action …

HHC01924I
---------

HHC01924I is not yet documented

Explanation …

Severity …

Action …

HHC01925I
---------

HHC01925I is not yet documented

Explanation …

Severity …

Action …

HHC01926I
---------

HHC01926I is not yet documented

Explanation …

Severity …

Action …

HHC01927I
---------

HHC01927I is not yet documented

Explanation …

Severity …

Action …

HHC01928I
---------

HHC01928I is not yet documented

Explanation …

Severity …

Action …

HHC01929I
---------

HHC01929I is not yet documented

Explanation …

Severity …

Action …

HHC01930I
---------

HHC01930I is not yet documented

Explanation …

Severity …

Action …

HHC01931I
---------

HHC01931I is not yet documented

Explanation …

Severity …

Action …

HHC01932I
---------

HHC01932I is not yet documented

Explanation …

Severity …

Action …

HHC01933I
---------

HHC01933I is not yet documented

Explanation …

Severity …

Action …

HHC01934I
---------

HHC01934I is not yet documented

Explanation …

Severity …

Action …

HHC01935I
---------

HHC01935I is not yet documented

Explanation …

Severity …

Action …

HHC01936I
---------

HHC01936I is not yet documented

Explanation …

Severity …

Action …

HHC01937I
---------

HHC01937I is not yet documented

Explanation …

Severity …

Action …

HHC01938E
---------

HHC01938E is not yet documented

Explanation …

Severity …

Action …

HHC01939I
---------

HHC01939I is not yet documented

Explanation …

Severity …

Action …

HHC01940I
---------

HHC01940I is not yet documented

Explanation …

Severity …

Action …

HHC01941I
---------

HHC01941I is not yet documented

Explanation …

Severity …

Action …

HHC01942I
---------

HHC01942I is not yet documented

Explanation …

Severity …

Action …

HHC01943I
---------

HHC01943I is not yet documented

Explanation …

Severity …

Action …

HHC01944I
---------

HHC01944I is not yet documented

Explanation …

Severity …

Action …

HHC01945I
---------

HHC01945I is not yet documented

Explanation …

Severity …

Action …

HHC01950I
---------

HHC01950I Panel command ‘cmd’ issued by guest started HHC01950I Panel
command ‘cmd’ issued by guest completed

Explanation The guest operating system has started or completed a
DIAGNOSE 8 instruction to perform the panel command ‘cmd’ to be carried
out by the Hercules panel command processor.

Severity Information.

Action This is an informational message. No action is requested if this
behaviour is expected. If this behaviour poses a security concern
however, the DIAG8CMD configuration statement should either be ommited
or specified with the DISABLED argument.

HHC01951W
---------

HHC01951W is not yet documented

Explanation …

Severity …

Action …

HHC01952I
---------

HHC01952I is not yet documented

Explanation …

Severity …

Action …

HHC01953E
---------

HHC01953E Host command processing disabled by configuration statement

Explanation The guest operating system attempted using the DIAGNOSE 8
Instruction to carry out a panel command, but the system configuration
disabled this feature (with the DIAG8CMD configuration statement). The
pa- nel command is ignored.

Severity Error.

Action If it is deemed necessary for the guest operating system to issue
DIAGNOSE 8 commands to issue panel commands, the DIAG8CMD with the
ENABLE argument should be specified in the configuration file.

HHC01954E
---------

HHC01954E Host command processing not included in engine build

Explanation

The Hercules engine has been built without Diagnose 8 panel command
facility support. The panel com- mand is not issued. The system
continues.

Severity Error.

Action If it is desired that DIAGNOSE 8 instructions be carried out as
panel commands, the facility should be in- cluded in the build process.
Additionally, the DIAG8CMD configuration statement should be specified
with the ENABLE parameter.

HHC02000s – HHC02099s (Suspend / Resume Processing)
===================================================

HHC02000E
---------

HHC02000E is not yet documented

Explanation …

Severity …

Action …

HHC02001E
---------

HHC02001E is not yet documented

Explanation …

Severity …

Action …

HHC02002W
---------

HHC02002W is not yet documented

Explanation …

Severity …

Action …

HHC02003W
---------

HHC02003W is not yet documented

Explanation …

Severity …

Action …

HHC02004E
---------

HHC02004E is not yet documented

Explanation …

Severity …

Action …

HHC02005E
---------

HHC02005E is not yet documented

Explanation …

Severity …

Action …

HHC02006E
---------

HHC02006E is not yet documented

Explanation …

Severity …

Action …

HHC02007E
---------

HHC02007E is not yet documented

Explanation …

Severity …

Action …

HHC02008E
---------

HHC02008E is not yet documented

Explanation …

Severity …

Action …

HHC02009E
---------

HHC02009E is not yet documented

Explanation …

Severity …

Action …

HHC02010E
---------

HHC02010E is not yet documented

Explanation …

Severity …

Action …

HHC02011E
---------

HHC02011E is not yet documented

Explanation …

Severity …

Action …

HHC02012E
---------

HHC02012E is not yet documented

Explanation …

Severity …

Action …

HHC02013E
---------

HHC02013E is not yet documented

Explanation …

Severity …

Action …

HHC02014E
---------

HHC02014E is not yet documented

Explanation …

Severity …

Action …

HHC02015E
---------

HHC02015E is not yet documented

Explanation …

Severity …

Action …

HHC02016E
---------

HHC02016E is not yet documented

Explanation …

Severity …

Action …

HHC02017E
---------

HHC02017E is not yet documented

Explanation …

Severity …

Action …

HHC02018E
---------

HHC02018E is not yet documented

Explanation …

Severity …

Action …

HHC02019E
---------

HHC02019E is not yet documented

Explanation …

Severity …

Action …

HHC0 2020 E
---------~~

HHC02020E is not yet documented

Explanation …

Severity …

Action …

HHC02021E
---------

HHC02021E is not yet documented

Explanation …

Severity …

Action …

HHC02100s – HHC02199s (System Logger)
=====================================

HHC02100E
---------

HHC02100E is not yet documented

Explanation …

Severity …

Action …

HHC02101I
---------

HHC02101I is not yet documented

Explanation …

Severity …

Action …

HHC02102E
---------

HHC02102E is not yet documented

Explanation …

Severity …

Action …

HHC02103I
---------

HHC02103I Logger: logger thread terminating

Explanation During shutdown of Hercules the logger thread is
terminating.

Severity Information.

Action None.

HHC02104I
---------

HHC02104I is not yet documented

Explanation …

Severity …

Action …

HHC02105I
---------

HHC02105I is not yet documented

Explanation …

Severity …

Action …

HHC02106I
---------

HHC02106I is not yet documented

Explanation …

Severity …

Action …

HHC02197E
---------

HHC02197E is not yet documented

Explanation …

Severity …

Action …

HHC02198I
---------

HHC02198I is not yet documented

Explanation …

Severity …

Action …

HHC02199I
---------

HHC02199I is not yet documented

Explanation …

Severity …

Action …

HHC02200s – HHC02299s (Command Processing)
==========================================

HHC02200E
---------

HHC02200E is not yet documented

Explanation …

Severity …

Action …

HHC02201E
---------

HHC02201E is not yet documented

Explanation …

Severity …

Action …

HHC02202E
---------

HHC02202E is not yet documented

Explanation …

Severity …

Action …

HHC02203I
---------

HHC02203I is not yet documented

Explanation …

Severity …

Action …

HHC02204I
---------

HHC02204I cmdsep set to x

Explanation The command separator sign for separating Hercules console
commands has been set to sign ‘x’.

Severity Information.

Action None. This is an informational message.

HHC02205E
---------

HHC02205E is not yet documented

Explanation …

Severity …

Action …

HHC02206I
---------

HHC02206I is not yet documented

Explanation …

Severity …

Action …

HHC02207I
---------

HHC02207I is not yet documented

Explanation …

Severity …

Action …

HHC02208I
---------

HHC02208I is not yet documented

Explanation …

Severity …

Action …

HHC02209E
---------

HHC02209E is not yet documented

Explanation …

Severity …

Action …

HHC02210I
---------

HHC02210I is not yet documented

Explanation …

Severity …

Action …

HHC02211E
---------

HHC02211E is not yet documented

Explanation …

Severity …

Action …

HHC02212E
---------

HHC02212E is not yet documented

Explanation …

Severity …

Action …

HHC02213E
---------

HHC02213E is not yet documented

Explanation …

Severity …

Action …

HHC02214I
---------

HHC02214I is not yet documented

Explanation …

Severity …

Action …

HHC02215W
---------

HHC02215W is not yet documented

Explanation …

Severity …

Action …

HHC02216E
---------

HHC02216E is not yet documented

Explanation …

Severity …

Action …

HHC02217I
---------

HHC02217I is not yet documented

Explanation …

Severity …

Action …

HHC02218E
---------

HHC02218E is not yet documented

Explanation …

Severity …

Action …

HHC02219E
---------

HHC02219E is not yet documented

Explanation …

Severity …

Action …

HHC02220I
---------

HHC02220I is not yet documented

Explanation …

Severity …

Action …

HHC02221E
---------

HHC02221E is not yet documented

Explanation …

Severity …

Action …

HHC02222E
---------

HHC02222E is not yet documented

Explanation …

Severity …

Action …

HHC02223I
---------

HHC02223I is not yet documented

Explanation …

Severity …

Action …

HHC02224E
---------

HHC02224E is not yet documented

Explanation …

Severity …

Action …

HHC02226I
---------

HHC02226I is not yet documented

Explanation …

Severity …

Action …

HHC02227E
---------

HHC02227E is not yet documented

Explanation …

Severity …

Action …

HHC02228I
---------

HHC02228I is not yet documented

Explanation …

Severity …

Action …

HHC02229I
---------

HHC02229I is not yet documented

Explanation …

Severity …

Action …

HHC02230I
---------

HHC02230I is not yet documented

Explanation …

Severity …

Action …

HHC02231E
---------

HHC02231E is not yet documented

Explanation …

Severity …

Action …

HHC02232E
---------

HHC02232E is not yet documented

Explanation …

Severity …

Action …

HHC02233E
---------

HHC02233E is not yet documented

Explanation …

Severity …

Action …

HHC02234W
---------

HHC02234W is not yet documented

Explanation …

Severity …

Action …

HHC02235E
---------

HHC02235E is not yet documented

Explanation …

Severity …

Action …

HHC0 223 6E
---------~~

HHC02236E is not yet documented

Explanation …

Severity …

Action …

HHC02237W
---------

HHC02237W is not yet documented

Explanation …

Severity …

Action …

HHC02238E
---------

HHC02238E is not yet documented

Explanation …

Severity …

Action …

HHC02239I
---------

HHC02239I is not yet documented

Explanation …

Severity …

Action …

HHC02240I
---------

HHC02240I is not yet documented

Explanation …

Severity …

Action …

HHC02241I
---------

HHC02241I is not yet documented

Explanation …

Severity …

Action …

HHC02242I
---------

HHC02242I is not yet documented

Explanation …

Severity …

Action …

HHC02243E
---------

HHC02243E is not yet documented

Explanation …

Severity …

Action …

HHC02244E
---------

HHC02244E is not yet documented

Explanation …

Severity …

Action …

HHC02245I
---------

HHC02245I is not yet documented

Explanation …

Severity …

Action …

HHC02246E
---------

HHC02246E is not yet documented

Explanation …

Severity …

Action …

HHC02247E
---------

HHC02247E is not yet documented

Explanation …

Severity …

Action …

HHC02248I
---------

HHC02248I is not yet documented

Explanation …

Severity …

Action …

HHC02249I
---------

HHC02249I is not yet documented

Explanation …

Severity …

Action …

HHC02250I
---------

HHC02250I is not yet documented

Explanation …

Severity …

Action …

HHC02251E
---------

HHC02251E is not yet documented

Explanation …

Severity …

Action …

HHC02252E
---------

HHC02252E is not yet documented

Explanation …

Severity …

Action …

HHC02253E
---------

HHC02253E is not yet documented

Explanation …

Severity …

Action …

HHC02254I
---------

HHC02254I is not yet documented

Explanation …

Severity …

Action …

HHC02255I
---------

HHC02255I is not yet documented

Explanation …

Severity …

Action …

HHC02256W
---------

HHC02256W is not yet documented

Explanation …

Severity …

Action …

HHC02257I
---------

HHC02257I is not yet documented

Explanation …

Severity …

Action …

HHC02259E
---------

HHC02259E is not yet documented

Explanation …

Severity …

Action …

HHC02260I
---------

HHC02260I is not yet documented

Explanation …

Severity …

Action …

HHC02261W
---------

HHC02261W is not yet documented

Explanation …

Severity …

Action …

HHC02262I
---------

HHC02262I is not yet documented

Explanation …

Severity …

Action …

HHC02263I
---------

HHC02263I is not yet documented

Explanation …

Severity …

Action …

HHC02264I
---------

HHC02264I is not yet documented

Explanation …

Severity …

Action …

HHC02265I
---------

HHC02265I is not yet documented

Explanation …

Severity …

Action …

HHC02266A
---------

HHC02266A is not yet documented

Explanation …

Severity …

Action …

HHC02267I
---------

HHC02267I is not yet documented

Explanation …

Severity …

Action …

HHC02268I
---------

HHC02268I is not yet documented

Explanation …

Severity …

Action …

HHC02269I
---------

HHC02269I is not yet documented

Explanation …

Severity …

Action …

HHC02270I
---------

HHC02270I is not yet documented

Explanation …

Severity …

Action …

HHC02271I
---------

HHC02271I is not yet documented

Explanation …

Severity …

Action …

HHC02272I
---------

HHC02272I Highest observed MIPS and IO/s rates: HHC02272I From
begin_last_interval to end_last_interval HHC02272I MIPS: nnn.nnnnnn
HHC02272I IO/s: nnnn HHC02272I From begin_new_interval to
end_new_interval HHC02272I MIPS: nnn.nnnnnn HHC02272I IO/s: nnnn
HHC02272I Current interval is nnnn minutes

Explanation Message HHC02272I is the result of a MAXRATES console
command either issued manually or driven by the interval. The current
interval time in minutes is shown in the last message.

The first message block shows the maximum MIPS rate (million
instructions per second) and the mximum IO/s (IO’s per second) in the
last interval, while the second blocks shows the rates for the current
interval. The begin and end interval timestamps are in the format “Day
Mon dd hh:mm:ss yyyy”

Severity Information.

Action None. This is an informational message.

HHC02273I
---------

HHC02273I is not yet documented

Explanation …

Severity …

Action …

HHC02274I
---------

HHC02274I is not yet documented

Explanation …

Severity …

Action …

HHC02275I
---------

HHC02275I is not yet documented

Explanation …

Severity …

Action …

HHC02276I
---------

HHC02276I is not yet documented

Explanation …

Severity …

Action …

HHC02277I
---------

HHC02277I is not yet documented

Explanation …

Severity …

Action …

HHC02278I
---------

HHC02280I is not yet documented

Explanation …

Severity …

Action …

HHC02279I
---------

HHC02279I is not yet documented

Explanation …

Severity …

Action …

HHC02280I
---------

HHC02280I is not yet documented

Explanation …

Severity …

Action …

HHC02281I
---------

HHC02281I is not yet documented

Explanation …

Severity …

Action …

HHC02282I
---------

HHC02282I is not yet documented

Explanation …

Severity …

Action …

HHC02283I
---------

HHC02283I is not yet documented

Explanation …

Severity …

Action …

HHC02284I
---------

HHC02284I is not yet documented

Explanation …

Severity …

Action …

HHC02285I
---------

HHC02285I is not yet documented

Explanation …

Severity …

Action …

HHC02286I
---------

HHC02286I is not yet documented

Explanation …

Severity …

Action …

HHC02287I
---------

HHC02287I is not yet documented

Explanation …

Severity …

Action …

HHC02288I
---------

HHC02288I is not yet documented

Explanation …

Severity …

Action …

HHC02289I
---------

HHC02289I is not yet documented

Explanation …

Severity …

Action …

HHC02290I
---------

HHC02290I is not yet documented

Explanation …

Severity …

Action …

HHC02291I
---------

HHC02291I is not yet documented

Explanation …

Severity …

Action …

HHC02292I
---------

HHC02292I is not yet documented

Explanation …

Severity …

Action …

HHC02293I
---------

HHC02293I is not yet documented

Explanation …

Severity …

Action …

HHC02294I
---------

HHC02294I is not yet documented

Explanation …

Severity …

Action …

HHC02298E
---------

HHC02298E is not yet documented

Explanation …

Severity …

Action …

HHC02299E
---------

HHC02299E is not yet documented

Explanation …

Severity …

Action …

HHC02300s – HHC02399s (IEEE Component)
======================================

HHC02300I
---------

HHC02300I is not yet documented

Explanation …

Severity …

Action …

HHC02301E
---------

HHC02301E is not yet documented

Explanation …

Severity …

Action …

HHC02302W
---------

HHC02302W is not yet documented

Explanation …

Severity …

Action …

HHC02303E
---------

HHC02303E is not yet documented

Explanation …

Severity …

Action …

HHC02304W
---------

HHC02304W is not yet documented

Explanation …

Severity …

Action …

HHC02305E
---------

HHC02305E is not yet documented

Explanation …

Severity …

Action …

HHC02306E
---------

HHC02306E is not yet documented

Explanation …

Severity …

Action …

HHC02307E
---------

HHC02307E is not yet documented

Explanation …

Severity …

Action …

HHC02308W
---------

HHC02308W is not yet documented

Explanation …

Severity …

Action …

HHC02309W
---------

HHC02309W is not yet documented

Explanation …

Severity …

Action …

HHC02310S
---------

HHC0 23 10S is not yet documented

Explanation …

Severity …

Action …

HHC02311I
---------

HHC02311I is not yet documented

Explanation …

Severity …

Action …

HHC02312W
---------

HHC02312W is not yet documented

Explanation …

Severity …

Action …

HHC02313I
---------

HHC02313I is not yet documented

Explanation …

Severity …

Action …

HHC02314I
---------

HHC02314I is not yet documented

Explanation …

Severity …

Action …

HHC02315I
---------

HHC02315I is not yet documented

Explanation …

Severity …

Action …

HHC02316E
---------

HHC02316E is not yet documented

Explanation …

Severity …

Action …

HHC02318I
---------

HHC02318I is not yet documented

Explanation …

Severity …

Action …

HHC02319I
---------

HHC02319I is not yet documented

Explanation …

Severity …

Action …

HHC02386E
---------

HHC02386E is not yet documented

Explanation …

Severity …

Action …

HHC02389E
---------

HHC02389E is not yet documented

Explanation …

Severity …

Action …

30. HHC02400s – HHC02499s (DASD Utilities)
---------------------------------------------------

HHC02400E
---------

HHC02400E is not yet documented

Explanation …

Severity …

Action …

HHC02401E
---------

HHC02401E is not yet documented

Explanation …

Severity …

Action …

HHC02402E
---------

HHC02402E is not yet documented

Explanation …

Severity …

Action …

HHC02403E
---------

HHC02403E is not yet documented

Explanation …

Severity …

Action …

HHC02404E
---------

HHC02404E is not yet documented

Explanation …

Severity …

Action …

HHC02405I
---------

HHC02405I is not yet documented

Explanation …

Severity …

Action …

HHC02410I
---------

HHC02410I is not yet documented

Explanation …

Severity …

Action …

HHC02411E
---------

HHC02411E is not yet documented

Explanation …

Severity …

Action …

HHC02412E
---------

HHC02412E is not yet documented

Explanation …

Severity …

Action …

HHC02413E
---------

HHC02413E is not yet documented

Explanation …

Severity …

Action …

HHC02414I
---------

HHC02414I is not yet documented

Explanation …

Severity …

Action …

HHC02415E
---------

HHC02415E is not yet documented

Explanation …

Severity …

Action …

HHC02416E
---------

HHC02416E is not yet documented

Explanation …

Severity …

Action …

HHC02417E
---------

HHC02417E is not yet documented

Explanation …

Severity …

Action …

HHC02418E
---------

HHC02418E is not yet documented

Explanation …

Severity …

Action …

HHC02419E
---------

HHC02419E is not yet documented

Explanation …

Severity …

Action …

HHC02420I
---------

HHC02420I is not yet documented

Explanation …

Severity …

Action …

HHC02421E
---------

HHC02421E is not yet documented

Explanation …

Severity …

Action …

HHC02422I
---------

HHC02422I is not yet documented

Explanation …

Severity …

Action …

HHC02423I
---------

HHC02420I is not yet documented

Explanation …

Severity …

Action …

HHC02430E
---------

HHC02430E is not yet documented

Explanation …

Severity …

Action …

HHC02431E
---------

HHC02431E is not yet documented

Explanation …

Severity …

Action …

HHC02432E
---------

HHC02432E is not yet documented

Explanation …

Severity …

Action …

HHC02433E
---------

HHC02433E is not yet documented

Explanation …

Severity …

Action …

HHC02434E
---------

HHC02434E is not yet documented

Explanation …

Severity …

Action …

HHC02435I
---------

HHC02435I is not yet documented

Explanation …

Severity …

Action …

HHC02436I
---------

HHC02436I is not yet documented

Explanation …

Severity …

Action …

HHC02437I
---------

HHC02437I is not yet documented

Explanation …

Severity …

Action …

HHC02438I
---------

HHC02438I is not yet documented

Explanation …

Severity …

Action …

HHC02439I
---------

HHC02439I is not yet documented

Explanation …

Severity …

Action …

HHC02444E
---------

HHC02444E is not yet documented

Explanation …

Severity …

Action …

HHC02445E
---------

HHC02445E is not yet documented

Explanation …

Severity …

Action …

HHC02446E
---------

HHC02446E is not yet documented

Explanation …

Severity …

Action …

HHC02447E
---------

HHC02447E is not yet documented

Explanation …

Severity …

Action …

HHC02448I
---------

HHC02448I is not yet documented

Explanation …

Severity …

Action …

HHC02449I
---------

HHC02449I is not yet documented

Explanation …

Severity …

Action …

HHC02450I
---------

HHC02450I is not yet documented

Explanation …

Severity …

Action …

HHC02451I
---------

HHC02451I is not yet documented

Explanation …

Severity …

Action …

HHC02452E
---------

HHC02452E is not yet documented

Explanation …

Severity …

Action …

HHC02453W
---------

HHC02453W is not yet documented

Explanation …

Severity …

Action …

HHC02454W
---------

HHC02454W is not yet documented

Explanation …

Severity …

Action …

HHC02455W
---------

HHC02455W is not yet documented

Explanation …

Severity …

Action …

HHC02456E
---------

HHC02456E is not yet documented

Explanation …

Severity …

Action …

HHC02457I
---------

HHC02457I is not yet documented

Explanation …

Severity …

Action …

HHC02458E
---------

HHC02458E is not yet documented

Explanation …

Severity …

Action …

HHC02459E
---------

HHC02459E is not yet documented

Explanation …

Severity …

Action …

HHC02460E
---------

HHC02460E is not yet documented

Explanation …

Severity …

Action …

HHC02461E
---------

HHC02461E is not yet documented

Explanation …

Severity …

Action …

HHC02462I
---------

HHC02462I is not yet documented

Explanation …

Severity …

Action …

HHC02463I
---------

HHC02463I is not yet documented

Explanation …

Severity …

Action …

HHC02464I
---------

HHC02464I is not yet documented

Explanation …

Severity …

Action …

HHC02465E
---------

HHC02465E is not yet documented

Explanation …

Severity …

Action …

HHC02466I
---------

HHC02466I is not yet documented

Explanation …

Severity …

Action …

HHC02467I
---------

HHC02467I is not yet documented

Explanation …

Severity …

Action …

HHC02468E
---------

HHC02468E is not yet documented

Explanation …

Severity …

Action …

HHC02469I
---------

HHC02469I is not yet documented

Explanation …

Severity …

Action …

HHC02470E
---------

HHC02470E is not yet documented

Explanation …

Severity …

Action …

HHC02471E
---------

HHC02471E is not yet documented

Explanation …

Severity …

Action …

HHC02472E
---------

HHC02472E is not yet documented

Explanation …

Severity …

Action …

HHC02473E
---------

HHC02473E is not yet documented

Explanation …

Severity …

Action …

HHC02474E
---------

HHC02474E is not yet documented

Explanation …

Severity …

Action …

HHC02475I
---------

HHC02475I is not yet documented

Explanation …

Severity …

Action …

HHC02476E
---------

HHC0 24 76E is not yet documented

Explanation …

Severity …

Action …

HHC02477E
---------

HHC02477E is not yet documented

Explanation …

Severity …

Action …

HHC02478E
---------

HHC02478E is not yet documented

Explanation …

Severity …

Action …

HHC02479E
---------

HHC02479E is not yet documented

Explanation …

Severity …

Action …

HHC02480E
---------

HHC02480E is not yet documented

Explanation …

Severity …

Action …

HHC02481I
---------

HHC02481I is not yet documented

Explanation …

Severity …

Action …

HHC02482I
---------

HHC02482I is not yet documented

Explanation …

Severity …

Action …

HHC02483I
---------

HHC02483I is not yet documented

Explanation …

Severity …

Action …

HHC02485I
---------

HHC02485I is not yet documented

Explanation …

Severity …

Action …

HHC02486I
---------

HHC02486I is not yet documented

Explanation …

Severity …

Action …

HHC02487I
---------

HHC02487I is not yet documented

Explanation …

Severity …

Action …

HHC02488I
---------

HHC02488I is not yet documented

Explanation …

Severity …

Action …

HHC02489E
---------

HHC02489E is not yet documented

Explanation …

Severity …

Action …

HHC02490E
---------

HHC02490E is not yet documented

Explanation …

Severity …

Action …

HHC02491E
---------

HHC02491E is not yet documented

Explanation …

Severity …

Action …

HHC02494I
---------

HHC02494I is not yet documented

Explanation …

Severity …

Action …

HHC02495I
---------

HHC02495I is not yet documented

Explanation …

Severity …

Action …

HHC02496I
---------

HHC02496I is not yet documented

Explanation …

Severity …

Action …

HHC02499I
---------

HHC02499I is not yet documented

Explanation …

Severity …

Action …

31. HHC02500s – HHC02599s (DASD Utilities)
---------------------------------------------------

HHC02500E
---------

HHC02500E is not yet documented

Explanation …

Severity …

Action …

HHC02501E
---------

HHC02501E is not yet documented

Explanation …

Severity …

Action …

HHC02502E
---------

HHC02502E is not yet documented

Explanation …

Severity …

Action …

HHC02503E
---------

HHC02503E is not yet documented

Explanation …

Severity …

Action …

HHC02504E
---------

HHC02504E is not yet documented

Explanation …

Severity …

Action …

HHC02505E
---------

HHC02505E is not yet documented

Explanation …

Severity …

Action …

HHC02506E
---------

HHC02506E is not yet documented

Explanation …

Severity …

Action …

HHC02507E
---------

HHC02507E is not yet documented

Explanation …

Severity …

Action …

HHC02508E
---------

HHC02508E is not yet documented

Explanation …

Severity …

Action …

HHC02509E
---------

HHC02509E is not yet documented

Explanation …

Severity …

Action …

HHC02510E
---------

HHC02510E is not yet documented

Explanation …

Severity …

Action …

HHC02511E
---------

HHC02511E is not yet documented

Explanation …

Severity …

Action …

HHC02512E
---------

HHC02512E is not yet documented

Explanation …

Severity …

Action …

HHC02513E
---------

HHC02513E is not yet documented

Explanation …

Severity …

Action …

HHC02514E
---------

HHC02514E is not yet documented

Explanation …

Severity …

Action …

HHC02515E
---------

HHC02515E is not yet documented

Explanation …

Severity …

Action …

HHC02516E
---------

HHC02516E is not yet documented

Explanation …

Severity …

Action …

HHC02517E
---------

HHC02517E is not yet documented

Explanation …

Severity …

Action …

HHC02518E
---------

HHC02518E is not yet documented

Explanation …

Severity …

Action …

HHC02519E
---------

HHC02519E is not yet documented

Explanation …

Severity …

Action …

HHC02520I
---------

HHC02520I is not yet documented

Explanation …

Severity …

Action …

HHC02521I
---------

HHC02521I is not yet documented

Explanation …

Severity …

Action …

HHC02522I
---------

HHC02522I is not yet documented

Explanation …

Severity …

Action …

HHC02523I
---------

HHC02523I is not yet documented

Explanation …

Severity …

Action …

HHC02524I
---------

HHC02524I is not yet documented

Explanation …

Severity …

Action …

HHC02525I
---------

HHC02525I is not yet documented

Explanation …

Severity …

Action …

HHC02526I
---------

HHC02526I is not yet documented

Explanation …

Severity …

Action …

HHC02527I
---------

HHC02527I is not yet documented

Explanation …

Severity …

Action …

HHC02528I
---------

HHC02528I is not yet documented

Explanation …

Severity …

Action …

HHC02529I
---------

HHC02529I is not yet documented

Explanation …

Severity …

Action …

HHC02530E
---------

HHC02530E is not yet documented

Explanation …

Severity …

Action …

HHC02531E
---------

HHC02531E is not yet documented

Explanation …

Severity …

Action …

HHC02532E
---------

HHC02532E is not yet documented

Explanation …

Severity …

Action …

HHC02533E
---------

HHC02533E is not yet documented

Explanation …

Severity …

Action …

HHC02534E
---------

HHC02534E is not yet documented

Explanation …

Severity …

Action …

HHC02535E
---------

HHC02535E is not yet documented

Explanation …

Severity …

Action …

HHC02536E
---------

HHC02536E is not yet documented

Explanation …

Severity …

Action …

HHC02537E
---------

HHC02537E is not yet documented

Explanation …

Severity …

Action …

HHC02538E
---------

HHC02538E is not yet documented

Explanation …

Severity …

Action …

HHC02539E
---------

HHC02539E is not yet documented

Explanation …

Severity …

Action …

HHC02540E
---------

HHC02540E is not yet documented

Explanation …

Severity …

Action …

HHC02541E
---------

HHC02541E is not yet documented

Explanation …

Severity …

Action …

HHC02542E
---------

HHC02542E is not yet documented

Explanation …

Severity …

Action …

HHC02543E
---------

HHC02543E is not yet documented

Explanation …

Severity …

Action …

HHC02544E
---------

HHC02544E is not yet documented

Explanation …

Severity …

Action …

HHC02545E
---------

HHC02545E is not yet documented

Explanation …

Severity …

Action …

HHC02546E
---------

HHC02546E is not yet documented

Explanation …

Severity …

Action …

HHC02547E
---------

HHC02547E is not yet documented

Explanation …

Severity …

Action …

HHC02548E
---------

HHC02548E is not yet documented

Explanation …

Severity …

Action …

HHC02549E
---------

HHC02549E is not yet documented

Explanation …

Severity …

Action …

HHC02550I
---------

HHC02550I is not yet documented

Explanation …

Severity …

Action …

HHC02551I
---------

HHC02551I is not yet documented

Explanation …

Severity …

Action …

HHC02552I
---------

HHC02552I is not yet documented

Explanation …

Severity …

Action …

HHC02553I
---------

HHC02553I is not yet documented

Explanation …

Severity …

Action …

HHC02554I
---------

HHC02554I is not yet documented

Explanation …

Severity …

Action …

HHC02555I
---------

HHC02555I is not yet documented

Explanation …

Severity …

Action …

HHC02556I
---------

HHC02556I is not yet documented

Explanation …

Severity …

Action …

HHC02557I
---------

HHC02557I is not yet documented

Explanation …

Severity …

Action …

HHC02558I
---------

HHC02558I is not yet documented

Explanation …

Severity …

Action …

HHC02559E
---------

HHC02559E is not yet documented

Explanation …

Severity …

Action …

HHC02560I
---------

HHC02560I is not yet documented

Explanation …

Severity …

Action …

HHC02561I
---------

HHC02561I is not yet documented

Explanation …

Severity …

Action …

HHC02562I
---------

HHC02562I is not yet documented

Explanation …

Severity …

Action …

HHC02563I
---------

HHC02563I is not yet documented

Explanation …

Severity …

Action …

HHC02564I
---------

HHC02564I is not yet documented

Explanation …

Severity …

Action …

HHC02565I
---------

HHC02565I is not yet documented

Explanation …

Severity …

Action …

HHC02566I
---------

HHC02566I is not yet documented

Explanation …

Severity …

Action …

HHC02567I
---------

HHC02567I is not yet documented

Explanation …

Severity …

Action …

HHC02568I
---------

HHC02568I is not yet documented

Explanation …

Severity …

Action …

HHC02569E
---------

HHC02569E is not yet documented

Explanation …

Severity …

Action …

HHC02570E
---------

HHC02570E is not yet documented

Explanation …

Severity …

Action …

HHC02571E
---------

HHC02571E is not yet documented

Explanation …

Severity …

Action …

HHC02572W
---------

HHC02572W is not yet documented

Explanation …

Severity …

Action …

HHC02573E
---------

HHC02573E is not yet documented

Explanation …

Severity …

Action …

HHC02574E
---------

HHC02574E is not yet documented

Explanation …

Severity …

Action …

HHC02575E
---------

HHC02575E is not yet documented

Explanation …

Severity …

Action …

HHC02576E
---------

HHC02576E is not yet documented

Explanation …

Severity …

Action …

HHC02577E
---------

HHC02577E is not yet documented

Explanation …

Severity …

Action …

HHC02578E
---------

HHC02578E is not yet documented

Explanation …

Severity …

Action …

HHC02579E
---------

HHC02579E is not yet documented

Explanation …

Severity …

Action …

HHC02580E
---------

HHC02580E is not yet documented

Explanation …

Severity …

Action …

HHC02581E
---------

HHC02581E is not yet documented

Explanation …

Severity …

Action …

HHC02582E
---------

HHC02582E is not yet documented

Explanation …

Severity …

Action …

HHC02583E
---------

HHC02583E is not yet documented

Explanation …

Severity …

Action …

HHC02584E
---------

HHC02584E is not yet documented

Explanation …

Severity …

Action …

HHC02585E
---------

HHC02585E is not yet documented

Explanation …

Severity …

Action …

HHC02586E
---------

HHC02586E is not yet documented

Explanation …

Severity …

Action …

HHC02587E
---------

HHC02587E is not yet documented

Explanation …

Severity …

Action …

HHC02588E
---------

HHC02588E is not yet documented

Explanation …

Severity …

Action …

HHC02589I
---------

HHC02589I is not yet documented

Explanation …

Severity …

Action …

HHC02590W
---------

HHC02590W is not yet documented

Explanation …

Severity …

Action …

HHC02591I
---------

HHC02591I is not yet documented

Explanation …

Severity …

Action …

HHC02592I
---------

HHC02592I is not yet documented

Explanation …

Severity …

Action …

HHC02593E
---------

HHC02593E is not yet documented

Explanation …

Severity …

Action …

32. HHC02600s – HHC02699s (Various Utilities)
------------------------------------------------------

HHC02600I
---------

HHC02600I is not yet documented

Explanation …

Severity …

Action …

HHC02601I
---------

HHC02601I is not yet documented

Explanation …

Severity …

Action …

HHC02602E
---------

HHC02602E is not yet documented

Explanation …

Severity …

Action …

HHC02603E
---------

HHC02603E is not yet documented

Explanation …

Severity …

Action …

HHC02604E
---------

HHC02604E is not yet documented

Explanation …

Severity …

Action …

HHC02605I
---------

HHC02605I is not yet documented

Explanation …

Severity …

Action …

HHC02606I
---------

HHC02606I is not yet documented

Explanation …

Severity …

Action …

HHC02607I
---------

HHC02607I is not yet documented

Explanation …

Severity …

Action …

HHC02608I
---------

HHC02608I is not yet documented

Explanation …

Severity …

Action …

33. HHC02700s – HHC02799s (Tape Utilities)
---------------------------------------------------

HHC02700I
---------

HHC02700I is not yet documented

Explanation …

Severity …

Action …

HHC02701E
---------

HHC02701E is not yet documented

Explanation …

Severity …

Action …

HHC02702I
---------

HHC02702I is not yet documented

Explanation …

Severity …

Action …

HHC02703E
---------

HHC02703E is not yet documented

Explanation …

Severity …

Action …

HHC02704I
---------

HHC02704I is not yet documented

Explanation …

Severity …

Action …

HHC02705E
---------

HHC02705E is not yet documented

Explanation …

Severity …

Action …

HHC02706I
---------

HHC02706I is not yet documented

Explanation …

Severity …

Action …

HHC02707E
---------

HHC02707E is not yet documented

Explanation …

Severity …

Action …

HHC02708E
---------

HHC02708E is not yet documented

Explanation …

Severity …

Action …

HHC02709E
---------

HHC02709E is not yet documented

Explanation …

Severity …

Action …

HHC02710E
---------

HHC02710E is not yet documented

Explanation …

Severity …

Action …

HHC02711E
---------

HHC02711E is not yet documented

Explanation …

Severity …

Action …

HHC02712E
---------

HHC02712E is not yet documented

Explanation …

Severity …

Action …

HHC02713E
---------

HHC02713E is not yet documented

Explanation …

Severity …

Action …

HHC02714E
---------

HHC02714E is not yet documented

Explanation …

Severity …

Action …

HHC02715E
---------

HHC02715E is not yet documented

Explanation …

Severity …

Action …

HHC02716E
---------

HHC02716E is not yet documented

Explanation …

Severity …

Action …

HHC02717E
---------

HHC02717E is not yet documented

Explanation …

Severity …

Action …

HHC02718I
---------

HHC02718I is not yet documented

Explanation …

Severity …

Action …

HHC02719I
---------

HHC02719I is not yet documented

Explanation …

Severity …

Action …

HHC02720E
---------

HHC02720E is not yet documented

Explanation …

Severity …

Action …

HHC02721I
---------

HHC02721I is not yet documented

Explanation …

Severity …

Action …

HHC02722I
---------

HHC02722I is not yet documented

Explanation …

Severity …

Action …

HHC02723I
---------

HHC02723I is not yet documented

Explanation …

Severity …

Action …

HHC02724I
---------

HHC02724I is not yet documented

Explanation …

Severity …

Action …

HHC02725I
---------

HHC02725I is not yet documented

Explanation …

Severity …

Action …

HHC02726I
---------

HHC02726I is not yet documented

Explanation …

Severity …

Action …

HHC02728I
---------

HHC02728I is not yet documented

Explanation …

Severity …

Action …

HHC02729I
---------

HHC02729I is not yet documented

Explanation …

Severity …

Action …

HHC02730I
---------

HHC02730I is not yet documented

Explanation …

Severity …

Action …

HHC02740I
---------

HHC02740I is not yet documented

Explanation …

Severity …

Action …

HHC02741E
---------

HHC02741E is not yet documented

Explanation …

Severity …

Action …

HHC02742E
---------

HHC02742E is not yet documented

Explanation …

Severity …

Action …

HHC02743E
---------

HHC02743E is not yet documented

Explanation …

Severity …

Action …

HHC02744I
---------

HHC02744I is not yet documented

Explanation …

Severity …

Action …

HHC02745I
---------

HHC02745I is not yet documented

Explanation …

Severity …

Action …

HHC02750E
---------

HHC02750E is not yet documented

Explanation …

Severity …

Action …

HHC02751I
---------

HHC02751I is not yet documented

Explanation …

Severity …

Action …

HHC02752I
---------

HHC02752I is not yet documented

Explanation …

Severity …

Action …

HHC02753E
---------

HHC02753E is not yet documented

Explanation …

Severity …

Action …

HHC02754E
---------

HHC02754E is not yet documented

Explanation …

Severity …

Action …

HHC02755I
---------

HHC02755I is not yet documented

Explanation …

Severity …

Action …

HHC02756E
---------

HHC02756E is not yet documented

Explanation …

Severity …

Action …

HHC02757I
---------

HHC02757I is not yet documented

Explanation …

Severity …

Action …

34. HHC02800s – HHC02899s (Tape Utilities)
---------------------------------------------------

HHC02800I
---------

HHC02800I is not yet documented

Explanation …

Severity …

Action …

HHC02801E
---------

HHC02801E is not yet documented

Explanation …

Severity …

Action …

HHC02802I
---------

HHC02802I is not yet documented

Explanation …

Severity …

Action …

HHC02803I
---------

HHC02803I is not yet documented

Explanation …

Severity …

Action …

HHC02804E
---------

HHC02804E is not yet documented

Explanation …

Severity …

Action …

HHC02805I
---------

HHC02805I is not yet documented

Explanation …

Severity …

Action …

HHC02806I
---------

HHC02806I is not yet documented

Explanation …

Severity …

Action …

35. HHC03900s – HHC03999s (PTP Adapter Emulation)
----------------------------------------------------------

HHC03901E
---------

HHC03901E is not yet documented

Explanation …

Severity …

Action …

HHC03902E
---------

HHC03902E is not yet documented

Explanation …

Severity …

Action …

HHC03903I
---------

HHC03903I is not yet documented

Explanation …

Severity …

Action …

HHC03904I
---------

HHC03904I is not yet documented

Explanation …

Severity …

Action …

HHC03905I
---------

HHC03905I is not yet documented

Explanation …

Severity …

Action …

HHC03906I
---------

HHC03906I is not yet documented

Explanation …

Severity …

Action …

HHC03907I
---------

HHC03907I is not yet documented

Explanation …

Severity …

Action …

HHC03908I
---------

HHC03908I is not yet documented

Explanation …

Severity …

Action …

HHC03909I
---------

HHC03909I is not yet documented

Explanation …

Severity …

Action …

HHC03910I
---------

HHC03910I is not yet documented

Explanation …

Severity …

Action …

HHC03911I
---------

HHC03911I is not yet documented

Explanation …

Severity …

Action …

HHC03912E
---------

HHC03912E is not yet documented

Explanation …

Severity …

Action …

HHC03913W
---------

HHC03913W is not yet documented

Explanation …

Severity …

Action …

HHC03914W
---------

HHC03914W is not yet documented

Explanation …

Severity …

Action …

HHC03915I
---------

HHC03915I is not yet documented

Explanation …

Severity …

Action …

HHC03916I
---------

HHC03916I is not yet documented

Explanation …

Severity …

Action …

HHC03917W
---------

HHC03917W is not yet documented

Explanation …

Severity …

Action …

HHC03918W
---------

HHC03918W is not yet documented

Explanation …

Severity …

Action …

HHC03921W
---------

HHC03921W is not yet documented

Explanation …

Severity …

Action …

HHC03922W
---------

HHC03922W is not yet documented

Explanation …

Severity …

Action …

HHC03923W
---------

HHC03923W is not yet documented

Explanation …

Severity …

Action …

HHC03924W
---------

HHC03924W is not yet documented

Explanation …

Severity …

Action …

HHC03931W
---------

HHC03931W is not yet documented

Explanation …

Severity …

Action …

HHC03932W
---------

HHC03932W is not yet documented

Explanation …

Severity …

Action …

HHC03933W
---------

HHC03933W is not yet documented

Explanation …

Severity …

Action …

HHC03934W
---------

HHC03934W is not yet documented

Explanation …

Severity …

Action …

HHC03935W
---------

HHC03935W is not yet documented

Explanation …

Severity …

Action …

HHC03936W
---------

HHC03936W is not yet documented

Explanation …

Severity …

Action …

HHC03937W
---------

HHC03937W is not yet documented

Explanation …

Severity …

Action …

HHC03952I
---------

HHC03952I is not yet documented

Explanation …

Severity …

Action …

HHC03953I
---------

HHC03953I is not yet documented

Explanation …

Severity …

Action …

HHC03954I
---------

HHC03954I is not yet documented

Explanation …

Severity …

Action …

HHC03983I
---------

HHC03983I is not yet documented

Explanation …

Severity …

Action …

HHC03984I
---------

HHC03984I is not yet documented

Explanation …

Severity …

Action …

HHC03985E
---------

HHC03985E is not yet documented

Explanation …

Severity …

Action …

HHC03991I
---------

HHC03991I is not yet documented

Explanation …

Severity …

Action …

HHC03992D
---------

HHC03992D is not yet documented

Explanation …

Severity …

Action …

HHC03993D
---------

HHC03993D is not yet documented

Explanation …

Severity …

Action …

HHC03995D
---------

HHC03995D is not yet documented

Explanation …

Severity …

Action …

36. HHC04100s – HHC04199s (Windows Specific Components)
----------------------------------------------------------------

HHC04100I
---------

HHC04100I is not yet documented

Explanation …

Severity …

Action …

HHC04101I
---------

HHC04101I is not yet documented

Explanation …

Severity …

Action …

HHC04102E
---------

HHC04102E is not yet documented

Explanation …

Severity …

Action …

HHC04110W
---------

HHC04110W is not yet documented

Explanation …

Severity …

Action …

HHC04111E
---------

HHC04111E is not yet documented

Explanation …

Severity …

Action …

HHC04112S
---------

HHC04112S is not yet documented

Explanation …

Severity …

Action …

37. HHC17000s – HHC17099s (Query Commands)
---------------------------------------------------

HHC17000E
---------

HHC17000E is not yet documented

Explanation …

Severity …

Action …

HHC17001I
---------

HHC17001I is not yet documented

Explanation …

Severity …

Action …

HHC17002I
---------

HHC17002I is not yet documented

Explanation …

Severity …

Action …

HHC17003I
---------

HHC17003I is not yet documented

Explanation …

Severity …

Action …

HHC17004I
---------

HHC17004I is not yet documented

Explanation …

Severity …

Action …

HHC17005I
---------

HHC17005I is not yet documented

Explanation …

Severity …

Action …

HHC17007I
---------

HHC17007I is not yet documented

Explanation …

Severity …

Action …

HHC17008I
---------

HHC17008I is not yet documented

Explanation …

Severity …

Action …

HHC17009I
---------

HHC17009I is not yet documented

Explanation …

Severity …

Action …

HHC17010I
---------

HHC17010I is not yet documented

Explanation …

Severity …

Action …

HHC17011I
---------

HHC17011I is not yet documented

Explanation …

Severity …

Action …

HHC17012I
---------

HHC17012I is not yet documented

Explanation …

Severity …

Action …

HHC17013I
---------

HHC17013I is not yet documented

Explanation …

Severity …

Action …

38. HHC17500s – HHC17599s (REXX Support)
-------------------------------------------------

HHC17500I
---------

HHC17500I is not yet documented

Explanation …

Severity …

Action …

HHC17501I
---------

HHC17501I is not yet documented

Explanation …

Severity …

Action …

HHC17502E
---------

HHC17502E is not yet documented

Explanation …

Severity …

Action …

HHC17503E
---------

HHC17503E is not yet documented

Explanation …

Severity …

Action …

HHC17504E
---------

HHC17504E is not yet documented

Explanation …

Severity …

Action …

HHC17505E
---------

HHC17505E is not yet documented

Explanation …

Severity …

Action …

HHC17506E
---------

HHC17506E is not yet documented

Explanation …

Severity …

Action …

HHC17507W
---------

HHC17507W is not yet documented

Explanation …

Severity …

Action …

HHC17508W
---------

HHC17508W is not yet documented

Explanation …

Severity …

Action …

HHC17509W
---------

HHC17509W is not yet documented

Explanation …

Severity …

Action …

HHC17510W
---------

HHC17510W is not yet documented

Explanation …

Severity …

Action …

HHC17521I
---------

HHC17521I is not yet documented

Explanation …

Severity …

Action …

HHC17522I
---------

HHC17522I is not yet documented

Explanation …

Severity …

Action …

HHC17523I
---------

HHC17523I is not yet documented

Explanation …

Severity …

Action …

HHC17524I
---------

HHC17524I is not yet documented

Explanation …

Severity …

Action …

HHC17525I
---------

HHC17525I is not yet documented

Explanation …

Severity …

Action …

HHC17526I
---------

HHC17521I is not yet documented

Explanation …

Severity …

Action …

HHC17527I
---------

HHC17527I is not yet documented

Explanation …

Severity …

Action …

HHC17530E
---------

HHC17530E is not yet documented

Explanation …

Severity …

Action …

HHC17531E
---------

HHC17531E is not yet documented

Explanation …

Severity …

Action …

HHC17532E
---------

HHC17532E is not yet documented

Explanation …

Severity …

Action …

HHC17533E
---------

HHC17533E is not yet documented

Explanation …

Severity …

Action …

HHC17534E
---------

HHC17534E is not yet documented

Explanation …

Severity …

Action …

39. HHC90000s – HHC90099s (Debug Messages PTTRACE)
-----------------------------------------------------------

HHC90000D
---------

HHC90000D is not yet documented

Explanation …

Severity …

Action …

HHC90010E
---------

HHC90010E is not yet documented

Explanation …

Severity …

Action …

HHC90011E
---------

HHC90011E is not yet documented

Explanation …

Severity …

Action …

HHC90012I
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90013E
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90014I
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90015E
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90016E
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90017I
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90018I
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

HHC90019W
---------

HHC90012I is not yet documented

Explanation …

Severity …

Action …

40. HHC90100s – HHC90199s (Debug Messages DYNCRYPT)
------------------------------------------------------------

HHC90100D
---------

HHC90100D is not yet documented

Explanation …

Severity …

Action …

HHC90101D
---------

HHC90101D is not yet documented

Explanation …

Severity …

Action …

HHC90102D
---------

HHC90102D is not yet documented

Explanation …

Severity …

Action …

HHC90103D
---------

HHC90103D is not yet documented

Explanation …

Severity …

Action …

HHC90104D
---------

HHC90104D is not yet documented

Explanation …

Severity …

Action …

HHC90105D
---------

HHC90105D is not yet documented

Explanation …

Severity …

Action …

HHC90106D
---------

HHC90106D is not yet documented

Explanation …

Severity …

Action …

HHC90107D
---------

HHC90107D is not yet documented

Explanation …

Severity …

Action …

HHC90108D
---------

HHC90108D is not yet documented

Explanation …

Severity …

Action …

HHC90109D
---------

HHC90109D is not yet documented

Explanation …

Severity …

Action …

HHC90110D
---------

HHC90110D is not yet documented

Explanation …

Severity …

Action …

HHC90111D
---------

HHC90111D is not yet documented

Explanation …

Severity …

Action …

HHC90112D
---------

HHC90112D is not yet documented

Explanation …

Severity …

Action …

HHC90190D
---------

HHC90190D is not yet documented

Explanation …

Severity …

Action …

41. HHC90200s – HHC90299s (Debug Messages SCSITAPE)
------------------------------------------------------------

HHC90205D
---------

HHC90205D is not yet documented

Explanation …

Severity …

Action …

42. HHC90300s – HHC90399s (Debug Messages CMPSC)
---------------------------------------------------------

HHC90300D
---------

HHC90300D is not yet documented

Explanation …

Severity …

Action …

HHC90301D
---------

HHC90301D is not yet documented

Explanation …

Severity …

Action …

HHC90302D
---------

HHC90302D is not yet documented

Explanation …

Severity …

Action …

HHC90303D
---------

HHC90303D is not yet documented

Explanation …

Severity …

Action …

HHC90304D
---------

HHC90304D is not yet documented

Explanation …

Severity …

Action …

HHC90305D
---------

HHC90305D is not yet documented

Explanation …

Severity …

Action …

HHC90306D
---------

HHC90306D is not yet documented

Explanation …

Severity …

Action …

HHC90307D
---------

HHC90307D is not yet documented

Explanation …

Severity …

Action …

HHC90308D
---------

HHC90308D is not yet documented

Explanation …

Severity …

Action …

HHC90309D
---------

HHC90309D is not yet documented

Explanation …

Severity …

Action …

HHC90310D
---------

HHC90310D is not yet documented

Explanation …

Severity …

Action …

HHC90311D
---------

HHC90311D is not yet documented

Explanation …

Severity …

Action …

HHC90312D
---------

HHC90312D is not yet documented

Explanation …

Severity …

Action …

HHC90313D
---------

HHC90313D is not yet documented

Explanation …

Severity …

Action …

HHC90314D
---------

HHC90314D is not yet documented

Explanation …

Severity …

Action …

HHC90315D
---------

HHC90315D is not yet documented

Explanation …

Severity …

Action …

HHC90316D
---------

HHC90316D is not yet documented

Explanation …

Severity …

Action …

HHC90317D
---------

HHC90317D is not yet documented

Explanation …

Severity …

Action …

HHC90318D
---------

HHC90318D is not yet documented

Explanation …

Severity …

Action …

HHC90319D
---------

HHC90319D is not yet documented

Explanation …

Severity …

Action …

HHC90320D
---------

HHC90320D is not yet documented

Explanation …

Severity …

Action …

HHC90321D
---------

HHC90321D is not yet documented

Explanation …

Severity …

Action …

HHC90322D
---------

HHC90322D is not yet documented

Explanation …

Severity …

Action …

HHC90323D
---------

HHC90323D is not yet documented

Explanation …

Severity …

Action …

HHC90324D
---------

HHC90324D is not yet documented

Explanation …

Severity …

Action …

HHC90325D
---------

HHC90325D is not yet documented

Explanation …

Severity …

Action …

HHC90326D
---------

HHC90326D is not yet documented

Explanation …

Severity …

Action …

HHC90327D
---------

HHC90327D is not yet documented

Explanation …

Severity …

Action …

HHC90328D
---------

HHC90328D is not yet documented

Explanation …

Severity …

Action …

HHC90329D
---------

HHC90329D is not yet documented

Explanation …

Severity …

Action …

HHC90330D
---------

HHC90330D is not yet documented

Explanation …

Severity …

Action …

HHC90331D
---------

HHC90331D is not yet documented

Explanation …

Severity …

Action …

HHC90332D
---------

HHC90332D is not yet documented

Explanation …

Severity …

Action …

HHC90333D
---------

HHC90333D is not yet documented

Explanation …

Severity …

Action …

HHC90334D
---------

HHC90334D is not yet documented

Explanation …

Severity …

Action …

HHC90335D
---------

HHC90335D is not yet documented

Explanation …

Severity …

Action …

HHC90336D
---------

HHC90336D is not yet documented

Explanation …

Severity …

Action …

HHC90337D
---------

HHC90337D is not yet documented

Explanation …

Severity …

Action …

HHC90338D
---------

HHC90338D is not yet documented

Explanation …

Severity …

Action …

HHC90339D
---------

HHC90339D is not yet documented

Explanation …

Severity …

Action …

HHC90340D
---------

HHC90340D is not yet documented

Explanation …

Severity …

Action …

HHC90341D
---------

HHC90341D is not yet documented

Explanation …

Severity …

Action …

HHC90342D
---------

HHC90342D is not yet documented

Explanation …

Severity …

Action …

HHC90343D
---------

HHC90343D is not yet documented

Explanation …

Severity …

Action …

HHC90344D
---------

HHC90344D is not yet documented

Explanation …

Severity …

Action …

HHC90345D
---------

HHC90345D is not yet documented

Explanation …

Severity …

Action …

HHC90346D
---------

HHC90346D is not yet documented

Explanation …

Severity …

Action …

HHC90347D
---------

HHC90347D is not yet documented

Explanation …

Severity …

Action …

HHC90349D
---------

HHC90349D is not yet documented

Explanation …

Severity …

Action …

HHC90350D
---------

HHC90350D is not yet documented

Explanation …

Severity …

Action …

HHC90351D
---------

HHC90351D is not yet documented

Explanation …

Severity …

Action …

HHC90352D
---------

HHC90352D is not yet documented

Explanation …

Severity …

Action …

HHC90353D
---------

HHC90353D is not yet documented

Explanation …

Severity …

Action …

HHC90354D
---------

HHC90354D is not yet documented

Explanation …

Severity …

Action …

HHC90355D
---------

HHC90355D is not yet documented

Explanation …

Severity …

Action …

HHC90356D
---------

HHC90356D is not yet documented

Explanation …

Severity …

Action …

HHC90357D
---------

HHC90357D is not yet documented

Explanation …

Severity …

Action …

HHC90358D
---------

HHC90358D is not yet documented

Explanation …

Severity …

Action …

HHC90359D
---------

HHC90359D is not yet documented

Explanation …

Severity …

Action …

HHC90360D
---------

HHC90360D is not yet documented

Explanation …

Severity …

Action …

HHC90361D
---------

HHC90361D is not yet documented

Explanation …

Severity …

Action …

HHC90362D
---------

HHC90362D is not yet documented

Explanation …

Severity …

Action …

HHC90363D
---------

HHC90363D is not yet documented

Explanation …

Severity …

Action …

HHC90364D
---------

HHC90364D is not yet documented

Explanation …

Severity …

Action …

Part II: Old Messages
---------------------

43. HHCAOnnns - Hercules Automatic Operator
----------------------------------------------------

HHCAOnnns
---------

Messages HHCAOnnns are not yet documented.

44. HHCCAnnns - Communication Adapter Emulation
--------------------------------------------------------

HHCCA001I
---------

HHCCA001I CCUU:Connect out to ipaddr:port failed during initial status :
System Cause Text

Explanation Hercules attempted to make an outgoing TCP connection to
ipaddr:port but the system indicated that there was an error while
processing the request.

System Action The DIAL or ENABLE CCW that caused the connection attempt
ends with Unit Check and Intervention Required. The reason for the
failure is indicated in the System Cause Text field

Operator Action None. This is an informational message.

Programmer Action Correct the RHOST/RPORT configuration statements in
the configuration file. If this message occured during a program
initiated DIAL, correct the dial data.

HHCCA002I
---------

HHCCA002I CCUU:Line Communication thread thread id started

Explanation The thread responsible for asynchronous operations for the
BSC emulated line CCUU has been started.

System Action The system continues.

Operator Action None. This is an informational message.

Programmer Action None. This is an informational message.

HHCCA003E
---------

HHCCA003E CCUU:Cannot obtain socket for incoming calls : System Cause
Text

Explanation A system error occured while attempting to create a socket
to listen for incoming calls.

System Action The device creation is aborted.

Operator Action None.

Programmer Action Check the System Cause Text for any information
relating to the host system. Notify support.

HHCCA004W
---------

HHCCA004W CCUU:Waiting 5 seconds for port port to become available

Explanation While attempting to reserve port port to listen to, the
system indicated the port was already being used.

System Action The system waits 5 seconds and then retries the operation.

Operator Action Terminate the device if the port is in error.

Programmer Action Determine the program holding the specified port. If
the port cannot be made available, use a different port.

HHCCA005I
---------

HHCCA005I CCUU:Listening on port port for incoming TCP connections

Explanation The system is now listening on port port for incoming a tcp
connection.

System Action The system continues.

Operator Action None. This is an informational message.

Programmer Action None. This is an informational message.

HHCCA006T
---------

HHCCA006T CCUU:Select failed : System Cause Text

Explanation An error occured during a ‘select’ system call.

System Action The BSC thread is terminated.

Operator Action None.

Programmer Action Check the System Cause Text for any indication of
where the error might come from. Notify Support.

HHCCA007W
---------

HHCCA007W CCUU:Outgoing call failed during ENABLE|DIAL command : System
Cause Text

Explanation The system reported that a previously initiated TCP
connection could not be completed.

System Action The I/O operation responsible for the TCP outgoing
connection is ended with Unit Check and Intervention Required.

Operator Action If the error indicates that the error is temporary,
retry the operation.

Programmer Action Check that the destination for this line is correctly
configured. If the operation was a DIAL attempt, check in the
application configuration or operation data.

HHCCA008I
---------

HHCCA008I CCUU:cthread - Incoming Call

Explanation The BSC thread has received an incoming call.

System Action Depending on configuration and operational status, the
call is either accepted or rejected. Eventually an ongoing I/O operation
may complete.

Operator Action None. This is an informational message.

Programmer Action None. This is an informational message.

HHCCA009I
---------

HHCCA009I CCUU:BSC utility thread terminated

Explanation The BSC thread has ended.

System Action The system continues.

Operator Action Refer to any previous error message to determine if this
message was not unexpected.

Programmer Action Refer to any previous error message to determine if
this message was not unexpected.

HHCCA010I
---------

HHCCA010I CCUU:initialization not performed

Explanation The Device initialization process has failed.

System Action The system terminates or continues, depending on the
reason for which the device was initialization was initiated.

Operator Action Refer to any previous error message.

Programmer Action Refer to any previous error message.

HHCCA011E
---------

HHCCA011E CCUU:Error parsing Keyword

Explanation The device keyword parser found an error while parsing a
known keyword.

System Action The system continues. The device initialization routine
turns on a NOGO flag.

Operator Action For a runtime initialization, correct the device
initialization parameters, otherwise notify the programmer.

Programmer Action For an engine initialization, correct the device
configuration parameters in the configuration file.

HHCCA012E
---------

HHCCA012E CCUU:Unrecognized parameter Keyword

Explanation The device keyword parser found an unknown keyword in the
device parameter list.

System Action The system continues. The device initialization routine
turns on a NOGO flag.

Operator Action For a runtime initialization, correct the device
initialization parameters, otherwise notify the programmer.

Programmer Action For an engine initialization, correct the device
configuration parameters in the configuration file.

HHCCA013E
---------

HHCCA013E CCUU:Incorrect local port|remote port|local host|remote host
specification value

Explanation The device initialization routine could not correctly parse
a parameter value.

System Action The system continues. The device initialization routine
turns on a NOGO flag.

Operator Action For a runtime initialization, correct the device
initialization parameters, otherwise notify the programmer.

Programmer Action For an engine initialization, correct the device
configuration parameters in the configuration file.

HHCCA014E
---------

HHCCA014E CCUU:Incorrect switched/dial specification value; defaulting
to DIAL=OUT

Explanation The device initialization routine found an incorrect DIAL
value.

System Action The system continues. The device initialization routine
turns on a NOGO flag.

Operator Action For a runtime initialization, correct the device
initialization parameters, otherwise notify the programmer.

Programmer Action For an engine initialization, correct the device
configuration parameters in the configuration file.

HHCCA015E
---------

HHCCA015E CCUU:Missing parameter : DIAL=NO|IN|OUT|INOUT and
LPORT|RPORT|LHOST|RHOST not specified

Explanation The device initialization routine found that a mandatory
parameter was not provided for a specific DIAL Value.

System Action The system continues. The device initialization routine
turns on a NOGO flag.

Operator Action For a runtime initialization, correct the device
initialization parameters, otherwise notify the programmer.

Programmer Action For an engine initialization, correct the device
configuration parameters in the configuration file.

Note For DIAL=NO , LPORT, RPORT and RHOST are needed For DIAL=IN , LPORT
is required

For DIAL=OUT None of LPORT,LHOST,RPORT,RHOST are required For
DIAL=INOUT, LPORT is required

HHCCA016W
---------

HHCCA016W CCUU:Conflicting parameter : DIAL=NO|IN|OUT|INOUT and
LPORT|RPORT|LHOST|RHOST=value specified

Explanation The device initialization routine found that a parameter was
provided for a parameter that is not relevant for a specific DIAL value.

System Action The parameter is ignored. The system continues.

Operator Action For a runtime initialization, correct the device
initialization parameters, otherwise notify the programmer.

Programmer Action For an engine initialization, correct the device
configuration parameters in the configuration file.

Note For DIAL=IN , RPORT and RHOST are ignored For DIAL=OUT , LPORT,
LHOST, RPORT and RHOST are ignored For DIAL=INOUT, RPORT and RHOST are
ignored

HHCCA017I
---------

HHCCA017I CCUU:LPORT|RPORT|LHOST|RHOST parameter ignored

Explanation The system indicates that the parameter specified is
ignored. This message is preceeded by message HHCCA016W.

System Action The system continues.

Operator Action None. This is an informational message.

Programmer Action None. This is an informational message.

HHCCA018E
---------

HHCCA018E CCUU:Bind failed : System Cause Text

Explanation While attempting to bind a socket to a specific host/port,
the host system returned an uncorrectable error.

System Action BSC Thread terminates.

Operator Action None.

Programmer Action Check that the LHOST parameter for this device is
indeed a local IP address, otherwise notify support.

HHCCA019E
---------

HHCCA019E CCUU:BSC comm thread did not initialise

Explanation The BSC communication thread reported that it terminated
while the device was initialising.

System Action The device is not initialised.

Operator Action Check for any previously issued error message.

Programmer Action Check for any previously issued error message.

HHCCA020E
---------

HHCCA020E CCUU:Memory allocation failure for main control block

Explanation A memory allocation failure occurred, while attempting to
reserve memory for the Communication Adapter control block.

System Action The device is not initialised.

Operator Action None.

Programmer Action Contact support.

HHCCA021I
---------

HHCCA021I CCUU:Initialization failed due to previous errors

Explanation The initialization process for device CCUU did not complete
successfully.

System Action The device is not initialised.

Operator Action None.

Programmer Action Refer to any previous error message.

HHCCA300D
---------

HHCCA300D Debug Message

Explanation This is a debug message. CCW Tracing has been turned on for
this device and the Line Handler issues debug messages to help diagnose
interface, conformance and protocol issues.

System Action The system continues.

Operator Action If the debug messages are no longer necessary, turn off
CCW tracing (panel command : ‘t-CCUU’).

Programmer Action None.

45. HHCCFnnns - Configuration File Processing
------------------------------------------------------

HHCCF001S
---------

HHCCF001S Error reading file filename line lineno: error

Explanation An error was encountered reading the configuration file
named filename at line number lineno. The error is described by error.

Action Correct the error and restart Hercules.

HHCCF002S
---------

HHCCF002S File filename line lineno is too long

Explanation The line at line number lineno in the configuration file
filename is too long and cannot be processed.

Action Correct the line and restart Hercules.

HHCCF003S
---------

HHCCF003S Cannot open file filename: error

Explanation The configuration file named filename could not be opened.
The error is described by error.

Action Correct the error and restart Hercules.

HHCCF004S
---------

HHCCF004S No device records in file filename

Explanation The configuration file named filename does not contain any
device definition records. Without these, Hercules cannot do any
meaningful work.

Action Specify one or more device definitions in the configuration file
and restart Hercules.

HHCCF005S
---------

HHCCF005S Unrecognized argument argument

Explanation An invalid argument, argument, was specified on the HTTPPORT
configuration statement in the file named filename at line number
lineno. Only the arguments auth and noauth are valid.

Action Correct the invalid argument and restart Hercules.

HHCCF006S
---------

HHCCF006S Error in filename line lineno: Userid, but no password given
userid

Explanation A userid, userid, was specified on the HTTPPORT
configuration statement in the file named filename at line number
lineno, but no password was provided. A password is required if a userid
is present.

Action Either remove the userid, or specify a password, and restart
Hercules.

HHCCF007S
---------

HHCCF007S Error in filename line lineno: Missing argument

Explanation The HTTPROOT configuration statement was specified in the
file named filename at line number lineno, but no directory was
specified. A directory is required.

Action Specify the directory where the Hercules web server will find its
HTML files and restart Hercules.

HHCCF008E
---------

HHCCF008E Error in filename line lineno: Unrecognized keyword keyword

Explanation An invalid configuration statement was specified in the file
named filename at line number lineno. The invalid keyword was keyword.

Action Correct the invalid statement and restart Hercules.

HHCCF009S
---------

HHCCF009S Error in filename line lineno: Incorrect number of operands

Explanation The configuration statement at line lineno of the file named
filename had an invalid number of operands. For all but the HTTPPORT
statement exactly one operand is required.

Action Correct the invalid statement and restart Hercules.

HHCCF010S
---------

HHCCF010S Error in filename line lineno: Unknown or unsupported ARCHMODE
specification mode

Explanation The ARCHMODE configuration statement at line lineno of the
file named filename specified an invalid architecture. Only S/370,
ESA/390, or ESAME are valid. If one of these was specified, then support
for that architecture was excluded when the copy of Hercules in use was
compiled.

Action Correct the specified value and restart Hercules. If the message
was issued because support for the desired architecture was excluded,
then recompile Hercules.

HHCCF011S
---------

HHCCF011S Error in filename line lineno: serialno is not a valid serial
number

Explanation The serial number serialno specified on the CPUSERIAL
configuration statement at line number lineno of the file named filename
must be exactly six digits long and must be a valid hexadecimal number.

Action Correct the serial number and restart Hercules.

HHCCF012S
---------

HHCCF012S Error in filename line lineno: modelno is not a valid CPU
model

Explanation The model number modelno specified on the CPUMODEL
configuration statement at line number lineno of the file named filename
must be exactly four digits long, and must be a valid hexadecimal
number.

Action Correct the model number and restart Hercules.

HHCCF013S
---------

HHCCF013S Error in filename line lineno: Invalid main storage size size

Explanation The main storage size size specified on the MAINSIZE
configuration statement at line number lineno of the file named filename
must be a valid decimal number whose value is at least 2. For 32-bit
platforms the value must not exceed 4095.

Action Correct the main storage size and restart Hercules.

HHCCF014S
---------

HHCCF014S Error in filename line lineno: Invalid expanded storage size
size

Explanation The expanded storage size size specified on the XPNDSIZE
configuration statement at line number lineno of the file named filename
must be a valid decimal number between 0 and 16777215.

Action Correct the expanded storage size and restart Hercules.

HHCCF015S
---------

HHCCF015S Error in filename line lineno: Invalid console port number
port

Explanation The console port number port specified on the CNSLPORT
configuration statement at line number lineno of the file named filename
must be a valid nonzero decimal number.

Action Correct the console port number and restart Hercules.

HHCCF016S
---------

HHCCF016S Error in filename line lineno: Invalid threadname thread
priority priority

Explanation The thread priority priority specified on the xxxPRIO
configuration statement at line number lineno of the file named filename
must be a valid decimal number.

Action Correct the priority on the statement and restart Hercules.

HHCCF017W
---------

HHCCF017W Hercules is not running as setuid root, cannot raise
threadname priority

Explanation A negative value for the threadname thread priority
parameter xxxPRIO was specified but Hercules is not running as the root
user (either directly or via the setuid mechanism). This parameter value
would cause the priority of the CPU execution thread to be raised above
the normal level if Hercules were running as root. Since it is not,
however, the parameter will have no effect.

Action Either specify a positive value to lower the CPU thread priority,
zero to not alter the priority, or omit the statement entirely to use
the Hercules default CPU thread priority of 15.

HHCCF018S
---------

HHCCF018S Error in filename line lineno: Invalid number of CPUs number

Explanation The number of emulated CPUs number specified on the NUMCPU
configuration statement at line number lineno of the file named filename
must be a valid decimal number between 1 and the maximum number defined
when Hercules was built (usually 2; this number is never more than 2 for
S/370 mode, or 16 for ESA/390 or ESAME mode).

Action Correct the number of emulated CPUs and restart Hercules.

HHCCF019S
---------

HHCCF019S Error in filename line lineno: Invalid number of VFs number

Explanation The number of emulated Vector Facility engines number
specified on the NUMVEC configuration statement at line number lineno of
the file named filename must be a valid decimal number between 1 and the
maximum number defined when Hercules was built (usually 2).

Action Correct the number of emulated Vector Facility engines and
restart Hercules.

HHCCF020W
---------

HHCCF020W Vector Facility support not configured

Explanation A request for Vector Facility support was made by the NUMVEC
configuration statement, but Hercules was built without the Vector
Facility code. The request has been ignored.

Action If Vector Facility support is desired, recompile Hercules. If
not, remove the NUMVEC configuration statement.

HHCCF021S
---------

HHCCF021S Error in filename line lineno: Invalid maximum number of CPUs
number

Explanation The maximum number of emulated CPUs number specified on the
MAXCPU configuration statement at line number lineno of the file named
filename must be a valid decimal number. It must not exceed the maximum
number (MAX_CPU_ENGINES) defined when Hercules was built.

Action Correct the MAXCPU parameter and restart Hercules.

HHCCF022S
---------

HHCCF022S Error in filename line lineno: epoch is not a valid system
epoch

Explanation The system epoch epoch specified on the SYSEPOCH
configuration statement at line number lineno of the file named filename
must be one of the following: 1900, 1928, 1960, 1988, or 1970.

Action Correct the system epoch and restart Hercules. If a different
epoch is desired, a change must be made to the Hercules source file
config.c and Hercules rebuilt.

HHCCF023S
---------

HHCCF023S Error in filename line lineno: offset is not a valid timezone
offset

Explanation The system timezone offset offset specified on the TZOFFSET
configuration statement at line number lineno of the file named filename
must be five characters long and a valid decimal number of the form
(+\|- )number, where number must be between zero and 2359 (representing
23 hours, 59 minutes).

Action Correct the time zone offset and restart Hercules.

HHCCF024S
---------

HHCCF024S Error in filename line lineno: Invalid TOD clock drag factor
drag

Explanation The TOD clock drag factor drag specified on the TODDRAG
configuration statement at line number lineno of the file named filename
must be a valid decimal number between 1 and 10000.

Action Correct the TOD clock drag factor and restart Hercules.

HHCCF025S
---------

HHCCF025S Error in filename line lineno: Invalid panel refresh rate rate

Explanation The control panel refresh rate rate specified on the PANRATE
configuration statement at line number lineno of the file named filename
must be either F, S, or a valid decimal number between 1 and 5000.

Action Correct the control panel refresh rate and restart Hercules.

HHCCF026S
---------

HHCCF026S Error in filename line lineno: Unknown OS tailor specification
tailor

Explanation The OS tailoring value tailor specified on the OSTAILOR
configuration statement at line number lineno of the file named filename
must be either OS/390, VSE, VM, LINUX, NULL, or QUIET.

Action Correct the OS tailoring value and restart Hercules.

HHCCF027S
---------

HHCCF027S Error in filename line lineno: Invalid maximum device threads
threads

Explanation The maximum device threads threads specified on the DEVTMAX
configuration statement at line number lineno of the file named filename
must be a valid decimal number greater than -1.

Action Correct the maximum device threads and restart Hercules.

HHCCF028S
---------

HHCCF028S Invalid program product OS permission permission

Explanation The program product OS permission permission specified on
the PGMPRDOS configuration statement must be either LICENSED or
RESTRICTED. The alternative spelling LICENCED is also accepted.

Action Correct the program product OS permission and restart Hercules.

HHCCF029S
---------

HHCCF029S Invalid HTTP port number port

Explanation The HTTP server port number port specified on the HTTPPORT
configuration statement must be either 80, or a valid decimal number
greater than 1024.

Action Correct the HTTP server port number and restart Hercules.

HHCCF030S
---------

HHCCF030S Error in filename line lineno: Invalid I/O delay value delay

Explanation The I/O delay value delay specified on the IODELAY
configuration statement at line number lineno of the file named filename
must be a valid decimal number.

Action Correct the I/O delay value and restart Hercules.

HHCCF031S
---------

HHCCF031S Cannot obtain sizeMB main storage: error

Explanation An attempt to obtain the amount of main storage specified by
MAINSTOR failed for the reason described by error.

Action Correct the error and restart Hercules.

HHCCF032S
---------

HHCCF032S Cannot obtain storage key array: error

Explanation An attempt to obtain storage for the array of storage keys
failed for the reason described by error.

Action Correct the error and restart Hercules.

HHCCF033S
---------

HHCCF033S Cannot obtain sizeMB expanded storage: error

Explanation An attempt to obtain the amount of expanded storage
specified by XPNDSTOR failed for the reason described by error.

Action Correct the error and restart Hercules.

HHCCF034W
---------

HHCCF034W Expanded storage support not installed

Explanation A request was made for expanded storage by the XPNDSTOR
configuration parameter, but Hercules was built without expanded storage
support. The request was ignored.

Action Either remove the XPNDSTOR configuration parameter or recompile
Hercules with expanded storage support included.

HHCCF035S
---------

HHCCF035S Error in filename line lineno: Missing device number or device
type

Explanation The I/O device definition statement at line number lineno of
the file named filename did not contain a device number or a device
type.

Action Supply the missing value and restart Hercules.

HHCCF036S
---------

HHCCF036S Error in filename line lineno: number is not a valid device
number(s) specification

Explanation The I/O device definition statement at line number lineno of
the file named filename specified an invalid device number number. The
device number must be one to four hexadecimal digits.

Action Correct the device number and restart Hercules.

HHCCF037S
---------

HHCCF037S Message pipe creation failed: error

Explanation An attempt to create a pipe for communication with the
control panel failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCCF038S
---------

HHCCF038S Message pipe open failed: error

Explanation An attempt to open the pipe for communication with the
control panel failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCCF039W
---------

HHCCF039W PGMPRDOS LICENSED specified. A licensed program product
operating systems is running. You are responsible for meeting all
conditions of your software license.

Explanation The configuration parameter PGMPRDOS LICENSED was specified
and Hercules has detected that the operating system is a licensed
program product. This message is issued to remind you that compliance
with the terms of the license for your system’s software is your
responsibility.

Action Be sure you know what you are doing.

HHCCF040E
---------

HHCCF040E Cannot create CPU number thread: error

Explanation An attempt to create a new thread for execution of CPU
number failed. The error is described by error. The CPU has not been
added to the configuration.

Action Correct the error and retry the operation.

HHCCF041E
---------

HHCCF041E Device address already exists

Explanation An attempt was made to define a device at address address.
There is already a device at that address.

Action Either choose another device address or use the detach command to
remove the existing device.

HHCCF042E
---------

HHCCF042E Device type type not recognized

Explanation An attempt was made to define a device of type type. This
device type is not supported by Hercules. It may also indicate that the
system was unable to load the device handler for the specified device
type.

Action Specify a supported device type. If the device type is supported,
make sure the the system can load the load modules necessary for device
operations. Either use the LD_LIBRARY_PATH environment variable or use
ldconfig(8) to customize the library search path.

HHCCF043E
---------

HHCCF043E Cannot obtain device block for device address: error

Explanation An attempt to allocate memory for the control block
describing the device with address address failed. The error is
described by error. The device has not been defined.

Action Correct the error and retry the operation.

HHCCF044E
---------

HHCCF044E Initialization failed for device address

Explanation The device at address address could not be initialized. The
device initialization routine has issued a message describing the
problem in further detail; refer to that message for more information.

Action Correct the error and retry the operation.

HHCCF045E
---------

HHCCF045E Cannot obtain buffer for device address: error

Explanation An attempt to allocate memory for the data buffer for the
device with address address failed. The error is described by error. The
device has not been defined.

Action Correct the error and retry the operation.

HHCCF046E
---------

HHCCF046E Device address does not exist

Explanation An attempt was made to remove a device at address address.
There is no device at that address.

Action Choose another device address to remove, if desired.

HHCCF047I
---------

HHCCF047I Device address detached

Explanation The device at address address has been successfully removed
from the system.

Action None. This is an informational message.

HHCCF048E
---------

HHCCF048E Device address does not exist

Explanation An attempt was made to rename a device at address address.
There is no device at that address.

Action Choose another device address to rename, if desired.

HHCCF049E
---------

HHCCF049E Device address already exists

Explanation An attempt was made to rename a device to address address.
There is already a device at that address.

Action Either choose another device address or use the detach command to
remove the existing device.

HHCCF050I
---------

HHCCF050I Device oldaddr defined as newaddr

Explanation The device which was previously defined with the address
oldaddr has been changed to the address newaddr.

Action None. This is an informational message.

HHCCF051S
---------

HHCCF051S Error in filename line lineno: verid is not a valid CPU
version code

Explanation The version code verid specified on the CPUVERID
configuration statement at line number lineno of the file named filename
must be exactly two digits long and must be a valid hexadecimal number.

Action Correct the model number and restart Hercules.

HHCCF052S
---------

HHCCF052S DIAG8CMD invalid option: option

Explanation The argument option on the DIAG8CMD is invalid. Valid
options are enable, disable, echo, and noecho.

Action Correct the statement and restart Hercules.

HHCCF053E
---------

HHCCF053E Incorrect second device number in device range near character
c

Explanation The second argument of a device range contains an incorrect
device number

Action Correct the statement and restart Hercules.

HHCCF054E
---------

HHCCF054E Incorrect Device count near character c

Explanation The count field in a device count specification is invalid

Action Correct the statement and restart Hercules.

HHCCF055E
---------

HHCCF055E Incorrect device address specification near character c

Explanation The first or only CUU in a device specification statement is
invalid

Action Correct the statement and restart Hercules.

HHCCF056E
---------

HHCCF056E Incorrect device address range. CUU1>CUU2

Explanation The first device number of a range is greater than the last
device number

Action Correct the statement and restart Hercules.

HHCCF057E
---------

HHCCF057E CUU is on wrong channel (1st device defined on channel CC)

Explanation At least one of the devices in a device number specification
is on a different channel than a previously defined device number within
the same specification. All device numbers on a single configuration
line must be on a single channel (Group of 256 devices)

Action Correct the statement and restart Hercules.

HHCCF058E
---------

HHCCF058E Some or all devices in CUU-CUU duplicate devices already
defined

Explanation At least one of the device numbers on a device specification
statement defines a device number that is already specified on that same
statement.

Action Correct the statement and restart Hercules.

HHCCF061W
---------

HHCCF061W ECPS:VM Statement deprecated. Use ECPSVM instead

Explanation The “ECPS:VM” statement was encountered. This statement is
deprecated in favor of the “ECPSVM” statement.

Action The configuration statement is still carried out but the
statement syntax should be changed as soon as possible.

HHCCF062W
---------

HHCCF062W Missing ECPSVM level value. 20 Assumed

Explanation The “ECPSVM” statement keyword “LEVEL” was encountered but
no numeric level followed it.

Action The default level of 20 is used and the ECPS:VM feature is made
available. The statement should be corrected as soon as possible.

HHCCF063W
---------

HHCCF063W Specifying ECPSVM level directly is deprecated. Use the
‘LEVEL’ keyword instead

Explanation The deprecated “ECPSVM” level syntax form (without the LEVEL
keyword) was found.

Action The ECPS:VM Level is set to the specified value. The
configuration statement should be updated to include the “LEVEL”
keyword.

HHCCF064W
---------

HHCCF064W Hercules set priority priority failed: error

Explanation An attempt to change the priority of the Hercules process to
priority failed. The error is described by error. The process priority
has not been changed. Hercules overall performance may be impaired as a
result.

Action If performance problems are noted, correct the error and restart
Hercules.

HHCCF065I
---------

HHCCF065I Hercules: tid=threadid, pid=processid, pgid=processgroupid,
priority=priority

Explanation Hercules thread id is threadid, its process id is processid,
its process group id is processgroupid and its execution priority is
priority.

Action None. This is an informational message.

HHCCF066E
---------

HHCCF066E Invalid HTTPROOT: error

Explanation The pathname specified on your HTTPROOT statement is
invalid. The error is described by error.

Action Correct the error and restart Hercules.

HHCCF067S
---------

HHCCF067S Incorrect keyword keyword for the ASN_AND_LX_REUSE statement

Explanation The keyword specified for the ASN_AND_LX_REUSE statement is
not ENABLE or DISABLE.

Action Correct the error and restart Hercules.

HHCCF068E
---------

HHCCF068E Invalid value: value; Enter “help scsimount” for help.

Explanation The automatic SCSI tape mount value is not “NO” nor a value
between 1 and 99 seconds inclusive.

Action Reissue the SCSIMOUNT command.

HHCCF069I
---------

HHCCF069I Run-options enabled for this run: NUMCPU: n ASN-and-LX-reuse:
Enabled/Disabled DIAG8CMD: Enabled/Disabled

Explanation This message confirms the setting of various run-time
options specified in the configuration file at startup time.

Action None. This is an informational message.

HHCCF074E
---------

HHCCF074E Unspecified error occured while parsing Logical Channel
Subsystem Identification

Explanation A logic error occured while parsing the Logical Channel
Subsystem Identification component of a device number or device number
group.

Action Notify Hercules support. This is an error in the Hercules parsing
routines.

HHCCF075E
---------

HHCCF075E No more than 1 Logical Channel Subsystem Identification may be
specified

Explanation While specifying a device number or device number group,
more than one ‘:’ character was encountered while parsing the Logical
Channel Subsystem Identification component. There can be only one
Logical Channel Subsystem Identification for a device or group of
devices.

Action Correct the device number or device number group specification
and either reissue the command or restart the Hercules engine, depending
on whether the error occured while issuing a command or while starting
the engine.

HHCCF076E
---------

HHCCF076E Non numeric Logical Channel Subsystem Identification XX

Explanation While specifying a device number or device number group, a
non-decimal value was encountered while parsing the Logical Channel
Subsystem Identification component. The Logical Channel Subsystem
Identification for a device or group of devices must be specified as a
numeric value.

Action Correct the device number or device number group specification
and either reissue the command or restart the Hercules engine, depending
on whether the error occured while issuing a command or while starting
the engine.

HHCCF077E
---------

HHCCF077E Logical Channel Subsystem Identification NN exceeds maximum of
3

Explanation While specifying a device number or device number group, a
Logical Channel Identification was encoun- tered that exceeded the
architecture maximum value of NN. The Logical Channel Subsystem
Identifica- tion for a device or group of devices must be within 0 and 3
(inclusive).

Action Correct the device number or device number group specification
and either reissue the command or restart the Hercules engine, depending
on whether the error occured while issuing a command or while starting
the engine.

HHCCF079A
---------

HHCCF079A A licensed program product operating system has been detected.
All processors have been stopped.

Explanation Hercules has detected that the operating system is a
licensed program product, but the PGMPRDOS LICENSED parameter was not
specified in the Hercules configuration file.

Action Hercules enters the stopped state. To run this operating system
you must obtain a license from the operating system supplier and specify
the PGMPRDOS LICENSED parameter in the configuration file. If you are
unable to obtain a valid license allowing you to run this operating
system on your machine, you must use another operating system (such as
MVS 3.8J or Linux for System z) which does not require a license.

HHCCF081I
---------

HHCCF081I fname will ignore include errors.

Explanation An ignore include_errors statement was encountered in file
fname requesting that any include statements subsequently found within
file fname which happen to reference include files which do not exist
should simply cause a HHCCF084W warning instead of a HHCCF085S fatal
error.

Action Processing continues. This is an informational-only message.

HHCCF082S
---------

HHCCF082S Error in fname line nnn: Maximum nesting level (nn) reached

Explanation The maximum number of nested include statements has been
exceeded. The include statement which caused the maximum nesting level
of nn to be exceeded is identified as statement number nnn of file
fname. Action This is a fatal error. Configuration file processing is
immediately terminated and Hercules startup is abor- ted. Correct the
error and restart Hercules.

HHCCF083I
---------

HHCCF083I fname1 Including fname2 at nnn.

Explanation An include statement for file fname2 was encountered on line
nnn of file fname1.

Action Configuration file processing switches immediately to processing
the statements contained in file fname2. Once all of the ststements in
file fname2 have been completely processed, configuration file
processing will then return to statement nnn+1 of file fname1. This is
an informational-only message.

HHCCF084W
---------

HHCCF084W fname1 Open error ignored file fname2: error

Explanation File fname1 contained an include statement for file fname2
which could not be opened because of error.

Action Processing continues. This is a informational warning only. Check
to make sure the filename specified by fname2 was spelled correctly and
restart Hercules if desired.

HHCCF085S
---------

HHCCF085S fname1 Open error file fname2: error

Explanation File fname1 contained an include statement for file fname2
which could not be opened because of error.

Action This is a fatal error. Configuration file processing is
immediately terminated and Hercules startup is abor- ted. Correct any
misspelling of filename fname2 and restart Hercules.

HHCCF086S
---------

HHCCF086S Error in filename: NUMCPU nn must not exceed MAXCPU mm

Explanation The number of online CPUs nn specified in the NUMCPU
configuration statement in the file named filename cannot exceed the
maximum number of CPUs mm specified in the MAXCPU configuration
statement.

Action Either decrease the NUMCPU parameter, or increase the MAXCPU
parameter, and restart Hercules.

HHCCF089S
---------

HHCCF089S Error in fname line linenum: Invalid log option keyword val

Explanation File fname containes an invalid log option keyword val on
line num.

Action Correct the log option keyword in file fname and restart
Hercules.

46. HHCCPnnns - CPU Emulation
--------------------------------------

HHCCP001W
---------

HHCCP001W CPU thread set priority priority failed: error

Explanation An attempt to change the priority of the CPU thread to
priority failed. The error is described by error. The thread priority
has not been changed. Hercules overall performance may be impaired as a
result.

Action If performance problems are noted, correct the error and restart
Hercules.

HHCCP002I
---------

HHCCP002I CPU number thread started: tid=threadid, pid=processid,
priority=priority

Explanation The execution thread for CPU number number has been started.
Its thread id is threadid, its process id is processid and its execution
priority is priority.

Action None. This is an informational message.

HHCCP003I
---------

HHCCP003I CPU number architecture mode mode

Explanation CPU number has been set to the mode architecture mode.

Action None. This is an informational message.

If a different architecture mode is desired, it may be changed with the
ARCHMODE configuration statement or the archmode control panel command.

HHCCP004I
---------

HHCCP004I CPU number Vector Facility online

Explanation The Vector Facility for CPU number is online and available
for use.

Action None. This is an informational message.

HHCCP005E
---------

HHCCP005E CPU number thread already started

Explanation An attempt was made to add CPU number number to the
configuration. This CPU already exists.

Action If another CPU is desired in the configuration, select a
different number.

HHCCP006S
---------

HHCCP006S Cannot create timer thread: error

Explanation An attempt to create the thread used for timing functions
has failed. The error is described by error. The CPU thread terminates
and successful continuation of Hercules is not possible.

Action Correct the error and restart Hercules.

HHCCP007I
---------

HHCCP007I CPU number architecture mode set to mode

Explanation CPU number number has been changed to the architecture mode
mode.

Action None. This is an informational message.

HHCCP008I
---------

HHCCP008I CPU number thread ended: tid=threadid, pid=processid

Explanation The execution thread for CPU number number has ended. Its
thread id was threadid, and its process id was processid.

Action None. This is an informational message.

HHCCP009E
---------

HHCCP009E CPU MASK MISMATCH: prevmask - currmask. Last instruction:
instruction.

Explanation The CPU interrupt mask has changed unexpectedly. The
previous mask was prevmask and the current mask is currmask. The last
instruction executed was instruction. This is an internal error.

Action Report this message and the circumstances to the Hercules
developers.

HHCCP010I
---------

HHCCP010I CPU number store status completed.

Explanation CPU number number has completed a store status operation.

Action None. This is an informational message.

HHCCP011I
---------

HHCCP011I CPU number: Disabled wait state

Explanation CPU number number has entered a disabled wait state. It will
not execute any further instructions unless it is reset or restarted.
This is usually done to report a severe error in execution of an
operating system.

Action Correct the error denoted by the wait state code if applicable.

HHCCP023I
---------

HHCCP0 23 I External interrupt: Interrupt key

Explanation The CPU has taken an external interrupt because the operator
pressed the interrupt key or issued the panel command ext.

Action None. This is an informational message.

HHCCP024I
---------

HHCCP024I External interrupt: Clock comparator

Explanation The CPU has taken a clock comparator interrupt. This message
is issued only when the CPU is in single- stepping or
instruction-tracing mode.

Action None. This is an informational message. External interrupts are
part of normal system operation.

HHCCP025I
---------

HHCCP025I External interrupt: CPU timer=xx…xx

Explanation The CPU has taken a CPU timer interrupt. xx…xx is the
hexadecimal value of the CPU timer. This message is issued only when the
CPU is in single-stepping or instruction-tracing mode.

Action None. This is an informational message. External interrupts are
part of normal system operation.

HHCCP026I
---------

HHCCP0 26 I External interrupt: Interval timer

Explanation The CPU has taken an external interrupt caused by the
interval timer. This message is issued only when the CPU is in
single-stepping or instruction-tracing mode.

Action None. This is an informational message. External interrupts are
part of normal system operation.

HHCCP027I
---------

HHCCP0 27 I External interrupt: Service signal intparm

Explanation The CPU has taken a service signal external interrupt.
intparm is the interrupt parameter. This message is issued only when the
CPU is in single-stepping or instruction-tracing mode.

Action None. This is an informational message. External interrupts are
part of normal system operation.

HHCCP090W
---------

HHCCP090W The configuration has been placed into a system check-stop
state because of an incompatible service call

Explanation A READ SCP INFO (code X’00020001’) Service call has been
issued from a CPU which is not a CP engine. All the CPUs in the
configuration are put into a Check-Stop state.

Action Ensure the CPU that issues the service call is a CP engine and
restart the program.

47. HHCCTnnns - Channel-to-Channel Adapter Emulation
-------------------------------------------------------------

HHCCTnnns
---------

Messages HHCCTnnns are not yet documented.

48. HHCCUnnns - CCKD Utilities
---------------------------------------

48.1 Format of the CCKD utilities messages
------------------------------------~~~~~~

Messages generated by the CCKD utilities are in the format message_id
file message_text. The format of the message ID is the same as with all
other Hercules messages. file will either be the part of the file name
following the last slash (“/” or “") when called by a utility command,
or will be xxxx: file[n] where xxxx is the device number and n is the
shadow file number when called by Hercules. The file portion of the
message is omitted in the sections below for brevity.

HHCCU101I
---------

HHCCU101I converting to endian-format

Explanation The file is in the wrong endian (byte order) format for the
host architecture. The file is being converted to the host endian format
endian-format.

Action None. This is an informational message.

HHCCU102I
---------

HHCCU102I compress successful, n bytes released

Explanation The compress function successfully completed and free n
bytes from the file. If n is 0, then the level 2 tables were
repositioned to the beginning of the file in order.

Action None. This is an informational message.

HHCCU103I
---------

HHCCU103I file already compressed

Explanation The compress function determined that the file is already
compressed. The file is not updated.

Action None. This is an informational message.

HHCCU104I
---------

HHCCU104I free space rebuilt

Explanation Free space errors were detected and free space has been
successfully rebuilt.

Action None. This is an informational message.

HHCCU300I
---------

HHCCU300I number space images recovered

Explanation Recovery phase 1 completed, recovering number spaces (trks
or blkgrps).

Action None. This is an informational message.

HHCCU301I
---------

HHCCU301I space[id] recovered offset offset len length

Explanation The space space (trk or blkgrp) was recovered at offset
offset and length length. id is the trk or blkgrp number.

Action None. This is an informational message.

HHCCU500W
---------

HHCCU500W recovery not completed, file opened read-only

Explanation Phase 3 recovery did not complete because the file is not
opened for write.

Action Omit the -ro option for cckdcdsk or change the file permissions
to enable the file to be opened for read- write for Hercules.

HHCCU501W
---------

HHCCU501W recovery not completed, missing compression

Explanation Phase 3 recovery did not complete because one or more trk or
blkgrp images were compressed using a compression (zlib or bzip2) that
was not built into Hercules.

Action Processing terminates. The file has not been updated. Build
Hercules with the missing compression libraries.

HHCCU502W
---------

HHCCU502W free space not rebuilt, file opened read-only

Explanation Free space errors were detected but the free space was not
rebuilt because the file is not opened for write.

Action Omit the -ro option for cckdcdsk or change the file permissions
to enable the file to be opened for read- write by Hercules.

HHCCU600W
---------

HHCCU600W forcing check level level[; reason]

Explanation Errors have been detected in the compressed file that
warrant the escalation of the check level to level. An additional
explanation reason may be supplied.

Action At a minimum, free space will be rebuilt.

HHCCU601W
---------

HHCCU601W cdevhdr inconsistencies found code=code

Explanation The space statistics in the cckddasd device header (cdevhdr)
contain inconsistencies described by code. code is a 16-bit bit field
and more than one bit may be on. See cckdutil.c for the different bit
settings.

Action At a minimum, free space will be rebuilt.

HHCCU602W
---------

HHCCU602W space offset offset len length is out of bounds

Explanation The space space (trk, blkgrp or l2) either precedes the end
of the L1 table (at the beginning of the file) or exceeds the end of the
file.

Action The space will be recovered. If the space is an L2 table, then
all tracks or block groups associated with the table will also be
recovered.

HHCCU603W
---------

HHCCU603W space1 offset offset1 len length overlaps space2 offset
offset2

Explanation The space space1 overlaps space space2.

Action The spaces will be recovered. If either space is an L2 table,
then all tracks or block groups associated with that table will also be
recovered.

HHCCU604W
---------

HHCCU604W space l2 inconsistency: len length, size size

Explanation The space space (trk or blkgrp) has an inconsistent l2
entry. Either the length length is too small or is too large or exceeds
the size size.

Action The space will be recovered.

HHCCU610W
---------

HHCCU610W free space errors detected

Explanation Free space is not consistent.

Action Free space will be rebuilt.

HHCCU620W
---------

HHCCU620W space[id] hdr error offset offset: xxxxxxxxxx

Explanation A header error was found for space (trk or blkgrp) during
validation. id is the trk or blkgrp number. The header is located at
file offset offset. The contents of the 5 byte header is xxxxxxxxxx in
hex.

The first byte of the header should be either 00 (compress none), 01
(compress zlib) or 02 (compress bzip2).

For ckd, the next two bytes is the cylinder (in big-endian byte order)
and the two bytes after that is the head (also in big-endian byte
order).

For fba, the next four bytes is the block group number (in big-endian
byte order).

The header contains an invalid value. Either the offset is incorrect or
the header has been overlaid.

Action The space will be recovered.

HHCCU621W
---------

HHCCU621W space[id] compressed using compression, not supported

Explanation During validation, the header for space (trk or blkgrp)
indicates that the space was compressed using compression (zlib or
bzip2) but support for that compression method was not built into
Hercules. id is the trk or blkgrp number.

Action Processing continues. However no recovery will take place. Build
Hercules with the specified compres- sion library.

HHCCU622W
---------

HHCCU622W space[id] offset offset len length validation error

Explanation The space (trk or blkgrp) at offset offset and length length
failed validation. id is the trk or blkgrp number. Either the space did
not uncompress successfully or the uncompressed space contains some kind
of error. This error is detected during check level 3 validation.

Action The space will be recovered.

HHCCU700E
---------

HHCCU700E open error: error text

Explanation Open failed for the file. The text associated with the error
number is displayed.

Action Processing for the file terminates.

HHCCU701E
---------

HHCCU701E fstat error: error text

Explanation The file status system call failed. The text associated with
the error number is displayed.

Action Function processing terminates. Probable Hercules logic error.
Contact the Hercules mailing list for assistance.

HHCCU702E
---------

HHCCU702E lseek error offset offset: error text

Explanation File reposition to offset offset failed. The text associated
with the error number is displayed.

Action Function processing terminates. Probable Hercules logic error.
Contact the Hercules mailing list for assistance.

HHCCU703E
---------

HHCCU703E read error rc=retcode offset offset len length: error text

Explanation A read failed at offset offset for length length. If retcode
is not negative then the read was incomplete and the value indicates how
many bytes were read. Otherwise the text associated with the error
number is displayed.

Action Function processing terminates. Possible Hercules logic error.
Possible hardware error. Contact the hercules mailing list for
assistance.

HHCCU704E
---------

HHCCU704E write error rc=retcode offset offset len length: error text

Explanation A write failed at offset offset for length length. If
retcode is not negative then the write was incomplete and the value
indicates how many bytes were written. Otherwise the text associated
with the error number is displayed.

Action Function processing terminates. Possible Hercules logic error.
Possible hardware error. Contact the hercules mailing list for
assistance.

HHCCU705E
---------

HHCCU705E malloc error, size size: error text

Explanation Malloc (allocate memory) failed for size size.

Action Function processing terminates. Try reducing Hercules storage
requirements (e.g. mainsize).

HHCCU706E
---------

HHCCU706E calloc error, size size: error text

Explanation Calloc (allocate cleared memory) failed for size size.

Action Function processing terminates. Try reducing Hercules storage
requirements (eg mainsize).

HHCCU707E
---------

HHCCU707E OPENED bit is on, use -f

Explanation The file OPENED bit is on in the cckd header but -f was not
specified.

Action File processing terminates. Make sure the file is not in use. If
it is not, try the command again specifying the -f option.

HHCCU708E
---------

HHCCU708E chkdsk errors

Explanation The utility called cckd_chkdsk for the file and it returned
in error.

Action File processing terminates. Perform the actions suggested by the
preceding cckd_chkdsk errors.

HHCCU900E
---------

HHCCU900E dasd lookup error type=type cyls=cyls

Explanation The device type type from the device header along with the
number of cylinders cyls did not match a table entry in dasdtab.c. Note
that type is the last two bytes of the device type (eg 90 for a 3390
device type).

Action Function processing terminates. Specify the correct file name or
manually correct the device header.

HHCCU901E
---------

HHCCU901E bad trksize: size1, expecting size2

Explanation The track size size1 from the device header does match the
track size size2 from the table entry in dasdtab.c.

Action Function processing terminates. Specify the correct file name or
manually correct the device header.

HHCCU902E
---------

HHCCU902E bad number of heads: heads1, expecting heads2

Explanation The number of heads heads1 from the device header does match
the number of heads heads2 from the table entry in dasdtab.c.

Action Function processing terminates. Specify the correct file name or
manually correct the device header.

HHCCU903E
---------

HHCCU903E bad \`numl1tab’: nbr1, expecting nbr2

Explanation The number of L1 table entries nbr1 in the cckd device
header does not match the number calculated nbr2. The number calculated
is the number of cylinders times the number of heads (i.e. the number of
tracks) divided by 256, rounded up by 1 if there is a remainder.

Action Function processing terminates. Specify the correct file name or
manually correct the device headers.

HHCCU904E
---------

HHCCU904E file too small to contain L1 table: %size1, need size2

Explanation The size of the file size1 is not large enough to contain
all L1 table entries; the size required is size2. The minimum size of a
cckd file is 512 + 512 + ( 4 \* number of L1 entries).

Action Function processing terminates. Specify the correct file name.

HHCCU905E
---------

HHCCU905E not enough file space for recovery

Explanation During phase 2 recovery there was not enough space in the
maximum file size to contain the rebuilt L2 tables. This is an unusual
situation and probably indicates some kind of programming error.

Action Function processing terminates. The file has not been updated.
Contact the hercules mailing list for assistance.

HHCCU910E
---------

HHCCU910E error during swap

Explanation Error occurred during cckd_swap().

Action See the preceding error messages.

HHCCU999E
---------

HHCCU999E not a compressed file

Explanation The first 8 bytes of the file did not match an expected
identifier. For a cckd file, the identifier must be either CKD_C370 or
CKD_S370. For a cfba file, the identifier must be either FBA_C370 or
FBA_S370.

Action Function processing terminates. Specify the correct file name.

49. HHCDAnnns - DASD Emulation (CKD, CCKD and FBA)
-----------------------------------------------------------

HHCDAnnns
---------

Messages HHCDAnnns are not yet documented.

50. HHCDCnnns - DASDCOPY Utility
-----------------------------------------

HHCDC001E
---------

HHCDC001E progname: filename open error: error

Explanation An error was encountered when trying to open the input file
named filename to determine its type. The error is described by error.

Action Correct the error and retry the operation.

HHCDC002E
---------

HHCDC002E progname: filename read error: error

Explanation An error was encountered when trying to read the input file
named filename to determine its type. The error is described by error.

Action Correct the error and retry the operation.

HHCDC003E
---------

HHCDC003E progname: filename open failed

Explanation An error was encountered when trying to open the input file
named filename for copying. A previous message described the error.

Action Correct the error and retry the operation.

HHCDC004E
---------

HHCDC004E progname: ckd lookup failed for size cyls

Explanation There was no disk drive table entry that matched the number
of cylinders in the CKD source file, size. The program cannot determine
how much data to copy.

Action Correct the error and retry the operation.

HHCDC005E
---------

HHCDC005E progname: fba lookup failed, blks size

Explanation There was no disk drive table entry that matched the number
of blocks in the FBA source file, size. The program cannot determine how
much data to copy.

Action Correct the error and retry the operation.

HHCDC006E
---------

HHCDC006E progname: filename create failed

Explanation An error was encountered when trying to create the output
file named filename. A previous message described the error.

Action Correct the error and retry the operation.

HHCDC007E
---------

HHCDC007E progname: filename open failed

Explanation An error was encountered when trying to open the newly
created output file named filename. A previous message described the
error.

Action Correct the error and retry the operation.

HHCDC008E
---------

HHCDC008E progname: filename read error (track|block) number stat=status

Explanation An error was encountered when trying to read a block or
track from the input file named filename. The block or track is number
number. The status returned is shown as status.

Action Correct the error and retry the operation.

HHCDC009E
---------

HHCDC009E progname: filename write error (track|block) number
stat=status

Explanation An error was encountered when trying to read a block or
track from the input file named filename. The block or track is number
number. The status returned is shown as status.

Action Correct the error and retry the operation.

HHCDC010I
---------

HHCDC010I Copy successful !!!

Explanation The copy operation has completed successfully.

Action None. This is an informational message.

51. HHCDGnnns - Dyngui.DLL
-----------------------------------

HHCDG001I
---------

HHCDG001I dyngui.dll - name - version vers initiated

Explanation The dyngui loadable module was successfully loaded and
initiated.

Action None. This is an informational message.

HHCDG002I
---------

HHCDG002I dyngui.dll terminated

Explanation The dyngui loadable module was successfully terminated.

Action None. This is an informational message.

HHCDG003S
---------

HHCDG003S select failed on input stream: errmsg

Explanation The socket select function call failed on the input stream.
errmsg describes the exact error.

Action None; this is a fatal error, the system is immediately
terminated.

HHCDG004S
---------

HHCDG004S read failed on input stream: errmsg

Explanation An unrecoverable i/o error occurred while reading from the
input stream. errmsg describes the exact error.

Action None; this is a fatal error; the system is immediately
terminated.

HHCDG005E
---------

HHCDG005E Device query buffer overflow! (device=xxxx)

Explanation The device query buffer is not large enough to hold all of
the information returned by the device handler. xxxx is the device whose
information was being queried at the time the error occurred.

Action The system attempts to continue functioning but unpredictable
results may occur (i.e. the system could crash). You should report this
error to the Hercules developers immediately so that they can build you
a new dyngui.dll with a larger device query buffer. Since the dyngui.dll
is an unloadable module you will need to restart Hercules in order to
begin using the newly fixed version of dyngui.dll.

HHCDG006S
---------

HHCDG006S malloc pszInputBuff failed: errmsg

Explanation There was not enough virtual memory on the host system to
satisfy the malloc request for the input stream buffer. errmsg describes
the exact error.

Action None; this is a fatal error, the system is immediately
terminated. You should increase the size of your host system’s virtual
memory allocation so that there is enough for Hercules to run, or else
decrease the amount of memory that Hercules needs in order to run
(e.g. decrease your MAINSIZE value).

HHCDG007S
---------

HHCDG007S malloc pszCommandBuff failed: errmsg

Explanation There was not enough virtual memory on the host system to
satisfy the malloc request for the command processing buffer. errmsg
describes the exact error.

Action None; this is a fatal error, the system is immediately
terminated. You should increase the size of your host system’s virtual
memory allocation so that there is enough for Hercules to run, or else
decrease the amount of memory that Hercules needs in order to run
(e.g. decrease your MAINSIZE value).

52. HHCDInnns - DASDINIT Utility
-----------------------------------------

HHCDI001I
---------

HHCDI001I DASD initialization successfully completed.

Explanation The requested DASD volume has been successfully initialized
and is ready for use.

Action None. This is an informational message.

HHCDI002I
---------

HHCDI002I DASD initialization unsuccessful.

Explanation Initialization of the requested DASD volume was not
successful.

Action None. This is an informational message. Refer to preceding error
messages to determine the cause.

53. HHCDLnnns - DASDLOAD Utility
-----------------------------------------

HHCDL001E
---------

HHCDL001E Cannot open filename: error

Explanation The control file named filename cannot be opened. The error
is described by error.

Action Correct the error and rerun dasdload.

HHCDL002E
---------

HHCDL002E Volume serial statement missing from filename

Explanation The control file named filename does not contain a volume
serial statement. A volume serial is required.

Action Supply a volume serial statement and rerun dasdload.

HHCDL003E
---------

HHCDL003E Volume serial serial in filename line lineno is not valid

Explanation The volume serial serial supplied in line lineno of the
control file named filename is not valid. It must be from one to six
characters long.

Action Supply a valid volume serial and rerun dasdload.

HHCDL004E
---------

HHCDL004E Device type type in filename line lineno is not recognized

Explanation The device type type specified in line lineno of the control
file named filename is not a supported CKD device.

Action Specify a supported CKD device type and rerun dasdload.

HHCDL005E
---------

HHCDL005E count in filename line lineno is not a valid cylinder count

Explanation The requested number count of cylinders for the volume in
line lineno of the control file named filename is invalid. It must be a
decimal number.

Action Supply a valid cylinder count and rerun dasdload.

HHCDL006I
---------

HHCDL006I Creating type volume serial: tracks trks/cyl, length
bytes/track

Explanation The volume named serial of type type is being created with
tracks tracks per cylinder and length bytes per track.

Message Level 0.

Action None. This is an informational message.

HHCDL007E
---------

HHCDL007E Cannot create filename

Explanation The DASD image file named filename cannot be created. A
previous message described the problem.

Action Correct the reported error and rerun dasdload.

HHCDL008E
---------

HHCDL008E Cannot open filename

Explanation The DASD image file named filename could not be opened. A
previous message described the problem.

Action Correct the reported error and rerun dasdload.

HHCDL009I
---------

HHCDL009I Loading type volume serial

Explanation The newly created volume with serial serial of type type is
being loaded.

Message Level 0.

Action None. This is an informational message.

HHCDL010E
---------

HHCDL010E Cannot obtain storage for DSCB pointer array: error

Explanation An attempt to obtain storage for the array of DSCB pointers,
which will populate the VTOC, failed. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL011E
---------

HHCDL011E Invalid statement in filename line lineno

Explanation An invalid control statement was found at line lineno of the
control file named filename.

Action Correct the invalid statement and rerun dasdload.

HHCDL012I
---------

HHCDL012I Creating dataset dsn at cyl cylinder head head

Explanation The dataset named dsn is being created. It begins at
cylinder cylinder head head.

Message level 1

Action None. This is an informational message.

HHCDL013I
---------

HHCDL013I Dataset dsn contains size tracks

Explanation The dataset named dsn is size tracks long.

Message level 2

Action None. This is an informational message.

HHCDL014I
---------

HHCDL014I Free space starts at cyl cylinder head head

Explanation Free space on the volume begins at cylinder cylinder head
head and extends to the end of the volume.

Message level 1

Action None. This is an informational message.

HHCDL015W
---------

HHCDL015W Volume exceeds cylinders

Explanation The amount of space used on the volume exceeds the number of
cylinders cylinders requested in the control file. The number of
cylinders was explicitly requested instead of being allowed to default
to the size of a full volume for the device type. The volume has been
extended to accomodate the data written.

Action Specify more cylinders in the control file or allow the number to
default.

HHCDL016I
---------

HHCDL016I Total of count cylinders written to filename

Explanation A total of count cylinders have been written to the DASD
image file named filename.

Message level 0

Action None. This is an informational message.

HHCDL017I
---------

HHCDL017I Updating VTOC pointer pointer

Explanation The pointer to the VTOC in the volume label is being updated
to point to the VTOC at location pointer.

Message level 5

Action None. This is an informational message.

HHCDL018E
---------

HHCDL018E Cannot read VOL1 record

Explanation An attempt to read the volume label failed. A previous
message described the error.

Action Correct the error and rerun dasdload.

HHCDL019E
---------

HHCDL019E Cannot read filename line lineno: error

Explanation An error was encountered while trying to read the statement
at line number lineno of the control file named filename. The error is
described by error.

Action Correct the error and rerun dasdload.

HHCDL020E
---------

HHCDL020E Line too long in filename line lineno

Explanation The line at line number lineno of the control file named
filename is too long to be processed. This error can be caused by
failing to terminate the last line with an end-of-line marker.

Action Correct the error and rerun dasdload.

HHCDL021E
---------

HHCDL021E DSNAME or initialization method missing

Explanation Either the dataset name or the method to be used to
initialize it is missing from the control file. Both are required.

Action Supply the missing value and rerun dasdload.

HHCDL022E
---------

HHCDL022E Invalid initialization method: method

Explanation The method specified to initialize the dataset method is
invalid. It must be one of xmit, vs, empty, dip, cvol, vtoc, or seq.

Action Correct the initialization method and rerun dasdload.

HHCDL023E
---------

HHCDL023E Initialization file name missing

Explanation A dataset was specified as being initialized by either the
xmit, vs, or seq initialization methods but no source file was specified
to provide the data to be loaded.

Action Specify a source file name or specify the empty dataset
initialization method if the dataset is not to be loaded.

HHCDL024E
---------

HHCDL024E Invalid allocation units: units

Explanation The allocation unit specified units is invalid. It must be
either cyl or trk.

Action Specify a valid allocation unit and rerun dasdload.

HHCDL025E
---------

HHCDL025E Invalid primary space: space

Explanation The primary space requested space is not a valid decimal
number greater than 0.

Action Specify a valid space request and rerun dasdload.

HHCDL026E
---------

HHCDL026E Invalid secondary space: space

Explanation The secondary space requested space is not a valid decimal
number greater than 0.

Action Specify a valid space request and rerun dasdload.

HHCDL027E
---------

HHCDL027E Invalid directory space: space

Explanation The PDS directory space requested space is not a valid
decimal number greater than 0.

Action Specify a valid space request and rerun dasdload.

HHCDL028E
---------

HHCDL028E Invalid dataset organization: dsorg

Explanation The requested dataset organization dsorg is invalid. It must
be one of is, ps, da, or po.

Action Specify a valid dataset organization and rerun dasdload.

HHCDL029E
---------

HHCDL029E Invalid record format: recfm

Explanation The requested record format recfm is invalid. It must be one
of f, fb, fbs, v, vb, vbs, or u.

Action Specify a valid record format and rerun dasdload.

HHCDL030E
---------

HHCDL030E Invalid logical record length: lrecl

Explanation The requested logical record length lrecl is invalid. It
must be a decimal number between 0 and 32767.

Action Specify a valid logical record length and rerun dasdload.

HHCDL031E
---------

HHCDL031E Invalid block size: blksize

Explanation The requested block size blksize is invalid. It must be a
decimal number between 0 and 32767.

Action Specify a valid block size and rerun dasdload.

HHCDL032E
---------

HHCDL032E Invalid key length: keylen

Explanation The requested key length keylen is invalid. It must be a
decimal number between 0 and 255.

Action Specify a valid key length and rerun dasdload.

HHCDL033E
---------

HHCDL033E CCHH=cchh not found in extent table

Explanation The absolute track address cchh was not found in the table
listing the locations occupied by the dataset being loaded. There is
likely a problem with the input file.

Action Correct the input file and rerun dasdload.

HHCDL034E
---------

HHCDL034E Cannot open filename: error

Explanation The file named filename, which was specified as the source
of IPL text to be written to the volume, could not be opened. The error
is described by error.

Action Correct the error and rerun dasdload.

HHCDL035E
---------

HHCDL035E Cannot read filename: error

Explanation An error was encountered while reading the IPL text file
named filename. The error is described by error. If no error is
reported, the file did not contain an integral number of 80-byte card
images.

Action Correct the reported error or supply a valid IPL text file
consisting of 80-byte card images and rerun dasdload.

HHCDL036E
---------

HHCDL036E filename is not a valid object file

Explanation The IPL text file named filename is not a valid object file.
A record read from the file did not contain the required flag in the
first byte.

Action Supply a valid object file and rerun dasdload.

HHCDL037I
---------

HHCDL037I IPL text address=addr length=length

Explanation The object code from the current record of the IPL text file
will be loaded into memory at address address, and is length bytes long.

Message level 5

Action None. This is an informational message.

HHCDL038E
---------

HHCDL038E TXT record in filename has invalid count length

Explanation A text record in the IPL text file named filename has an
invalid length length. The length cannot exceed 56.

Action Supply a valid IPL text file and rerun dasdload.

HHCDL039E
---------

HHCDL039E IPL text in filename exceeds buflen bytes

Explanation The IPL text file named filename is too long to fit in the
available space on the volume. The IPL text cannot exceed buflen bytes
in length.

Action Supply a shorter IPL text file or specify a volume with a larger
track size and rerun dasdload.

HHCDL040E
---------

HHCDL040E Input record CCHHR=cchhr exceeds output device track size

Explanation The block to be written at absolute address cchhr is too
large to fit on a track on the disk being loaded.

Action Specify a device with a larger track size and rerun dasdload.

HHCDL041E
---------

HHCDL041E Dataset exceeds extent size: reltrk=track, maxtrk=maxtrk

Explanation The data to be written to the dataset is too large for the
space requested for it. If the space request was allowed to default, the
input file is corrupt.

Action If the space request was made explicitly, then request more
space. If the request was defaulted, supply a valid input file. Rerun
dasdload.

HHCDL042E
---------

HHCDL042E Input record CCHHR=cchhr exceeds virtual device track size

Explanation The block to be written at absolute address cchhr is too
large to fit on a track on the disk being loaded. In addition, this
message being issued instead of message HHCDL040E indicates an internal
inconsistency in the way Hercules computes the space available on a
track.

Action Specify a device with a larger track size and rerun dasdload.
Report the inconsistenct to the Hercules development team.

HHCDL043E
---------

HHCDL043E filename cyl cylinder head head read error

Explanation The data at cylinder cylinder, head head of the disk image
file named filename could not be read in order to be updated. A previous
message described the error.

Action Correct the previously reported error and rerun dasdload.

HHCDL044E
---------

HHCDL044E filename cyl cylinder head head invalid track header header

Explanation The track header header at cylinder cylinder, head head in
the disk image file named filename contained an address that did not
match the actual address.

Action Rerun dasdload. If the error persists, report it to the Hercules
development team.

HHCDL045E
---------

HHCDL045E filename cyl cylinder head head record record record not found

Explanation The record requested for update at cylinder cylinder, head
head, record record of the DASD image file named filename was not found.

Action Rerun dasdload. If the error persists, report it to the Hercules
development team.

HHCDL046E
---------

HHCDL046E Cannot update cyl cylinder head head rec record: Unmatched
KL/DL

Explanation The record to be written at cylinder cylinder, head head,
record record does not have the same key or data length as the record
that already exists at that location. This is not allowed for a record
update operation.

Action Rerun dasdload. If the error persists, report it to the Hercules
development team.

HHCDL047E
---------

HHCDL047E filename cyl cylinder head head read error

Explanation A read error was encountered when reading the track at
cylinder cylinder, head head, in the disk image file named filename. A
previous message described the error.

Action Correct the error reported by the previous message and rereun
dasdload.

HHCDL048I
---------

HHCDL048I Updating cyl cylinder head head rec record kl keylen dl
datalen

Explanation The record at cylinder cylinder, head head, record record is
being updated. It has a key length of keylen and data length datalen.

Message level 4

Action None. This is an informational message.

HHCDL049E
---------

HHCDL049E Cannot obtain storage for DSCB: error

Explanation An attempt to obtain storage to build a DSCB to describe a
dataset on the volume being loaded failed. The error is described by
error.

Action Correct the error and rerun dasdload.

HHCDL050E
---------

HHCDL050E DSCB count exceeds maximum, increase MAXDSCB

Explanation There are too many datasets on the volume being loaded and
an internal structure in dasdload is full.

Action Increase the value of the symbol MAXDSCB in the source program
and recompile dasdload, then rerun the program.

HHCDL051E
---------

HHCDL051E Cannot obtain storage for DSCB: error

Explanation An attempt to obtain storage to build a DSCB to describe the
VTOC on the volume being loaded failed. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL052E
---------

HHCDL052E DSCB count exceeds maximum, increase MAXDSCB

Explanation There are too many datasets on the volume being loaded and
an internal structure in dasdload is full.

Action Increase the value of the symbol MAXDSCB in the source program
and recompile dasdload, then rerun the program.

HHCDL053E
---------

HHCDL053E Cannot obtain storage for DSCB: error

Explanation An attempt to obtain storage to build a DSCB to describe the
free space on the volume being loaded failed. The error is described by
error.

Action Correct the error and rerun dasdload.

HHCDL054E
---------

HHCDL054E DSCB count exceeds maximum, increase MAXDSCB

Explanation There are too many datasets on the volume being loaded and
an internal structure in dasdload is full.

Action Increase the value of the symbol MAXDSCB in the source program
and recompile dasdload, then rerun the program.

HHCDL055E
---------

HHCDL055E VTOC too small, tracks tracks required

Explanation The VTOC allocation of tracks is too small to hold the VTOC.

Action Specify at least tracks tracks for the VTOC and rerun dasdload.

HHCDL056E
---------

HHCDL056E Error reading VTOC cyl cylinder head head

Explanation The first track of the VTOC could not be read so it could be
updated. A previous message described the error.

Action Correct the error reported by the previous message and rerun
dasdload.

HHCDL057I
---------

HHCDL057I VTOC starts at cyl cylinder head head and is tracks tracks

Explanation The VTOC on the volume being loaded starts at cylinder
cylinder, head head and is tracks tracks long.

Message level 1

Action None. This is an informational message.

HHCDL058I
---------

HHCDL058I Format format DSCB CCHHR=cchhr (TTR=ttr) dsname

Explanation The format format DSCB is located at absolute address cchhr
and relative address within the VTOC ttr. If format is 1, the dataset
described by the DSCB is named dsname.

Message level 4

Action None. This is an informational message.

HHCDL059I
---------

HHCDL059I Format 0 DSCB CCHHR cchhr (TTR=ttr)

Explanation A format 0 (empty) DSCB is located at absolute address cchhr
and relative address within the VTOC ttr.

Message level 4

Action None. This is an informational message.

HHCDL060E
---------

HHCDL060E Error reading track cyl cylinder head head

Explanation An error was encountered reading the track at cylinder cyl,
head head. A previous message described the error.

Action Correct the error reported by the previous message and rerun
dasdload.

HHCDL061E
---------

HHCDL061E Incomplete text unit

Explanation An text unit read from the input file was too short to
contain a valid header. The input data is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL062I
---------

HHCDL062I position tuname key fields

Explanation The text unit at position of the input buffer has the name
tuname and the numeric key value key. There are fields fields in the
text unit.

Message level 4

Action None. This is an informational message.

HHCDL063E
---------

HHCDL063E Too many fields in text unit

Explanation A text unit was read from the input file that had too many
fields in the header for that type of text unit. The input file is
probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL064E
---------

HHCDL064E Incomplete text unit

Explanation A text unit read from the input file was too short to
contain a valid field length. The input data is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL065E
---------

HHCDL065E Incomplete text unit

Explanation A text unit read from the input file was shorter than the
length in the field header. The input data is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL066E
---------

HHCDL066E filename read error: error

Explanation An error was encountered when reading the input file named
filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL067E
---------

HHCDL067E filename invalid segment header: header

Explanation A segment read from the file named filename has an invalid
header header. The input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL068E
---------

HHCDL068E filename first segment indicator expected

Explanation A segment read from the file named filename should have the
first segment indicator set but does not. The input file is probably
corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL069E
---------

HHCDL069E filename first segment indicator not expected

Explanation A segment read from the file named filename should not have
the first segment indicator set but does. The input file is probably
corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL070E
---------

HHCDL070E filename control record indicator mismatch

Explanation There was a mismatch between the first segment and the
control record. The input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL071E
---------

HHCDL071E filename read error: error

Explanation An error was encountered when reading a segment from the
input file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL072E
---------

HHCDL072E filename read error: error

Explanation An error was encountered when reading a COPYR1 record from
the input file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL073E
---------

HHCDL073E filename read error: error

Explanation An error was encountered when reading a COPYR2 record from
the input file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL074E
---------

HHCDL074E filename read error: error

Explanation An error was encountered when reading a data block header
from the input file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL075E
---------

HHCDL075E filename read error: error

Explanation An error was encountered when reading a data block from the
input file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL076I
---------

HHCDL076I File number: number

Explanation The file being processed is number number.

Message level 4

Action None. This is an informational message.

HHCDL077E
---------

HHCDL077E Invalid text unit at offset offset

Explanation An invalid text unit was read from position offset. A
previous message described the error. The input file is probably
corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL078I
---------

HHCDL078I File filenum: DSNAME=dsname

Explanation The dataset name of file number filenum is dsname.

Message level 2

Action None. This is an informational message.

HHCDL079I
---------

HHCDL079I DSORG=dsorg RECFM=recfm LRECL=lrecl BLKSIZE=blksize
KEYLEN=keylen DIRBLKS=dirblks

Explanation For the dataset listed in the preceding HHCDL078I message
the dataset organization is dsorg, the record format is recfm, the
logical record length is lrecl, the block size is blksize, the key
length is keylen and the directory block count is dirblks.

Message level 2

Action None. This is an informational message.

HHCDL080E
---------

HHCDL080E Invalid text unit at offset offset

Explanation An invalid text unit was read from position offset. A
previous message described the error. The input file is probably
corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL081E
---------

HHCDL081E COPYR1 record length is invalid

Explanation The length of the COPYR1 record is invalid. The input file
is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL082E
---------

HHCDL082E COPYR1 header identifier not correct

Explanation The header identifier of the COPYR1 record is invalid. The
input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL083E
---------

HHCDL083E COPYR1 unload format is unsupported

Explanation The COPYR1 record indicates that the file was unloaded in a
format that is not supported by dasdload. The file may be corrupt or it
may simply be in a newer format than is supported by this version of
dasdload.

Action Supply a supported input file and rerun dasdload.

HHCDL084I
---------

HHCDL084I Original dataset: DSORG=dsorg RECFM=recfm LRECL=lrecl
BLKSIZE=blksize KEYLEN=keylen

Explanation For the original dataset, the dataset organization is dsorg,
the record format is recfm, the logical record length is lrecl, the
block size is blksize, the key length is keylen and the directory block
count is dirblks.

Message level 2

Action None. This is an informational message.

HHCDL085I
---------

HHCDL085I Dataset was unloaded from device type ucbtype (device)

Explanation The dataset was unloaded from a device device, with UCB
device type ucbtype.

Message level 2

Action None. This is an informational message.

HHCDL086I
---------

HHCDL086I Original device has cylinders cyls and heads heads

Explanation The device listed in the preceding HHCDL085I message has
cylinders cylinders and heads heads.

Message level 2

Action None. This is an informational message.

HHCDL087E
---------

HHCDL087E COPYR2 record length is invalid

Explanation The length of the COPYR2 record just read is not valid. The
input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL088E
---------

HHCDL088E Invalid number of extents extents

Explanation The number of extents reported in the COPYR2 record is
invalid, either less than 1 or more than 16. The input file is probably
corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL089I
---------

HHCDL089I Extent extent: Begin CCHH=begcchh End CCHH=endcchh
Tracks=tracks

Explanation For extent number extent, the extent starts at cylinder and
head begcchh, and ends at endcchh, for a total of tracks tracks.

Message level 4

Action None. This is an informational message.

HHCDL090I
---------

HHCDL090I End of directory

Explanation The end of the PDS directory has been reached.

Message level 3

Action None. This is an informational message.

HHCDL091E
---------

HHCDL091E Directory block record length is invalid

Explanation The directory block read from the input file has the wrong
length. It must be 276 bytes long. The input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL092E
---------

HHCDL092E Cannot obtain storage for directory block: error

Explanation An attempt to obtain storage for the directory block being
processed failed. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL093E
---------

HHCDL093E Number of directory blocks exceeds maxdblk, increase MAXDBLK

Explanation The number of directory blocks in the dataset being
processed exceeds the size of an internal control structure. The maximum
number is maxdblk.

Action Increase the value of the constant MAXDBLK in the program source
and recompile dasdload.

HHCDL094E
---------

HHCDL094E Directory block byte count is invalid

Explanation The length of the current directory block is invalid. The
input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL095I
---------

HHCDL095I (Alias|Member) memname TTR=ttr Userdata=userdata

Explanation The alias or member named memname is located at relative
address ttr. If user data is present, it is printed as userdata.

Message level 3

Action None. This is an informational message.

HHCDL096I
---------

HHCDL096I Member name TTR=oldttr replaced by newttr

Explanation In the directory entry for member name, the old pointer to
the mamber oldttr was replaced by the member’s actual relative address
newttr.

Message level 4

Action None. This is an informational message.

HHCDL097E
---------

HHCDL097E Member name TTR=ttrnot found in dataset

Explanation A request was made to update the directory entry for the
member named name but there was no directory entry to update.

Action This is likely an internal logic error. Report the error to the
Hercules development team.

HHCDL098I
---------

HHCDL098I Updating note list for member name at TTR=ttr CCHHR=cchhr

Explanation The note list for the member named name, at relative address
ttr, absolute address cchhr, is being updated.

Message level 4

Action None. This is an informational message.

HHCDL099E
---------

HHCDL099E filename cyl cylinder head head read error

Explanation An attempt to read the track in the DASD image file named
filename at cylinder cylinder, head head, failed. A previous error
described the failure.

Action Correct the error reported by the previous message and rerun
dasdload.

HHCDL100E
---------

HHCDL100E filename cyl cylinder head head invalid track header header

Explanation The header header of the track in the DASD image file named
filename at cylinder cylinder, head head did not agree with the actual
address of the track. This is probably an internal logic error.

Action Report the error to the Hercules development team.

HHCDL101E
---------

HHCDL101E filename cyl cylinder head head rec record note list record
not found

Explanation A request was made to update a note list record at cylinder
cylinder, head head, record record, but the record was not found. The
input dataset may be corrupt.

Action Supply a valid input dataset and rerun dasdload.

HHCDL102E
---------

HHCDL102E Member member note list at cyl cylinder head head rec record
dlen datalen is too short for numttrs TTRs

Explanation The data length datalen of the note list record for member
member at cylinder cylinder, head head, record record, is too short to
contain the requested number numttrs of record pointers. The input
dataset is probably corrupt.

Action Supply a valid input dataset and rerun dasdload.

HHCDL103E
---------

HHCDL103E filename track read error cyl cylinder head head

Explanation An attempt to read the track in the DASD image file named
filename at cylinder cylinder, head head, failed. A previous error
described the failure.

Action Correct the error reported by the previous message and rerun
dasdload.

HHCDL104I
---------

HHCDL104I Updating cyl cylinder head head rec record kl keylen dl
datalen

Explanation The record at cylinder cylinder, head head, record record,
with key length keynel and data length datalen is being updated.

Message level 4

Action None. This is an informational message.

HHCDL105E
---------

HHCDL105E Directory block byte count is invalid

Explanation The length of the current directory block is invalid. The
input file is probably corrupt.

Action Supply a valid input file and rerun dasdload.

HHCDL106E
---------

HHCDL106E Cannot open file filename: error

Explanation An attempt to open the IEBCOPY input file named filename
failed. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL107E
---------

HHCDL107E Cannot obtain input buffer: error

Explanation An attempt to obtain a 64K byte input buffer for reaading
the IEBCOPY input file failed. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL108E
---------

HHCDL108E Cannot obtain storage for directory block array:error

Explanation An attempt to obtain storage for the internal array used to
store directory blocks failed. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL109E
---------

HHCDL109E Cannot obtain storage for TTR table: error

Explanation An attempt to obtain storage for the internal array used to
store track pinters for later conversion failed. The error is described
by error.

Action Correct the error and rerun dasdload.

HHCDL110I
---------

HHCDL110I Processing file filename

Explanation The input file named filename is being processed.

Message level 1

Action None. This is an informational message.

HHCDL111I
---------

HHCDL111I Control record: recname length length

Explanation A control record named recname of length length has been
read.

Message level 4

Action None. This is an informational message.

HHCDL112I
---------

HHCDL112I File number: filenum ((not) selected)

Explanation The data file, number filenum, was (or was not) selected for
processing.

Message level 4

Action None. This is an informational message.

HHCDL113I
---------

HHCDL113I Data record: length length

Explanation A data record of length length has been read.

Message level 4

Action None. This is an informational message.

HHCDL114E
---------

HHCDL114E write error: input record CCHHR=cchhr (TTR=ttr) KL=keylen
DL=datalen

Explanation An error was encountered writing the data record at absolute
address cchhr, relative address ttr, with key length keylen and data
length datalen. A previous message described the error.

Action Correct the error described by the previous message and rerun
dasdload.

HHCDL115I
---------

HHCDL115I CCHHR=incchhr (TTR=inttr) KL=keylen DL=datalen ->
CCHHR=outcchhr (TTR=outttr)

Explanation The record at absolute address incchhr, relative address
inttr, with key length keylen and data length datalen, is being written
to the output DASD image at absolute address outcchhr, relative address
outttr.

Message level 4

Action None. This is an informational message.

HHCDL116E
---------

HHCDL116E TTR count exceeds maxttr, increase MAXTTR

Explanation The list of relative address pointers exceeds the size of
the internal array used to contain them, maxttr.

Action Increase the constant MAXTTR in the program source and recompile
dasdload.

HHCDL117I
---------

HHCDL117I Catalog block at cyl cylinder head head rec record

Explanation A catalog record has been written to disk at cylinder
cylinder, head head and record record.

Message level 4

Action None. This is an informational message.

HHCDL118I
---------

HHCDL118I Catalog block at cyl cylinder head head rec record

Explanation A catalog index record has been written to disk at cylinder
cylinder, head head and record record.

Message level 4

Action None. This is an informational message.

HHCDL119I
---------

HHCDL119I Catalog block at cyl cylinder head head rec record

Explanation An empty catalog record has been written to disk at cylinder
cylinder, head head and record record.

Message level 4

Action None. This is an informational message.

HHCDL120I
---------

HHCDL120I DIP complete at cyl cylinder head head record record

Explanation The LOGREC dataset has been initialized. The last block
written was at cylinder cylinder, head head, record record.

Message level 3

Action None. This is an informational message.

HHCDL121E
---------

HHCDL121E SEQ dsorg must be PS or DA: dsorg=dsorg

Explanation The dataset organization specified for the input dataset was
dsorg. It must be either PS or DA but is not.

Action Specify a valid dataset organization for sequential file
processing or specify the correct processing option for the file being
loaded and rerun dasdload.

HHCDL122E
---------

HHCDL122E SEQ recfm must be F or FB: recfm=recfm

Explanation The record format specified for the input dataset was recfm.
It must be either F or FB but is not.

Action Specify a valid record format for sequential file processing and
rerun dasdload.

HHCDL123E
---------

HHCDL123E SEQ invalid lrecl or blksz: lrecl=lrecl blksz=blksz

Explanation The logical record length specified for the input dataset
was lrecl, and the block size was blksz. Either the block size was not a
multiple of the logical record length and the record format was
specified as FB or the block size was different from the logical record
length and the record format was specified as F.

Action Specify a valid logical record length and block size for
sequential file processing and rerun dasdload.

HHCDL124E
---------

HHCDL124E SEQ keyln must be 0 for blocked files

Explanation The key length was specified as nonzero and the record
format was specified as FB. This combination is invalid.

Action If a key is required, specify a record format of F. If no key is
required, specify a key length of 0. Rerun dasdload.

HHCDL125E
---------

HHCDL125E Cannot open filename: error

Explanation An error was encountered when attempting to open the input
file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL126E
---------

HHCDL126E Cannot stat filename: error

Explanation An error was encountered when attempting to obtain the size
of the file named filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL127E
---------

HHCDL127E filename cyl cylinder head head read error

Explanation An attempt to read the track in the DASD image file named
filename at cylinder cylinder, head head, failed. A previous error
described the failure.

Action Correct the error reported by the previous message and rerun
dasdload.

HHCDL128E
---------

HHCDL128E filename read error: error

Explanation An error was encountered reading the input file named
filename. The error is described by error.

Action Correct the error and rerun dasdload.

HHCDL130W
---------

HHCDL130W WARNING – XMIT file utility is not IEBCOPY; file filename not
loaded

Explanation The file filename cannot be loaded as an XMIT file because
it is not an unloaded PDS.

Action If filename is an unloaded sequential file, rerun DASDLOAD
specifying XMSEQ instead of XMIT.

HHCDL131I
---------

HHCDL131I Control record: recname length length

Explanation A control record named recname of length length has been
read.

Action None.

HHCDL132I
---------

HHCDL132I File number: filenum ((not) selected)

Explanation The date file, number filenum was (or was not) selected for
processing.

Action None.

HHCDL133I
---------

HHCDL133I Data record: length length

Explanation A data record of length length has been read.

Action None.

HHCDL135I
---------

HHCDL135I CCHHR=outcchhr (TTR=outttr) KL=keylen DL=datalen

Explanation A record with key length keylen and date length datalen is
being written to the output DASD image at absolute address outcchhr,
relative address outttr.

Action None.

HHCDL136E
---------

HHCDL136E Cannot open file filename: error

Explanation An attempt to open the sequential XMIT input file named
filename failed. The error is described by error.

Action Correct the error and rerun DASDLOD.

HHCDL137E
---------

HHCDL137E Cannot obtain input buffer: error

Explanation An attempt to obtain a 64K byte input buffer for reading the
sequential XMIT input file failed. The error is described by error.

Action Correct the error and rerun DASDLOD.

HHCDL138W
---------

HHCDL130W WARNING – XMIT file utility is not INMCOPY; file filename not
loaded

Explanation The file filename cannot be loaded as an XMSEQ file because
it does not appear to contain an unloaded sequential file.

Action If filename is an unloaded PDS file, rerun DASDLOAD specifying
XMIT.

HHCDL139I
---------

HHCDL139I Processinf file filename

Explanation The input file named filename is being processed as a
sequential XMIT file.

Action None.

54. HHCDSnnns - DASDISUP Utility
-----------------------------------------

HHCDS001E
---------

HHCDS001E Cannot obtain storage for member array: error

Explanation An attempt to obtain storage for the array of SYS1.SVCLIB
members failed. The error is described by error.

Action Correct the error and rerun dasdisup.

HHCDS002I
---------

HHCDS002I End of directory: count members selected

Explanation The end of the SYS1.SVCLIB directory has been reached. count
members have been selected for processing.

Action None. This is an informational message.

HHCDS003E
---------

HHCDS003E Directory block byte count is invalid

Explanation The length of the directory block read is invalid. The
SYS1.SVCLIB directory is probably corrupt.

Action Rebuild SYS1.SVCLIB and rerun dasdisup.

HHCDS004E
---------

HHCDS004E Number of members exceeds MAX_MEMBERS

Explanation SYS1.SVCLIB has too many members to fit in the array used to
store their information.

Action Increase the value of MAX_MEMBERS in dasdisup.c and recompile the
program, then run it again.

HHCDS005E
---------

HHCDS005E Member member TTR count is zero

Explanation The member named member has no data associated with it.
Since aliases have been skipped already, this means that the SYS1.SVCLIB
directory is corrupt.

Action Rebuild SYS1.SVCLIB and run dasdisup again.

HHCDS006W
---------

HHCDS006W Member member is not single text record

Explanation The member named member is not contained in a single text
record. This is an invalid condition. The member will be skipped later
and message HHCDS011E will be issued.

Action If this member must be processed, rebuild SYS1.SVCLIB and rerun
dasdisup.

HHCDS007W
---------

HHCDS007W Member member size size exceeds X’7F8’ bytes

Explanation The member named member is too long. The maximum length of
an OS/360 SVC load module is X’7F8’ (2040 decimal) bytes. The member
will be processed but OS/360 may not process it correctly.

Action Correct the member in SYS1.SVCLIB and rerun dasdisup.

HHCDS008W
---------

HHCDS008W Member member size size is not a multiple of 8

Explanation The member named member is not a multiple of 8 bytes long.
Its actual size is size. This is not valid for an OS/360 load module.
OS/360 will issue an ABEND when an attempt is made to load the module.

Action Correct the member in SYS1.SVCLIB and rerun dasdisup.

HHCDS009I
---------

HHCDS009I Alias alias skipped

Explanation The alias named alias has been skipped, since no processing
is necessary for it.

Action None. This is an informational message.

HHCDS010I
---------

HHCDS010I Member member skipped

Explanation The member named member has been skipped, since it does not
have an XCTL table.

Action None. This is an informational message. If the member should have
an XCTL table, rebuild it in SYS1.SVCLIB and rerun dasdisup.

HHCDS011E
---------

HHCDS011E Member member has multiple text records

Explanation The member named member has multiple text records. This is
not a valid condition for an OS/360 SVC module. The member will not be
processed. Message HHCDS006W was issued for this member earlier.

Action If this member must be processed, rebuild it in SYS1.SVCLIB and
rerun dasdisup.

HHCDS012E
---------

HHCDS012E Member member has invalid TTR ttr

Explanation The pointer to the text record for the member named member
is invalid. The pointer found is ttr. The member cannot be located to be
processed. The SYS1.SVCLIB directory is probably corrupt.

Action Rebuild SYS1.SVCLIB and rerun dasdisup.

HHCDS013I
---------

HHCDS013I Processing member member text record TTR=ttr CCHHR=cchhr

Explanation The member named member is being processed. Its relative
location is ttr and its absolute location is cchhr.

Action None. This is an informational message.

HHCDS014E
---------

HHCDS014E Member member error reading TTR ttr

Explanation An attempt to read the member named member, at the relative
location ttr, failed. The member cannot be processed.

Action Rebuild SYS1.SVCLIB and rerun dasdisup. If this is unsuccessful,
rebuild the entire DASD volume.

HHCDS015E
---------

HHCDS015E Member member TTR ttr text record length length is not valid

Explanation The length length of the text record at location ttr of the
member named member is less than 8, greater than 1024, or not a multiple
of 8. All of these conditions must be met for the length to be valid.
The member is probably corrupt.

Action Rebuild the member in SYS1.SVCLIB and rerun dasdisup.

HHCDS016E
---------

HHCDS016E Member member TTR ttr text record length textlength does not
match length dirlength in directory

Explanation The length textlength of the text record at location ttr is
not the same as the length dirlength in the directory entry for member
member. Either the member, or the directory, is probably corrupt.

Action Rebuild the member in SYS1.SVCLIB and rerun dasdisup. If this
does not correct the problem, rebuild SYS1.SVCLIB in its entirety.

HHCDS017E
---------

HHCDS017E Member member TTR ttr XCTL table improperly terminated

Explanation The XCTL table in member member at location ttr runs past
the end of the text record. The member is probably corrupt.

Action Rebuild the member and rerun dasdisup.

HHCDS018I
---------

HHCDS018I member (Alias|Member) skipped

Explanation The member or alias named member is not an Open, Close, or
EOV module, and so does not have an XCTL table that needs to be updated.
It has been skipped.

Action None. This is an informational message.

HHCDS019I
---------

HHCDS019I In member member: reference TTRL=ttrl status

Explanation A reference to the member named reference in the member
named member was found, the referenced member is at the location ttrl in
the table. status is optional; it may be one of:

\*\* Member reference not found The referenced member was not found in
SYS1.SVCLIB. The reference cannot be updated.

replaced by TTRL=newttrl flag The reference was updated to point to the
referenced member’s actual location at newttrl. If flag is \***\*, the
actual length of the referenced member is different from the length of
the member in the reference pointer.

Action None. This is an informational message.

55. HHCDTnnns - DASDCAT Utility
----------------------------------------

HHCDT001E
---------

HHCDT001E failed to open image filename

Explanation An error was ancountered trying to open the DASD image file
named filename. A previous message described the error.

Action Correct the error and rerun dasdcat.

HHCDT002E
---------

HHCDT002E Can’t make 80 column card images from block length length

Explanation A block read from the member specified is not a multiple of
80 characters long, and so cannot be split evenly into 80-character card
images. The actual length read is length.

Action Select a different member, or omit the c flag from the member
specification.

HHCDT003E
---------

HHCDT003E Directory block byte count is invalid

Explanation The length of a PDS directory block in the specified dataset
is invalid. The PDS directory is corrupt or the dataset is not a PDS.

Action Make sure the dataset specified is a PDS (partitioned dataset).
If it is, then the dataset is corrupt.

HHCDT004E
---------

HHCDT004E non-PDS-members not yet supported

Explanation This version of dasdcat does not support reading sequential
datasets.

Action Specify a PDS as input to dasdcat.

HHCDT005E
---------

HHCDT005E unknown dataset name option: ‘option’

Explanation An invalid option was specified on the dataset name
specification. Only the options ‘a’ and ‘c’ are valid.

Action Remove the invalid option from the dataset name specification and
rerun dasdcat.

56. HHCDUnnns - DASD Utilities Common Functions
--------------------------------------------------------

HHCDU001I
---------

HHCDU001I Updating cyl cylinder head head

Explanation The track at cylinder number cylinder and head number head
is being rewritten after being modified. This message is only issued if
verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU002E
---------

HHCDU002E filename write track error: stat=status

Explanation An attempt to rewrite a track from the DASD image named
filename failed. The status returned was status.

Action Correct the error and retry the operation.

HHCDU003I
---------

HHCDU003I Reading cyl cylinder head head

Explanation The track at cylinder number cylinder and head number head
is being read. This message is only issued if verbose message reporting
has been selected.

Action None. This is an informational message.

HHCDU004E
---------

HHCDU004E filename read track error: stat=status

Explanation An attempt to read a track from the DASD image named
filename failed. The status returned was status.

Action Correct the error and retry the operation.

HHCDU005I
---------

HHCDU005I Searching extent 0 begin (begcyl,beghead) end (endcyl,endhead)

Explanation The first extent of the dataset is being searched for a key.
The extent starts at the track at cylinder begcyl, head beghead, and
ends at the track at cylinder endcyl, head endhead. This message is only
issued if verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU006I
---------

HHCDU006I Searching extent extent begin (begcyl,beghead) end
(endcyl,endhead)

Explanation An extent, extent, of the dataset is being searched for a
key. The extent starts at the track at cylinder begcyl, head beghead,
and ends at the track at cylinder endcyl, head endhead. This message is
only issued if verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU007E
---------

HHCDU007E Track track not found in extent table

Explanation An attempt was made to convert a track number to an absolute
address, but the track specified, track, is beyond the end of the
dataset.

Action Correct the error and retry the operation. The dataset, the VTOC,
or the DASD image may be corrupt.

HHCDU008E
---------

HHCDU008E Cannot obtain storage for device descriptor buffer: error

Explanation An attempt to obtain storage for the buffer used to hold a
CKD DASD image description failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU009E
---------

HHCDU009E Cannot open filename: error

Explanation The CKD image file named filename could not be opened. The
error is described by error.

Action Correct the error and retry the operation.

HHCDU010E
---------

HHCDU010E filename read error: error

Explanation An error was encountered while reading the CKD header record
from the file named filename. The error is described by error.

Action Correct the error and retry the operation.

HHCDU011E
---------

HHCDU011E filename CKD header invalid

Explanation The file filename is not a valid CKD DASD image file. Either
the first record is not the length of a CKD header record or the marker
in the header record is not correct.

Action Supply the name of a valid CKD DASD image file and retry the
operation.

HHCDU012E
---------

HHCDU012E DASD table entry not found for devtype type

Explanation The device type in the CKD header record does not correspond
to any known DASD device. The CKD DASD image file may be corrupt or the
device is not supported by Hercules.

Action Supply the name of a supported CKD DASD image file and retry the
operation.

HHCDU013E
---------

HHCDU013E CKD initialization failed for filename

Explanation The device-specific initialization routine for the file
named filename failed. Another message describes the specific failure.

Action See the specific message for the action needed.

HHCDU014I
---------

HHCDU014I filename heads=heads trklen=trklen

Explanation The device represented by the CKD DASD image file named
filename has heads heads and tracks of trklen bytes length. This message
is only issued if verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU015I
---------

HHCDU015I Updating cyl cylinder head head

Explanation During processing of a request to close the CKD image file,
the track at cylinder number cylinder and head number head is being
rewritten, since it has been modified. This message is only issued if
verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU016E
---------

HHCDU016E filename write track error: stat=status

Explanation During processing of a request to close the CKD image file,
an attempt to rewrite a track from the DASD image named filename failed.
The status returned was status.

Action Correct the error and retry the operation.

HHCDU017E
---------

HHCDU017E Cannot obtain storage for device descriptor buffer: error

Explanation An attempt to obtain storage for the buffer used to hold a
FBA DASD image description failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU018E
---------

HHCDU018E DASD table entry not found for devtype type

Explanation The default FBA device type does not correspond to any known
DASD device. This is likely an internal programming error.

Action Report the bug to the Hercules development team.

HHCDU019E
---------

HHCDU019E FBA initialization failed for filename

Explanation The device-specific initialization routine for the file
named filename failed. Another message describes the specific failure.

Action See the specific message for the action needed.

HHCDU020I
---------

HHCDU020I filename sectors=sectors size=size

Explanation The device represented by the FBA DASD image file named
filename has sectors sectors of size bytes length. This message is only
issued if verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU021E
---------

HHCDU021E VOL1 record not found

Explanation The volume being processed does not have a volume label. It
is probably blank and unformatted.

Action Format the volume or specify a formatted volume and retry the
operation.

HHCDU022I
---------

HHCDU022I VOLSER=serial VTOC=cchhr

Explanation The volume being processed has the volume serial serial and
its VTOC format 4 DSCB is at absolute location cchhr. This message is
only issued if verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU023I
---------

HHCDU023I VTOC start begcchh end endcchh

Explanation The VTOC of the volume being processed begins at cylinder
and head begcchh and ends at cylinder and head endcchh. This message is
only issued if verbose message reporting has been selected.

Action None. This is an informational message.

HHCDU024E
---------

HHCDU024E Dataset dsn not found in VTOC

Explanation The requested dataset dsn was not found in the VTOC and does
not exist on this volume.

Action Specify the correct dataset name or select the volume on which it
appears.

HHCDU025I
---------

HHCDU025I DSNAME=dsn F1DSCB CCHHR=cchhr

Explanation The format 1 DSCB for the requested dataset dsn is at
absolute location cchhr. This message is only issued if verbose message
reporting has been selected.

Action None. This is an informational message.

HHCDU026E
---------

HHCDU026E F1DSCB record not found

Explanation The requested dataset is listed in the VTOC but its format 1
DSCB record was not found when an attempt was made to read it. The VTOC
may be corrupt.

Action Recreate the dataset and retry the operation.

HHCDU027E
---------

HHCDU027E F3DSCB record not found

Explanation The requested dataset is reported to contain more than three
extents in the format 1 DSCB but its format 3 DSCB record was not found
when an attempt was made to read it. The VTOC may be corrupt.

Action Recreate the dataset and retry the operation.

HHCDU028E
---------

HHCDU028E filename open error: error

Explanation An attempt to create the CKD DASD image file named filename
failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU029E
---------

HHCDU029E filename device header write error: error

Explanation An attempt to write the device header to the CKD DASD image
file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU030E
---------

HHCDU030E filename compressed device header write error: error

Explanation An attempt to write the compressed device header to the CKD
DASD image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU031E
---------

HHCDU031E Cannot obtain l1tab buffer: error

Explanation An attempt to obtain storage for the primary lookup table
buffer failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU032E
---------

HHCDU032E filename primary lookup table write error: error

Explanation An attempt to write the primary lookup table to the CKD DASD
image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU033E
---------

HHCDU033E filename secondary lookup table write error: error

Explanation An attempt to write the secondary lookup table to the CKD
DASD image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU034E
---------

HHCDU034E filename dasdcopy ftruncate error: error

Explanation An attempt to truncate the CKD DASD image file named
filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU035E
---------

HHCDU035E filename cylinder cyl head head write error: error

Explanation An attempt to write the track at cylinder cyl, head head to
the CKD DASD image file named filename failed. The error is described by
error.

Action Correct the error and retry the operation.

HHCDU036E
---------

HHCDU036E filename compressed device header lseek error: error

Explanation An attempt to reposition to the beginning of the CKD DASD
image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU037E
---------

HHCDU037E filename compressed device header write error: error

Explanation An attempt to rewrite the compressed device header record of
the CKD DASD image file named filename failed. The error is described by
error.

Action Correct the error and retry the operation.

HHCDU038E
---------

HHCDU038E filename secondary lookup table lseek error: error

Explanation An attempt to reposition to the secondary lookup table of
the CKD DASD image file named filename failed. The error is described by
error.

Action Correct the error and retry the operation.

HHCDU039E
---------

HHCDU039E filename secondary lookup table write error: error

Explanation An attempt to rewrite the secondary lookup table of the CKD
DASD image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU040E
---------

HHCDU040E filename close error: error

Explanation An attempt to close the CKD DASD image file named filename
failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU041I
---------

HHCDU041I count cylinders successfully written to file filename

Explanation The CKD DASD image file named filename has been successfully
created. It contains count cylinders.

Action None. This is an informational message.

HHCDU042E
---------

HHCDU042E Cylinder count count is outside range min-max

Explanation The requested number of cylinders count is outside the valid
range from min to max.

Action Specify a valid number of cylinders and retry the operation.

HHCDU043E
---------

HHCDU043E Cannot obtain track buffer: error

Explanation An attempt to obtain storage for the track buffer failed.
The error is described by error.

Action Correct the error and retry the operation.

HHCDU044I
---------

HHCDU044I Creating type volume serial: cylinders cyls, tracks trks/cyl,
length bytes/track

Explanation A new volume is being created of device type type and volume
serial number serial. It has cylinders cylinders, tracks tracks per
cylinder and length bytes per track.

Action None. This is an informational message.

HHCDU045E
---------

HHCDU045E Sector count count is outside range min-max

Explanation The requested number of sectors count is outside the valid
range from min to max.

Action Specify a valid number of cylinders and retry the operation.

HHCDU046E
---------

HHCDU046E Cannot obtain sector buffer: error

Explanation An attempt to obtain storage for the sector buffer failed.
The error is described by error.

Action Correct the error and retry the operation.

HHCDU047I
---------

HHCDU047I Creating type volume serial: sectors sectors, length
bytes/sector

Explanation A new volume is being created of device type type and volume
serial number serial. It has sectors sectors and length bytes per
sector.

Action None. This is an informational message.

HHCDU048E
---------

HHCDU048E filename open error: error

Explanation An attempt to create the FBA DASD image file named filename
failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU049E
---------

HHCDU049E filename dasdcopy ftruncate error: error

Explanation An attempt to truncate the FBA DASD image file named
filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU050E
---------

HHCDU050E filename sector sector write error: error

Explanation An attempt to write sector number sector to the FBA DASD
image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU051E
---------

HHCDU051E filename close error: error

Explanation An attempt to close the FBA DASD image file named filename
failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU052I
---------

HHCDU052I count sectors successfully written to file filename

Explanation The FBA DASD image file named filename has been successfully
created. It contains count sectors.

Action None. This is an informational message.

HHCDU053E
---------

HHCDU053E File size too large: size [l1tab]

Explanation The requested file size size would result in a primary
lookup table that is too large. The DASD image cannot be created as a
compressed image.

Action Either specify fewer sectors or create the DASD image
uncompressed.

HHCDU054E
---------

HHCDU054E filename open error: error

Explanation An attempt to create the compressed FBA DASD image file
named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU055I
---------

HHCDU055I Creating type compressed volume serial: sectors sectors,
length bytes/sector

Explanation A new compressed FBA volume is being created of device type
type and volume serial number serial. It has sectors sectors and length
bytes per sector.

Action None. This is an informational message.

HHCDU056E
---------

HHCDU056E filename devhdr write error: error

Explanation An attempt to write the device header to the compressed FBA
DASD image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU057E
---------

HHCDU057E filename cdevhdr write error: error

Explanation An attempt to write the compressed device header to the
compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU058E
---------

HHCDU058E filename l1tab write error: error

Explanation An attempt to write the primary lookup table to the
compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU059E
---------

HHCDU059E filename l2tab write error: error

Explanation An attempt to write the secondary lookup table to the
compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU060E
---------

HHCDU060E filename block header write error: error

Explanation An attempt to write a compressed block header to the
compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU061E
---------

HHCDU061E filename block write error: error

Explanation An attempt to write a compressed block to the compressed FBA
DASD image file named filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU062E
---------

HHCDU062E filename block write error: error

Explanation An attempt to write an uncompressed block to the compressed
FBA DASD image file named filename failed. The error is described by
error.

Action Correct the error and retry the operation.

HHCDU063E
---------

HHCDU063E filename cdevhdr lseek error: error

Explanation An attempt to reposition to the beginning of the compressed
FBA DASD image file named filename failed. The error is described by
error.

Action Correct the error and retry the operation.

HHCDU064E
---------

HHCDU064E filename cdevhdr rewrite error: error

Explanation An attempt to rewrite the compressed device header record of
the compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU065E
---------

HHCDU065E filename l2tab lseek error: error

Explanation An attempt to reposition to the secondary lookup table of
the compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU066E
---------

HHCDU066E filename l2tab rewrite error: error

Explanation An attempt to rewrite the secondary lookup table of the
compressed FBA DASD image file named filename failed. The error is
described by error.

Action Correct the error and retry the operation.

HHCDU067E
---------

HHCDU067E filename close error: error

Explanation An attempt to close the compressed FBA DASD image file named
filename failed. The error is described by error.

Action Correct the error and retry the operation.

HHCDU068I
---------

HHCDU068I count sectors successfully written to file filename

Explanation The compressed FBA DASD image file named filename has been
successfully created. It contains count sectors.

Action None. This is an informational message.

57. HHCHDnnns - Hercules Dynamic Loader
------------------------------------------------

HHCHD001E
---------

HHCHD001E registration alloc failed for entry

Explanation Storage could not be obtained to register entrypoint entry

Action Correct the error and restart Hercules.

HHCHD002E
---------

HHCHD002E cannot allocate memory for DLL descriptor: error

Explanation Initialisation of the dynamic loader environment failed due
to the error described by error.

Action Correct the error and restart Hercules.

HHCHD003E
---------

HHCHD003E unable to open Hercules as DLL: error

Explanation The main Hercules load module could not be opened by the
dynamic loader. The dynamic loader error is described by error

Action Correct the error and restart Hercules.

HHCHD004I
---------

HHCHD004I No initializer in module: error

Explanation The initializer in DLL named module could not be found. The
error is described by error

Action Correct the error and restart Hercules.

HHCHD005E
---------

HHCHD005E module already loaded.

Explanation An attempt was made to load an already loaded module.

Action Unload to module first.

HHCHD006S
---------

HHCHD006S cannot allocate memory for DLL descriptor: error

Explanation Initialisation of the dynamic loader environment failed due
to the error described by error.

Action Correct the error and restart Hercules.

HHCHD007E
---------

HHCHD007E unable to open DLL module: error

Explanation The DLL named module could not be opened. The error is
described by error.

Action Ensure that the correct module is specified and is accessible.

HHCHD008I
---------

HHCHD008I No initializer in module: error

Explanation The initializer in DLL named module could not be found. The
error is described by error

Action Correct the error and restart Hercules.

HHCHD009E
---------

HHCHD009E module not found

Explanation An attempt was made to unload a module that was not loaded.

Action No action required.

HHCHD010I
---------

HHCHD010I Dependency check failed for module, version(vers_actual)
expected(vers_exp)

Explanation The version of the module’s required dependency does not
match the version of the dependency in the module that contains the
dependency.

Action No action required.

HHCHD011I
---------

HHCHD011I Dependency check failed for module, size(size_actual)
expected(size_exp)

Explanation The size of the modules required dependency does not match
the size of the dependency in the module that contains the dependency.

Action No action required.

HHCHD012E
---------

HHCHD012E No depency section in module: error

Explanation The module being loaded does not contain the required
dependency section. The error is described by error.

Action Rebuild the module with the required HDL_DEPENDENCY_SECTION
defined.

HHCHD013E
---------

HHCHD013E No depency section in module: error

Explanation The module being loaded does not contain the required
dependency section. The error is described by error.

Action Rebuild the module with the required HDL_DEPENDENCY_SECTION
defined.

HHCHD014E
---------

HHCHD014E Dependency check failed for module module

Explanation One or more required dependencies were not satisfied. The
preceding HHCHD010I and/or HHCHD011I message(s) identifies which of the
dependencies failed and the reason why.

Action If the module was not loaded, rebuild the module using the same
version of the required dependency as the module that contains the
dependency and try again.

HHCHD015E
---------

HHCHD015E Unloading of module not allowed

Explanation An attempt was made to unload a module that was not allowed
to be unloaded.

Action No action required.

HHCHD018I
---------

HHCHD018I Loadable module directory is dir

Explanation The default loadable module directory was manually changed
to dir via either a supplied MODPATH configuration file statement or via
the -d command line option.

Action No action required.

HHCHD100I
---------

HHCHD100I Loading module …

Explanation Module module is being loaded.

Action No action required.

HHCHD101I
---------

HHCHD101I Module module loaded

Explanation Module module has been loaded.

Action No action required

HHCHD102I
---------

HHCHD102I Unloading module …

Explanation Module module is being unloaded.

Action No action required

HHCHD103I
---------

HHCHD103I Module module unloaded

Explanation Module module has been unloaded.

Action No action required

58. HHCHEnnns - HETINIT Utility……………………………………………………………………………
---------------------------------------------------------------------

HHCHEnnns
---------

Messages HHCHEnnns are not yet documented.

59. HHCHGnnns - HETGET Utility…………………………………………………………………………..
---------------------------------------------------------------------

HHCHGnnns
---------

Messages HHCHGnnns are not yet documented.

60. HHCHMnnns - HETMAP Utility
---------------------------------------

HHCHMnnns
---------

Messages HHCHMnnns are not yet documented.

61. HHCHTnnns - HTTP Server………………………………………………………………………………
------------------------------------------------------------------

HHCHT001I
---------

HHCHT001I HTTP listener thread started: tid=threadid, pid=processid

Explanation The HTTP server thread to accept and process incoming
requests has been started. The thread id is threadid and the process id
is processid.

Action No action required.

HHCHT002E
---------

HHCHT002E socket: error

Explanation An attempt to obtain a TCP socket to receive HTTP requests
failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCHT003W
---------

HHCHT003W Waiting for port port to become free

Explanation The thread that handles HTTP connection requests is waiting
for the TCP port denoted by port to become available for use.

Action If this message persists, some other program has control of the
TCP port listed. Find out which one it is and terminate it.

HHCHT004E
---------

HHCHT004E bind: error

Explanation An attempt to bind the socket to the TCP port to receive
HTTP requests failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCHT005E
---------

HHCHT005E listen: error

Explanation An attempt to put the socket into listening state for HTTP
requests failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCHT006I
---------

HHCHT006I Waiting for HTTP requests on port port pid=num

Explanation Hercules is ready to accept HTTP requests on port port.

Action No action required.

HHCHT007E
---------

HHCHT007E select: error

Explanation An attempt to wait for data from HTTP requests failed. The
error is described by error.

Action Correct the error and restart Hercules.

HHCHT008E
---------

HHCHT008E accept: error

Explanation An attempt to accept a TCP connection for HTTP requests
failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCHT009E
---------

HHCHT009E fdopen: error

Explanation An attempt to open the socket for reading HTTP requests
failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCHT010E
---------

HHCHT010E http_request create_thread: error

Explanation An attempt to create a thread for processing HTTP requests
failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCHT011E
---------

HHCHT011E html_include: Cannot open filename: error

Explanation The file named filename, which was included from another
file, could not be opened. The error is described by error.

Action Correct the error and retry the operation.

HHCHT014I
---------

HHCHT014I HTTPROOT = pathname

Explanation The root directory path for the HTTP server is pathname.

Action No action required.

62. HHCHUnnns - HETUPD Utility…………………………………………………………………………..
---------------------------------------------------------------------

HHCHUnnns
---------

Messages HHCHUnnns are not yet documented.

63. HHCIFnnns - Network Interface Configuration Handler (hercifc)
--------------------------------------------------------------------------

HHCIF001E
---------

HHCIF001E programname: Must be called from within Hercules.

Explanation This program can only be called from Hercules itself and may
not be executed from the command line. The program was executed using
the name programname.

Action Don’t do that.

HHCIF002E
---------

HHCIF002E programname: Cannot obtain socket: error

Explanation An attempt to obtain a socket for controlling the
destination interface failed. The error is described by error. The
program was executed using the name programname.

Action Correct the error and retry the operation.

HHCIF003E
---------

HHCIF003E programname: I/O error on read: error

Explanation An attempt to read a request from Hercules failed. The error
is described by error. The program was executed using the name
programname.

Action Correct the error and retry the operation.

HHCIF004W
---------

HHCIF004W programname: Unknown request: request.

Explanation The request from Hercules was invalid. The request code was
request. The request has been ignored. The program was executed using
the name programname.

Action Make sure that the hercifc program is the same version as the
running copy of Hercules. If so, this is an internal error. Report it.

HHCIF005E
---------

HHCIF005E programname: ioctl error doing operation on interface: error

Explanation An attempt to perform an ioctl operation operation on
interface interface failed. The error is described by error. The program
was executed using the name programname.

Action Correct the error and retry the operation.

64. HHCINnnns - Hercules Initialization
------------------------------------------------

HHCIN001S
---------

HHCIN001S Cannot register SIGINT handler: error

Explanation An attempt to register a handler for the SIGINT signal
failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCIN002E
---------

HHCIN002E Cannot suppress SIGPIPE signal: error

Explanation An attempt to ignore the SIGPIPE signal failed. The error is
described by error. This will cause Hercules to terminate abnormally if
a printer device is defined to a pipe and that pipe is closed while data
is being written to it.

Action Correct the error and restart Hercules. Do not print to a pipe
until you have corrected the error.

HHCIN003S
---------

HHCIN003S Cannot register SIGILL/FPE/SEGV/BUS/USR handler: error

Explanation An attempt to register a handler for one of the listed
signals failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCIN004S
---------

HHCIN004S Cannot create watchdog thread: error

Explanation An attempt to create the watchdog thread to monitor Hercules
execution failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCIN005S
---------

HHCIN005S Cannot create http_server thread: error

Explanation An attempt to create the HTTP server thread failed. The
error is described by error.

Action Correct the error and restart Hercules.

HHCIN006S
---------

HHCIN006S Cannot create panel thread: error

Explanation An attempt to create the operator control panel thread
failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCIN007S
---------

HHCIN007S Cannot create devnum connection thread: error

Explanation The shared device server was unable to create the thread
meant to manage remote device devnum. The error is described by error.

Action Correct the error and restart Hercules.

HHCIN008S
---------

HHCIN008S DYNGUI.DLL load failed; Hercules terminated.

Explanation The external GUI interface module ‘dyngui.dll’ could not
loaded. The preceding HHCHD007E message should provide the reason for
the failure.

Action Correct the error and restart Hercules. If the error is Win32
error 126 (“The specified module could not be found”), check your
Windows PATH setting and/or your MODPATH control statement to ensure one
or both of them includes the directory where Hercules is executing from.

HHCIN099I
---------

HHCIN099I Hercules terminated

Explanation Hercules has ended.

Action No action required.

65. HHCLCnnns - LCS Emulation
--------------------------------------

HHCLC001E
---------

HHCLC001E nnnn unable to allocate LCSBLK

Explanation There is insufficient storage to allocate the control block
for LCS device number nnnn.

Action Correct the error and restart Hercules.

HHCLC017E
---------

HHCLC017E nnnn invalid device name devname

Explanation The value of the -n or -dev parameter in the configuration
statement for LCS device number nnnn is missing or too long.

Action Correct the parameter and reinitialize the device.

HHCLC018E
---------

HHCLC018E nnnn invalid MAC address macaddr

Explanation The value of the -m or -mac parameter in the configuration
statement for LCS device number nnnn is not a valid MAC address.

Action Correct the parameter and reinitialize the device.

HHCLC019E
---------

HHCLC019E nnnn too many arguments in statement

Explanation The configuration statement for LCS device number nnnn
contains too many positional parameters.

Action Correct the statement and restart Hercules.

HHCLC020E
---------

HHCLC020E nnnn invalid IP address ipaddr

Explanation The first positional parameter in the configuration
statement for LCS device number nnnn is not a valid IP address.

Action Correct the statement and reinitialize the device.

HHCLC021E
---------

HHCLC021E Invalid HWADD statement in filename: stmt

Explanation The port number parameter of the HWADD statement stmt in OAT
file filename is not numeric.

Action Correct the statement and reinitialize the device.

HHCLC022E
---------

HHCLC022E Invalid MAC in HWADD statement in filename: stmt (macaddr)

Explanation The second positional parameter of the HWADD statement stmt
in OAT file filename is not a valid MAC address.

Action Correct the parameter and reinitialize the device.

HHCLC023E
---------

HHCLC023E Invalid ROUTE statement in filename: stmt

Explanation The port number parameter of the ROUTE statement stmt in OAT
file filename is not numeric.

Action Correct the statement and reinitialize the device.

HHCLC024E
---------

HHCLC024E Invalid net address in ROUTE filename: stmt (netaddr)

Explanation The second positional parameter of the ROUTE statement stmt
in OAT file filename is not a valid IP network address.

Action Correct the parameter and reinitialize the device.

HHCLC025E
---------

HHCLC025E Invalid net mask in ROUTE filename: stmt (netaddr)

Explanation The third positional parameter of the ROUTE statement stmt
in OAT file filename is not a valid IP network mask.

Action Correct the parameter and reinitialize the device.

HHCLC026E
---------

HHCLC026E Error in filename: Missing device number or mode

Explanation The OAT file filename contains a statement which cannot be
identified.

Action Correct the statement and reinitialize the device.

HHCLC027E
---------

HHCLC027E Error in filename: devnum: Invalid device number

Explanation The device number devnum specified in the OAT file filename
is not a valid hexadecimal number.

Action Correct the statement and reinitialize the device.

HHCLC028E
---------

HHCLC028E Error in filename: stmt: Missing PORT number

Explanation Statement stmt in OAT file filename for the IP port of an
LCS device does not contain a port number.

Action Correct the statement and reinitialize the device.

HHCLC029E
---------

HHCLC029E Error in filename: port: Invalid PORT number

Explanation The port number port specified in the OAT file filename for
the IP port of an LCS device is not a valid decimal number.

Action Correct the statement and reinitialize the device.

HHCLC031E
---------

HHCLC031E Error in filename: stmt: Invalid entry starting at text

Explanation The parameter text specified in statement stmt in the OAT
file filename should be PRI, SEC, or NO.

Action Correct the statement and reinitialize the device.

HHCLC032E
---------

HHCLC032E Error in filename: stmt: Invalid IP address (ipaddr)

Explanation The parameter ipaddr specified in statement stmt in the OAT
file filename is not a valid IP address.

Action Correct the statement and reinitialize the device.

HHCLC033E
---------

HHCLC033E Error in filename: stmt: Missing PORT number

Explanation Statement stmt in OAT file filename for the SNA port of an
LCS device does not contain a port number.

Action Correct the statement and reinitialize the device.

HHCLC034E
---------

HHCLC034E Error in filename: port: Invalid PORT number

Explanation The port number port specified in the OAT file filename for
the SNA port of an LCS device is not a valid decimal number.

Action Correct the statement and reinitialize the device.

HHCLC035E
---------

HHCLC035E Error in filename: stmt: SNA does not accept any arguments

Explanation Statement stmt in OAT file filename for the SNA port of an
LCS device contains positional parameters which are not used for SNA
ports.

Action Correct the statement and reinitialize the device.

HHCLC036E
---------

HHCLC036E Error in filename: mode: Invalid MODE

Explanation Mode mode specified in a device statement in the OAT file
filename should be IP or SNA.

Action Correct the statement and reinitialize the device.

HHCLC037E
---------

HHCLC037E Error reading file filename line nnnn: description

Explanation An error occurred reading the OAT file for an LCS device.
description is the operating system’s description of the error. The
error occurred at line nnnn of file filename.

Action Check that the correct OAT file name is specified in the
configuration file.

HHCLC038E
---------

HHCLC038E File filename line nnnn is too long

Explanation An error occurred reading the OAT file for an LCS device.
The error occurred at line nnnn of file filename. Either the line
exceeds 255 characters, or there is no linefeed at the end of the file.

Action Correct the OAT file.

HHCLC039E
---------

HHCLC039E Cannot open file filename: description

Explanation An error occurred opening the OAT file filename for an LCS
device. description is the operating system’s description of the error.

Action Check that the correct OAT file name is specified in the
configuration file.

HHCLC040E
---------

HHCLC040E nnnn LCSDEV mmmm not in configuration

Explanation The device number mmmm specified in the OAT file does not
match the LCS device number nnnn in the configuration file.

Action None.

HHCLC055I
---------

HHCLC055I tapn using MAC hh:hh:hh:hh:hh:hh

Explanation The MAC address assigned the TUN/TAP device tapn is
hh:hh:hh:hh:hh:hh.

Action None. This is an informational message.

HHCLC056W
---------

HHCLC056W tapn NOT using MAC hh:hh:hh:hh:hh:hh

Explanation MAC address hh:hh:hh:hh:hh:hh was requested in the
configuration statement or in the OAT file for an LCS device but the
operating system did not accept the request to change the MAC address
for TUN/TAP device tapn.

Action The device will use the MAC address shown in the preceding
HHCLC055I message.

HHCLC073I
---------

HHCLC073I nnnn: TAP device tapn opened

Explanation LCS device number nnnn is now associated with the kernel
TUN/TAP device named tapn.

Action None. This is an informational message.

66. HHCLGnnns - System Log Functions
---------------------------------------------

HHCLG001E
---------

HHCLG001E Error redirecting stdout: error

Explanation The stdout stream could not be redirected to the system
logger. The error is described by error.

HHCLG002E
---------

HHCLG002E Error reading syslog pipe: error

Explanation An error occurred while reading the syslog pipe. The error
is described by error.

HHCLG003E
---------

HHCLG003E Error writing hardcopy log: error

Explanation The error as indicated by error occurred while writing the
hardcopy log.

HHCLG004E
---------

HHCLG004E Error duplicating stderr: error

Explanation Stdout could not be redirected to stderr. The error is
described by error.

HHCLG005E
---------

HHCLG005E Error duplicating stdout: error

Explanation Stderr could not be redirected to stdout. The error is
described by error.

HHCLG006E
---------

HHCLG006E Duplicate error redirecting hardcopy log: error

Explanation The error described by error occurred whilst redirecting the
hardcopy log.

HHCLG007S
---------

HHCLG007S Hardcopy log fdopen failed: error

Explanation An attempt to open a stream for the hardcopy log failed. The
error is described by error.

HHCLG008S
---------

HHCLG008S logbuffer malloc failed: error

Explanation An instorage buffer for the system log could not be
obtained. The error is described by error.

HHCLG009S
---------

HHCLG009S Syslog message pipe creation failed: error

Explanation An attempt to create the pipe for the system logger failed.
The error is described by error.

Action Check that your firewall is not preventing Hercules from opening
a listening pipe.

HHCLG012E
---------

HHCLG012E Cannot create logger thread: error

Explanation An attempt to create the logger thread failed. Error is the
description of the error code returned by the pthread_create call.

Action If the error is “No error” ensure that Hercules has been
correctly linked with the pthread library.

HHCLG014E
---------

HHCLG014E Log not active

Explanation A log off command was issued but there was no active log
file.

Action None.

HHCLG015I
---------

HHCLG015I Log closed

Explanation The active log file has been closed as a result of a log off
command.

Action None. This is an informational message.

HHCLG016E
---------

HHCLG016E Error opening log file filename: error

Explanation The new log file requested by a log command could not be
opened. error is the description of the error code returned by the open
call.

Action Reissue the log command with the correct filename.

HHCLG017S
---------

HHCLG017S Log file fdopen failed for filename: error

Explanation The logger was unable to obtain the file descriptor for the
new log file requested by a log command. error is the description of the
error code returned by the fdopen call.

Action Reissue the log command with the correct filename.

HHCLG018I
---------

HHCLG018I Log switched to filename

Explanation As a result of a log command the logger is now writing to
the requested log file.

Action None. This is an informational message.

67. HHCPNnnns - Control Panel Command Messages
-------------------------------------------------------

HHCPN001I
---------

HHCPN001I Control panel thread started: tid=threadid, pid=processid

Explanation The control panel thread has been started. Its thread id is
threadid and its process id is processid.

Action No action required.

HHCPN002S
---------

HHCPN002S Cannot obtain keyboard buffer: error

Explanation An attempt to obtain memory for the keyboard buffer, used to
hold operator input, failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCPN003S
---------

HHCPN003S Cannot obtain message buffer: error

Explanation An attempt to obtain memory for the message buffer, used to
hold operator output, failed. The error is described by error.

Action Correct the error and restart Hercules.

HHCPN004E
---------

HHCPN004E select: error

Explanation An error was encountered while waiting for input from the
console. The error is described by error.

Action Correct the error and retry the operation.

HHCPN005E
---------

HHCPN005E keyboard read: error

Explanation An error was encountered while attempting to read keyboard
input. The error is described by error.

Action Correct the error and retry the operation.

HHCPN006E
---------

HHCPN006E message pipe read: error

Explanation An error was encountered while attempting to read from the
pipe used to communicate to the control panel thread from the rest of
Hercules. The error is described by error.

Action Correct the error and retry the operation.

HHCPN007E
---------

HHCPN007E RC file filename open failed: error

Explanation The RC file containing commands to be executed at Hercules
startup, named filename, could not be opened. The error is described by
error.

Action Correct the error and restart Hercules if necessary. The commands
contained in the file may be issued manually.

HHCPN008I
---------

HHCPN008I RC file processing thread started using file filename

Explanation Processing of the commands contained in the file named
filename has begun.

Action No action required.

HHCPN009E
---------

HHCPN009E RC file buffer malloc failed: error

Explanation An attempt to obtain storage for the buffer for commands
being read from the startup command file failed. The error is described
by error.

Action Correct the error and restart Hercules, if needed. The comands
contained in the file may be issued manually.

HHCPN010W
---------

HHCPN010W Ignoring invalid RC file pause statement: argument

Explanation The argument argument on the pause statement in the startup
command file is invalid. It must be a decimal number between 0 and 999.
Processing will continue without any pause.

Action Correct the invalid argument and restart Hercules, if desired.

HHCPN011I
---------

HHCPN011I Pausing RC file processing for delay seconds…

Explanation Processing of the startup command file is being delayed for
delay seconds because of a pause statement in the file.

Action No action required.

HHCPN012I
---------

HHCPN012I Resuming RC file processing…

Explanation Processing of the startup command file has resumed at the
expiration of the delay interval.

Action No action required.

HHCPN013I
---------

HHCPN013I EOF reached on RC file. Processing complete.

Explanation The end of the startup command file has been reached and
processing of the file is complete.

Action No action required.

HHCPN014E
---------

HHCPN014E I/O error reading RC file: error

Explanation An error was encountered while reading a command from the
startup command file. The error is described by error. Any remaining
commands in the file will not be processed.

Action Correct the error and restart Hercules if desired. Any
unprocessed commands may be issued manually.

HHCPN052E
---------

HHCPN052E Target CPU nnnn type cputype does not allow ipl

Explanation An IPL command was issued but the target CPU nnnn is a
processor engine of type cputype which does not support the initial
program load procedure.

Action Use the CPU command to set the target CPU to a processor of type
CP, IFL, or ICF, then re-issue the IPL command.

HHCPN162I
---------

HHCPN162I Hercules instruction trace displayed in { regsfirst \| noregs
\| traditional } mode

Explanation This message shows the current setting of the traceopt mode.

Action None. This is an informational message.

HHCPN180E
---------

HHCPN180E ‘sh’ commands are disabled

Explanation The ‘sh’ (shell) command has been purposely disabled via a
SHCMDOPT configuration file statement. Shell commands entered via the
Hercules hardware console will not be processed.

Action Remove or modify the SHCMDOPT configuration file statement and
restart Hercules.

HHCPN181E
---------

HHCPN181E Device number s:CCUU not found

Explanation The device number “CCUU” on Logical Channel Subsystem “s”
was not found in the configuration.

Action Reissue the command with an existing device number.

HHCPN195I
---------

HHCPN195I Log options: val

Explanation This message displays the current logging options. It is
issued when the LOGOPT command is entered without operands. val is
TIMESTAMP or NOTIMESTAMP.

Action None. This is an informational message.

HHCPN196E
---------

HHCPN196E Invalid logopt value val

Explanation This message is issued when the operand of a LOPGOPT command
is an invalid value. Valid values for val are TIMESTAMP or NOTIMESTAMP.

Action Reenter the LOGOPT command with a valid operand.

HHCPN197I
---------

HHCPN197I Log option set: val

Explanation As the result of the LOGOPT command, the Hercules logging
option val has been set. val is TIMESTAMP or NOTIMESTAMP.

Action None. This is an informational message.

68. HHCPRnnns - Printer Emulation
------------------------------------------

HHCPR001E
---------

HHCPR001E File name missing or invalid for printer address

Explanation There was no file name specified for the printer at address
address, or else there was one specified but it was too long.

Action Correct the error in the Hercules configuration file. The device
may be made available by specifying a filename with the devinit command.

HHCPR002E
---------

HHCPR002E Invalid argument for printer address: argument

Explanation An invalid argument was specified on the definition of the
printer at address address.

Action Correct or remove the invalid argument.

HHCPR003E
---------

HHCPR003E address Error writing to filename: error

Explanation An error was encountered when writing output for the printer
at address address to the file named filename. The error is described by
error.

Action Correct the error and retry the operation.

HHCPR004E
---------

HHCPR004E Error opening file filename: error

Explanation An error was encountered when opening the file named
filename. The error is described by error.

Action Correct the error and retry the operation.

HHCPR005E
---------

HHCPR005E address device initialization error: pipe: error

Explanation An error was encountered when opening a pipe for the printer
at address address. The error is described by error.

Action Correct the error and retry the operation.

HHCPR006E
---------

HHCPR006E address device initialization error: fork: error

Explanation An error was encountered when starting the program to
process the output from the printer at address address. The error is
described by error.

Action Correct the error and retry the operation.

HHCPR007I
---------

HHCPR007I pipe receiver (pid=processid) starting for address

Explanation The program to process the output from the printer at
address address is starting. Its process id is processid.

Action No action required.

HHCPR008E
---------

HHCPR008E address dup2 error: error

Explanation The file descriptor for stdin could not be duplicated for
the program to process the output from the printer at address address.
The error is described by error.

Action Correct the error and retry the operation.

HHCPR009E
---------

HHCPR009E address dup2 error: error

Explanation The file descriptor for stdout could not be duplicated for
the program to process the output from the printer at address address.
The error is described by error.

Action Correct the error and retry the operation.

HHCPR010E
---------

HHCPR010E address dup2 error: error

Explanation The file descriptor for stderr could not be duplicated for
the program to process the output from the printer at address address.
The error is described by error.

Action Correct the error and retry the operation.

HHCPR011I
---------

HHCPR011I pipe receiver (pid=processid) terminating for address

Explanation The program to process the output from the printer at
address address has ended sucessfully. Its process id was processid.

Action No action required.

HHCPR012E
---------

HHCPR012E address Unable to execute program: error

Explanation The program named program to process the output from the
printer at address address could not be started. The error is described
by error.

Action Correct the error and retry the operation.

69. HHCPUnnns - Card Punch Emulation
---------------------------------------------

HHCPU001E
---------

HHCPU001E File name missing or invalid

Explanation The file name specified for punched output is invalid or no
file name is given.

Action Correct the error and retry the operation.

HHCPU002E
---------

HHCPU002E Invalid argument: argument

Explanation An invalid argument argument was specified for the card
punch. Valid arguments are ascii, ebcdic, and crlf.

Action Correct the invalid argument and retry the operation.

HHCPU003E
---------

HHCPU003E Error opening file filename: error

Explanation The file named filename could not be opened for output of
card punch data. The error is described by error.

Action Correct the error and retry the operation.

HHCPU004E
---------

HHCPU004E Error writing to filename: error

Explanation The file named filename encountered an error while writing
card punch data. The error is described by error.

Action Correct the error and retry the operation.

70. HHCRDnnns - Card Reader Emulation
----------------------------------------------

HHCRD001E
---------

HHCRD001E Out of memory

Explanation A request to allocate memory for the list of files to be
read failed.

Action Correct the error and retry the operation.

HHCRD002E
---------

HHCRD002E File name too long (max=max): “filename”

Explanation The file name specified by filename is too long. The maximum
length is max.

Action Specify a shorter name.

HHCRD003E
---------

HHCRD003E Unable to access file “filename”: error

Explanation The file specified by filename could not be accessed. The
error is described by error.

Action Correct the error and retry the operation.

HHCRD004E
---------

HHCRD004E Out of memory

Explanation A request to allocate memory for the list of files to be
read failed.

Action Correct the error and retry the operation.

HHCRD005E
---------

HHCRD005E Specify ‘ascii’ or ‘ebcdic’ (or neither) but not both

Explanation Both of the character set translation options ascii and
ebcdic were specified. At most one is allowed.

Action Select only one character set translation option.

HHCRD006E
---------

HHCRD006E Only one filename (sock_spec) allowed for socket devices

Explanation More than one filename argument was given for a socket card
reader device. Only one is allowed. This error can also result if an
option name is misspelled.

Action Remove the extraneous filenames or correct the misspelled
options.

HHCRD007I
---------

HHCRD007I Defaulting to ‘ascii’ for socket device address

Explanation The socket card reader device at address address has been
set to ASCII mode since neither translation option was specified. The
socket card reader device cannot automatically select the translation
option.

Action If you wish to read cards without translation from ASCII to
EBCDIC, you must specify the ebcdic option on the reader definition.

HHCRD008W
---------

HHCRD008W ‘multifile’ option ignored: only one file specified

Explanation Only one file was specified for input to the card reader and
the multifile option was specified. This option is Explanationless with
only one input file. The option has been ignored.

Action If you wish to read more than one input file without signalling
end-of-file or intervention required between them, then all files must
all be specified on the same reader definition. If you only wish to
process one file, omit the multifile option.

HHCRD009E
---------

HHCRD009E File name too long (max=max): “filename”

Explanation The file name specified by filename is too long. The maximum
length is max.

Action Specify a shorter name.

HHCRD010E
---------

HHCRD010E Unable to access file “filename”: error

Explanation The file specified by filename could not be accessed. The
error is described by error.

Action Correct the error and retry the operation.

HHCRD011E
---------

HHCRD011E Close error on file “filename”: error

Explanation An attempt to close the file specified by filename failed.
The error is described by error.

Action Correct the error and retry the operation.

HHCRD012I
---------

HHCRD012I ipaddr (hostname) disconnected from device address
(socketspec)

Explanation The client on the host named hostname, with the IP address
ipaddr, has disconnected from the socket card reader device at address
address, specified by socketspec.

Action No action required.

HHCRD013E
---------

HHCRD013E Error opening file filename: error

Explanation The file named filename could not be opened for reading. The
error is described by error.

Action Correct the error and retry the operation.

HHCRD014E
---------

HHCRD014E Error reading file filename: error

Explanation An error was encountered while attempting to read the first
160 bytes of the file named filename in order to determine its character
set. The error is described by error.

Action Correct the error and retry the operation.

HHCRD015E
---------

HHCRD015E Seek error in file filename: error

Explanation An error was encountered while attempting to return to the
beginnning of file named filename after determining its character set.
The error is described by error.

Action Correct the error and retry the operation.

HHCRD016E
---------

HHCRD016E Error reading file filename: error

Explanation An error was encountered while attempting to read an EBCDIC
card image from the file named filename. The error is described by
error.

Action Correct the error and retry the operation.

HHCRD017E
---------

HHCRD017E Unexpected end of file on filename

Explanation Too few characters were read from the file named filename.
The autopad option was not specified.

Action Either ensure that all records in the file are 80 bytes long, or
specify the autopad option on the reader definition.

HHCRD018E
---------

HHCRD018E Error reading file filename: error

Explanation An error was encountered while attempting to read an ASCII
card image from the file named filename. The error is described by
error.

Action Correct the error and retry the operation.

HHCRD019E
---------

HHCRD019E Card image exceeds size bytes in file filename

Explanation A line in the file named filename is too long to fit on one
card. The trunc option was not specified. The maximum length is size
bytes.

Action Either ensure that all lines in the file are less than size bytes
long or specify the trunc option on the reader definition.

71. HHCSDnnns - Socket Devices Common Functions
--------------------------------------------------------

HHCSDnnns
---------

Messages HHCSDnnns are not yet documented.

72. HHCTAnnns - Tape Device Emulation
----------------------------------------------

HHCTAnnns
---------

Messages HHCTAnnns are not yet documented.

73. HHCTCnnns - TAPECOPY Utility
-----------------------------------------

HHCTCnnns
---------

Messages HHCTCnnns are not yet documented.

74. HHCTEnnns - Terminal Emulation
-------------------------------------------

HHCTE001I
---------

HHCTE001I Console connection thread started: tid=threadid, pid=processid

Explanation The thread that handles connection requests from console
devices has been started.

Action No action required.

HHCTE002W
---------

HHCTE002W Waiting for port port to become free

Explanation The thread that handles connection requests from console
devices is waiting for the TCP port denoted by port to become available
for use.

Action If this message persists, some other program has control of the
TCP port listed. Determine the program involved and terminate it.

HHCTE003I
---------

HHCTE003I Waiting for console connection on port port pid=num

Explanation Hercules is ready to accept console connections on port
port.

Action No action required.

HHCTE004I
---------

HHCTE004I Console connection thread terminated

Explanation The thread that handles connection requests from console
devices has been terminated.

Action No action required.

HHCTE005E
---------

HHCTE005E Cannot create console thread: reason

Explanation The thread that handles connection requests from console
devices could not be started. The reason is shown as reason.

Action Correct the reason listed and restart Hercules.

HHCTE006A
---------

HHCTE006A Enter input for console device address

Explanation The 1052 console device at address is waiting for input.

Action Type the desired input for the console and press the ENTER key.
If you do not wish to get this message when input is requested, define
the console with the option noprompt.

HHCTE007I
---------

HHCTE007I Device address closed by client ipaddr

Explanation The client at IP address ipaddr that was connected to the
3270 console at address address has closed the connection. The device is
no longer available for use.

Action No action required.

HHCTE008I
---------

HHCTE008I Device address closed by client ipaddr

Explanation The client at IP address ipaddr that was connected to the
1052 console at address address has closed the connection. The device is
no longer available for use.

Action No action required.

HHCTE009I
---------

HHCTE009I Client ipaddr connected to type device address

Explanation The client at IP address ipaddr has connected to Hercules as
a type device and is now available at address address.

Action No action required.

HHCTE010E
---------

HHCTE010E CNSLPORT statement invalid: statement

Explanation The CNSLPORT statement in the Hercules configuration file is
invalid.

Action Correct the CNLSPORT statement in the configuration file and
restart Hercules.

HHCTE011E
---------

HHCTE011E Device devn: Invalid IP address: ipaddr

Explanation The IP address ipaddr is invalid.

Action Correct the IP address in the configuration file and restart
Hercules.

HHCTE012E
---------

HHCTE012E Device devn: Invalid mask value: ipmask

Explanation The mask value ipmask is invalid.

Action Correct the mask value in the configuration file and restart
Hercules.

HHCTE013E
---------

HHCTE013E Device devn: Extraneous argument(s): xxx…

Explanation The argument(s) xxx and any which follow it (if any) was not
recognized or understood and are thus invalid.

Action Correct the arguments in the configuration file and restart
Hercules.

HHCTE014I
---------

HHCTE014I type device devn disconnected.

Explanation The client connected to device devn has abruptly terminated
the connection (ECONNRESET).

Action No action required.

HHCTE017E
---------

HHCTE017E Device devn: Duplicate SYSG console definition.

Explanation Device number devn has been defined as an integrated 3270
(SYSG) console, but a SYSG console already exists. Only one SYSG console
can be defined per system.

Action Correct the statement in the configuration file and restart
Hercules.

75. HHCTMnnns - TAPEMAP Utility
----------------------------------------

HHCTMnnns
---------

Messages HHCTMnnns are not yet documented.

76. HHCTSnnns - TAPESPLT Utility
-----------------------------------------

HHCTSnnns
---------

Messages HHCTSnnns are not yet documented.

77. HHCTTnnns - TOD Clock and Timer Services
-----------------------------------------------------

HHCTT001W
---------

HHCTT001W Timer thread set priority priority failed: error

Explanation An attempt to change the priority of the timer thread to
priority failed. The error is described by error. The thread priority
has not been changed. Hercules overall performance may be impaired as a
result.

Action If performance problems are noted, correct the error and restart
Hercules.

HHCTT002I
---------

HHCTT002I Timer thread started: tid=threadid, pid=processid,
priority=priority

Explanation The thread for timing functions has been started. Its thread
id is threadid, its process id is processid and the thread priority is
priority.

Action No action required.

HHCTT003I
---------

HHCTT003I Timer thread ended

Explanation The thread for timing functions has ended.

Action No action required.

78. HHCTUnnns - TUN / TAP Driver Support
-------------------------------------------------

HHCTUnnns
---------

Messages HHCTUnnns are not yet documented.

79. HHCVMnnns - VM / CP Emulation
------------------------------------------

HHCVM001I
---------

HHCVM001I *panel_command* panel command Module guest

Explanation The guest operating system has issued a DIAGNOSE 8
instruction to perform the panel_command panel command to be carried out
by the Hercules panel command processor

System Action The Hercules panel command processor carries out the
command if possible.

Operator Action None. This is an informational message.

Programmer Action No action is requested if this behaviour is expected.
If this behaviour poses a security concern, the DIAG8CMD configuration
statement should either be ommited or specified with the disabled
argument.

HHCVM002I
---------

HHCVM002I \*panel_command command complete

Explanation The panel_commandpanel command has been carried out by the
panel command processor. Note that this message only appears if the
guest issued diagnose 8 instruction specified that it did not request
the command response to be placed in a supplied buffer.

System Action The system continues

Operator Action None. This is an informational message

Programmer Action None. This is an informational message

HHCVM003I
---------

HHCVM003I Host command processing disabled by configuration statement

Explanation The guest operating system attempted using the DIAGNOSE 8
Instruction to carry out a panel command, but the system configuration
disabled this feature (with the DIAG8CMD configuration statement)

System Action The panel command is ignored.

Operator Action None. This is an informational message.

Programmer Action If it is deemed necessary for the guest operating
system to issue DIAGNOSE 8 commands to issue panel commands, the
DIAG8CMD with the enable argument should be specified in the
configuration file.

HHCVM004E
---------

HHCVM004E Host command processing not included in engine build

Explanation The Hercules engine has been built without Diagnose 8 panel
command facility support

System Action The panel command is not issued. The system continues.

Operator Action None.

Programmer Action If it is desired that DIAGNOSE 8 Instruction be
carried out as panel commands, the facility should be included in the
build process. Additionally, the DIAG8CMD configuration statement should
be specified with the enable parameter.

Appendix A. Message Index (New → Old)
-------------------------------------

The following list shows each Hercules message ID in the new message
format followed by the related message ID in the old message format.
There are five possible cases for the index entries.

A.1 Replacement
---------~~~~~~

This is the normal case, where a new message ID replaces exactly one old
message ID.

Example: HHC01303I – HHCCP064I The new message “HHC01303I” replaces the
old message “HHCCP064I”.

A.2 New message
---------~~~~~~

New messages, that have not existed before, have no related old message
ID.

Example: HHC00069I – none Message “HHC00069I” is a new message that did
not exist before.

A3. Removed message
------------------~

Old messages that have been deleted do not have a relaed new message ID.

Example: None – HHCPR019E Message “HHCPR019E” is an old message that has
been deleted and therefore has no new message ID.

A.4 Consolidation
---------~~~~~~~~

There are cases where one new message ID replaces several old message
IDs. This can happen, if there have been several old messages that had
the same or a similar message text, but different message IDs. These
messages have now been consolidated under one new message ID.

Example: HHC02209E – HHCPN017E HHC02209E – HHCPN024E HHC02209E –
HHCPN034E The old messages “HHCPN017E”, “HHCPN024E” and “HHCPN034E” have
been consolidated and replaced through the new message “HHC02209E”.

A.5 Split
---------

In some rare cases an old message has been split into two or more new
messages.

Example: HHC02235E – HHCPN053E HHC02236E – HHCPN053E The old message
with ID “HHCPN053E” has been split into two new messages with IDs
“HHC02235E” and “HHC02236E”.

A.5 Message Index (New → Old)
---------------------------~~

::

   HHC00001I - none
   HHC00002E – HHCCP036E
   HHC00002E – HHCCP037E
   HHC00002E – HHCCP081E
   HHC00003E – HHCCP038E
   HHC00004I – HHC770I
   HHC00004I – HHC771I
   HHC00004I – HHC772I
   HHC00004I – HHC773I
   HHC00004I – HHC774I
   HHC00004I – HHCCP040I
   HHC00005W – HHCCP909W
   HHC00006I – HHCCP041I
   HHC00006I – HHCCP042I
   HHC00007I – none
   HHC00008I – none
   HHC00009I – none
   HHC00010A – HHC1C001A
   HHC00011E – HHCCH001E
   HHC00011E – HHCCH002W
   HHC00011E – HHCCH003W
   HHC00011E – HHCCH004W
   HHC00011E – HHCCH006E
   HHC00012W – HHCCH005W
   HHC00013I – none
   HHC00014E – none
   HHC00015E – none
   HHC00016E - none
   HHC00017I – none
   HHC00018I – none
   HHC00018W - none
   HHC00069I – none
   HHC00070E – HHCAO007E
   HHC00071E – HHCAO010E
   HHC00071E – HHCAO017E
   HHC00072E – HHCAO011E
   HHC00072E – HHCAO017E
   HHC00073E – HHCAO012E
   HHC00073E – HHCAO018E
   HHC00074E – HHCAO013E
   HHC00075E – HHCAO014E
   HHC00075E - HHCAO015E
   HHC00075E – HHCAO015E
   HHC00075E - HHCMS001E
   HHC00076E – HHCAO021E
   HHC00077I – HHCAO016I
   HHC00078E – HHCAO026E
   HHC00079E – HHCAO008E
   HHC00080I – HHCAO022I
   HHC00081I – HHCAO003I
   HHC00082I – none
   HHC00083E – HHCAO023E
   HHC00084E – HHCAO009E
   HHC00084E – HHCAO009E
   HHC00085E – HHCAO024E
   HHC00086I – HHCAO025I
   HHC00087I – HHCAO005I
   HHC00088I – HHCAO005I
   HHC00089I – HHCAO006I
   *********************
   HHC00100I – HHCAO001I
   HHC00100I – HHCCA002I
   HHC00100I - HHCCD001I
   HHC00100I - HHCCD002I
   HHC00100I - HHCCD003I
   HHC00100I – HHCCF065I
   HHC00100I – HHCCP002I
   HHC00100I – HHCCT002I
   HHC00100I – HHCHT001I
   HHC00100I - HHCPN001I
   HHC00100I - HHCSD020I
   HHC00100I – HHCSH045I
   HHC00100I – HHCSH049I
   HHC00100I - HHCTE001I
   HHC00101I – HHCAO002I
   HHC00101I – HHCCA009I
   HHC00101I – HHCCA009I
   HHC00101I - HHCCD011I
   HHC00101I - HHCCD012I
   HHC00101I - HHCCD013I
   HHC00101I - HHCCP008I
   HHC00101I – HHCCT003I
   HHC00101I – HHCHT009I
   HHC00101I - HHCSD022I
   HHC00101I – HHCSH048I
   HHC00101I - HHCTE004I
   HHC00102E – HHCAO004S
   HHC00102E – HHCAO007E
   HHC00102E – HHCCA022E
   HHC00102E – HHCCF040E
   HHC00102E – HHCCP067E
   HHC00102E – HHCCP006S
   HHC00102E – HHCCP068E
   HHC00102E – HHCHT010E
   HHC00102E - HHCIN004S
   HHC00102E - HHCIN006S
   HHC00102E - HHCIN007S
   HHC00102E - HHCPR015E
   HHC00102E - HHCSD023E
   HHC00102E - HHCSH061E
   HHC00102E - HHCSR133E
   HHC00102E - HHCTA323I
   HHC00102E - HHCTE005E
   HHC00102E - HHCVM010E
   HHC00102S - HHCCP006S
   HHC00102S – HHCIN005S
   HHC00103I - none
   HHC00105E - none
   HHC00130W – HHCCF079W
   HHC00131A – none
   HHC00135E – HHCTU001E
   HHC00136E – HHCTU001E
   HHC00136E – HHCTU025E
   HHC00136E – HHCTU026E
   HHC00136E – HHCTU027E
   HHC00136E – HHCCF064W
   HHC00136E – HHCCP001W
   HHC00136E – HHCCT001W
   HHC00137E – HHCTU002E
   HHC00138E – HHCTU003E
   HHC00139E – HHCTU004E
   HHC00140E – HHCTU005E
   HHC00140E – HHCTU007E
   HHC00140E – HHCTU009E
   HHC00140E – HHCTU011E
   HHC00140E – HHCTU014E
   HHC00140E – HHCTU016E
   HHC00140E – HHCTU017E
   HHC00140E – HHCTU021E
   HHC00141E – HHCTU006E
   HHC00142E – HHCTU008E
   HHC00142E – HHCTU018E
   HHC00142E – HHCTU022E
   HHC00143E – HHCTU010E
   HHC00143E – HHCTU019E
   HHC00143E – HHCTU023E
   HHC00144E – HHCTU012E
   HHC00144E – HHCTU013E
   HHC00145E – HHCTU015E
   HHC00146E – HHCTU020E
   HHC00146E – HHCTU024E
   HHC00147I – none
   HHC00148I – none
   HHC00149I – none
   HHC00150I – none
   HHC00151I – none
   HHC00152E – none
   HHC00153E – none
   HHC00154E – none
   HHC00160I – none
   HHC00161E – none
   *********************
   HHC00201I – HHCTA101I
   HHC00201I – HHCTA501I
   HHC00202E – HHCTA107E
   HHC00202E – HHCTA508E
   HHC00203E – HHCTA108E
   HHC00204E – HHCTA103E
   HHC00204E – HHCTA104E
   HHC00204E – HHCTA105E
   HHC00204E – HHCTA106E
   HHC00204E – HHCTA109E
   HHC00204E – HHCTA110E
   HHC00204E – HHCTA111E
   HHC00204E – HHCTA112E
   HHC00204E – HHCTA113E
   HHC00204E – HHCTA114E
   HHC00204E – HHCTA115E
   HHC00204E – HHCTA116E
   HHC00204E – HHCTA117E
   HHC00204E – HHCTA118E
   HHC00204E – HHCTA119E
   HHC00204E – HHCTA252E
   HHC00204E – HHCTA253E
   HHC00204E – HHCTA254E
   HHC00204E – HHCTA255E
   HHC00204E – HHCTA256E
   HHC00204E – HHCTA257E
   HHC00204E – HHCTA258E
   HHC00204E – HHCTA259E
   HHC00204E – HHCTA260E
   HHC00204E – HHCTA261E
   HHC00204E – HHCTA262E
   HHC00204E – HHCTA263E
   HHC00204E - HHCTA414E
   HHC00204E - HHCTA415E
   HHC00204E - HHCTA416E
   HHC00204E – HHCTA417E
   HHC00204E – HHCTA418E
   HHC00204E – HHCTA419E
   HHC00204E – HHCTA420E
   HHC00204E – HHCTA421E
   HHC00204E – HHCTA503E
   HHC00204E – HHCTA504E
   HHC00204E – HHCTA506E
   HHC00204E – HHCTA507E
   HHC00204E – HHCTA510E
   HHC00204E – HHCTA511E
   HHC00204E – HHCTA512E
   HHC00204E – HHCTA513E
   HHC00204E – HHCTA514E
   HHC00204E – HHCTA515E
   HHC00204E – HHCTA516E
   HHC00204E – HHCTA517E
   HHC00204E – HHCTA518E
   HHC00204E – HHCTA519E
   HHC00204E – HHCTA520E
   HHC00204E – HHCTA521E
   HHC00205E - HHCTA001E
   HHC00205E - HHCTA002E
   HHC00205E - HHCTA090E
   HHC00205E - HHCTA092E
   HHC00205E – HHCTA102E
   HHC00205E – HHCTA120E
   HHC00205E - HHCTA239E
   HHC00205E - HHCTA240E
   HHC00205E - HHCTA241E
   HHC00205E - HHCTA242E
   HHC00205E - HHCTA244E
   HHC00205E - HHCTA250E
   HHC00205E - HHCTA251E
   HHC00205E - HHCTA264E
   HHC00205E - HHCTA265E
   HHC00205E - HHCTA324E
   HHC00205E - HHCTA330E
   HHC00205E - HHCTA332E
   HHC00205E - HHCTA333E
   HHC00205E - HHCTA334E
   HHC00205E - HHCTA335E
   HHC00205E - HHCTA336E
   HHC00205E - HHCTA337E
   HHC00205E - HHCTA338E
   HHC00205E - HHCTA373E
   HHC00205E - HHCTA373W
   HHC00205E - HHCTA376E
   HHC00205E - HHCTA380E
   HHC00205E - HHCTA381E
   HHC00205E - HHCTA382E
   HHC00205E - HHCTA383E
   HHC00205E - HHCTA389E
   HHC00205E - HHCTA401E
   HHC00205E - HHCTA402E
   HHC00205E – HHCTA488E
   HHC00205E - HHCTA502E
   HHC00205E - HHCTA521E
   HHC00206E – HHCTA243E
   HHC00207E – HHCTA245E
   HHC00207E – HHCTA246E
   HHC00207E – HHCTA247E
   HHC00207E – HHCTA248E
   HHC00207E – HHCTA249E
   HHC00208I – HHCTA430I
   HHC00209I – HHCTA431I
   HHC00210I – HHCTA377I
   HHC00211I – none
   HHC00212E – HHCTA072E
   HHC00213E - HHCTA324E
   HHC00214E – HHCTA091E
   HHC00215I – HHCTA094I
   HHC00216I – HHCTA093I
   HHC00217I – HHCTA081I
   HHC00218I – HHCTA099I
   HHC00219I – HHCTA099I
   HHC00220W – HHCTA003W
   HHC00221I – HHCTA004I
   HHC00222I – HHCTA066I
   HHC00223E – HHCTA067E
   HHC00223E – HHCTA068E
   HHC00223E – HHCTA069E
   HHC00223E – HHCTA070E
   HHC00223E – HHCTA071E
   HHC00223E – HHCTA078E
   HHC00224I – HHCTA010I
   HHC00225E – none
   HHC00226I – none
   HHC00227I – none
   HHC00228I – none
   HHC00229I – none
   HHC00235I – none
   HHC00243W – none
   *********************
   HHC00300E – HHCCD101E
   HHC00301E – HHCCD130E
   HHC00302E – HHCCD130E
   HHC00303E – HHCCD130E
   HHC00304E – HHCCD102E
   HHC00305E – HHCCD110E
   HHC00306E – HHCCD121E
   HHC00307E – HHCCD122E
   HHC00308E – HHCCD123E
   HHC00309E – HHCCD124E
   HHC00310E – HHCCD125E
   HHC00311E – HHCCD142E
   HHC00312E – HHCCD151E
   HHC00313E – HHCCD161E
   HHC00314E – HHCCD161E
   HHC00315I – HHCCD207I
   HHC00316I – HHCCD092I
   HHC00317E – HHCCD160E
   HHC00317E – HHCCD170E
   HHC00317E – HHCCD205W
   HHC00317E – HHCCD209W
   HHC00318W – HHCCD165W
   HHC00319E – HHCCD161E
   HHC00320I – HHCCD162I
   HHC00321I – HHCCD179I
   HHC00322W – HHCCD175W
   HHC00323E – HHCCD171E
   HHC00324E – HHCCD172E
   HHC00324E – HHCCD173E
   HHC00324E – HHCCD174E
   HHC00325I – HHCCD181I
   HHC00326E – HHCCD180E
   HHC00327E – HHCCD180E
   HHC00328I – HHCCD207I
   HHC00329W – HHCCD206W
   HHC00330I – HHCCD207I
   HHC00331W – HHCCD206W
   HHC00332I – HHCCD208I
   HHC00333I – HHCCD210I
   HHC00334I – HHCCD211I
   HHC00335I – HHCCD212I
   HHC00336I – HHCCD213I
   HHC00337I – HHCCD214I
   HHC00338I – HHCCD215I
   HHC00339I – HHCCD216I
   HHC00340I – HHCCD217I
   HHC00341I – HHCCD218I
   HHC00342E – HHCCD190E
   HHC00343E – HHCCD193E
   HHC00344E – HHCCD194E
   HHC00345I – none
   HHC00346I – none
   HHC00347I – none
   HHC00348E – none
   HHC00349E – none
   HHC00352E – none
   HHC00353E – none
   HHC00354E – none
   HHC00355E – none
   HHC00356E – none
   HHC00357I – none
   HHC00358I – none
   HHC00359I – none
   HHC00360I – none
   HHC00361E – none
   HHC00362E – none
   HHC00363W – none
   HHC00364W – none
   HHC00365W – none
   HHC00366W – none
   HHC00367W – none
   HHC00368W – none
   HHC00369W – none
   HHC00370W – none
   HHC00371W – none
   HHC00372I – none
   HHC00373I – none
   HHC00374E – none
   HHC00375W – none
   HHC00376W – none
   HHC00377I – none
   HHC00378E – none
   HHC00396I – none
   HHC00397I – none
   HHC00398I – none
   HHC00399I – HHCCD900I
   *********************
   HHC00400E – HHCDA001E
   HHC00401E – HHCDA002E
   HHC00402E – HHCDA003E
   HHC00403I – HHCDA004I
   HHC00404E – HHCDA005E
   HHC00404E – HHCDA007E
   HHC00404E – HHCDA008E
   HHC00404E – HHCDA009E
   HHC00404E – HHCDA012E
   HHC00404E – HHCDA013E
   HHC00404E – HHCDA026E
   HHC00404E – HHCDA027E
   HHC00404E – HHCDA032E
   HHC00404E – HHCDA033E
   HHC00405E – HHCDA006E
   HHC00406E – HHCDA010E
   HHC00407E – HHCDA011E
   HHC00408E – HHCDA014E
   HHC00409I – HHCDA015I
   HHC00410E – HHCDA016E
   HHC00411E – HHCDA017E
   HHC00412E – HHCDA018E
   HHC00413E – HHCDA019E
   HHC00414I – HHCDA020I
   HHC00415E – HHCDA021E
   HHC00416E – HHCDA022E
   HHC00417I – HHCDA023I
   HHC00418E – HHCDA035E
   HHC00419E – HHCDA042E
   HHC00419E – HHCDA046E
   HHC00420E – HHCDA049E
   HHC00421E – HHCDA051E
   HHC00422E – HHCDA053E
   HHC00423I – HHCDA055I
   HHC00424I – none
   HHC00425I – none
   HHC00426I – none
   HHC00427I – none
   HHC00428I – none
   HHC00429I – none
   HHC00430I – none
   HHC00431I – none
   HHC00432E – none
   HHC00433I – none
   HHC00434I – none
   HHC00435I – none
   HHC00436I – none
   HHC00437I – none
   HHC00438I – none
   HHC00439I – none
   HHC00440I – none
   HHC00441I – none
   HHC00442I – none
   HHC00443E – HHCDA999E
   HHC00445I – none
   HHC00446E – none
   HHC00447I – none
   HHC00448E – none
   HHC00449I – none
   HHC00450E – none
   HHC00451E – none
   HHC00452E – none
   HHC00453I – none
   HHC00454I – none
   HHC00455E – none
   HHC00456I – none
   HHC00457I – none
   HHC00458E – none
   HHC00459I – none
   HHC00460I – none
   HHC00461E – none
   HHC00462I – none
   HHC00463I – none
   HHC00464E – none
   HHC00465I – none
   HHC00466I – none
   HHC00467I – none
   HHC00468I – none
   *********************
   HHC00500E – HHCDA056E
   HHC00501E – HHCDA057E
   HHC00502E – HHCDA058E
   HHC00502E – HHCDA059E
   HHC00502E – HHCDA060E
   HHC00502E – HHCDA061E
   HHC00502E – HHCDA062E
   HHC00502E – HHCDA064E
   HHC00502E – HHCDA069E
   HHC00502E – HHCDA070E
   HHC00502E – HHCDA075E
   HHC00502E – HHCDA076E
   HHC00502E – HHCDA082E
   HHC00503E – HHCDA063E
   HHC00504I – none
   HHC00505E – HHCDA065E
   HHC00506E – HHCDA066E
   HHC00507I – HHCDA067I
   HHC00508E – HHCDA068E
   HHC00509E – HHCDA078E
   HHC00510E – HHCDA079E
   HHC00511E – HHCDA080E
   HHC00512E – HHCDA081E
   HHC00513E – HHCDA901E
   HHC00514E – HHCDA902E
   HHC00515E – HHCDA903E
   HHC00516I – none
   HHC00517I – none
   HHC00518I – none
   HHC00519I – none
   HHC00520I – none
   HHC00521I – none
   *********************
   HHC00600E – HHCSC002E
   HHC00600E – HHCSC011E
   HHC00600E – HHCSC012E
   HHC00600E – HHCSC031E
   HHC00600E – HHCSC041E
   HHC00600E – HHCSC051E
   HHC00601E – HHCSC001E
   HHC00602E – HHCSC003E
   HHC00603W – HHCSC032W
   HHC00604E – HHCSC101E
   HHC00605E – HHCSC201E
   HHC00605E - HHCSC202I
   *********************
   HHC00700S – HHCSH001S
   HHC00700S – HHCSH010S
   HHC00701W – HHCSH002W
   HHC00701W – HHCSH011I
   HHC00702S – HHCSH003S
   HHC00703S – HHCSH004S
   HHC00703S – HHCSH017S
   HHC00704S – HHCSH005S
   HHC00704S – HHCSH016S
   HHC00705S – HHCSH006S
   HHC00705S – HHCSH015S
   HHC00706S – HHCSH007S
   HHC00706S – HHCSH018S
   HHC00707S – HHCSH008S
   HHC00708I – HHCSH009I
   HHC00709S – HHCSH012S
   HHC00710S – HHCSH013S
   HHC00711S – HHCSH014S
   HHC00712I – HHCSH019I
   HHC00713E – HHCSH020E
   HHC00714E – HHCSH021E
   HHC00715E – HHCSH022E
   HHC00715E - HHCSH023E
   HHC00716E – HHCSH024E
   HHC00716E – HHCSH025E
   HHC00717E – HHCSH026E
   HHC00718E – HHCSH027E
   HHC00719E – HHCSH028E
   HHC00720E – HHCSH029E
   HHC00720E – HHCSH030E
   HHC00721I – HHCSH031E
   HHC00722E – HHCSH032E
   HHC00723E – HHCSH033E
   HHC00724E – HHCSH034E
   HHC00725E – HHCSH035E
   HHC00726E – HHCSH036E
   HHC00727E – HHCSH037E
   HHC00727E – HHCSH039E
   HHC00728E – HHCSH038E
   HHC00728E – HHCSH040E
   HHC00729E – HHCSH041E
   HHC00730W – HHCSH042W
   HHC00731I – HHCSH043I
   HHC00732E – HHCSH0474
   HHC00733I – HHCSH053I
   HHC00734E – HHCSH047E
   HHC00735E – HHCSH046E
   HHC00735E – HHCSH050E
   HHC00735E – HHCSH053E
   HHC00735E – HHCSH055E
   HHC00735E – HHCSH058E
   HHC00735E – HHCSH059E
   HHC00735E – HHCSH060E
   HHC00735E – HHCSH065E
   HHC00735E – HHCSH051W
   HHC00735E – HHCSH054W
   HHC00735E – HHCSH056W
   HHC00736W – HHCSH052W
   HHC00737I – HHCSH057I
   HHC00738E – HHCSH062E
   HHC00739E – HHCSH063E
   HHC00740E – HHCSH064E
   HHC00741E – HHCSH066E
   HHC00742E – HHCSH999E
   HHC00743I – none
   *********************
   HHC00800I – HHCCP043I
   HHC00801I – HHCCP014I
   HHC00802I – HHCCP015I
   HHC00803I – HHCCP016I
   HHC00804I – HHCCP044I
   HHC00805I – HHCCP045I
   HHC00806I – HHCCP046I
   HHC00807I – HHCCP022I
   HHC00808I – HHCCP010I
   HHC00809I – HHCCP011I
   HHC00810E - none
   HHC00811I – HHCCP003I
   HHC00811I – HHCCP007I
   HHC00812I – HHCCP004I
   HHC00813E – HHCCP079E
   HHC00813E – HHCCP080E
   HHC00814I – none
   HHC00815I – HHCPN123I
   HHC00816W – HHCPN160W
   HHC00817I – HHCPN010I
   HHC00818E – HHCPN052E
   HHC00819I – HHCPN152I
   HHC00819I – HHCPN154I
   HHC00820I – HHCPN123I
   HHC00820I – HHCPN153I
   HHC00820I – HHCPN155I
   HHC00821I – none
   HHC00822I – HHCCP017I
   HHC00823I – HHCCP018I
   HHC00824I – HHCCP019I
   HHC00825E – HHCCP020E
   HHC00826E – HHCCP021E
   HHC00827I – HHCCF077I
   HHC00828E – HHCCP027E
   HHC00828E - HHCCP030E
   HHC00832I - none
   HHC00834I - none
   HHC00838I – none
   HHC00839E - none
   HHC00840I – HHCCP023I
   HHC00841I – HHCCP024I
   HHC00842I – HHCCP025I
   HHC00843I – HHCCP026I
   HHC00844I – HHCCP031I
   HHC00845I – HHCCP028I
   HHC00846I – HHCCP027I
   HHC00850I – none
   HHC00851I – none
   HHC00852I – none
   HHC00853I – none
   HHC00854I – none
   HHC00855I – none
   HHC00856I – none
   HHC00857I – none
   HHC00858I – none
   HHC00859I – none
   HHC00860I – none
   HHC00861I – none
   HHC00862I – none
   HHC00863I – none
   HHC00864I – none
   HHC00865I – none
   HHC00866I – none
   HHC00867I – none
   HHC00868I – none
   HHC00869I – none
   HHC00870I – none
   HHC00871I – none
   HHC00872I – none
   HHC00873I – none
   HHC00874I – none
   HHC00875I – none
   HHC00876I – none
   HHC00877I – none
   HHC00880I – none
   HHC00881I – none
   HHC00882I – none
   HHC00890I – none
   HHC00891E – none
   HHC00892E – none
   HHC00893E – none
   HHC00895E – none
   HHC00896E – none
   HHC00898I – none
   *********************
   HHC00900E – HHCCT007E
   HHC00900E – HHCCT008E
   HHC00900E – HHCCT010E
   HHC00900E – HHCCT011E
   HHC00900E – HHCCT012E
   HHC00900E – HHCCT025E
   HHC00900E – HHCCT026E
   HHC00900E – HHCCT027E
   HHC00900E – HHCCT033E
   HHC00900E – HHCCT037E
   HHC00900E – HHCCT038E
   HHC00900E – HHCLC001E
   HHC00901I – HHCLC073I
   HHC00901I – HHCCT073I
   HHC00902W – HHCCT074W
   HHC00902W – HHCCT075W
   HHC00902W – HHCLC074W
   HHC00902W – HHCLC075W
   HHC00904I – HHCCT040I
   HHC00904I – HHCLC002I
   HHC00905I – HHCCT041E
   HHC00906E – HHCCT014E
   HHC00906E – HHCCT042E

   HHC00907I – HHCCT015I

   HHC00907I – HHCCT043I

   HHC00908E – HHCCT016E

   HHC00908E – HHCCT044E

   HHC00909E – HHCCT017E

   HHC00909E – HHCCT045E

   HHC00910I – HHCCT046E

   HHC00911E – HHCCT047E

   HHC00912E – HHCCT048E

   HHC00913I – HHCCT022I

   HHC00913I – HHCCT049I

   HHC00914W – HHCCT072W

   HHC00915E – HHCCT001E

   HHC00915E – HHCCT002E

   HHC00915E – HHCCT024E

   HHC00915E – HHCCT056E

   HHC00915E – HHCCT057E

   HHC00915E – HHCCT060E

   HHC00915E – HHCCT066E

   HHC00915E – HHCCT071E

   HHC00915E – HHCLC019E

   HHC00915E – HHCLC027E

   HHC00916E – HHCCT003E

   HHC00916E – HHCCT004E

   HHC00916E – HHCCT005E

   HHC00916E – HHCCT006E

   HHC00916E – HHCCT028E

   HHC00916E – HHCCT050E

   HHC00916E – HHCCT051E

   HHC00916E – HHCCT052E

   HHC00916E – HHCCT053E

   HHC00916E – HHCCT054E

   HHC00916E – HHCCT055E

   HHC00916E – HHCCT056E

   HHC00916E – HHCCT058E

   HHC00916E – HHCCT059E

   HHC00916E – HHCCT061E

   HHC00916E – HHCCT062E

   HHC00916E – HHCCT063E

   HHC00916E – HHCCT064E

   HHC00916E – HHCCT065E

   HHC00916E – HHCCT067E

   HHC00916E – HHCCT068E

   HHC00916E – HHCCT069E

   HHC00916E – HHCCT070E

   HHC00916E – HHCLC017E

   HHC00916E – HHCLC018E

   HHC00916E – HHCLC020E

   HHC00916E – HHCLC052E

   HHC00916E – HHCLC053E
   HHC00918E – none
   HHC00920E – HHCLC040E
   HHC00921I – HHCLC003I
   HHC00922I – HHCLC051I
   HHC00933I – HHCLC043I
   HHC00933I – HHCLC044I
   HHC00933I – HHCLC045I
   HHC00933I – HHCLC046I
   HHC00933I – HHCLC047I
   HHC00933I – HHCLC048I

   HHC00934I – HHCCT018I

   HHC00934I – HHCLC004I

   HHC00936E – HHCCT019E

   HHC00936E – HHCLC005E

   HHC00937E – HHCLC050E

   HHC00938I – HHCLC006I

   HHC00939W – HHCLC049W

   HHC00939W – HHCLC054W

   HHC00940E – HHCLC007E

   HHC00940E – HHCLC039E

   HHC00941E – HHCLC008E

   HHC00942I – HHCLC055I

   HHC00943W – HHCLC056W

   HHC00944E – HHCLC042E

   HHC00945I – HHCLC009I

   HHC00946I – HHCLC010I

   HHC00947I – HHCLC011I

   HHC00948I – none
   HHC00949I – HHCLC012I
   HHC00950I – HHCLC013I
   HHC00950I – HHCLC014I
   HHC00951I – HHCLC015I
   HHC00952I – HHCLC016I
   HHC00953W – HHCLC041W
   HHC00954E – HHCLC021E
   HHC00954E – HHCLC023E
   HHC00955E – none
   HHC00956E – none
   HHC00957E – HHCLC027E
   HHC00957E – HHCLC029E
   HHC00957E – HHCLC032E
   HHC00957E – HHCLC034E
   HHC00958E – HHCLC028E
   HHC00958E – HHCLC033E
   HHC00959E – HHCLC031E
   HHC00960E – HHCLC035E
   HHC00961E – HHCLC036E
   HHC00962E – HHCLC037E

   HHC00963E – HHCLC038E

   HHC00964I – none
   HHC00970E – HHCCT034E
   HHC00971I – HHCCT009I
   HHC00972I – HHCCT013I
   HHC00973E – HHCCT020E
   HHC00973E – HHCCT021E
   HHC00974E – HHCCT023E
   HHC00975E – HHCCT029E
   HHC00975E – HHCCT030E
   HHC00975E – HHCCT031E
   HHC00976E – HHCCT032E

   *********************

   HHC01000E – HHCCA006T

   HHC01000E – HHCCA018E

   HHC01000E – HHCCA020E

   HHC01000E – HHCSD002E

   HHC01000E – HHCSD003E

   HHC01000E – HHCSD017E

   HHC01000E - HHCTE019E

   HHC01000E - HHCTE090E

   HHC01001I – HHCCA001I

   HHC01002E – HHCCA003E

   HHC01003W – HHCCA004W

   HHC01004I – HHCCA005I

   HHC01005W – HHCCA007W

   HHC01006I – HHCCA008I

   HHC01007E – HHCCA013E

   HHC01007E – HHCTE010E

   HHC01007E – HHCTE011E

   HHC01007E – HHCTE012E

   HHC01008E – HHCCA015E

   HHC01009W – HHCCA016W

   HHC01010I – HHCCA017I

   HHC01011I – HHCCA010I

   HHC01012E – HHCCA011E

   HHC01012E – HHCCA012E

   HHC01013E – HHCCA014E

   HHC01014I – HHCCA021I

   HHC01015E – HHCCA019E

   HHC01016I – HHCGI001I

   HHC01016I - HHCGI002I

   HHC01017E – HHCGI003E

   HHC01017E – HHCTE010E

   HHC01018I – HHCTE009I

   HHC01019E – HHCCA012E

   HHC01019E – HHCTE013E

   HHC01020E – none
   HHC01022I – HHCTE007I
   HHC01022I – HHCTE008I
   HHC01023W – HHCTE002W
   HHC01024I – HHCTE003I
   HHC01025E – HHCTE017E
   HHC01026A – none
   HHC01027I – none
   HHC01028E – none
   HHC01029E – none
   HHC01030I – none
   HHC01031I – none
   HHC01032E – HHCSD024E
   HHC01033E – HHCSD008E
   HHC01034E – HHCSD009E
   HHC01034E - HHCSD010E
   HHC01034E - HHCSD013E
   HHC01034E - HHCSD014E
   HHC01034E - HHCSD021E
   HHC01035E – HHCSD011E
   HHC01036E – HHCSD012E
   HHC01037E – HHCSD015E
   HHC01038E – HHCSD016E
   HHC01039E – HHCSD026E
   HHC01040I – HHCSD018I
   HHC01041E – HHCSD001E
   HHC01042I – HHCSD004I
   HHC01043E – HHCSD005E
   HHC01044I – HHCSD025I
   HHC01045E – HHCSD006E
   HHC01046I – HHCSD007I
   HHC01047I – none
   HHC01048D – HHCCA300D
   HHC01049D – HHCCA300D
   HHC01050D – HHCCA300D
   HHC01051D – HHCCA300D
   HHC01052D – HHCCA300D
   HHC01053D – HHCCA300D
   HHC01054D – HHCCA300D
   HHC01055D – HHCCA300D
   HHC01056D – HHCCA300D
   HHC01057D – HHCCA300D
   HHC01058D – HHCCA300D
   HHC01059D – HHCCA300D
   HHC01060D – HHCCA300D
   HHC01061D – HHCCA300D
   HHC01062D – HHCCA300D
   HHC01063D – HHCCA300D
   HHC01064D – HHCCA300D
   HHC01065D – HHCCA300D
   HHC01066D – HHCCA300D
   HHC01067D – HHCCA300D
   HHC01068D – HHCCA300D
   HHC01069D – HHCCA300D
   HHC01070D – HHCCA300D
   HHC01071D – HHCCA300D
   HHC01072D – HHCCA300D
   HHC01073I – none
   HHC01074D – HHCCA300D
   HHC01075D – HHCCA300D
   HHC01076D – HHCCA300D
   HHC01077D – HHCCA300D
   HHC01078D – HHCCA300D
   HHC01079D – HHCCA300D
   HHC01080D – HHCCA300D
   HHC01081D – HHC CA300D
   HHC01082D – HHCCA300D
   HHC01083D – HHCCA300D

   HHC01084D – HHCCA300D

   HHC01090I – HHCTE014I

   HHC01091E – none

   *********************

   HHC01100I – HHCPR016I

   HHC01100I – HHCPR017I

   HHC01100I – HHCPR018I

   HHC01101E – none
   HHC01102E – none
   HHC01103E – none
   HHC01104E – none
   HHC01105E – HHCPR003E
   HHC01105E – HHCPR004E
   HHC01105E – HHCPR005E
   HHC01105E – HHCPR006E
   HHC01105E – HHCPR008E
   HHC01106I – HHCPR007I
   HHC01107I – HHCPR011I
   HHC01108E – HHCPR012E

   *********************

   HHC01200E – HHCPU003E

   HHC01200E – HHCPU004E

   HHC01200E – HHCRD001E

   HHC01200E – HHCRD003E

   HHC01200E – HHCRD004E

   HHC01200E – HHCRD010E

   HHC01200E – HHCRD011E

   HHC01200E – HHCRD013E

   HHC01200E – HHCRD014E

   HHC01200E – HHCRD015E

   HHC01200E – HHCRD016E

   HHC01200E – HHCRD017E

   HHC01200E – HHCRD018E

   HHC01201E – HHCPU001E

   HHC01201E – HHCRD002E

   HHC01201E – HHCRD009E

   HHC01202E – HHCRD005E

   HHC01203E – HHCRD006E

   HHC01204I – HHCRD007I

   HHC01205W – HHCRD008W

   HHC01206I – HHCRD012I

   HHC01207E – HHCRD019E

   HHC01208E – none
   HHC01209E – HHCPU002E

   *********************

   HHC01300I – HHCCP057I

   HHC01300I – HHCCP058I

   HHC01300I – HHCCP059I

   HHC01300I – HHCCP062I

   HHC01301I – HHCCP078I

   HHC01302I – HHCCP063I

   HHC01303I – HHCCP064I

   HHC01304I – HHCCP065I

   HHC01305I – HHCCP066I

   HHC01306I – HHCCP069I

   HHC01307I – HHCCP070I

   HHC01308I – HHCCP071I

   HHC01309I – HHCCP072I

   HHC01310I – HHCCP073I

   HHC01311I – HHCCP074I

   HHC01312I – HHCCP075I

   HHC01313I – HHCCP076I

   HHC01314I – HHCCP077I

   HHC01315I – HHCCP048I

   HHC01316I – HHCCP049I

   HHC01317I – HHCCP050I

   HHC01318I – HHCCP051I

   HHC01319I – HHCCP052I

   HHC01329I – HHCCP053I

   HHC01330I – HHCCP054I

   HHC01330I – HHCCP055I

   HHC01332I – HHCCP056I

   HHC01333I – HHCCP060I

   HHC01333I – HHCCP061I

   HHC01334I – none
   HHC01335I – none
   HHC01350E – HHCGC003E
   HHC01351E – HHCGC001E
   HHC01352T – HHCGC002T
   HHC01353W – HHCGC999W

   *********************

   HHC01400I – none
   HHC01401I – none
   HHC01402I – none
   HHC01403W – none
   HHC01404S – none
   HHC01405E – HHCPN995E
   HHC01406W – none
   HHC01407S – none
   HHC01408S – none
   HHC01409S – none
   HHC01410S – HHCIN001S
   HHC01410S - HHCIN003S
   HHC01411E – HHCIN002E
   HHC01412I – none
   HHC01413I – none
   HHC01414I – none
   HHC01415I – HHCPN142I
   HHC01416I – none
   HHC01417I – none
   HHC01418E - none
   HHC01419E - none
   HHC01420I – HHCIN900I
   HHC01422I – HHCIN902I
   HHC01423I – HHCIN903I
   HHC01424I – HHCIN904I
   HHC01425I – HHCIN909I
   HHC01426I – HHCIN998I
   HHC01427I – none

   HHC01430S – HHCCF031S

   HHC01430S – HHCCF032S

   HHC01430S – HHCCF033S

   HHC01430S – HHCCF900S

   HHC01431I – HHCCF034W

   HHC01432S – HHCCF001S

   HHC01432S - HHCCF003S

   HHC01433S – HHCCF002S

   HHC01435I – HHCCF081I

   HHC01436S – HHCCF082S

   HHC01437I – HHCCF083I

   HHC01438W – HHCCF084W

   HHC01439S – HHCCF085S

   HHC01441E – HHCCF008E

   HHC01443S – none
   HHC01443S – HHCCF012S
   HHC01443S – HHCCF013S
   HHC01443S – HHCCF014S
   HHC01443S – HHCCF016S
   HHC01443S – HHCCF018S
   HHC01443S – HHCCF019S
   HHC01443S – HHCCF022S
   HHC01443S – HHCCF023S
   HHC01443S – HHCCF029S
   HHC01443S – HHCCF036S
   HHC01443S – HHCCF051S
   HHC01443S – HHCCF070S
   HHC01443S – HHCCF074S
   HHC01443S – HHCCF075S
   HHC01447I – HHCCF090I
   HHC01448S – HHCCF035S
   HHC01451E – none
   HHC01452W - none
   HHC01453S - none
   HHC01454S – none
   HHC01455E – none
   HHC01456E – none
   HHC01457E - none
   HHC01458W – HHCCF078W

   HHC01459I – HHCCF050I

   HHC01460E – HHCCF043E

   HHC01460E – HHCCF045E

   HHC01461E – HHCCF041E

   HHC01461E – HHCCF049E

   HHC01462E – HHCCF042E

   HHC01463E – HHCCF044E

   HHC01464E – HHCCF046E

   HHC01464E – HHCCF048E

   HHC01465I – HHCCF047I

   HHC01466E – HHCCF074E

   HHC01467E – HHCCF075E

   HHC01468E – HHCCF076E

   HHC01469E – HHCCF077E

   HHC01470E – HHCCF053E

   HHC01470E – HHCCF054E

   HHC01470E – HHCCF055E

   HHC01471E – HHCCF056E

   HHC01472E – HHCCF057E

   HHC01473E – HHCCF058E

   HHC01474I – HHCCF072I

   HHC01475E – HHCCF051E


   HHC01476I – none
   HHC01477W – none
   HHC01478I – none
   HHC01479I – none
   HHC01480E – none
   HHC01481I – none
   HHC01482I – none
   HHC01483E – none
   HHC01484I – none
   HHC01485I – none
   HHC01486I – none
   HHC01487I – none
   HHC01488I – none
   HHC01489E – none
   HHC01490I – none
   HHC01491I – none
   HHC01492I – none

   HHC01493I – none

   *********************

   HHC01500I – HHCHD900I

   HHC01501I – HHCHD901I

   HHC01502I – HHCHD902I

   HHC01504I – HHCHD909I

   HHC01505E – HHCHD018I


   HHC01506W – none
   HHC01507W – none
   HHC01508I – HHCHD018I
   HHC01509I – HHCHD010I
   HHC01510I – HHCHD011I
   HHC01511S – HHCHD001E
   HHC01511S – HHCHD006S
   HHC01512I – HHCHD950I
   HHC01513I – HHCHD051I
   HHC01514I – HHCHD052I
   HHC01515I – HHCHD959I
   HHC01516E – HHCHD007E
   HHC01517E – HHCHD013E
   HHC01518E – HHCHD014E
   HHC01519E – HHCHD005E
   HHC01520E – HHCHD016E
   HHC01521E – HHCHD015E
   HHC01522E – HHCHD008E
   HHC01523E – HHCHD017E
   HHC01524E – HHCHD009E
   HHC01525E – none
   HHC01526I – HHCHD100I
   HHC01527I – HHCHD101I
   HHC01528I – HHCHD102I
   HHC01529I – HHCHD103I
   HHC01530E – none
   HHC01531I – none
   HHC01532I – none
   HHC01533I – none
   HHC01534I – none


   HHC01535I – none
   HHC01540I – none
   HHC01541I – HHCDG001I
   HHC01542I – HHCDG002I

   *********************

   HHC01600E – HHCPN139E

   HHC01602I – HHCPN140I

   HHC01603I – HHCPN140I

   HHC01604I – HHCPN142I

   HHC01605E – none
   HHC01606I – none
   HHC01607I – none
   HHC01608W - none
   HHC01609E – none
   HHC01610I – none

   *********************

   HHC01700W – HHCEV004W

   HHC01701I – HHCEV001I

   HHC01702I – HHCVE002I

   HHC01703I – HHCEV004I

   HHC01704I – HHCEV005I

   HHC01705I – HHCEV006I

   HHC01706I – none
   HHC01707I – HHCEV015I
   HHC01708I – HHCEV016I
   HHC01709I – HHCEV003I
   HHC01710I – HHCEV014I
   HHC01711I – HHCEV014I
   HHC01712I – HHCEV016I
   HHC01713I – HHCEV017I
   HHC01714I – HHCEV016I
   HHC01715W – HHCEV017W
   HHC01715W – HHCEV018W
   HHC01716I – HHCEV019I
   HHC01717I – HHCEV010I

   HHC01717I – HHCEV012I

   HHC01718E – HHCEV011E

   HHC01719I – HHCEV011I

   HHC01720E – HHCEV008E

   HHC01721E – HHCEV008E

   HHC01722I – HHCEV011I

   HHC01723W - none
   *********************
   HHC01800E – HHCHT002E
   HHC01800E – HHCHT004E
   HHC01800E – HHCHT005E
   HHC01800E – HHCHT007E
   HHC01800E – HHCHT008E
   HHC01800E – HHCHT011E
   HHC01801E – HHCCF066E
   HHC01801E – HHCHT013E
   HHC01802I – none
   HHC01803I – HHCHT006I
   HHC01804W – HHCHT003W
   HHC01805I – none
   HHC01806W – none
   HHC01807I – none
   HHC01808I – none
   HHC01809I – none
   HHC01810I – none
   HHC01811I – none
   HHC01812E – none
   HHC01813I – none
   HHC01814E – none
   HHC01815E – none
   *********************
   HHC01900I – HHCDN001I
   HHC01901I – HHCDN002I
   HHC01902I – HHCDN003I
   HHC01905I – HHCVM023I
   HHC01906I – HHCVM008I
   HHC01907I – HHCVM007I
   HHC01908E – HHCVM006E

   HHC01908E – HHCVM011E

   HHC01909I – HHCVM012I

   HHC01920I – HHCVM013I

   HHC01921I – HHCVM022I

   HHC01922I – HHCVM018I

   HHC01923I – HHCVM021I

   HHC01924I – HHCVM019I

   HHC01925I – HHCVM019I

   HHC01926I – HHCVM017I

   HHC01927I – HHCVM009E

   HHC01928I – HHCVM015I

   HHC01929I – HHCVM020I

   HHC01930I – HHCVM016I

   HHC01931I – HHCVM020I

   HHC01932I – HHCVM020I

   HHC01933I – HHCVM020I

   HHC01934I – HHCVM014I

   HHC01935I – HHCVM019I

   HHC01936I – HHCVM019I

   HHC01937I – HHCVM017I

   HHC01938E – HHCVM009E

   HHC01939I – HHCVM015I

   HHC01940I – HHCVM020I

   HHC01941I – HHCVM016I

   HHC01942I – HHCVM020I

   HHC01943I – HHCVM020I

   HHC01944I – HHCVM020I

   HHC01945I – HHCVM014I

   HHC01950I – HHCVM001I

   HHC01950I – HHCVM002I

   HHC01951W – HHCVM005W


   HHC01952I – none
   HHC01953E – HHCVM003I
   HHC01954E – HHCVM004E

   *********************

   HHC02000E – HHCSR101E

   HHC02001E – HHCSR010E

   HHC02001E – HHCSR011E

   HHC02001E – HHCSR012E

   HHC02001E – HHCSR102E

   HHC02002W – HHCSR103W

   HHC02003W – HHCSR104W

   HHC02004E – HHCSR015E

   HHC02005E – HHCSR103E

   HHC02006E – HHCSR104E

   HHC02007I – HHCSR001I

   HHC02008E – HHCSR105E

   HHC02009E – HHCSR106E

   HHC02009E – HHCSR107E

   HHC02009E – HHCSR108E

   HHC02009E – HHCSR109E

   HHC02009E – HHCSR110E

   HHC02009E – HHCSR111E

   HHC02010E – HHCSR113E

   HHC02011E – HHCSR114E

   HHC02012E – HHCSR115E

   HHC02013E – HHCSR116E

   HHC02014E – HHCSR117E

   HHC02015E – HHCSR118E

   HHC02016E – HHCSR132E

   HHC02016W – HHCSR119W

   HHC02017E – HHCSR120E

   HHC02017E – HHCSR121E

   HHC02017E – HHCSR122E

   HHC02017E – HHCSR123E

   HHC02017E – HHCSR124E

   HHC02017E – HHCSR125E

   HHC02017E – HHCSR126E

   HHC02017E – HHCSR127E

   HHC02017E – HHCSR128E

   HHC02017E – HHCSR129E

   HHC02017E – HHCSR130E

   HHC02017E – HHCSR131E

   HHC02017E – HHCSR134E

   HHC02018E – HHCSR999E

   HHC02019E – HHCSR016E

   HHC02020E – HHCSR001E

   HHC02020E – HHCSR013E

   HHC02021E – HHCSR014E

   *********************

   HHC02100E – HHCLG014E

   HHC02101I – HHCLG015I

   HHC02102E – HHCLG016E

   HHC02102E - HHCLG017S


   HHC02103I – none
   HHC02104I – none
   HHC02105I – none
   HHC02106I – HHCPN160E
   HHC02197E – none

   *********************

   HHC02200E – HHCPN181E

   HHC02201E – HHCPN031E

   HHC02201E – HHCPN054E

   HHC02201E – HHCPN057E

   HHC02201E – HHCPN058E

   HHC02202E – HHCPN062E

   HHC02202E – HHCPN093E

   HHC02202E – HHCPN099E

   HHC02202E – HHCPN108E

   HHC02202E – HHCPN114E

   HHC02202E – HHCPN188E

   HHC02202E – HHCPN200E

   HHC02202E – HHCPN201E

   HHC02202E – HHCPN204E

   HHC02202E – HHCPN213E

   HHC02202E – HHCPN996E

   HHC02203I – HHCPN027I

   HHC02203I – HHCPN037I

   HHC02203I – HHCPN042I

   HHC02203I – HHCPN051I

   HHC02203I – HHCPN053I

   HHC02203I – HHCPN056I

   HHC02203I – HHCPN060I

   HHC02203I – HHCPN126I

   HHC02203I – HHCPN162I

   HHC02203I – HHCPN190I

   HHC02203I – HHCPN195I

   HHC02203I – HHCPN210I

   HHC02203I – HHCPN212I

   HHC02203I – HHCPN216I

   HHC02204I – HHCCF028I

   HHC02204I – HHCPN030I

   HHC02204I – HHCPN036I

   HHC02204I – HHCPN037I

   HHC02204I – HHCPN124I

   HHC02204I – HHCPN131I

   HHC02204I – HHCPN134I

   HHC02204I – HHCPN136I

   HHC02204I – HHCPN137I

   HHC02204I – HHCPN189I

   HHC02204I – HHCPN197I

   HHC02205E – HHCPN029E

   HHC02205E – HHCPN039E

   HHC02205E – HHCPN055E

   HHC02205E – HHCPN059E

   HHC02205E – HHCPN060S

   HHC02205E – HHCPN066E

   HHC02205E – HHCPN067E

   HHC02205E – HHCPN075E

   HHC02205E – HHCPN077E

   HHC02205E – HHCPN087E

   HHC02205E – HHCPN089E

   HHC02205E – HHCPN091E

   HHC02205E – HHCPN100E

   HHC02205E – HHCPN101E

   HHC02205E – HHCPN110E

   HHC02205E – HHCPN115E

   HHC02205E – HHCPN128E

   HHC02205E – HHCPN130E

   HHC02205E – HHCPN138E

   HHC02205E – HHCPN143E

   HHC02205E – HHCPN144E

   HHC02205E – HHCPN145E

   HHC02205E – HHCPN162E

   HHC02205E – HHCPN164E

   HHC02205E – HHCPN165E

   HHC02205E – HHCPN180E

   HHC02205E – HHCPN187E

   HHC02205E – HHCPN192E

   HHC02205E – HHCPN196E

   HHC02205E – HHCPN207E

   HHC02205E – HHCPN208E

   HHC02205E – HHCPN209E

   HHC02205I – none
   HHC02205S – HHCCF005S
   HHC02205S – HHCCF028S
   HHC02205S – HHCCF029S
   HHC02205S – HHCCF052S
   HHC02205S – HHCCF054S
   HHC02205S – HHCCF066S
   HHC02205S – HHCCF067S
   HHC02205W – HHCPN103E
   HHC02206I – none
   HHC02207I – none
   HHC02208I – HHCPN018I
   HHC02209E – HHCPN017E
   HHC02209E – HHCPN024E
   HHC02209E – HHCPN034E
   HHC02210I – none
   HHC02211E – none
   HHC02212I – none
   HHC02213E – HHCPN019E
   HHC02213E – HHCPN020E
   HHC02213E – HHCPN021E
   HHC02214I – HHCPN025I
   HHC02215W – HHCPN026W

   HHC02216E – HHCPN081E

   HHC02216E – HHCPN084E

   HHC02216E – HHCPN202E

   HHC02216E – HHCPN217E

   HHC02217I – HHCPN203I

   HHC02218E – HHCPN205E

   HHC02219E – HHCPN007E

   HHC02219E – HHCPN009E

   HHC02219E – HHCPN014E

   HHC02219E – HHCPN105E

   HHC02219E – HHCPN106E

   HHC02219E – HHCPN107E

   HHC02219E – HHCPN109E

   HHC02219E – HHCPN118E

   HHC02219E – HHCPN119E

   HHC02219E – HHCPN146E

   HHC02219E – HHCPN206E

   HHC02219E – HHCPN211E

   HHC02219E – HHCPN215E

   HHC02219E – HHCUT001I

   HHC02219E – HHCUT002I

   HHC02219E – HHCUT003I

   HHC02219E – HHCUT004I

   HHC02219E – HHCUT005I

   HHC02220I – HHCPN214I

   HHC02221E – HHCPN218E

   HHC02222E – HHCPN219E


   HHC02223I – none
   HHC02224E – HHCPN035E
   HHC02226I – none
   HHC02227E – HHCPN163E
   HHC02227E – HHCPN180E
   HHC02228I – HHCPN038I
   HHC02228I – HHCPN050I
   HHC02229I – HHCPN040I
   HHC02230I – HHCPN045I
   HHC02231E – HHCPN046E
   HHC02231E – HHCPN096E
   HHC02232E – HHCPN047E

   HHC02233E – HHCPN048E

   HHC02234W – HHCPN049E

   HHC02235E – HHCPN053E

   HHC02236E – HHCPN053E

   HHC02237W – HHCPN147W

   HHC02238E – HHCPN182E

   HHC02239I – HHCPN072I

   HHC02240I – HHCPN074I

   HHC02241I – HHCPN076I

   HHC02242I – HHCPN078E

   HHC02243E – HHCPN083E

   HHC02244E – HHCPN097E

   HHC02245I – HHCPN098I

   HHC02246E – HHCPN148E

   HHC02247E – HHCPN102E

   HHC02247E – HHCPN111E

   HHC02247E – HHCPN117E

   HHC02248I – HHCPN104I

   HHC02249I – HHCPN070I

   HHC02249I – HHCPN113I

   HHC02249I – HHCPN120I

   HHC02250I – HHCPN112I

   HHC02251E – HHCPN116E

   HHC02252E – none
   HHC02253E – HHCPN127E
   HHC02254I – none
   HHC02255I – none
   HHC02256W – HHCPN150W
   HHC02257I – HHCPN161I
   HHC02259E – HHCPN998E
   HHC02260I – HHCPN008I
   HHC02261W – HHCPN010W
   HHC02262I – HHCPN011I
   HHC02263I – HHCPN012I
   HHC02264I – HHCPN013I
   HHC02265I – HHCPN999I
   HHC02266A – none
   HHC02267I – none
   HHC02268I – none

   HHC02269I – none
   HHC02270I – none
   HHC02271I – none
   HHC02272I – none
   HHC02273I – none
   HHC02274I – HHCPN028I
   HHC02275I – none
   HHC02276I – none
   HHC02277I – none
   HHC02278I – none
   HHC02279I – none
   HHC02280I – none
   HHC02281I – none
   HHC02282I – none
   HHC02283I – none
   HHC02284I – none
   HHC02285I – none
   HHC02286I – none
   HHC02287I – none
   HHC02288I – none
   HHC02289I – none
   HHC02290I - none
   HHC02291I – none
   HHC02292I – HHCPN125I
   HHC02293I – none
   HHC02294I – none
   HHC02298E – none
   HHC02299E – none

   *********************

   HHC02300I – none
   HHC02301E – none
   HHC02302W - none
   HHC02303E - none
   HHC02304W - none
   HHC02305E - none
   HHC02306E - none
   HHC02307E - none


   HHC02308W - none
   HHC02309W - none
   HHC02310S - none
   HHC02311I - none
   HHC02312W – none
   HHC02313I – HHCPN073I
   HHC02314I – none
   HHC02315I – none
   HHC02316E – none
   HHC02318I – none
   HHC02319I – none
   HHC02386E - none
   HHC02389E - none
   *********************
   HHC02400E – none
   HHC02401E – none
   HHC02402E – none
   HHC02403E – none
   HHC02404E – none
   HHC02405I – none
   HHC02410I – none
   HHC02411E – none
   HHC02412E – none
   HHC02413E – none
   HHC02414I – none
   HHC02415E – none
   HHC02416E – none
   HHC02417E – none
   HHC02418E – none
   HHC02419E – none
   HHC02420I – none
   HHC02421E – none
   HHC02422I – none
   HHC02423I – none
   HHC02430E – none
   HHC02431E – none
   HHC02432E – none
   HHC02433E – none
   HHC02434E – none
   HHC02435I – none
   HHC02436I – none
   HHC02437I – none
   HHC02438I – none
   HHC02439I – none
   HHC02444E – none
   HHC02445E – none
   HHC02446E – none
   HHC02447E – none
   HHC02448I – none
   HHC02449I – none
   HHC02450I – none
   HHC02451I – none
   HHC02452E – none
   HHC02453W – none
   HHC02454W – none
   HHC02455W – none
   HHC02456E – none
   HHC02457I – none
   HHC02458E – none
   HHC02459E – none
   HHC02460E – none
   HHC02461E – none
   HHC02462I – none
   HHC02463I – none
   HHC02464I – none
   HHC02465E – none
   HHC02465I – none
   HHC02466I – none
   HHC02467I – none
   HHC02468E – none
   HHC02469I – none
   HHC02470E – none
   HHC02471E – none
   HHC02472E – none
   HHC02473E – none
   HHC02474E – none
   HHC02475I – none
   HHC02476E – none
   HHC02477E – none
   HHC02478E – none
   HHC02479E – none
   HHC02480E – none
   HHC02481I – none
   HHC02482I – none
   HHC02483I – none
   HHC02485I – none
   HHC02486I - none
   HHC02487I – none
   HHC02488I – none
   HHC02489E – none
   HHC02490E – none
   HHC02491E – none
   HHC02494I – none
   HHC02495I – none
   HHC02496I – none
   HHC02499I – none
   *********************
   HHC02500E – none
   HHC02501E – none
   HHC02502E – none
   HHC02503E – none
   HHC02504E – none
   HHC02505E – none
   HHC02506E – none
   HHC02507E – none
   HHC02508E – none
   HHC02509E – none
   HHC02510E – none
   HHC02511E – none
   HHC02512E – none
   HHC02513E – none
   HHC02514E – none
   HHC02515E – none


   HHC02516E – none
   HHC02517E – none
   HHC02518E – none
   HHC02519E – none
   HHC02520I – none
   HHC02521I – none
   HHC02522I – none
   HHC02523I – none
   HHC02524I – none
   HHC02525I – none
   HHC02526I – none
   HHC02527I – none
   HHC02528I – none
   HHC02529I – none
   HHC02530E – none
   HHC02531E – none
   HHC02532E – none
   HHC02533E – none
   HHC02534E – none
   HHC02535E – none
   HHC02536E – none
   HHC02537E – none
   HHC02538E – none
   HHC02539E – none
   HHC02540E – none
   HHC02541E – none
   HHC02542E – none
   HHC02543E – none
   HHC02544E – none
   HHC02545E – none
   HHC02546E – none
   HHC02547E – none
   HHC02548E – none
   HHC02549E – none
   HHC02550I – none
   HHC02551I – none
   HHC02552I – none
   HHC02553I – none
   HHC02554I – none
   HHC02555I – none
   HHC02556I – none
   HHC02557I – none
   HHC02558I – none
   HHC02559E – none
   HHC02560I – none
   HHC02561I – none
   HHC02562I – none
   HHC02563I – none
   HHC02564I – none
   HHC02565I – none
   HHC02566I – none
   HHC02567I – none
   HHC02568I – none
   HHC02569E – none
   HHC02570E – none
   HHC02571E – none
   HHC02572W – none
   HHC02573E – none
   HHC02574E – none
   HHC02575E – none
   HHC02576E – none
   HHC02577E – none
   HHC02578E – none
   HHC02579E – none
   HHC02580E – none
   HHC02581E – none
   HHC02582E – none
   HHC02583E – none
   HHC02584E – none
   HHC02585E – none
   HHC02586E – none
   HHC02587E – none
   HHC02588E – none
   HHC02589I – none
   HHC02590W – none
   HHC02591I – none
   HHC02592I – none
   HHC02593E – none

   *********************

   HHC02600I – none
   HHC02601I – none
   HHC02602E – none
   HHC02603E – none
   HHC02604E – none
   HHC02605I – none
   HHC02606I – none
   HHC02607I – none
   HHC02608I – none

   *********************

   HHC02700I – none
   HHC02701E – none
   HHC02702I – none
   HHC02703E – none
   HHC02704I – none
   HHC02705E – none
   HHC02706I – none
   HHC02707E – none
   HHC02708E – none
   HHC02709E – none
   HHC02710E – none
   HHC02711E – none
   HHC02712E – none
   HHC02713E – none
   HHC02714E – none
   HHC02715E – none
   HHC02716E – none
   HHC02717E – none
   HHC02718I – none
   HHC02719I – none
   HHC02720E – none
   HHC02721I – none
   HHC02722I – none
   HHC02723I – none
   HHC02724I – none
   HHC02725I – none
   HHC02726I – none
   HHC02728I – none
   HHC02729I – none
   HHC02730I – none
   HHC02740I – none
   HHC02741E – none
   HHC02742E – none
   HHC02743E – none
   HHC02744I – none
   HHC02745I – none
   HHC02750E - none
   HHC02751I - none
   HHC02752I - none
   HHC02753E - none
   HHC02754E - none
   HHC02755I - none
   HHC02756E - none
   HHC02757I - none
   *********************


   HHC02800I - none
   HHC02801E - none
   HHC02802I - none
   HHC02803I - none
   HHC02804E – none
   HHC02805I – none
   HHC02806I - none
   *********************
   HHC03901E – none
   HHC03902E – none
   HHC03903I – none
   HHC03904I – none
   HHC03905I – none
   HHC03906I – none
   HHC03907I – none
   HHC03908I – none
   HHC03909I – none
   HHC03910I – none
   HHC03911I – none
   HHC03912E – none
   HHC03913W – none
   HHC03914W – none
   HHC03915I – none
   HHC03916I – none
   HHC03917W – none
   HHC03918W – none
   HHC03921W – none
   HHC03922W – none
   HHC03923W – none
   HHC03924W – none
   HHC03931W – none
   HHC03932W – none
   HHC03933W – none
   HHC03934W – none
   HHC03935W – none
   HHC03936W – none
   HHC03937W – none
   HHC03952I – none
   HHC03953I – none
   HHC03954I – none
   HHC03983I – none
   HHC03984I – none
   HHC03985E – none
   HHC03991I – none
   HHC03992D – none
   HHC03993D – none
   HHC03995D – none
   *********************
   HHC04100I – none
   HHC04101I – none
   HHC04102E – none
   HHC04110W – HHCCP085W
   HHC04111E – HHCCP084E
   HHC04111E – HHCCP086E
   HHC04111E – HHCCP087E
   HHC04111E – HHCCP088E
   HHC04111E – HHCCP089E
   HHC04112S – none
   *********************

   HHC17000E – none
   HHC17001I – none
   HHC17002I – none
   HHC17003I – none
   HHC17004I – none
   HHC17005I – none
   HHC17007I – none
   HHC17008I – none
   HHC17009I – none
   HHC17010I – none
   HHC17011I – none
   HHC17012I – none
   HHC17013I – none
   HHC17100I – none
   HHC17199I - none
   HHC17500I – none
   HHC17501I – none
   HHC17502E – none
   HHC17503E – none
   HHC17504E – none
   HHC17505E – none
   HHC17506E – none
   HHC17507W – none
   HHC17508W – none
   HHC17509W – none
   HHC17510W – none
   HHC17521I – none
   HHC17522I – none
   HHC17523I – none


   HHC17524I – none
   HHC17525I – none
   HHC17526I – none
   HHC17527I – none
   HHC17530E – none
   HHC17531E – none
   HHC17532E – none
   HHC17533E – none
   HHC17534E – none

   *********************

   HHC90000D – HHCCA300D

   HHC90000D – HHCEV300D

   HHC90010E – HHCPT002E

   HHC90011E – HHCPT001E

   HHC90012I – HHCPT003I


   HHC90013E – none
   HHC90014I – none
   HHC90015E – none
   HHC90016E – none
   HHC90017I – none
   HHC90018I – none
   HHC90019W – none
   HHC90100D – none
   HHC90101D – none
   HHC90102D – none
   HHC90103D – none
   HHC90104D – none
   HHC90105D – none
   HHC90106D – none
   HHC90107D – none
   HHC90108D – none
   HHC90109D – none
   HHC90110D – none
   HHC90111D – none
   HHC90112D – none
   HHC90190D - none
   HHC90205D - HHCTA382W

   HHC90300D – none
   HHC90301D – none
   HHC90302D – none
   HHC90303D – none
   HHC90304D – none
   HHC90305D – none
   HHC90306D – none
   HHC90307D – none
   HHC90308D – none
   HHC90309D – none
   HHC90310D – none
   HHC90311D – none
   HHC90312D – none
   HHC90313D – none
   HHC90314D – none
   HHC90315D – none
   HHC90316D – none
   HHC90317D – none
   HHC90318D – none
   HHC90319D – none
   HHC90320D – none
   HHC90321D – none
   HHC90322D – none
   HHC90323D – none
   HHC90324D – none
   HHC90325D – none
   HHC90326D – none
   HHC90327D – none
   HHC90328D – none
   HHC90329D – none
   HHC90330D – none
   HHC90331D – none
   HHC90332D – none
   HHC90333D – none
   HHC90334D – none
   HHC90335D – none
   HHC90336D – none
   HHC90337D – none
   HHC90338D – none
   HHC90339D – none
   HHC90340D – none
   HHC90341D – none
   HHC90342D – none
   HHC90343D – none
   HHC90344D – none
   HHC90345D – none
   HHC90346D – none
   HHC90347D – none
   HHC90349D – none
   HHC90350D – none

   HHC90351D – none
   HHC90352D – none
   HHC90353D – none
   HHC90354D – none
   HHC90355D – none
   HHC90356D – none
   HHC90357D – none
   HHC90358D – none
   HHC90359D – none
   HHC90360D – none
   HHC90361D – none
   HHC90362D – none
   HHC90363D – none
   HHC90364D – none
   *********************
   none – HHCPR001E
   none – HHCPR002E
   none – HHCPR019E
   none – HHCTE006A

Appendix B. Message Index (Old → New)
-------------------------------------

The following list shows each Hercules message ID in the old message
format followed by the related message ID in the new message format.
There are four possible cases for the index entries.

B.1 Replacement
---------~~~~~~

This is the normal case, where a new message ID replaces exactly one old
message ID.

Example: HHCCP064I - HHC01303I The new message “HHC01303I” replaces the
old message “HHCCP064I”.

B.2 New message
---------~~~~~~

New messages, that have not existed before and have no related old
message ID.

Example: none - HHC00069I Message “HHC00069I” is a new message that did
not exist before.

B3. Removed message
------------------~

Old messages, that have been deleted do not have a related new message
ID.

Example: HHCPR09E - none Message “HHCPR019E” has been removed.

B.4 Consolidation
---------~~~~~~~~

There are cases where one new message ID replaces several old message
IDs. This can happen, if there have been several old messages that had
the same or a similar message text, but different message IDs. These
messages have now been consolidated under one new message ID.

Example: HHCPN017E - HHC02209E HHCPN024E - HHC02209E HHCPN034E -
HHC02209E The old messages “HHCPN017E”, “HHCPN024E” and “HHCPN034E” have
been consolidated and replaced through the new message “HHC02209E”.

Hercules Emulator – Messages and Codes Page 641

B.5 Split
---------

In some rare cases an old message has been split into two or more new
messages.

Example: HHCPN053E - HHC02235E HHCPN053E - HHC02236E The old message
with ID “HHCPN053E” has been split into two new messages with IDs
“HHC02235E” and “HHC02236E”.

B.5 Message Index (Old → New)
---------------------------~~

::

   HHC1C001A – HHC00010A
   HHC770I – HHC00004I
   HHC771I – HHC00004I
   HHC772I – HHC00004I
   HHC773I – HHC00004I
   HHC774I – HHC00004I
   *********************
   HHCAO001I – HHC00100I
   HHCAO002I – HHC00101I
   HHCAO003I – HHC00081I
   HHCAO004S – HHC00102E
   HHCAO005I – HHC00087I
   HHCAO005I – HHC00088I
   HHCAO006I – HHC00089I
   HHCAO007E – HHC00070E
   HHCAO007E – HHC00102E
   HHCAO008E – HHC00079E
   HHCAO009E – HHC00084E
   HHCAO009E – HHC00084E
   HHCAO010E – HHC00071E
   HHCAO011E – HHC00072E
   HHCAO012E – HHC00073E
   HHCAO013E – HHC00074E
   HHCAO014E – HHC00075E
   HHCAO015E - HHC00075E
   HHCAO015E – HHC00075E
   HHCAO016I – HHC00077I
   HHCAO017E – HHC00071E
   HHCAO017E – HHC00072E
   HHCAO018E – HHC00073E
   HHCAO021E – HHC00076E
   HHCAO022I – HHC00080I
   HHCAO023E – HHC00083E
   HHCAO024E – HHC00085E
   HHCAO025I – HHC00086I
   HHCAO026E – HHC00078E
   *********************
   HHCCA001I – HHC01001I
   HHCCA002I – HHC00100I
   HHCCA003E – HHC01002E
   HHCCA004W – HHC01003W
   HHCCA005I – HHC01004I
   HHCCA006T – HHC01000E
   HHCCA007W – HHC01005W
   HHCCA008I – HHC01006I
   HHCCA009I – HHC00101I
   HHCCA009I – HHC00101I
   HHCCA010I – HHC01011I
   HHCCA011E – HHC01012E
   HHCCA012E – HHC01012E
   HHCCA012E – HHC01019E
   HHCCA013E – HHC01007E
   HHCCA014E – HHC01013E
   HHCCA015E – HHC01008E
   HHCCA016W – HHC01009W
   HHCCA017I – HHC01010I
   HHCCA018E – HHC01000E
   HHCCA019E – HHC01015E
   HHCCA020E – HHC01000E
   HHCCA021I – HHC01014I
   HHCCA022E – HHC00102E
   HHCCA300D - HHC01048D
   HHCCA300D - HHC01049D
   HHCCA300D - HHC01050D
   HHCCA300D - HHC01051D
   HHCCA300D - HHC01052D
   HHCCA300D - HHC01053D
   HHCCA300D - HHC01054D
   HHCCA300D - HHC01055D
   HHCCA300D - HHC01056D
   HHCCA300D - HHC01057D
   HHCCA300D - HHC01058D
   HHCCA300D - HHC01059D
   HHCCA300D - HHC01060D
   HHCCA300D - HHC01061D
   HHCCA300D - HHC01062D
   HHCCA300D - HHC01063D
   HHCCA300D - HHC01064D
   HHCCA300D - HHC01065D
   HHCCA300D - HHC01066D
   HHCCA300D - HHC01067D
   HHCCA300D - HHC01068D
   HHCCA300D - HHC01069D
   HHCCA300D - HHC01070D
   HHCCA300D - HHC01071D
   HHCCA300D - HHC01072D
   HHCCA300D - HHC01074D
   HHCCA300D - HHC01075D
   HHCCA300D - HHC01076D
   HHCCA300D - HHC01077D
   HHCCA300D - HHC01078D
   HHCCA300D - HHC01079D
   HHCCA300D - HHC01080D
   HHCCA300D - HHC01081D
   HHCCA300D - HHC01082D
   HHCCA300D - HHC01083D
   HHCCA300D - HHC01084D
   HHCCA300D – HHC90000D
   *********************
   HHCCD001I - HHC00100I
   HHCCD002I - HHC00100I
   HHCCD003I - HHC00100I
   HHCCD011I - HHC00101I
   HHCCD012I - HHC00101I
   HHCCD013I - HHC00101I
   HHCCD092I – HHC00316I
   HHCCD101E – HHC00300E
   HHCCD102E – HHC00304E
   HHCCD110E – HHC00305E
   HHCCD121E – HHC00306E
   HHCCD122E – HHC00307E
   HHCCD123E – HHC00308E
   HHCCD124E – HHC00309E
   HHCCD125E – HHC00310E
   HHCCD130E – HHC00301E
   HHCCD130E – HHC00302E
   HHCCD130E – HHC00303E
   HHCCD142E – HHC00311E
   HHCCD151E – HHC00312E
   HHCCD160E – HHC00317E
   HHCCD161E – HHC00313E
   HHCCD161E – HHC00314E
   HHCCD161E – HHC00319E
   HHCCD162I – HHC00320I
   HHCCD165W – HHC00318W
   HHCCD170E – HHC00317E
   HHCCD171E – HHC00323E
   HHCCD172E – HHC00324E
   HHCCD173E – HHC00324E
   HHCCD174E – HHC00324E
   HHCCD175W – HHC00322W
   HHCCD179I – HHC00321I
   HHCCD180E – HHC00326E
   HHCCD180E – HHC00327E
   HHCCD181I – HHC00325I
   HHCCD190E – HHC00342E
   HHCCD193E – HHC00343E
   HHCCD194E – HHC00344E
   HHCCD205W – HHC00317E
   HHCCD206W – HHC00329W
   HHCCD206W – HHC00331W

   HHCCD207I – HHC00315I

   HHCCD207I – HHC00328I

   HHCCD207I – HHC00330I

   HHCCD208I – HHC00332I

   HHCCD209W – HHC00317E

   HHCCD210I – HHC00333I

   HHCCD211I – HHC00334I

   HHCCD212I – HHC00335I

   HHCCD213I – HHC00336I

   HHCCD214I – HHC00337I

   HHCCD215I – HHC00338I

   HHCCD216I – HHC00339I

   HHCCD217I – HHC00340I

   HHCCD218I – HHC00341I

   HHCCD900I – HHC00399I

   *********************

   HHCCF001S – HHC01432S

   HHCCF002S – HHC01433S

   HHCCF003S - HHC01432S

   HHCCF004S – none
   HHCCF005S – HHC02205S
   HHCCF008E – HHC01441E
   HHCCF009E – none
   HHCCF012S – HHC01443S
   HHCCF013S – HHC01443S
   HHCCF014S – HHC01443S
   HHCCF016S – HHC01443S
   HHCCF017W – none
   HHCCF018S – HHC01443S
   HHCCF019S – HHC01443S
   HHCCF020W – none
   HHCCF022S – HHC01443S
   HHCCF023S – HHC01443S
   HHCCF028I – HHC02204I
   HHCCF028S – HHC02205S
   HHCCF029S – HHC01443S
   HHCCF029S – HHC02205S
   HHCCF031S – HHC01430S
   HHCCF032S – HHC01430S
   HHCCF033S – HHC01430S
   HHCCF034W – HHC01431I
   HHCCF035S – HHC01448S
   HHCCF036S – HHC01443S
   HHCCF040E – HHC00102E
   HHCCF041E – HHC01461E
   HHCCF042E – HHC01462E
   HHCCF043E – HHC01460E
   HHCCF044E – HHC01463E
   HHCCF045E – HHC01460E
   HHCCF046E – HHC01464E

   HHCCF047I – HHC01465I

   HHCCF048E – HHC01464E

   HHCCF049E – HHC01461E

   HHCCF050I – HHC01459I

   HHCCF051E – HHC01475E

   HHCCF051S – HHC01443S

   HHCCF051W – none
   HHCCF052S – HHC02205S
   HHCCF053E – HHC01470E
   HHCCF054E – HHC01470E
   HHCCF054S – HHC02205S
   HHCCF055E – HHC01470E
   HHCCF056E – HHC01471E
   HHCCF057E – HHC01472E
   HHCCF058E – HHC01473E
   HHCCF061W – none
   HHCCF062W – none
   HHCCF063W – none
   HHCCF064W – HHC00136E
   HHCCF065I – HHC00100I
   HHCCF066E – HHC01801E
   HHCCF066S – HHC02205S
   HHCCF067S – HHC02205S
   HHCCF070S – HHC01443S
   HHCCF072I – HHC01474I
   HHCCF072W – none
   HHCCF073W – none
   HHCCF074E – HHC01466E
   HHCCF074S – HHC01443S
   HHCCF075E – HHC01467E
   HHCCF075S – HHC01443S
   HHCCF076E – HHC01468E
   HHCCF077E – HHC01469E
   HHCCF077I – HHC00827I
   HHCCF078W – HHC01458W
   HHCCF079W – HHC00130W
   HHCCF081I – HHC01435I
   HHCCF082S – HHC01436S

   HHCCF083I – HHC01437I

   HHCCF084W – HHC01438W

   HHCCF085S – HHC01439S

   HHCCF086S – none
   HHCCF090I – HHC01447I
   HHCCF900S – HHC01430S
   *********************

   HHCCH001E – HHC00011E

   HHCCH002W – HHC00011E

   HHCCH003W – HHC00011E

   HHCCH004W – HHC00011E

   HHCCH005W – HHC00012W

   HHCCH006E – HHC00011E

   *********************

   HHCCP001W – HHC00136E

   HHCCP002I – HHC00100I

   HHCCP003I – HHC00811I

   HHCCP004I – HHC00812I

   HHCCP006S - HHC00102E

   HHCCP007I – HHC00811I

   HHCCP008I - HHC00101I

   HHCCP010I – HHC00808I

   HHCCP011I – HHC00809I

   HHCCP014I – HHC00801I

   HHCCP015I – HHC00802I

   HHCCP016I – HHC00803I

   HHCCP017I – HHC00822I

   HHCCP018I – HHC00823I

   HHCCP019I – HHC00824I

   HHCCP020E – HHC00825E

   HHCCP021E – HHC00826E

   HHCCP021I – HHC01319I

   HHCCP022I – HHC00807I

   HHCCP023I – HHC00840I

   HHCCP024I – HHC00841I

   HHCCP025I – HHC00842I

   HHCCP026I – HHC00843I

   HHCCP027E – HHC00828E

   HHCCP027I – HHC00846I

   HHCCP028I – HHC00845I

   HHCCP030E - HHC00828E

   HHCCP031I – HHC00844I

   HHCCP031I – HHC01329I

   HHCCP036E – HHC00002E

   HHCCP037E – HHC00002E

   HHCCP038E – HHC00003E

   HHCCP040I – HHC00004I

   HHCCP041I – HHC00006I

   HHCCP042I – HHC00006I

   HHCCP043I – HHC00800I

   HHCCP044I – HHC00804I

   HHCCP045I – HHC00805I

   HHCCP046I – HHC00806I

   HHCCP048I – HHC01315I

   HHCCP049I – HHC01316I

   HHCCP050I – HHC01317I

   HHCCP051I – HHC01318I

   HHCCP052I – HHC01319I

   HHCCP053I – HHC01329I

   HHCCP054I – HHC01330I

   HHCCP055I – HHC01330I

   HHCCP056I - HHC01332I

   HHCCP057I – HHC01300I

   HHCCP058I – HHC01300I

   HHCCP059I – HHC01300I

   HHCCP060I – HHC01333I

   HHCCP061I – HHC01333I

   HHCCP062I – HHC01300I

   HHCCP063I – HHC01302I

   HHCCP064I – HHC01303I

   HHCCP065I – HHC01304I

   HHCCP066I – HHC01305I

   HHCCP067E – HHC00102E

   HHCCP068E – HHC00102E


   HHCCP069I – HHC01306I

   HHCCP070I – HHC01307I

   HHCCP071I – HHC01308I

   HHCCP072I – HHC01309I

   HHCCP073I – HHC01310I

   HHCCP074I – HHC01311I

   HHCCP075I – HHC01312I

   HHCCP076I – HHC01313I

   HHCCP077I – HHC01314I

   HHCCP078I – HHC01301I

   HHCCP079E – HHC00813E

   HHCCP080E – HHC00813E

   HHCCP081E – HHC00002E

   HHCCP084E – HHC04111E

   HHCCP085W – HHC04110W

   HHCCP086E – HHC04111E

   HHCCP087E – HHC04111E

   HHCCP088E – HHC04111E

   HHCCP089E – HHC04111E

   HHCCP909W – HHC00005W

   *********************

   HHCCT001E – HHC00915E

   HHCCT001W – HHC00136E

   HHCCT002E – HHC00915E

   HHCCT002I – HHC00100I

   HHCCT003E – HHC00916E

   HHCCT003I – HHC00101I

   HHCCT004E – HHC00916E

   HHCCT005E – HHC00916E

   HHCCT006E – HHC00916E

   HHCCT007E – HHC00900E

   HHCCT008E – HHC00900E

   HHCCT009I – HHC00971I

   HHCCT010E – HHC00900E

   HHCCT011E – HHC00900E

   HHCCT012E – HHC00900E

   HHCCT013I – HHC00972I

   HHCCT014E – HHC00906E

   HHCCT015I – HHC00907I

   HHCCT016E – HHC00908E

   HHCCT017E – HHC00909E

   HHCCT018I – HHC00934I

   HHCCT019E – HHC00936E

   HHCCT020E – HHC00973E

   HHCCT021E – HHC00973E

   HHCCT022I – HHC00913I

   HHCCT023E – HHC00974E

   HHCCT024E – HHC00915E

   HHCCT025E – HHC00900E

   HHCCT026E – HHC00900E

   HHCCT027E – HHC00900E

   HHCCT027E – HHC00915E

   HHCCT028E – HHC00916E

   HHCCT029E – HHC00975E

   HHCCT030E – HHC00975E

   HHCCT031E – HHC00975E

   HHCCT032E – HHC00976E

   HHCCT033E – HHC00900E

   HHCCT034E – HHC00970E

   HHCCT037E – HHC00900E

   HHCCT038E – HHC00900E

   HHCCT040I – HHC00904I

   HHCCT041E – HHC00905I

   HHCCT042E – HHC00906E

   HHCCT043I – HHC00907I

   HHCCT044E – HHC00908E

   HHCCT045E – HHC00909E

   HHCCT046E – HHC00910I

   HHCCT047E – HHC00911E

   HHCCT048E – HHC00912E

   HHCCT049I – HHC00913I

   HHCCT050E – HHC00916E

   HHCCT051E – HHC00916E

   HHCCT052E – HHC00916E

   HHCCT053E – HHC00916E

   HHCCT054E – HHC00916E

   HHCCT055E – HHC00916E

   HHCCT056E – HHC00915E

   HHCCT056E – HHC00916E

   HHCCT057E – HHC00915E

   HHCCT058E – HHC00916E

   HHCCT059E – HHC00916E

   HHCCT060E – HHC00915E

   HHCCT061E – HHC00916E

   HHCCT062E – HHC00916E

   HHCCT063E – HHC00916E

   HHCCT064E – HHC00916E

   HHCCT065E – HHC00916E

   HHCCT066E – HHC00915E

   HHCCT067E – HHC00916E

   HHCCT068E – HHC00916E

   HHCCT069E – HHC00916E

   HHCCT070E – HHC00916E

   HHCCT071E – HHC00915E

   HHCCT072W – HHC00914W

   HHCCT073I – HHC00901I

   HHCCT074W – HHC00902W

   HHCCT075W – HHC00902W

   *********************

   HHCDA001E – HHC00400E

   HHCDA002E – HHC00401E

   HHCDA003E – HHC00402E

   HHCDA004I – HHC00403I

   HHCDA005E – HHC00404E

   HHCDA006E – HHC00405E

   HHCDA007E – HHC00404E

   HHCDA008E – HHC00404E

   HHCDA009E – HHC00404E

   HHCDA010E – HHC00406E

   HHCDA011E – HHC00407E

   HHCDA012E – HHC00404E

   HHCDA013E – HHC00404E

   HHCDA014E – HHC00408E

   HHCDA015I – HHC00409I

   HHCDA016E – HHC00410E

   HHCDA017E – HHC00411E

   HHCDA018E – HHC00412E

   HHCDA019E – HHC00413E

   HHCDA020I – HHC00414I

   HHCDA021E – HHC00415E

   HHCDA022E – HHC00416E

   HHCDA023I – HHC00417I

   HHCDA026E – HHC00404E

   HHCDA027E – HHC00404E

   HHCDA032E – HHC00404E

   HHCDA033E – HHC00404E

   HHCDA035E – HHC00418E

   HHCDA042E – HHC00419E

   HHCDA046E – HHC00419E

   HHCDA049E – HHC00420E

   HHCDA051E – HHC00421E

   HHCDA053E – HHC00422E

   HHCDA055I – HHC00423I

   HHCDA056E – HHC00500E

   HHCDA057E – HHC00501E

   HHCDA058E – HHC00502E

   HHCDA059E – HHC00502E

   HHCDA060E – HHC00502E

   HHCDA061E – HHC00502E

   HHCDA062E – HHC00502E

   HHCDA063E – HHC00503E

   HHCDA064E – HHC00502E

   HHCDA065E – HHC00505E

   HHCDA066E – HHC00506E

   HHCDA067I – HHC00507I

   HHCDA068E – HHC00508E

   HHCDA069E – HHC00502E

   HHCDA070E – HHC00502E

   HHCDA075E – HHC00502E

   HHCDA076E – HHC00502E

   HHCDA078E – HHC00509E

   HHCDA079E – HHC00510E

   HHCDA080E – HHC00511E

   HHCDA081E – HHC00512E

   HHCDA082E – HHC00502E

   HHCDA901E – HHC00513E

   HHCDA902E – HHC00514E

   HHCDA903E – HHC00515E

   HHCDA999E – HHC00443E

   *********************

   HHCDG001I – HHC01541I

   HHCDG002I – HHC01542I

   *********************


   HHCDL130W – none
   HHCDL131I – none
   HHCDL132I – none
   HHCDL133I – none
   HHCDL135I – none
   HHCDL136E – none
   HHCDL137E – none
   HHCDL138W – none
   HHCDL139I – none
   *********************
   HHCDN001I – HHC01900I

   HHCDN002I – HHC01901I

   HHCDN003I – HHC01902I

   *********************

   HHCEV001I – HHC01701I

   HHCEV003I – HHC01709I

   HHCEV004I – HHC01703I

   HHCEV004W – HHC01700W

   HHCEV005I – HHC01704I

   HHCEV006I – HHC01705I

   HHCEV006I – HHC01708I

   HHCEV008E – HHC01720E

   HHCEV008E – HHC01721E

   HHCEV010I – HHC01717I

   HHCEV011E – HHC01718E

   HHCEV011I – HHC01719I

   HHCEV011I – HHC01722I

   HHCEV012I – HHC01717I

   HHCEV014I – HHC01710I

   HHCEV014I – HHC01711I

   HHCEV015I – HHC01707I

   HHCEV016I – HHC01708I

   HHCEV016I – HHC01712I

   HHCEV016I – HHC01714I

   HHCEV017I – HHC01713I

   HHCEV017W – HHC01715W

   HHCEV018W – HHC01715W

   HHCEV019I – HHC01716I

   HHCEV300D – HHC90000D

   *********************

   HHCGC001E – HHC01351E

   HHCGC002T – HHC01352T

   HHCGC003E – HHC01350E

   HHCGC999W – HHC01353W

   *********************

   HHCGI001I – HHC01016I

   HHCGI002I - HHC01016I

   HHCGI003E – HHC01017E

   *********************

   HHCHD001E – HHC01511S

   HHCHD005E – HHC01519E

   HHCHD006S – HHC01511S

   HHCHD007E – HHC01516E

   HHCHD008E – HHC01522E

   HHCHD009E – HHC01524E

   HHCHD010I – HHC01509I

   HHCHD011I – HHC01510I

   HHCHD013E – HHC01517E

   HHCHD014E – HHC01518E

   HHCHD015E – HHC01521E

   HHCHD016E – HHC01520E

   HHCHD017E – HHC01523E

   HHCHD018I – HHC01505E

   HHCHD051I – HHC01513I

   HHCHD052I – HHC01514I

   HHCHD100I – HHC01526I

   HHCHD101I – HHC01527I

   HHCHD102I – HHC01528I

   HHCHD103I – HHC01529I

   HHCHD900I – HHC01500I

   HHCHD901I – HHC01501I

   HHCHD902I – HHC01502I

   HHCHD909I – HHC01504I

   HHCHD950I – HHC01512I

   HHCHD959I – HHC01515I

   *********************

   HHCHT001I – HHC00100I

   HHCHT002E – HHC01800E

   HHCHT003W – HHC01804W

   HHCHT004E – HHC01800E

   HHCHT005E – HHC01800E

   HHCHT006I – HHC01803I

   HHCHT007E – HHC01800E

   HHCHT008E – HHC01800E

   HHCHT009I – HHC00101I

   HHCHT010E – HHC00102E

   HHCHT011E – HHC01800E

   HHCHT013E – HHC01801E

   *********************

   HHCIN001S – HHC01410S

   HHCIN002E – HHC01411E

   HHCIN003S - HHC01410S

   HHCIN004S - HHC00102E

   HHCIN005S – HHC00102S

   HHCIN006S - HHC00102E

   HHCIN007S - HHC00102E

   HHCIN900I – HHC01420I

   HHCIN901I – none
   HHCIN902I – HHC01422I
   HHCIN903I – HHC01423I
   HHCIN904I – HHC01424I
   HHCIN909I – HHC01425I
   HHCIN998I – HHC01426I

   *********************

   HHCLC001E – HHC00900E

   HHCLC002I – HHC00904I

   HHCLC003I – HHC00921I

   HHCLC004I – HHC00934I

   HHCLC005E – HHC00936E

   HHCLC006I – HHC00938I

   HHCLC007E – HHC00940E

   HHCLC008E – HHC00941E

   HHCLC009I – HHC00945I

   HHCLC010I – HHC00946I

   HHCLC011I – HHC00947I

   HHCLC012I – HHC00949I

   HHCLC013I – HHC00950I

   HHCLC014I – HHC00950I

   HHCLC015I – HHC00951I

   HHCLC016I – HHC00952I

   HHCLC017E – HHC00916E

   HHCLC018E – HHC00916E

   HHCLC019E – HHC00915E

   HHCLC020E – HHC00916E

   HHCLC021E – HHC00954E

   HHCLC023E – HHC00954E

   HHCLC027E – HHC00957E

   HHCLC028E – HHC00958E

   HHCLC029E – HHC00957E

   HHCLC031E – HHC00959E

   HHCLC032E – HHC00957E

   HHCLC033E – HHC00958E

   HHCLC034E – HHC00957E

   HHCLC035E – HHC00960E

   HHCLC036E – HHC00961E

   HHCLC037E – HHC00962E

   HHCLC038E – HHC00963E

   HHCLC039E – HHC00940E

   HHCLC040E – HHC00920E

   HHCLC041W – HHC00953W

   HHCLC042E – HHC00944E

   HHCLC043I – HHC00933I

   HHCLC044I – HHC00933I

   HHCLC045I – HHC00933I

   HHCLC046I – HHC00933I

   HHCLC047I – HHC00933I

   HHCLC048I – HHC00933I

   HHCLC049W – HHC00939W

   HHCLC050E – HHC00937E

   HHCLC051I – HHC00922I

   HHCLC052E – HHC00916E

   HHCLC053E – HHC00916E

   HHCLC054W – HHC00939W

   HHCLC055I – HHC00942I

   HHCLC056W – HHC00943W

   HHCLC073I – HHC00901I

   HHCLC074W – HHC00902W

   HHCLC075W – HHC00902W

   HHCLG014E – HHC02100E

   HHCLG015I – HHC02101I

   HHCLG016E – HHC02102E

   HHCLG017S - HHC02102E

   *********************

   HHCMS001E - HHC00075E

   *********************

   HHCPN001I - HHC00100I

   HHCPN007E – HHC02219E

   HHCPN008I – HHC02260I

   HHCPN009E – HHC02219E

   HHCPN010I – HHC00817I

   HHCPN010W – HHC02261W

   HHCPN011I – HHC02262I

   HHCPN012I – HHC02263I

   HHCPN013I – HHC02264I

   HHCPN014E – HHC02219E

   HHCPN017E – HHC02209E

   HHCPN018I – HHC02208I

   HHCPN019E – HHC02213E

   HHCPN020E – HHC02213E

   HHCPN021E – HHC02213E

   HHCPN024E – HHC02209E

   HHCPN025I – HHC02214I

   HHCPN026W – HHC02215W

   HHCPN027I – HHC02203I

   HHCPN028I – HHC02274I

   HHCPN029E – HHC02205E

   HHCPN030I – HHC02204I

   HHCPN031E – HHC02201E

   HHCPN034E – HHC02209E

   HHCPN035E – HHC02224E

   HHCPN036I – HHC02204I

   HHCPN037I – HHC02203I

   HHCPN037I – HHC02204I

   HHCPN038I – HHC02228I

   HHCPN039E – HHC02205E

   HHCPN040I – HHC02229I

   HHCPN042I – HHC02203I

   HHCPN045I – HHC02230I

   HHCPN046E – HHC02231E

   HHCPN047E – HHC02232E

   HHCPN048E – HHC02233E

   HHCPN049E – HHC02234W

   HHCPN050I – HHC02228I

   HHCPN051I – HHC02203I

   HHCPN052E – HHC00818E

   HHCPN053E – HHC02235E

   HHCPN053E – HHC02236E

   HHCPN053I – HHC02203I

   HHCPN054E – HHC02201E

   HHCPN055E – HHC02205E

   HHCPN056I – HHC02203I

   HHCPN057E – HHC02201E

   HHCPN058E – HHC02201E

   HHCPN059E – HHC02205E

   HHCPN060I – HHC02203I

   HHCPN060S – HHC02205E

   HHCPN062E – HHC02202E

   HHCPN066E – HHC02205E

   HHCPN067E – HHC02205E

   HHCPN070I – HHC02249I

   HHCPN072I – HHC02239I

   HHCPN073I – HHC02313I

   HHCPN074I – HHC02240I

   HHCPN075E – HHC02205E

   HHCPN076I – HHC02241I

   HHCPN077E – HHC02205E

   HHCPN078E – HHC02242I

   HHCPN081E – HHC02216E

   HHCPN083E – HHC02243E

   HHCPN084E – HHC02216E

   HHCPN087E – HHC02205E

   HHCPN089E – HHC02205E

   HHCPN091E – HHC02205E

   HHCPN093E – HHC02202E

   HHCPN096E – HHC02231E

   HHCPN097E – HHC02244E

   HHCPN098I – HHC02245I

   HHCPN099E – HHC02202E

   HHCPN100E – HHC02205E

   HHCPN101E – HHC02205E

   HHCPN102E – HHC02247E

   HHCPN103E – HHC02205W

   HHCPN104I – HHC02248I

   HHCPN105E – HHC02219E

   HHCPN106E – HHC02219E

   HHCPN107E – HHC02219E

   HHCPN108E – HHC02202E

   HHCPN109E – HHC02219E

   HHCPN110E – HHC02205E

   HHCPN111E – HHC02247E

   HHCPN112I – HHC02250I

   HHCPN113I – HHC02249I

   HHCPN114E – HHC02202E

   HHCPN115E – HHC02205E

   HHCPN116E – HHC02251E

   HHCPN117E – HHC02247E

   HHCPN118E – HHC02219E

   HHCPN119E – HHC02219E

   HHCPN120I – HHC02249I

   HHCPN123I – HHC00815I

   HHCPN123I – HHC00820I

   HHCPN124I – HHC02204I

   HHCPN125I – HHC02292I

   HHCPN126I – HHC02203I

   HHCPN127E – HHC02253E

   HHCPN128E – HHC02205E

   HHCPN130E – HHC02205E

   HHCPN131I – HHC02204I

   HHCPN134I – HHC02204I

   HHCPN136I – HHC02204I

   HHCPN137I – HHC02204I

   HHCPN138E – HHC02205E

   HHCPN139E – HHC01600E

   HHCPN140I – HHC01602I

   HHCPN140I – HHC01603I

   HHCPN142I – HHC01415I

   HHCPN142I – HHC01604I

   HHCPN143E – HHC02205E

   HHCPN144E – HHC02205E

   HHCPN145E – HHC02205E

   HHCPN146E – HHC02219E

   HHCPN147W – HHC02237W

   HHCPN148E – HHC02246E

   HHCPN150W – HHC02256W

   HHCPN152I – HHC00819I

   HHCPN153I – HHC00820I

   HHCPN154I – HHC00819I

   HHCPN155I – HHC00820I

   HHCPN160E – HHC02106E

   HHCPN160W – HHC00816W

   HHCPN161I – HHC02257I

   HHCPN162E – HHC02205E

   HHCPN162I – HHC02203I

   HHCPN163E – HHC02227E

   HHCPN164E – HHC02205E

   HHCPN165E – HHC02205E

   HHCPN180E – HHC02205E

   HHCPN180E – HHC02227E

   HHCPN181E – HHC02200E

   HHCPN182E – HHC02238E

   HHCPN187E – HHC02205E

   HHCPN188E – HHC02202E

   HHCPN189I – HHC02204I

   HHCPN190I – HHC02203I

   HHCPN192E – HHC02205E

   HHCPN195I – HHC02203I

   HHCPN196E – HHC02205E

   HHCPN197I – HHC02204I

   HHCPN200E – HHC02202E

   HHCPN201E – HHC02202E

   HHCPN202E – HHC02216E

   HHCPN203I – HHC02217I

   HHCPN204E – HHC02202E

   HHCPN205E – HHC02218E

   HHCPN206E – HHC02219E

   HHCPN207E – HHC02205E

   HHCPN208E – HHC02205E

   HHCPN209E – HHC02205E

   HHCPN210I – HHC02203I

   HHCPN211E – HHC02219E

   HHCPN212I – HHC02203I

   HHCPN213E – HHC02202E

   HHCPN214I – HHC02220I

   HHCPN215E – HHC02219E

   HHCPN216I – HHC02203I

   HHCPN217E – HHC02216E

   HHCPN218E – HHC02221E

   HHCPN219E – HHC02222E

   HHCPN995E – HHC01405E

   HHCPN996E – HHC02202E


   HHCPN997E – none
   HHCPN998E – HHC02259E
   HHCPN999I – HHC02265I

   *********************

   HHCPR001E – none
   HHCPR002E - none
   HHCPR003E – HHC01105E
   HHCPR004E – HHC01105E
   HHCPR005E – HHC01105E
   HHCPR006E – HHC01105E
   HHCPR007I – HHC01106I
   HHCPR008E – HHC01105E
   HHCPR011I – HHC01107I
   HHCPR012E – HHC01108E
   HHCPR015E - HHC00102E
   HHCPR016I – HHC01100I
   HHCPR017I – HHC01100I
   HHCPR018I – HHC01100I
   HHCPR019E - none

   HHCPT001E – HHC90011E

   HHCPT002E – HHC90010E

   HHCPT003I – HHC90012I

   *********************

   HHCPU001E – HHC01201E

   HHCPU002E – HHC01209E

   HHCPU003E – HHC01200E

   HHCPU004E – HHC01200E

   *********************

   HHCRD001E – HHC01200E

   HHCRD002E – HHC01201E

   HHCRD003E – HHC01200E

   HHCRD004E – HHC01200E

   HHCRD005E – HHC01202E

   HHCRD006E – HHC01203E

   HHCRD007I – HHC01204I

   HHCRD008W – HHC01205W

   HHCRD009E – HHC01201E

   HHCRD010E – HHC01200E

   HHCRD011E – HHC01200E

   HHCRD012I – HHC01206I

   HHCRD013E – HHC01200E

   HHCRD014E – HHC01200E

   HHCRD015E – HHC01200E

   HHCRD016E – HHC01200E

   HHCRD017E – HHC01200E

   HHCRD018E – HHC01200E

   HHCRD019E – HHC01207E

   *********************

   HHCSC001E – HHC00601E

   HHCSC002E – HHC00600E

   HHCSC003E – HHC00602E

   HHCSC011E – HHC00600E

   HHCSC012E – HHC00600E

   HHCSC031E – HHC00600E

   HHCSC032W – HHC00603W

   HHCSC041E – HHC00600E

   HHCSC051E – HHC00600E

   HHCSC101E – HHC00604E

   HHCSC201E – HHC00605E

   HHCSC202I - HHC00605E

   *********************

   HHCSD001E – HHC01041E

   HHCSD002E – HHC01000E

   HHCSD003E – HHC01000E

   HHCSD004I – HHC01042I

   HHCSD005E – HHC01043E

   HHCSD006E – HHC01045E

   HHCSD007I – HHC01046I

   HHCSD008E – HHC01033E

   HHCSD009E – HHC01034E

   HHCSD010E - HHC01034E

   HHCSD011E – HHC01035E

   HHCSD012E – HHC01036E

   HHCSD013E - HHC01034E

   HHCSD014E - HHC01034E

   HHCSD015E – HHC01037E

   HHCSD016E – HHC01038E

   HHCSD017E – HHC01000E

   HHCSD018I – HHC01040I

   HHCSD020I - HHC00100I

   HHCSD021E - HHC01034E

   HHCSD022I - HHC00101I

   HHCSD023E - HHC00102E

   HHCSD024E – HHC01032E

   HHCSD025I – HHC01044I

   HHCSD026E – HHC01039E

   *********************

   HHCSH001S – HHC00700S

   HHCSH002W – HHC00701W

   HHCSH003S – HHC00702S

   HHCSH004S – HHC00703S

   HHCSH005S – HHC00704S

   HHCSH006S – HHC00705S

   HHCSH007S – HHC00706S

   HHCSH008S – HHC00707S

   HHCSH009I – HHC00708I

   HHCSH010S – HHC00700S

   HHCSH011I – HHC00701W

   HHCSH012S – HHC00709S

   HHCSH013S – HHC00710S

   HHCSH014S – HHC00711S

   HHCSH015S – HHC00705S

   HHCSH016S – HHC00704S

   HHCSH017S – HHC00703S

   HHCSH018S – HHC00706S

   HHCSH019I – HHC00712I

   HHCSH020E – HHC00713E

   HHCSH021E – HHC00714E

   HHCSH022E – HHC00715E

   HHCSH023E - HHC00715E

   HHCSH024E – HHC00716E

   HHCSH025E – HHC00716E

   HHCSH026E – HHC00717E

   HHCSH027E – HHC00718E

   HHCSH028E – HHC00719E

   HHCSH029E – HHC00720E

   HHCSH030E – HHC00720E

   HHCSH031E – HHC00721I

   HHCSH032E – HHC00722E

   HHCSH033E – HHC00723E

   HHCSH034E – HHC00724E

   HHCSH035E – HHC00725E

   HHCSH036E – HHC00726E

   HHCSH037E – HHC00727E

   HHCSH038E – HHC00728E

   HHCSH039E – HHC00727E

   HHCSH040E – HHC00728E

   HHCSH041E – HHC00729E

   HHCSH042W – HHC00730W

   HHCSH043I – HHC00731I

   HHCSH045I – HHC00100I

   HHCSH046E – HHC00735E

   HHCSH0474 – HHC00732E

   HHCSH047E – HHC00734E

   HHCSH048I – HHC00101I

   HHCSH049I – HHC00100I

   HHCSH050E – HHC00735E

   HHCSH051W – HHC00735E

   HHCSH052W – HHC00736W

   HHCSH053E – HHC00735E

   HHCSH053I – HHC00733I

   HHCSH054W – HHC00735E

   HHCSH055E – HHC00735E

   HHCSH056W – HHC00735E

   HHCSH057I – HHC00737I

   HHCSH058E – HHC00735E

   HHCSH059E – HHC00735E

   HHCSH060E – HHC00735E

   HHCSH061E - HHC00102E

   HHCSH062E – HHC00738E

   HHCSH063E – HHC00739E

   HHCSH064E – HHC00740E

   HHCSH065E – HHC00735E

   HHCSH066E – HHC00741E

   HHCSH999E – HHC00742E

   *********************

   HHCSR001E – HHC02020E

   HHCSR001I – HHC02007I

   HHCSR010E – HHC02001E

   HHCSR011E – HHC02001E

   HHCSR012E – HHC02001E

   HHCSR013E – HHC02020E

   HHCSR014E – HHC02021E

   HHCSR015E – HHC02004E

   HHCSR016E – HHC02019E

   HHCSR101E – HHC02000E

   HHCSR102E – HHC02001E

   HHCSR103E – HHC02005E

   HHCSR103W – HHC02002W

   HHCSR104E – HHC02006E

   HHCSR104W – HHC02003W

   HHCSR105E – HHC02008E

   HHCSR106E – HHC02009E

   HHCSR107E – HHC02009E

   HHCSR108E – HHC02009E

   HHCSR109E – HHC02009E

   HHCSR110E – HHC02009E

   HHCSR111E – HHC02009E

   HHCSR113E – HHC02010E

   HHCSR114E – HHC02011E

   HHCSR115E – HHC02012E

   HHCSR116E – HHC02013E

   HHCSR117E – HHC02014E

   HHCSR118E – HHC02015E

   HHCSR119W – HHC02016W

   HHCSR120E – HHC02017E

   HHCSR121E – HHC02017E

   HHCSR122E – HHC02017E

   HHCSR123E – HHC02017E

   HHCSR124E – HHC02017E

   HHCSR125E – HHC02017E

   HHCSR126E – HHC02017E

   HHCSR127E – HHC02017E

   HHCSR128E – HHC02017E

   HHCSR129E – HHC02017E

   HHCSR130E – HHC02017E

   HHCSR131E – HHC02017E

   HHCSR132E – HHC02016E

   HHCSR133E - HHC00102E

   HHCSR134E – HHC02017E

   HHCSR999E – HHC02018E

   *********************

   HHCTA001E - HHC00205E

   HHCTA002E - HHC00205E

   HHCTA003W – HHC00220W

   HHCTA004I – HHC00221I

   HHCTA010I – HHC00224I

   HHCTA066I – HHC00222I

   HHCTA067E – HHC00223E

   HHCTA068E – HHC00223E

   HHCTA069E – HHC00223E

   HHCTA070E – HHC00223E

   HHCTA071E – HHC00223E

   HHCTA072E – HHC00212E

   HHCTA078E – HHC00223E

   HHCTA081I – HHC00217I

   HHCTA090E - HHC00205E

   HHCTA091E – HHC00214E

   HHCTA092E - HHC00205E

   HHCTA093I – HHC00216I

   HHCTA094I – HHC00215I

   HHCTA099I – HHC00218I

   HHCTA099I – HHC00219I

   HHCTA101I – HHC00201I

   HHCTA102E – HHC00205E

   HHCTA103E – HHC00204E

   HHCTA104E – HHC00204E

   HHCTA105E – HHC00204E

   HHCTA106E – HHC00204E

   HHCTA107E – HHC00202E

   HHCTA108E – HHC00203E

   HHCTA109E – HHC00204E

   HHCTA110E – HHC00204E

   HHCTA111E – HHC00204E

   HHCTA112E – HHC00204E

   HHCTA113E – HHC00204E

   HHCTA114E – HHC00204E

   HHCTA115E – HHC00204E

   HHCTA116E – HHC00204E

   HHCTA117E – HHC00204E

   HHCTA118E – HHC00204E

   HHCTA119E – HHC00204E

   HHCTA120E – HHC00205E

   HHCTA239E - HHC00205E

   HHCTA240E - HHC00205E

   HHCTA241E - HHC00205E

   HHCTA242E - HHC00205E

   HHCTA243E – HHC00206E

   HHCTA244E - HHC00205E

   HHCTA245E – HHC00207E

   HHCTA246E – HHC00207E

   HHCTA247E – HHC00207E

   HHCTA248E – HHC00207E

   HHCTA249E – HHC00207E

   HHCTA250E - HHC00205E

   HHCTA251E - HHC00205E

   HHCTA252E – HHC00204E

   HHCTA253E – HHC00204E

   HHCTA254E – HHC00204E

   HHCTA255E – HHC00204E

   HHCTA256E – HHC00204E

   HHCTA257E – HHC00204E

   HHCTA258E – HHC00204E

   HHCTA259E – HHC00204E

   HHCTA260E – HHC00204E

   HHCTA261E – HHC00204E

   HHCTA262E – HHC00204E

   HHCTA263E – HHC00204E

   HHCTA264E - HHC00205E

   HHCTA265E - HHC00205E

   HHCTA323I - HHC00102E

   HHCTA324E - HHC00205E

   HHCTA324E - HHC00213E

   HHCTA330E - HHC00205E

   HHCTA332E - HHC00205E

   HHCTA333E - HHC00205E

   HHCTA334E - HHC00205E

   HHCTA335E - HHC00205E

   HHCTA336E - HHC00205E

   HHCTA337E - HHC00205E

   HHCTA338E - HHC00205E

   HHCTA373E - HHC00205E

   HHCTA373W - HHC00205E

   HHCTA376E - HHC00205E

   HHCTA377I – HHC00210I

   HHCTA380E - HHC00205E

   HHCTA381E - HHC00205E

   HHCTA382E - HHC00205E

   HHCTA382W - HHC90205D

   HHCTA383E - HHC00205E

   HHCTA389E - HHC00205E

   HHCTA401E - HHC00205E

   HHCTA402E - HHC00205E

   HHCTA414E - HHC00204E

   HHCTA415E - HHC00204E

   HHCTA416E - HHC00204E

   HHCTA417E – HHC00204E

   HHCTA418E – HHC00204E

   HHCTA419E – HHC00204E

   HHCTA420E – HHC00204E

   HHCTA421E – HHC00204E

   HHCTA430I – HHC00208I

   HHCTA431I – HHC00209I

   HHCTA488E – HHC00205E

   HHCTA501I – HHC00201I

   HHCTA502E - HHC00205E

   HHCTA503E – HHC00204E

   HHCTA504E – HHC00204E

   HHCTA505E – HHC00204E

   HHCTA506E – HHC00204E

   HHCTA507E – HHC00204E

   HHCTA508E – HHC00202E

   HHCTA510E – HHC00204E

   HHCTA511E – HHC00204E

   HHCTA512E – HHC00204E

   HHCTA513E – HHC00204E

   HHCTA514E – HHC00204E

   HHCTA515E – HHC00204E

   HHCTA516E – HHC00204E

   HHCTA517E – HHC00204E

   HHCTA518E – HHC00204E

   HHCTA519E – HHC00204E

   HHCTA520E – HHC00204E

   HHCTA521E – HHC00204E

   HHCTA521E – HHC00205E

   *********************

   HHCTE001I - HHC00100I

   HHCTE002W – HHC01023W

   HHCTE003I – HHC01024I

   HHCTE004I - HHC00101I

   HHCTE005E - HHC00102E


   HHCTE006A - none
   HHCTE007I - HHC01022I
   HHCTE008I – HHC01022I
   HHCTE009I – HHC01018I
   HHCTE010E – HHC01007E
   HHCTE010E – HHC01017E
   HHCTE011E – HHC01007E
   HHCTE012E – HHC01007E
   HHCTE013E – HHC01019E
   HHCTE014I – HHC01090I
   HHCTE017E – HHC01025E
   HHCTE019E - HHC01000E
   HHCTE090E - HHC01000E

   HHCTU001E – HHC00135E

   HHCTU001E – HHC00136E

   HHCTU002E – HHC00137E

   HHCTU003E – HHC00138E

   HHCTU004E – HHC00139E

   HHCTU005E – HHC00140E

   HHCTU006E – HHC00141E

   HHCTU007E – HHC00140E

   HHCTU008E – HHC00142E

   HHCTU009E – HHC00140E

   HHCTU010E – HHC00143E

   HHCTU011E – HHC00140E

   HHCTU012E – HHC00144E

   HHCTU013E – HHC00144E

   HHCTU014E – HHC00140E

   HHCTU015E – HHC00145E

   HHCTU016E – HHC00140E

   HHCTU017E – HHC00140E

   HHCTU018E – HHC00142E

   HHCTU019E – HHC00143E

   HHCTU020E – HHC00146E

   HHCTU021E – HHC00140E

   HHCTU022E – HHC00142E

   HHCTU023E – HHC00143E

   HHCTU024E – HHC00146E

   HHCTU025E – HHC00136E

   HHCTU026E – HHC00136E

   HHCTU027E – HHC00136E

   *********************

   HHCUT001I – HHC02219E

   HHCUT002I – HHC02219E

   HHCUT003I – HHC02219E

   HHCUT004I – HHC02219E

   HHCUT005I – HHC02219E

   *********************

   HHCVE002I – HHC01702I

   *********************

   HHCVM001I – HHC01950I

   HHCVM002I – HHC01950I

   HHCVM003I – HHC01953E

   HHCVM004E – HHC01954E

   HHCVM005W – HHC01951W

   HHCVM006E – HHC01908E

   HHCVM007I – HHC01907I

   HHCVM008I – HHC01906I

   HHCVM009E – HHC01927I

   HHCVM009E – HHC01938E

   HHCVM010E - HHC00102E

   HHCVM011E – HHC01908E

   HHCVM012I – HHC01909I

   HHCVM013I – HHC01920I

   HHCVM014I – HHC01934I

   HHCVM014I – HHC01945I

   HHCVM015I – HHC01928I

   HHCVM015I – HHC01939I

   HHCVM016I – HHC01930I

   HHCVM016I – HHC01941I

   HHCVM017I – HHC01926I

   HHCVM017I – HHC01937I

   HHCVM018I – HHC01922I

   HHCVM019I – HHC01924I

   HHCVM019I – HHC01925I

   HHCVM019I – HHC01935I

   HHCVM019I – HHC01936I

   HHCVM020I – HHC01929I

   HHCVM020I – HHC01931I

   HHCVM020I – HHC01932I

   HHCVM020I – HHC01933I

   HHCVM020I – HHC01940I

   HHCVM020I – HHC01942I

   HHCVM020I – HHC01943I

   HHCVM020I – HHC01944I

   HHCVM021I – HHC01923I

   HHCVM022I – HHC01921I

   HHCVM023I – HHC01905I
   *********************
   none - HHC00001I
   none – HHC00007I
   none – HHC00008I
   none – HHC00009I
   none – HHC00013I
   none – HHC00014E
   none – HHC00015E
   none - HHC00016E
   none – HHC00017I
   none – HHC00069I
   none – HHC00082I
   none – HHC00103I
   none – HHC00105E
   none – HHC00131A
   none – HHC00147I
   none – HHC00148I
   none – HHC00149I
   none – HHC00150I
   none – HHC00151I
   none – HHC00152E
   none – HHC00153E
   none – HHC00154E
   none – HHC00160I
   none – HHC00161E
   none – HHC00211I
   none – HHC00225E
   none – HHC00226I
   none – HHC00227I
   none – HHC00228I
   none – HHC00229I
   none – HHC00235I
   none – HHC00243W
   none – HHC00345I
   none – HHC00346I
   none – HHC00347I
   none – HHC00348E
   none – HHC00349E
   none – HHC00352E
   none – HHC00353E
   none – HHC00354E
   none – HHC00355E
   none – HHC00356E
   none – HHC00357I
   none – HHC00358I
   none – HHC00359I
   none – HHC00360I
   none – HHC00361E
   none – HHC00362E
   none – HHC00363W
   none – HHC00364W
   none – HHC00365W
   none – HHC00366W
   none – HHC00367W
   none – HHC00368W
   none – HHC00369W
   none – HHC00370W
   none – HHC00371W
   none – HHC00372I
   none – HHC00373I
   none – HHC00374E
   none – HHC00375W
   none – HHC00376W
   none – HHC00377I
   none – HHC00378E
   none – HHC00396I
   none – HHC00397I
   none – HHC00398I
   none – HHC00424I
   none – HHC00425I
   none – HHC00426I
   none – HHC00427I
   none – HHC00428I
   none – HHC00429I
   none – HHC00430I
   none – HHC00431I
   none – HHC00432E
   none – HHC00433I
   none – HHC00434I
   none – HHC00435I
   none – HHC00436I
   none – HHC00437I
   none – HHC00438I
   none – HHC00439I
   none – HHC00440I
   none – HHC00441I
   none – HHC00442I
   none – HHC00445I
   none – HHC00446E
   none – HHC00447I
   none – HHC00448E
   none – HHC00449I
   none – HHC00450E
   none – HHC00451E
   none – HHC00452E
   none – HHC00453I
   none – HHC00454I
   none – HHC00455E
   none – HHC00456I
   none – HHC00457I
   none – HHC00458E
   none – HHC00459I
   none – HHC00460I
   none – HHC00461E
   none – HHC00462I
   none – HHC00463I
   none – HHC00464E
   none – HHC00465I
   none – HHC00466I
   none – HHC00467I
   none – HHC00468I
   none – HHC00504I
   none – HHC00516I
   none – HHC00517I
   none – HHC00518I
   none – HHC00519I
   none – HHC00520I
   none – HHC00521I
   none – HHC00743I
   none – HHC00810E
   none – HHC00814I
   none – HHC00821I
   none - HHC00832I
   none - HHC00834I
   none - HHC00838I
   none - HHC00839E
   none – HHC00850I
   none – HHC00851I
   none – HHC00852I
   none – HHC00853I
   none – HHC00854I
   none – HHC00855I
   none – HHC00856I
   none – HHC00857I
   none – HHC00858I
   none – HHC00859I
   none – HHC00860I
   none – HHC00861I
   none – HHC00862I
   none – HHC00863I
   none – HHC00864I
   none – HHC00865I
   none – HHC00866I
   none – HHC00867I
   none – HHC00868I
   none – HHC00869I
   none – HHC00870I
   none – HHC00871I
   none – HHC00872I
   none – HHC00873I
   none – HHC00874I
   none – HHC00875I
   none – HHC00876I
   none – HHC00877I
   none – HHC00880I
   none – HHC00881I
   none – HHC00882I
   none - HHC00890I
   none - HHC00891E
   none - HHC00892E
   none - HHC00893E
   none - HHC00895E
   none - HHC00896E
   none - HHC00898I
   none – HHC00918E
   none – HHC00948I
   none – HHC00955E
   none – HHC00956E
   none – HHC00964I
   none – HHC01020E
   none – HHC01026A
   none – HHC01027I
   none – HHC01028E
   none – HHC01029E
   none – HHC01030I
   none – HHC01031I
   none – HHC01047I
   none – HHC01073I
   none – HHC01091E
   none – HHC01101E
   none – HHC01102E
   none – HHC01103E
   none – HHC01104E
   none – HHC01208E
   none – HHC01334I
   none – HHC01335I
   none – HHC01400I
   none – HHC01401I
   none – HHC01402I
   none – HHC01403W
   none – HHC01404S
   none – HHC01406W
   none – HHC01407S
   none – HHC01408S
   none – HHC01409S
   none – HHC01412I
   none – HHC01413I
   none – HHC01414I
   none – HHC01415I
   none – HHC01416I
   none – HHC01417I
   none – HHC01418E
   none – HHC01419E
   none – HHC01427I
   none – HHC01443S
   none - HHC01451E
   none - HHC01452W
   none – HHC01453S
   none – HHC01454S
   none – HHC01455E
   none – HHC01456E
   none – HHC01457E
   none – HHC01476I
   none – HHC01477W
   none – HHC01478I
   none – HHC01479I
   none – HHC01480E
   none – HHC01481I
   none – HHC01482I
   none – HHC01483E
   none – HHC01484I
   none – HHC01485I
   none – HHC01486I
   none – HHC01487I
   none – HHC01488I
   none – HHC01489E
   none – HHC01490I
   none – HHC01491I
   none – HHC01492I
   none – HHC01493I
   none – HHC01505E
   none – HHC01506W
   none – HHC01507W
   none – HHC01525E
   none – HHC01530E
   none – HHC01531I
   none – HHC01532I
   none – HHC01533I
   none – HHC01534I
   none – HHC01535I
   none – HHC01540E
   none – HHC01605E
   none – HHC01606I
   none – HHC01607I
   none - HHC01608W
   none – HHC01609E
   none – HHC01610I
   none – HHC01706I
   none – HHC01723W
   none – HHC01802I
   none – HHC01805I
   none – HHC01806W
   none – HHC01807I
   none – HHC01808I
   none – HHC01809I
   none – HHC01810I
   none – HHC01811I
   none – HHC01812E
   none – HHC01813I
   none – HHC01814E
   none – HHC01815E
   none – HHC01952I
   none – HHC01953E
   none – HHC01954E
   none – HHC02103I
   none – HHC02104I
   none – HHC02105I
   none – HHC02197E
   none – HHC02205I
   none – HHC02206I
   none – HHC02207I
   none – HHC02210I
   none – HHC02211E
   none – HHC02212I
   none – HHC02223I
   none – HHC02226I
   none – HHC02252E
   none – HHC02254I
   none – HHC02255I
   none – HHC02266A
   none – HHC02267I
   none – HHC02268I
   none – HHC02269I
   none – HHC02270I
   none – HHC02271I
   none – HHC02272I
   none – HHC02273I
   none – HHC02275I
   none – HHC02276I
   none – HHC02277I
   none – HHC02278I
   none – HHC02279I
   none – HHC02280I
   none – HHC02281I
   none – HHC02282I
   none – HHC02283I
   none – HHC02284I
   none – HHC02285I
   none – HHC02286I
   none – HHC02287I
   none – HHC02288I
   none – HHC02289I
   none - HHC02290I
   none – HHC02291I
   none – HHC02293I
   none – HHC02294I
   none – HHC02298E
   none – HHC02299E
   none – HHC02300I
   none – HHC02301E
   none - HHC02302W
   none - HHC02303E
   none - HHC02304W
   none - HHC02305E
   none - HHC02306E
   none - HHC02307E
   none - HHC02308W
   none - HHC02309W
   none - HHC02310S
   none - HHC02311I
   none - HHC02312W
   none - HHC02314I
   none - HHC02315I
   none - HHC02316E
   none - HHC02318I
   none - HHC02319I
   none – HHC02386E
   none – HHC02389E
   none – HHC02400E
   none – HHC02401E
   none – HHC02402E
   none – HHC02403E
   none – HHC02404E
   none – HHC02405I
   none – HHC02410I
   none – HHC02411E
   none – HHC02412E
   none – HHC02413E
   none – HHC02414I
   none – HHC02415E
   none – HHC02416E
   none – HHC02417E
   none – HHC02418E
   none – HHC02419E
   none – HHC02420I
   none – HHC02421E
   none – HHC02422I
   none – HHC02423I
   none – HHC02430E
   none – HHC02431E
   none – HHC02432E
   none – HHC02433E
   none – HHC02434E
   none – HHC02435I
   none – HHC02436I
   none – HHC02437I
   none – HHC02438I
   none – HHC02439I
   none – HHC02444E
   none – HHC02445E
   none – HHC02446E
   none – HHC02447E
   none – HHC02448I
   none – HHC02449I
   none – HHC02450I
   none – HHC02451I
   none – HHC02452E
   none – HHC02453W
   none – HHC02454W
   none – HHC02455W
   none – HHC02456E
   none – HHC02457I
   none – HHC02458E
   none – HHC02459E
   none – HHC02460E
   none – HHC02461E
   none – HHC02462I
   none – HHC02463I
   none – HHC02464I
   none – HHC02465E
   none – HHC02465I
   none – HHC02466I
   none – HHC02467I
   none – HHC02468E
   none – HHC02469I
   none – HHC02470E
   none – HHC02471E
   none – HHC02472E
   none – HHC02473E
   none – HHC02474E
   none – HHC02475I
   none – HHC02476E
   none – HHC02477E
   none – HHC02478E
   none – HHC02479E
   none – HHC02480E
   none – HHC02481I
   none – HHC02482I
   none – HHC02483I
   none – HHC02485I
   none - HHC02486I
   none – HHC02487I
   none – HHC02488I
   none – HHC02489E
   none – HHC02490E
   none – HHC02491E
   none – HHC02494I
   none – HHC02495I
   none – HHC02496I
   none – HHC02499I
   none – HHC02500E
   none – HHC02501E
   none – HHC02502E
   none – HHC02503E
   none – HHC02504E
   none – HHC02505E
   none – HHC02506E
   none – HHC02507E
   none – HHC02508E
   none – HHC02509E
   none – HHC02510E
   none – HHC02511E
   none – HHC02512E
   none – HHC02513E
   none – HHC02514E
   none – HHC02515E
   none – HHC02516E
   none – HHC02517E
   none – HHC02518E
   none – HHC02519E
   none – HHC02520I
   none – HHC02521I
   none – HHC02522I
   none – HHC02523I
   none – HHC02524I
   none – HHC02525I
   none – HHC02526I
   none – HHC02527I
   none – HHC02528I
   none – HHC02529I
   none – HHC02530E
   none – HHC02531E
   none – HHC02532E
   none – HHC02533E
   none – HHC02534E
   none – HHC02535E
   none – HHC02536E
   none – HHC02537E
   none – HHC02538E
   none – HHC02539E
   none – HHC02540E
   none – HHC02541E
   none – HHC02542E
   none – HHC02543E
   none – HHC02544E
   none – HHC02545E
   none – HHC02546E
   none – HHC02547E
   none – HHC02548E
   none – HHC02549E
   none – HHC02550I
   none – HHC02551I
   none – HHC02552I
   none – HHC02553I
   none – HHC02554I
   none – HHC02555I
   none – HHC02556I
   none – HHC02557I
   none – HHC02558I
   none – HHC02559E
   none – HHC02560I
   none – HHC02561I
   none – HHC02562I
   none – HHC02563I
   none – HHC02564I
   none – HHC02565I
   none – HHC02566I
   none – HHC02567I
   none – HHC02568I
   none – HHC02569E
   none – HHC02570E
   none – HHC02571E
   none – HHC02572W
   none – HHC02573E
   none – HHC02574E
   none – HHC02575E
   none – HHC02576E
   none – HHC02577E
   none – HHC02578E
   none – HHC02579E
   none – HHC02580E
   none – HHC02581E
   none – HHC02582E
   none – HHC02583E
   none – HHC02584E
   none – HHC02585E
   none – HHC02586E
   none – HHC02587E
   none – HHC02588E
   none – HHC02589I
   none – HHC02590W
   none – HHC02591I
   none – HHC02592I
   none – HHC02593E
   none – HHC02600I
   none – HHC02601I
   none – HHC02602E
   none – HHC02603E
   none – HHC02604E
   none – HHC02605I
   none – HHC02606I
   none – HHC02607I
   none – HHC02608I
   none – HHC02700I
   none – HHC02701E
   none – HHC02702I
   none – HHC02703E
   none – HHC02704I
   none – HHC02705E
   none – HHC02706I
   none – HHC02707E
   none – HHC02708E
   none – HHC02709E
   none – HHC02710E
   none – HHC02711E
   none – HHC02712E
   none – HHC02713E
   none – HHC02714E
   none – HHC02715E
   none – HHC02716E
   none – HHC02717E
   none – HHC02718I
   none – HHC02719I
   none – HHC02720E
   none – HHC02721I
   none – HHC02722I
   none – HHC02723I
   none – HHC02724I
   none – HHC02725I
   none – HHC02726I
   none – HHC02728I
   none – HHC02729I
   none – HHC02730I
   none – HHC02740I
   none – HHC02741E
   none – HHC02742E
   none – HHC02743E
   none – HHC02744I
   none – HHC02745I
   none - HHC02750E
   none - HHC02751I
   none - HHC02752I
   none - HHC02753E
   none - HHC02754E
   none - HHC02755I
   none - HHC02756E
   none - HHC02757I
   none - HHC02800I
   none - HHC02801E
   none - HHC02802I
   none - HHC02803I
   none - HHC02804E
   none - HHC02805I
   none - HHC02806I
   none - HHC03901E
   none - HHC03902E
   none - HHC03903I
   none - HHC03904I
   none - HHC03905I
   none - HHC03906I
   none - HHC03907I
   none - HHC03908I
   none - HHC03909I
   none - HHC03910I
   none - HHC03911I
   none - HHC03912E
   none - HHC03913W
   none - HHC03914W
   none - HHC03915I
   none - HHC03916I
   none - HHC03917W
   none - HHC03918W
   none - HHC03921W
   none - HHC03922W
   none - HHC03923W
   none - HHC03924W
   none - HHC03931W
   none - HHC03932W
   none - HHC03933W
   none - HHC03934W
   none - HHC03935W
   none - HHC03936W
   none - HHC03937W
   none - HHC03952I
   none - HHC03953I
   none - HHC03954I
   none - HHC03983I
   none - HHC03984I
   none - HHC03985E
   none - HHC03991I
   none - HHC03992D
   none - HHC03993D
   none - HHC03995D
   none – HHC04100I
   none – HHC04101I
   none – HHC04102E
   none – HHC04112S
   none – HHC17000E
   none – HHC17001I
   none – HHC17002I
   none – HHC17003I
   none – HHC17004I
   none – HHC17005I
   none – HHC17007I
   none – HHC17008I
   none – HHC17009I
   none – HHC17010I
   none – HHC17011I
   none – HHC17012I
   none – HHC17013I
   none – HHC17100I
   none – HHC17199I
   none – HHC17500I
   none – HHC17501I
   none – HHC17502E
   none – HHC17503E
   none – HHC17504E
   none – HHC17505E
   none – HHC17506E
   none – HHC17507W
   none – HHC17508W
   none – HHC17509W
   none – HHC17510W
   none – HHC17521I
   none – HHC17522I
   none – HHC17523I
   none – HHC17524I
   none – HHC17525I
   none – HHC17526I
   none – HHC17527I
   none – HHC17530E
   none – HHC17531E
   none – HHC17532E
   none – HHC17533E
   none – HHC17534E
   none - HHC90013E
   none - HHC90014I
   none - HHC90015E
   none - HHC90016E
   none - HHC90017I
   none - HHC90018I
   none - HHC90019W
   none - HHC90100D
   none - HHC90101D
   none - HHC90102D
   none - HHC90103D
   none - HHC90104D
   none - HHC90105D
   none - HHC90106D
   none - HHC90107D
   none - HHC90108D
   none - HHC90109D
   none - HHC90110D
   none - HHC90111D
   none - HHC90112D
   none - HHC90190D
   none - HHC90300D
   none - HHC90301D
   none - HHC90302D
   none - HHC90303D
   none - HHC90304D
   none - HHC90305D
   none - HHC90306D
   none - HHC90307D
   none - HHC90308D
   none - HHC90309D
   none - HHC90310D
   none - HHC90311D
   none - HHC90312D
   none - HHC90313D
   none - HHC90314D
   none - HHC90315D
   none - HHC90316D
   none - HHC90317D
   none - HHC90318D
   none - HHC90319D
   none - HHC90320D
   none - HHC90321D
   none - HHC90322D
   none - HHC90323D
   none - HHC90324D
   none - HHC90325D
   none - HHC90326D
   none - HHC90327D
   none - HHC90328D
   none - HHC90329D
   none - HHC90330D
   none - HHC90331D
   none - HHC90332D
   none - HHC90333D
   none - HHC90334D
   none - HHC90335D
   none - HHC90336D
   none - HHC90337D
   none - HHC90338D
   none - HHC90339D
   none - HHC90340D
   none - HHC90341D
   none - HHC90342D
   none - HHC90343D
   none - HHC90344D
   none - HHC90345D
   none - HHC90346D
   none - HHC90347D
   none - HHC90349D
   none - HHC90350D
   none - HHC90351D
   none - HHC90352D
   none - HHC90353D
   none - HHC90354D
   none - HHC90355D
   none - HHC90356D
   none - HHC90357D
   none - HHC90358D
   none - HHC90359D
   none - HHC90360D
   none - HHC90361D
   none - HHC90362D
   none - HHC90363D
   none - HHC90364D



   ## Appendix C. Links

   - The Hercules System/370, ESA/390, and z/Architecture Emulator

http://www.hercules-390.eu

::

   - Hercules source code repositories

https://github.com/rbowler/spinhawk (release 3.xx development stream)
https://github.com/rbowler/sandhawk (release 4.xx development stream)
https://github.com/hercules-390/hyperion (cutting-edge developer
sandbox)

::

   - Hercules Developer Snapshots (Dave Wade)

http://www.smrcc.org.uk/members/g4ugm/snapshots/

::

   - Hercules PDF Documentation (Peter Glanzmann)

http://hercdoc.glanzmann.org

::

   - The MVS Tur(n)key System, Version 3 (Volker Bandke)

http://www.bsp-gmbh.com/turnkey/index.html

::

   - Hercules WinGUI (“Fish”, David B. Trout)

http://www.softdevlabs.com/Hercules/hercgui-index.html

::

   - CTCI-WIN (“Fish”, David B. Trout)

http://www.softdevlabs.com/Hercules/CTCI-WIN-index.html

::

   - Hercules Studio (Jacob Dekel)

http://www.mvsdasd.org/hercstudio

::



   - Hebe – Hercules Image Manager (Robin Atwood)

http://kde-apps.org/content/show.php/Hebe?content=126738

::

   - WinPcap, Politecnico di Torino

http://www.winpcap.org

::

   - Vista tn3270, Tom Brennan Software

http://www.tombrennansoftware.com

::

   - X3270, Paul Mattes

http://x3270.bgp.nu

::

   - AWSBROWSE (“Fish”, David B. Trout)

http://www.softdevlabs.com/Hercules/hercgui-index.html

::

   - XMIT Manager

http://www.cbttape.org

::

   - CBT MVS Utilities Tape (CBTTAPE)

http://www.cbttape.org

::

   - Microsoft Visual C++ 2008 Express

http://www.microsoft.com/express/download/

::



   - ZLIB

http://www.zlib.net
http://www.softdevlabs.com/Hercules/ZLIB1-1.2.3-bin-lib
-inc-vc2008-x86-x64.zip

::

   - BZIP2

http://www.bzip.org
http://www.softdevlabs.com/Hercules/BZIP2-1.0.5-bin-lib
-inc-vc2008-x86-x64.zip

::

   - PCRE

http://www.pcre.org
http://www.softdevlabs.com/Hercules/PCRE-6.4.1-bin-lib
-inc-vc2008-x86-x64.zip

::

   - Regina REXX

http://regina-rexx.sourceforge.net/

::

   - Open Object Rexx (ooRexx)

http://www.oorexx.org/ \``\`
