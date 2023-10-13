Operating Procedure
-------------------

.. note: If you intend to run any licensed software on your PC using Hercules, it is your responsibility to ensure that you do not violate the software vendor's licensing terms!

.. note: Hercules requires privileged access to your host's networking devices in order for Hercules networking to work          | | properly. If your configuration contains any* **networking           | | devices**\ *, then Hercules must be started with* **Administrative   | | (root) privileges**\ *. If Hercules is not started with              | | Administrative (root) privileges then initialization of your         | | networking devices will fail and your guest's networking will not    | | work properly. If your guest does not need access to your host's     | | network Hercules should be run as a normal unprivileged user (the    | | default).*                                                           |

Command line arguments
^^^^^^^^^^^^^^^^^^^^^^

To start Hercules enter this command at the host's command prompt:

   ::

          hercules  [ -f filename ]           |  [ --config=filename ]
                    [ -o logfile]             |  [ --output=logfile ]  |  [ --logfile=logfile ]
                    [ -r rcfile ]             |  [ --rcfile=rcfile ]
                    [ -b logofile ]           |  [ --herclogo=logofile ]
                    [ -d ]                    |  [ --daemon ]
                    [ -e ]                    |  [ --externalgui ]
                    [ -p modpath ]            |  [ --modpath=modpath ]
                    [ -l modname ] ...        |  [ --ldmod=modname ] ...
                    [ -s symbol=value ] ...   |  [ --defsym=symbol=value ] ...
                    [ -v ]                    |  [ --verbose ]
                    [ -h ]                    |  [ --help[=type] ]
                    [ -t[factor]]             |  [ --test[=factor]]

                    [ > logfile ]

where:

   *``filename``*

   is the name of the configuration file. The default, if none is
   specified, is **hercules.cnf**. The default may be overridden via the
   "``HERCULES_CNF``" environment variable. If the value "**none**" is
   specified as the name of the configuration file, then Hercules is
   started without a configuration file using internal default values
   and no devices. Alternatively, specifying the filename as "``NUL``"
   on Windows or "``/dev/null``" on Linux means the same thing as
   specifying "**none**".

   *``logfile``*

   is the name of the optional log file. A log file receives a copy of
   all messages displayed on the Hercules control panel. **PLEASE
   NOTE:** *providing a logfile is extremely important for bug reporting
   and problem analysis purposes! It is* **strongly recommended** *that
   you always specify this option!*

   *``rcfile``*

   is the name of the Hercules `.rc run commands file <#RCFILE>`__. The
   run commands file automatically executes panel commands upon startup.
   If not specified, the value of the "``HERCULES_RC``" environment
   variable is used. If no environment variable is defined, the default
   value "hercules.rc" is used. If the default "hercules.rc" file is not
   found, then the value "**none**" is used, indicating an .rc file will
   not be used.

   *``logofile``*

   is the name of the Hercules logo file. The logo file is the initial
   welcome screen presented when a TN 3270 terminal connects to a
   hercules 3270 device.

   *``--daemon``*

   specifies that Hercules is to be run in 'daemon' mode, wherein it
   runs invisibly with no attached console.

   *``--externalgui``*

   indicates Hercules is to be controlled by an External GUI.

   *``modpath``*

   is the directory from which dynamic modules are to be loaded. This
   option overrides both the ```MODPATH`` <hercconf.html#MODPATH>`__
   configuration file statement and system defaults. The system default
   varies depending on the host platform where Hercules is being run.

   *``modname``*

   is the name of an additional dynamic module to be loaded at startup.
   More than one additional module may be specified, although each must
   be preceded with the ``-l`` option specifier.

   *``symbol=value``*

   the name of a symbol and its associated value to be used in
   configuration file processing or panel commands. See the command
   'defsym' for more information on using symbols. The '-s' option may
   be repeated. Note: 'value' may be quoted to contain imbedded blanks.

   *``--verbose``*

   sets the message-level to verbose. This is the same as entering the
   command ``msglvl +verbose``.

   *``--help[=type]``*

   displays help regarding the syntax of command-line arguments and,
   optionally, other information as well if the optional help ``type``
   is also specified.

   The optional ``type`` value identifies what type of help you want to
   display. Valid values are: ``short``, ``long``, ``version`` or
   ``build``. Additionally, ``all`` and ``full`` are also accepted as
   aliases for ``long``.

   The ``short`` help option displays just the syntax of the the command
   line arguments. The ``version`` help option displays version
   information. The ``build`` option displays some of the more important
   optional features that Hercules was either built with or without. The
   ``long``, ``all`` and ``full`` options displays all three types. The
   default is ``short`` (i.e. only the command-line syntax is shown).

   *``--test[=factor]``*

   starts Hercules in test mode, activating special .rc file script
   commands used only by QA test scripts. Normal Hercules use should
   never specify this switch.

   ``factor`` is an optional test timeout factor within the range 1.0 to
   14.3. The test timeout factor is used to adjust each test script's
   specified timeout value to compensate for the speed of the system on
   which they are running.

   Use a factor greater than 1.0 on slower systems to slightly increase
   timeout values giving each test more time to complete.

   Please note that due to manner in which command line arguments are
   parsed this option must be specified as one argument. Thus "-t2.0" is
   correct whereas "-t  2.0" is not. Oftentimes it is easier to use the
   long ``--test=``\ *``factor``* syntax instead.

   Test timeout values (specified as optional arguments on the special
   runtest script command) are a safety feature designed to prevent
   runaway tests from never ending. Normally tests end automatically the
   very moment they are done.

   *``logfile``*

   is the name of the optional *(but highly recommended!)* log file. The
   log file receives a copy of all messages displayed on the control
   panel and is extremely important to have for problem analysis and bug
   reporting.

Next connect a tn3270 client to the console port (normally port 3270).
The client will be connected to the first 3270 device address specified
in the configuration file (this should be the master console address).
If your master console is a 1052 or 3215, connect a telnet client
instead of a tn3270 client.

Now you can enter an ipl command from the control panel.

| 

--------------

Using the keyboard
^^^^^^^^^^^^^^^^^^

The main Hercules screen contains a scrollable list of messages with a
command input area and system status line at the bottom of the screen.

To scroll through the messages, use either the Page Up or Page Down
keys, the Ctrl + Up Arrow or Ctrl + Down Arrow keys, or the Home or End
and/or the Ctrl + Home or Ctrl + End keys.

Use the Insert key to switch between insert and overlay mode when typing
in the command input area. Use the Home and End keys to move to the
first or last character of the command you are typing, or the use the
left/right arrow keys to move to a specific character. Use the Escape
key to erase the input area.

Pressing Escape when the command input area is already empty causes the
screen to switch to the semi-graphical "New Panel" display mode, which
shows the overall status of the system and devices.

| When in the semi-graphical "New Panel" display mode there is no
  command input area. Instead, single character "hot keys" are used to
  issue some of the more common functions such as starting or stopping
  the CPU. The hot-keys are those which are highlighted. Pressing the
  '?' key displays brief help information on how to use the
  semi-graphical panel.

+------------------------+--------------------------------------------+
| Normal cursor handling |                                            |
+========================+============================================+
| Key                    | Action                                     |
+------------------------+--------------------------------------------+
| Esc                    | Erases the contents of the command input   |
|                        | area. If the command input area is already |
|                        | empty, switches to semi-graphical New      |
|                        | Panel.                                     |
+------------------------+--------------------------------------------+
| Del                    | Deletes the character at the cursor        |
|                        | position.                                  |
+------------------------+--------------------------------------------+
| Backspace              | Erases the previous character.             |
+------------------------+--------------------------------------------+
| Insert                 | Toggles between insert mode and overlay    |
|                        | mode.                                      |
+------------------------+--------------------------------------------+
| Tab                    | Attempts to complete the partial file name |
|                        | at the cursor position in the command      |
|                        | input area. If more than one possible file |
|                        | exists, a list of matching file names is   |
|                        | displayed.                                 |
+------------------------+--------------------------------------------+
| Home                   | Moves the cursor to the start of the input |
|                        | in the command input area. If the command  |
|                        | input area is empty, scrolls the message   |
|                        | area to the top.                           |
+------------------------+--------------------------------------------+
| End                    | Moves the cursor to the end of the input   |
|                        | in the command input area. If the command  |
|                        | input area is empty, scrolls the message   |
|                        | area to the bottom.                        |
+------------------------+--------------------------------------------+
| Page Up                | Scrolls the message area up one screen.    |
+------------------------+--------------------------------------------+
| Page Down              | Scrolls the message area down one screen.  |
+------------------------+--------------------------------------------+
| Up arrow               | Recalls previous command into the input    |
|                        | area.                                      |
+------------------------+--------------------------------------------+
| Down arrow             | Recalls next command into the input area.  |
+------------------------+--------------------------------------------+
| Right arrow            | Moves cursor to next character of input    |
|                        | area.                                      |
+------------------------+--------------------------------------------+
| Left arrow             | Moves cursor to previous character of      |
|                        | input area.                                |
+------------------------+--------------------------------------------+
| Ctrl + Up arrow        | Scrolls the message area up one line.      |
+------------------------+--------------------------------------------+
| Ctrl + Down arrow      | Scrolls the message area down one line.    |
+------------------------+--------------------------------------------+
| Ctrl + Home            | Scrolls the message area to the top.       |
+------------------------+--------------------------------------------+
| Ctrl + End             | Scrolls the message area to the bottom.    |
+------------------------+--------------------------------------------+

| 
| The following additional keyboard functions are effective when the
  Hercules Extended Cursor Handling feature (OPTION_EXTCURS) is
  activated at compile time. At present, this feature is activated on
  the Windows platform only:

+--------------------------+------------------------------------------+
| Extended cursor handling |                                          |
+==========================+==========================================+
| Key                      | Action                                   |
+--------------------------+------------------------------------------+
| Alt + Up arrow           | Moves cursor up one row.                 |
+--------------------------+------------------------------------------+
| Alt + Down arrow         | Moves cursor down one row.               |
+--------------------------+------------------------------------------+
| Alt + Right arrow        | Moves cursor right one column.           |
+--------------------------+------------------------------------------+
| Alt + Left arrow         | Moves cursor left one column.            |
+--------------------------+------------------------------------------+
| Tab                      | If cursor is outside the command input   |
|                          | area, moves cursor to the start of the   |
|                          | input in the command input area.         |
|                          | Otherwise behaves as described in        |
|                          | previous table.                          |
+--------------------------+------------------------------------------+
| Home                     | If cursor is outside the command input   |
|                          | area, moves cursor to the start of the   |
|                          | input in the command input area.         |
|                          | Otherwise behaves as described in        |
|                          | previous table.                          |
+--------------------------+------------------------------------------+
| End                      | If cursor is outside the command input   |
|                          | area, moves cursor to the end of the     |
|                          | input in the command input area.         |
|                          | Otherwise behaves as described in        |
|                          | previous table.                          |
+--------------------------+------------------------------------------+

Panel commands
^^^^^^^^^^^^^^

The following is what is displayed on the Hercules hardware console
(HMC) in response to the '?' command being entered. Please note that it
may not be completely accurate or up-to-date. Enter the '?' command for
yourself for a more complete, accurate and up-to-date list of supported
panel commands:

::


        Command               Description
        ----------------      -----------------------------------------------
        !message             *SCP priority message
        #                     Silent comment
        $locate               Display sysblk, regs or hostinfo
        $runtest             *Start the test if test mode is active
        $test                *Your custom command (*DANGEROUS!*)
        $zapcmd              *Enable/disable command (*CAREFUL!*)
        *                     Loud comment
        .reply               *SCP command
        ?                     alias for help
        abs                  *Display or alter absolute storage
        aea                   Display AEA tables
        aia                   Display AIA fields
        alrf                  Command deprecated. Use facility command instead
        ar                    Display access registers
        archlvl              *Set or Query current Architecture Mode
        archmode              Deprecated. Use the archlvl command instead
        asn_and_lx_reuse      Command deprecated. Use facility command instead
        attach               *Configure device
        auto_scsi_mount      *Command deprecated - Use "SCSIMOUNT"
        autoinit             *Display/Set auto-create-empty-tape-file option
        automount            *Display/Update allowable tape automount directories
        b                    *Set breakpoint
        b+                    (Synonym for 'b')
        b-                    Delete breakpoint
        b?                    Query breakpoint
        cachestats            Cache stats command
        cckd                 *Compressed CKD command
        cctape               *Display a printer's current cctape
        cf                   *Configure current CPU online or offline
        cfall                 Configure all CPU's online or offline
        clocks                Display tod clkc and cpu timer
        cmdlvl               *Display/Set current command group
        cmdsep               *Display/Set command line separator
        cmpscpad             *Set/display the CMPSC zero padding value.
        cnslport              Set console port
        codepage             *Set/display code page conversion table
        conkpalv             *Display/alter console TCP keepalive settings
        cp_updt              *Create/Modify user character conversion table
        cpu                  *Define target cpu for panel display and commands
        cpuidfmt              Set format BASIC/0/1 STIDP generation
        cpumodel              Set CPU model number
        cpuprio              *(deprecated)
        cpuserial             Set CPU serial number
        cpuverid             *Set CPU verion number
        cr                   *Display or alter control registers
        cscript              *Cancels a running script thread
        ctc                  *Enable/Disable CTC debugging
        define               *Rename device
        defsym               *Define symbol
        delsym               *Delete a symbol
        detach               *Remove device
        devinit              *Reinitialize device
        devlist              *List device, device class, or all devices
        devprio              *(deprecated)
        devtmax              *Display or set max device threads
        diag8cmd             *Set DIAG 8 instruction options
        ds                    Display subchannel
        dumpdev              *Specify bootstrap loader DUMP parameters
        ecps:vm              *Command deprecated - Use "ECPSVM"
        ecpsvm               *ECPS:VM Commands
        engines               Set engines parameter
        evm                  *Command deprecated - Use "ECPSVM"
        exec                 *Execute a Rexx script
        exit                  (Synonym for 'quit')
        ext                   Generate external interrupt
        f?                    Query unusable page frame range(s)
        facility             *Enable/Disable/Query z/Arch STFLE Facility bits
        fcb                  *Display a printer's current FCB
        fpc                  *Display or alter floating point control register
        fpr                  *Display or alter floating point registers
        f{+/-}adr            *Mark page frame(s) as +usable/-unusable
        g                     Turn off instruction stepping and start all CPUs
        gpr                  *Display or alter general purpose registers
        hao                  *Hercules Automatic Operator
        help                 *list all commands / command specific help
        herclogo             *Read a new hercules logo file
        hercnice             *(deprecated)
        hercprio             *(deprecated)
        hst                  *History of commands
        http                 *Start/Stop/Modify/Display HTTP Server
        hwldr                *Specify boot loader filename
        i                     Generate I/O attention interrupt for device
        iodelay              *Display or set I/O delay value
        ipending              Display pending interrupts
        ipl                  *IPL from device or file
        iplc                 *Command deprecated - use IPL with clear option
        k                     Display cckd internal trace
        ldmod                *Load a module
        legacysenseid         Set legacysenseid setting
        loadcore             *Load a core image file
        loaddev              *Specify bootstrap loader IPL parameters
        loadparm             *Set the default IPL 'LOADPARM' parameter
        loadtext             *Load a text deck file
        locks                *Display internal locks list
        log                  *Direct logger output
        logopt               *Set/Display logging options
        lparname             *Set LPAR name
        lparnum              *Set LPAR identification number
        lsdep                 List module dependencies
        lsequ                 List device equates
        lsmod                *List dynamic modules
        mainsize             *Define/Display mainsize parameter
        manufacturer          Set STSI manufacturer code
        maxcpu                Set maxcpu parameter
        maxrates             *Display highest MIPS/SIOS rate or set interval
        message              *Display message on console a la VM
        model                *Set/Query STSI model code
        modpath              *Set module load path
        mounted_tape_reinit  *Control tape initialization
        msg                   Alias for message
        msglevel             *Display/Set current Message Display output
        msglvl                Alias for msglevel
        msgnoh                Similar to "message" but no header
        mt                   *Control magnetic tape operation
        netdev               *Set default host networking device
        numcpu                Set numcpu parameter
        osa                  *(Synonym for 'qeth')
        ostailor             *Tailor trace information for specific OS
        o{+/-}dev             Turn ORB tracing on/off
        panopt               *Set or display panel options
        panrate               (deprecated; use PANOPT RATE=nnn instead)
        pantitle              (deprecated; use PANOPT TITLE=xxx instead)
        pgmprdos             *Set LPP license setting
        pgmtrace             *Trace program interrupts
        plant                 Set STSI plant code
        pr                   *Display or alter prefix register
        psw                  *Display or alter program status word
        ptp                  *Enable/Disable PTP debugging
        ptt                  *Activate or display internal trace table
        qcpuid               *Display cpuid(s)
        qd                   *Query device information
        qeth                 *Enable/Disable QETH debugging
        qpfkeys               Display the current PF Key settings
        qpid                  Display Process ID of Hercules
        qports                Display TCP/IP ports in use
        qproc                 Display processors type and utilization
        qstor                 Display main and expanded storage values
        quiet                *Toggle automatic refresh of panel display data
        quit                 *Terminate the emulator
        r                    *Display or alter real storage
        restart               Generate restart interrupt
        resume                Resume hercules
        rexx                 *Modify/Display Hercules's Rexx settings
        rmmod                 Delete a module
        s                    *Instruction stepping
        s+                   *Activate instruction stepping
        s-                    Turn off instruction stepping
        s?                   *Query instruction stepping
        savecore             *Save a core image to file
        sclproot             *Set SCLP base directory
        scpecho              *Set/Display option to echo to console and history of scp replys
        scpimply             *Set/Display option to pass non-hercules commands to the scp
        script               *Run a sequence of panel commands contained in a file
        scsimount            *Automatic SCSI tape mounts
        sf+dev               *Add shadow file
        sf-dev               *Delete shadow file
        sfc                  *Compress shadow files
        sfd                  *Display shadow file stats
        sfk                  *Check shadow files
        sh                   *Shell command
        shcmdopt             *Set shell command options
        shrd                 *shrd command
        shrdport             *Set shrdport value
        sizeof                Display size of structures
        srvprio              *(deprecated)
        ssd                  *Signal shutdown
        start                *Start CPU (or printer/punch device if argument given)
        startall              Start all CPU's
        stop                 *Stop CPU (or printer/punch device if argument given)
        stopall               Stop all CPU's
        store                 Store CPU status at absolute zero
        suspend               Suspend hercules
        symptom               Alias for traceopt
        sysclear             *System Clear Reset manual operation
        sysepoch              Set sysepoch parameter
        sysreset             *System Reset manual operation
        s{+/-}dev             Turn CCW stepping on/off
        t                    *Set tracing range or Query tracing
        t+                   *Turn on instruction tracing
        t+-                  *Automatic instruction tracing
        t-                    Turn off instruction tracing
        t?                   *Query instruction tracing values
        threads              *Display internal threads list
        timerint             *Display or set timers update interval
        tlb                   Display TLB tables
        toddrag               Display or set TOD clock drag factor
        todprio              *(deprecated)
        traceopt             *Instruction and/or CCW trace display option
        tt32                 *Control/query CTCI-WIN functionality
        txf                  *Transactional-Execution Facility tracing
        tzoffset              Set tzoffset parameter
        t{+/-}CKD [devnum]    Turn CKD Search Key tracing on/off
        t{+/-}dev             Turn CCW tracing on/off
        u                    *Disassemble storage
        uptime                Display how long Hercules has been running
        v                    *Display or alter virtual storage
        version               Display version information
        xpndsize             *Define/Display xpndsize parameter
        yroffset              Set yroffset parameter

         (*)  Enter "help <command>" for more info.

The *ipl* command may also be used to perform a load from cdrom or
server. For example if a standard SuSE S/390 Linux distribution CD is
loaded and mounted on /cdrom for example, this cdrom may then be ipl-ed
by: *ipl /cdrom/suse.ins*

The *attach* and *detach* commands are used to dynamically add or remove
devices from the configuration, and the *define* command can be used to
alter the device number of an existing device.

The *devinit* command can be used to reopen an existing device. The
*args* (if specified) override the arguments specified in the
configuration file for this device. The device type cannot be changed
and must not be specified. This command can be used to rewind a tape, to
mount a new tape or disk image file on an existing device, to load a new
card deck into a reader, or to close and reopen a printer or punch
device.

In single-step mode, pressing the enter key will advance to the next
instruction.

There is also an alternate semi-graphical control panel. Press Esc to
switch between the command line format and the semi-graphical format.
Press ? to obtain help in either control panel.

| When a command is prefixed with '-', the the command will not be
  redisplayed at the console. This can be used in scripts and is also
  used internally when commands are to be invoked without being
  redisplayed at the panel.
|  **Additional Command Help**
| Some commands also offer additional help information regarding their
  syntax, etc. Enter  "``help``\ *``<command name>``*"   to display this
  additional help information. (Note: not every command supports
  additional help)

--------------

The  hercules.rc  (run-commands)  file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Hercules also supports the ability to automatically execute panel
commands upon startup via the 'run-commands' file. If the run-commands
file is found to exist when Hercules starts, each line contained within
it is read and interpreted as a panel command exactly as if the command
were entered from the HMC system console.

The default filename for the run-commands file is "hercules.rc", but may
be overridden by setting the "**``HERCULES_RC``**" environment variable
to the desired filename.

Except for the 'pause' command (see paragraph further below), each
command read from the run-commands file is logged to the console
preceded by a '> ' (greater-than sign) character so you can easily
distinguish between panel commands entered from the keyboard from those
entered via the .rc file.

Lines starting with '``#``' are treated as "silent comments" and are
thus not logged to the console. Line starting with '``*``' however are
treated as "loud comments" and *will* be logged.

| In addition to being able to execute any valid panel command
  (including the 'sh' shell command) via the run-commands file, an
  additional '**``pause``\ ``nnn``**' command is supported in order to
  introduce a brief delay before reading and processing the next line in
  the file. The value *``nnn``* can be any number from 0.001 to 999.0
  and specifies the number of seconds to delay before reading the next
  line. Creative use of the run-commands file can completely automate
  Hercules startup.

--------------

The "Hercules Automatic Operator" (HAO) Facility
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Hercules Automatic Operator (HAO) feature is a facility which can
automatically issue panel commands in response to specific messages
appearing on the Hercules console.

To use the Hercules Automatic Operator facility, you first define a
"rule" consisting of a "target" and an associated "command". The
"target" is a regular expression pattern used to match against the text
of the various messages that Hercules issues as it runs. Whenever a
match is found, the rule "fires" and its associated command is
automatically issued.

The Hercules Automatic Operator facility only operates on messages
issued to the Hercules console. These messages may originate from
Hercules itself, or from the guest operating system via the SCP SYSCONS
interface or via the integrated console printer-keyboard (3215-C or
1052-C). HAO cannot intercept messages issued by the guest operating
system to its own terminals.

Defining a Rule
'''''''''''''''

To define a HAO rule, enter the command:

::

      hao tgt target

to define the rule's "target" match pattern followed by the command:

::

      hao cmd command

to define the rule's associated panel-command.

The *target* is a regular expression as defined by your host platform.
When running on Linux, Hercules uses POSIX Extended Regular Expression
syntax. On a Windows platform, regular expression support is provided by
Perl Compatible Regular Expression (PCRE). The HAO facility can only be
used if regular expression support was included in Hercules at build
time.

The associated *command* is whatever valid Hercules panel command you
wish to issue in response to a message being issued that matches the
given *target* pattern.

Substituting substrings in the command
''''''''''''''''''''''''''''''''''''''

The *command* may contain special variables $1, $2, etc, which will be
replaced by the values of "capturing groups" in the match pattern. A
capturing group is a part of the regular expression enclosed in
parentheses which is matched with text in the target message. In this
way, commands may be constructed which contain substrings extracted from
the message which triggered the command.

The following special variables are recognized:

-  ``$1`` to ``$9`` - the text which matched the 1st to 9th capturing
   group in the target regular expression
-  :literal:`$\`` - the text preceding the regular expression match
-  ``$'`` - the text following the regular expression match
-  ``$$`` - replaced by a single dollar sign

Note that substitution of a $\ *n* variable does not occur if there are
fewer than *n* capturing groups in the regular expression.

As an example, the rule below issues the command "``i 001F``" in
response to the Hercules message
"``HHC01090I 0:001F COMM: client 127.0.0.1 devtype 3270: connection reset``":

::

      hao tgt HHC01090I .:([0-9A-F]{4}) COMM: .* connection reset
      hao cmd i $1

Another example, shown below, illustrates how the dot matrix display of
a 3590(?) tape unit might be used to implement an automatic tape library
in response to the Hercules message
"``HHC00224I 0:0581 Tape file *, type HET: display "K2DSBK2 " / "M2DSBK3S" (alternating)``":

::

      hao tgt HHC00224I .:([0-9A-F]{4}) Tape file .*: display (?:".{8}" \/ )?"M([A-Z0-9]{1,6})\s*S"
      hao cmd devinit $1 /u/tapes/$2.aws

Which would result in the Hercules command
"``devinit 0581 /u/tapes/2DSBK3.aws``" being automatically issued.

More information about Perl Compatible Regular Expression (PCRE) syntax
(as well as a nice online web page that allows you to test your
expressions) can be found here:

-  `PCRE Regex
   Cheatsheet <https://www.debuggex.com/cheatsheet/regex/pcre>`__
-  `Online PCRE test page <https://regex101.com/>`__

Other commands and limitations
''''''''''''''''''''''''''''''

To delete a fully or partially defined HAO rule, first use the
"``hao list``" command to list all of the defined (or partially defined)
rules, and then use the "``hao del``\ *``nnn``*" command to delete the
specific rule identified by *nnn* (all rules are assigned numbers as
they are defined and are thus identified by their numeric value).
Optionally, you can delete all defined or partially defined rules by
issuing the command "``hao clear``".

The current implementation limits the total number of defined rules to
64. This limit may be raised by increasing the value of the
``HAO_MAXRULE`` constant in source file ``hao.c`` and then rebuilding
Hercules.

| All defined rules are checked for a match each time Hercules issues a
  message. There is no way to specify "stop processing subsequent
  rules". If a message is issued that matches two or more rules, each
  associated command is then issued in sequence.

--------------
