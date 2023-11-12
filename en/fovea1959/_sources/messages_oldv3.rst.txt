.. _autodoc:

###############
System Messages
###############
 
Overview
========
This page describes the system messages for the Hercules S/370, ESA/390, and z/Architecture emulator.


Message Format
==============
All Hercules-issued messages are of the form ``HHCmmnnns text`` where:

- ``HHC`` is the message prefix for Hercules. All Hercules messages will have this prefix.
- ``mm``  specifies the function that issued the message, from the below list
- ``nnn`` Specific message number, assigned more or less sequentially.
- ``s``  Message severity
   - S  Severe error. Causes immediate termination of Hercules.
   - E  Error. The function being requested did not execute correctly, but Hercules should continue running.
   - W  Warning. Not necessarily an error, but something to take note of and possibly correct.
   - I  Information. General messages that do not require any further action.
   - A  Action. You need to do something.
- text  Message text.

.. csv-table::
  "CA","Communication Adapter emulation"
  "CF","Configuration file processing"
  "CP","CPU emulation"
  "CT","Channel-to-channel adapter emulation"
  "CU","CCKD utility"
  "DA","DASD emulation (both CKD and FBA)"
  "DC","dasdcopy"
  "DG","dyngui.dll"
  "DI","dasdinit"
  "DL","dasdload"
  "DS","dasdisup"
  "DT","dasdcat"
  "DU","DASD utilities common functions"
  "HD","Hercules Dynamic Loader"
  "HE","hetinit"
  "HG","hetget"
  "HM","hetmap"
  "HT","HTTP server"
  "HU","hetupd"
  "IF","hercifc (Network interface configuration handler)"
  "IN","Hercules initialization"
  "LC","LCS emulation"
  "LG","System Log functions"
  "PN","Hercules control panel command messages"
  "PR","Printer emulation"
  "PU","Card punch emulation"
  "RD","Card reader emulation"
  "SD","Socket devices common functions"
  "TA","Tape device emulation"
  "TC","tapecopy"
  "TE","1052 and 3270 terminal emulation"
  "TM","tapemap"
  "TS","tapesplt"
  "TT","TOD Clock and Timer Services"
  "TU","TUN/TAP driver support"
  "VM"," VM/CP emulation facility"


CA Communication Adapter emulation
----------------------------------

HHCCA001I
+++++++++
HHCCA001I CCUU:Connect out to ipaddr:port failed during initial status : System Cause Text
Explanation
HERCULES attempted to make an outgoing TCP connection to ipaddr:port, but the system indicated that there was an error while processing the request.
System Action
The DIAL or ENABLE CCW that caused the connection attempt ends with Unit Check and Intervention Required. The reason for the failure is indicated in the System Cause Text field
Operator Action
None
Programmer Action
Correct the RHOST/RPORT configuration statements in the configuration file. If this message occured during a program initiated DIAL, correct the dial data.
Module
commadpt.c
Function
commadpt_connout


HHCCA002I
+++++++++
HHCCA002I CCUU:Line Communication thread thread id started
Explanation
The thread responsible for asynchronous operations for the BSC emulated line CCUU has been started.
System Action
The system continues
Operator Action
None. This is an informational message
Programmer Action
None. This is an informational message
Module
commadpt.c
Function
commadpt_thread


HHCCA003E
+++++++++
HHCCA003E CCUU:Cannot obtain socket for incoming calls : System Cause Text
Explanation
A system error occured while attempting to create a socket to listen for incoming calls.
System Action
The device creation is aborted.
Operator Action
None.
Programmer Action
Check the System Cause Text for any information relating to the host system. Notify support.
Module
commadpt.c
Function
commadpt_thread


HHCCA004W
+++++++++
HHCCA004W CCUU:Waiting 5 seconds for port port to become available
Explanation
While attempting to reserve port port to listen to it, the system indicated the port was already being used.
System Action
The system waits 5 seconds and then retries the operation
Operator Action
Terminate the device if the port is in error
Programmer Action
Determine the program holding the specified port. If the port cannot be made available, use a different port.


HHCCA005I
+++++++++
HHCCA005I CCUU:Listening on port port for incoming TCP connections
Explanation
The system is now listening on port port for incoming a tcp connection.
System Action
The system continues
Operator Action
None. This is an informational message
Programmer Action
None. This is an informational message


HHCCA006T
+++++++++
HHCCA006T CCUU:Select failed : System Cause Text
Explanation
An error occured during a 'select' system call.
System Action
The BSC thread is terminated
Operator Action
None.
Programmer Action
Check the System Cause Text for any indication of where the error might come from. Notify Support.

HHCCA007W
+++++++++
HHCCA007W CCUU:Outgoing call failed during ENABLE|DIAL command : System Cause Text
Explanation
The system reported that a previously initiated TCP connection could not be completed
System Action
The I/O operation responsible for the TCP outgoing connection is ended with Unit Check and Intervention Required.
Operator Action
If the error indicates that the error is temporary, retry the operation.
Programmer Action
Check that the destination for this line is correctly configured. If the operation was a DIAL attempt, check in the application configuration or operation data.

HHCCA008I
+++++++++
HHCCA008I CCUU:cthread - Incoming Call
Explanation
The BSC thread has received an incoming call.
System Action
Depending on configuration and operational status, the call is either accepted or rejected. Eventually, an ongoign I/O operation may complete.
Operator Action
None. This is an informational message
Programmer Action
None. This is an informational message

HHCCA009I
+++++++++
HHCCA009I CCUU:BSC utility thread terminated
Explanation
The BSC thread has ended
System Action
the system continue.
Operator Action
Refer to any previous error message if this message was not unexpected
Programmer Action
Refer to any previous error message if this message was not unexpected

HHCCA010I
+++++++++
HHCCA010I CCUU:initialisation not performed
Explanation
The Device initialisation process has failed.
System Action
the system terminates or continues, depending on the reason for which the device was initialisation was initiated.
Operator Action
Refer to any previous error message
Programmer Action
Refer to any previous error message

HHCCA011E
+++++++++
HHCCA011E CCUU:Error parsing Keyword
Explanation
The device keyword parser found an error while parsing a known keyword.
System Action
The system continues. The device initialisation routine turns on a NOGO flag.
Operator Action
for a runtime initialisation, correct the device initialisation parameters, otherwise notify the programmer.
Programmer Action
For an engine initialisation, correct the device configuration parameters in the configuration file.

HHCCA012E
+++++++++
HHCCA012E CCUU:Unrecognized parameter Keyword
Explanation
The device keyword parser found an unknown keyword in the device parameter list.
System Action
The system continues. The device initialisation routine turns on a NOGO flag.
Operator Action
for a runtime initialisation, correct the device initialisation parameters, otherwise notify the programmer.
Programmer Action
For an engine initialisation, correct the device configuration parameters in the configuration file.

HHCCA013E
+++++++++
HHCCA013E CCUU:Incorrect local port|remote port|local host|remote host specification value
Explanation
The device initialisation routine could not correctly parse a parameter value.
System Action
The system continues. The device initialisation routine turns on a NOGO flag.
Operator Action
for a runtime initialisation, correct the device initialisation parameters, otherwise notify the programmer.
Programmer Action
For an engine initialisation, correct the device configuration parameters in the configuration file.

HHCCA014E
+++++++++
HHCCA014E CCUU:Incorrect switched/dial specification value; defaulting to DIAL=OUT
Explanation
The device initialisation routine found an incorrect DIAL value.
System Action
The system continues. The device initialisation routine turns on a NOGO flag.
Operator Action
for a runtime initialisation, correct the device initialisation parameters, otherwise notify the programmer.
Programmer Action
For an engine initialisation, correct the device configuration parameters in the configuration file.

HHCCA015E
+++++++++
HHCCA015E CCUU:Missing parameter : DIAL=NO|IN|OUT|INOUT and LPORT|RPORT|LHOST|RHOST not specified
Explanation
The device initialisation routine found that a mandatory parameter was not provided for a specific DIAL Value.
System Action
The system continues. The device initialisation routine turns on a NOGO flag.
Operator Action
for a runtime initialisation, correct the device initialisation parameters, otherwise notify the programmer.
Programmer Action
For an engine initialisation, correct the device configuration parameters in the configuration file.
Note
For DIAL=NO , LPORT, RPORT and RHOST are needed
For DIAL=IN , LPORT is required
For DIAL=OUT None of LPORT,LHOST,RPORT,RHOST are required
For DIAL=INOUT, LPORT is required

HHCCA016W
+++++++++
HHCCA016W CCUU:Conflicting parameter : DIAL=NO|IN|OUT|INOUT and LPORT|RPORT|LHOST|RHOST=value specified
Explanation
The device initialisation routine found that a parameter was provided for a parameter that is not relevant for a specific DIAL Value.
System Action
The parameter is ignored. The system continues
Operator Action
for a runtime initialisation, correct the device initialisation parameters, otherwise notify the programmer.
Programmer Action
For an engine initialisation, correct the device configuration parameters in the configuration file.
Note
For DIAL=IN , RPORT and RHOST are ignored
For DIAL=OUT , LPORT, LHOST, RPORT and RHOST are ignored
For DIAL=INOUT, RPORT and RHOST are ignored

HHCCA017I
+++++++++
HHCCA017I CCUU:LPORT|RPORT|LHOST|RHOST parameter ignored
Explanation
The system indicates that the parameter specified is ignored. This message is preceeded by message HHCCA016W
System Action
The system continues
Operator Action
None
Programmer Action
None

HHCCA018E
+++++++++
HHCCA018E CCUU:Bind failed : System Cause Text
Explanation
While attempting to bind a socket to a specific host/port, the host system returned an uncorrectable error.
System Action
BSC Thread terminates
Operator Action
None
Programmer Action
Check that the LHOST parameter for this device is indeed a local IP address. Otherwise, notify support.

HHCCA019E
+++++++++
HHCCA019E CCUU:BSC comm thread did not initialise
Explanation
The BSC communication thread reported that it terminated while the device was initialising.
System Action
The device is not initialised.
Operator Action
Check for any previously issued error message.
Programmer Action
Check for any previously issued error message.

HHCCA020E
+++++++++
HHCCA020E CCUU:Memory allocation failure for main control block
Explanation
A memory allocation failure occured while attempting to reserve memory for the Communication Adapter control block
System Action
The device is not initialised.
Operator Action
None
Programmer Action
Contact support

HHCCA021I
+++++++++
HHCCA021I CCUU:Initialization failed due to previous errors
Explanation
The initialisation process for device CCUU did not complete succesfully
System Action
The device is not initialised
Operator Action
None
Programmer Action
Refer to any previous error message

HHCCA300D
+++++++++
HHCCA300D Debug Message
Explanation
This is a debug message. CCW Tracing has been turned on for this device and the Line Handler issues debug messages to help diagnose interface, conformance and protocol issues.
System Action
The system continues
Operator Action
If the debug messages are no longer necessary, turn off CCW tracing (panel command : 't-CCUU').
Programmer Action
None


CF Configuration file processing
----------------------------------

HHCCF001S
+++++++++
HHCCF001S Error reading file filename line lineno: error
Meaning
An error was encountered reading the configuration file named filename at line number lineno. The error is described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function read_config

HHCCF002S
+++++++++
HHCCF002S File filename line lineno is too long
Meaning
The line at line number lineno in the configuration file filename is too long and cannot be processed.
Action
Correct the line and restart Hercules.
Issued by
bldcfg.c, function read_config

HHCCF003S
+++++++++
HHCCF003S Cannot open file filename: error
Meaning
The configuration file named filename could not be opened. The error is described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF004S
+++++++++
HHCCF004S No device records in file filename
Meaning
The configuration file named filename does not contain any device definition records. Without them, Hercules cannot do any meaningful work.
Action
Specify one or more device definitions in the configuration file and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF005S
+++++++++
HHCCF005S Unrecognized argument argument
Meaning
An invalid argument, argument, was specified on the HTTPPORT configuration statement in the file named filename at line number lineno. Only the arguments auth and noauth are valid.
Action
Correct the invalid argument and restart Hercules.
Issued by
hsccmd.c, function httpport_cmd

HHCCF008S
+++++++++
HHCCF008S Error in filename line lineno: Unrecognized keyword keyword
Meaning
An invalid configuration statement was specified in the file named filename at line number lineno. The invalid keyword was keyword.
Action
Correct the invalid statement and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF009S
+++++++++
HHCCF009S Error in filename line lineno: Incorrect number of operands
Meaning
The configuration statement at line lineno of the file named filename had an invalid number of operands. For all but the HTTPPORT statement, exactly one operand is required.
Action
Correct the invalid statement and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF010S
+++++++++
HHCCF010S Error in filename line lineno: Unknown or unsupported ARCHMODE specification mode
Meaning
The ARCHMODE configuration statement at line lineno of the file named filename specified an invalid architecture. Only S/370, ESA/390, or ESAME are valid. If one of these was specified, then support for that architecture was excluded when the copy of Hercules in use was compiled.
Action
Correct the specified value and restart Hercules. If the message was issued because support for the desired architecture was excluded, then recompile Hercules.
Issued by
bldcfg.c, function build_config

HHCCF011S
+++++++++
HHCCF011S Error in filename line lineno: serialno is not a valid serial number
Meaning
The serial number serialno specified on the CPUSERIAL configuration statement at line number lineno of the file named filename must be exactly six digits long, and must be a valid hexadecimal number.
Action
Correct the serial number and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF012S
+++++++++
HHCCF012S Error in filename line lineno: modelno is not a valid CPU model
Meaning
The model number modelno specified on the CPUMODEL configuration statement at line number lineno of the file named filename must be exactly four digits long, and must be a valid hexadecimal number.
Action
Correct the model number and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF013S
+++++++++
HHCCF013S Error in filename line lineno: Invalid main storage size size
Meaning
The main storage size size specified on the MAINSIZE configuration statement at line number lineno of the file named filename must be a valid decimal number whose value is at least 2. For 32-bit platforms the value must not exceed 4095.
Action
Correct the main storage size and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF014S
+++++++++
HHCCF014S Error in filename line lineno: Invalid expanded storage size size
Meaning
The expanded storage size size specified on the XPNDSIZE configuration statement at line number lineno of the file named filename must be a valid decimal number between 0 and 16777215. For 32-bit platforms the value must not exceed 4095.
Action
Correct the expanded storage size and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF015S
+++++++++
HHCCF015S Error in filename line lineno: Invalid console port number port
Meaning
The console port number port specified on the CNSLPORT configuration statement at line number lineno of the file named filename must be a valid nonzero decimal number.
Action
Correct the console port number and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF016S
+++++++++
HHCCF016S Error in filename line lineno: Invalid threadname thread priority priority
Meaning
The thread priority priority specified on the xxxPRIO configuration statement at line number lineno of the file named filename must be a valid decimal number.
Action
Correct the priority on the statement and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF017W
+++++++++
HHCCF017W Hercules is not running as setuid root, cannot raise threadname priority
Meaning
A negative value for the threadname thread priority parameter xxxPRIO was specified, but Hercules is not running as the root user (either directly or via the setuid mechanism). This parameter value would cause the priority of the CPU execution thread to be raised above the normal level if Hercules were running as root. Since it is not, however, the parameter will have no effect.
Action
Either specify a positive value to lower the CPU thread priority, zero to not alter the priority, or omit the statement entirely to use the Hercules default CPU thread priority of 15.
Issued by
bldcfg.c, function build_config

HHCCF018S
+++++++++
HHCCF018S Error in filename line lineno: Invalid number of CPUs number
Meaning
The number of emulated CPUs number specified on the NUMCPU configuration statement at line number lineno of the file named filename must be a valid decimal number between 1 and the maximum number (MAX_CPU_ENGS) defined when Hercules was built.
Action
Correct the number of emulated CPUs and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF019S
+++++++++
HHCCF019S Error in filename line lineno: Invalid number of VFs number
Meaning
The number of emulated Vector Facility engines number specified on the NUMVEC configuration statement at line number lineno of the file named filename must be a valid decimal number between 1 and the maximum number defined when Hercules was built (usually 2).
Action
Correct the number of emulated Vector Facility engines and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF020W
+++++++++
HHCCF020W Vector Facility support not configured
Meaning
A request for Vector Facility support was made by the NUMVEC configuration statement, but Hercules was built without the Vector Facility code. The request has been ignored.
Action
If Vector Facility support is desired, recompile Hercules. If not, remove the NUMVEC configuration statement.
Issued by
bldcfg.c, function build_config

HHCCF021S
+++++++++
HHCCF021S Error in filename line lineno: Invalid maximum number of CPUs number
Meaning
The maximum number of emulated CPUs number specified on the MAXCPU configuration statement at line number lineno of the file named filename must be a valid decimal number. It must not exceed the maximum number (MAX_CPU_ENGS) defined when Hercules was built.
Action
Correct the MAXCPU parameter and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF022S
+++++++++
HHCCF022S Error in filename line lineno: epoch is not a valid system epoch
Patch config.c to expand the table.
Meaning
The system epoch epoch specified on the SYSEPOCH configuration statement at line number lineno of the file named filename must be one of the following: 1900, 1928, 1960, 1988, or 1970.
Action
Correct the system epoch and restart Hercules. If a different epoch is desired, a change must be made to the Hercules source file config.c and Hercules rebuilt.
Issued by
bldcfg.c, function build_config

HHCCF023S
+++++++++
HHCCF023S Error in filename line lineno: offset is not a valid timezone offset
Meaning
The system timezone offset offset specified on the TZOFFSET configuration statement at line number lineno of the file named filename must be five characters long, and a valid decimal number of the form (+|-)number, where number must be between zero and 2359 (representing 23 hours, 59 minutes).
Action
Correct the time zone offset and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF024S
+++++++++
HHCCF024S Error in filename line lineno: Invalid TOD clock drag factor drag
Meaning
The TOD clock drag factor drag specified on the TODDRAG configuration statement at line number lineno of the file named filename must be a valid decimal number between 1 and 10000.
Action
Correct the TOD clock drag factor and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF025S
+++++++++
HHCCF025S Error in filename line lineno: Invalid panel refresh rate rate
Meaning
The control panel refresh rate rate specified on the PANRATE configuration statement at line number lineno of the file named filename must be either F, S, or a valid decimal number between 1 and 5000.
Action
Correct the control panel refresh rate and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF026S
+++++++++
HHCCF026S Error in filename line lineno: Unknown OS tailor specification tailor
Meaning
The OS tailoring value tailor specified on the OSTAILOR configuration statement at line number lineno of the file named filename must be either OS/390, z/OS, VSE, VM, LINUX, NULL, or QUIET.
Action
Correct the OS tailoring value and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF027S
+++++++++
HHCCF027S Error in filename line lineno: Invalid maximum device threads threads
Meaning
The maximum device threads threads specified on the DEVTMAX configuration statement at line number lineno of the file named filename must be a valid decimal number greater than -1.
Action
Correct the maximum device threads and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF028S
+++++++++
HHCCF028S Invalid program product OS license setting permission
Meaning
The program product OS permission permission specified on the PGMPRDOS configuration statement must be either LICENSED or RESTRICTED. The alternative spelling LICENCED is also accepted.
Action
Correct the program product OS permission and restart Hercules.
Issued by
hsccmd.c, function pgmprdos_cmd

HHCCF029S
+++++++++
HHCCF029S Invalid HTTP port number port
Meaning
The HTTP server port number port specified on the HTTPPORT configuration statement must be either 80, or a valid decimal number greater than 1024.
Action
Correct the HTTP server port number and restart Hercules.
Issued by
hsccmd.c, function httpport_cmd

HHCCF030S
+++++++++
HHCCF030S Error in filename line lineno: Invalid I/O delay value delay
Meaning
The I/O delay value delay specified on the IODELAY configuration statement at line number lineno of the file named filename must be a valid decimal number.
Action
Correct the I/O delay value and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF031S
+++++++++
HHCCF031S Cannot obtain sizeMB main storage: error
Meaning
An attempt to obtain the amount of main storage specified by MAINSTOR failed for the reason described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF032S
+++++++++
HHCCF032S Cannot obtain storage key array: error
Meaning
An attempt to obtain storage for the array of storage keys failed for the reason described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF033S
+++++++++
HHCCF033S Cannot obtain sizeMB expanded storage: error
Meaning
An attempt to obtain the amount of expanded storage specified by XPNDSTOR failed for the reason described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF034W
+++++++++
HHCCF034W Expanded storage support not installed
Meaning
A request was made for expanded storage by the XPNDSTOR configuration parameter, but Hercules was built without expanded storage support. The request was ignored.
Action
Either remove the XPNDSTOR configuration parameter, or recompile Hercules with expanded storage support included.
Issued by
bldcfg.c, function build_config

HHCCF035S
+++++++++
HHCCF035S Error in filename line lineno: Missing device number or device type
Meaning
The I/O device definition statement at line number lineno of the file named filename did not contain a device number or a device type.
Action
Supply the missing value and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF036S
+++++++++
HHCCF036S Error in filename line lineno: number is not a valid device number(s) specification
Meaning
The I/O device definition statement at line number lineno of the file named filename specified an invalid device number number. The device number must be one to four hexadecimal digits.
Action
Correct the device number and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF037S
+++++++++
HHCCF037S Message pipe creation failed: error
Meaning
An attempt to create a pipe for communication with the control panel failed. The error is described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF038S
+++++++++
HHCCF038S Message pipe open failed: error
Meaning
An attempt to open the pipe for communication with the control panel failed. The error is described by error.
Action
Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF039W
+++++++++
HHCCF039W PGMPRDOS LICENSED specified.
          A licensed program product operating system is running.
          You are responsible for meeting all conditions of your
          software licenses.
Meaning
The configuration parameter PGMPRDOS LICENSED was specified and Hercules has detected that the operating system is a licensed program product. This message is issued to remind you that compliance with the terms of the license for your system's software is your responsibility.
Action
Be sure you know what you're doing.
Issued by
losc.c, function losc_check

HHCCF040E
+++++++++
HHCCF040E Cannot create CPU number thread: error
Meaning
An attempt to create a new thread for execution of CPU number failed. The error is described by error. The CPU has not been added to the configuration.
Action
Correct the error and retry the operation.
Issued by
config.c, function configure_cpu

HHCCF041E
+++++++++
HHCCF041E Device address already exists
Meaning
An attempt was made to define a device at address address. There is already a device at that address.
Action
Either choose another device address, or use the detach command to remove the existing device.
Issued by
config.c, function attach_device

HHCCF042E
+++++++++
HHCCF042E Device type type not recognized
Meaning
An attempt was made to define a device of type type. This device type is not supported by Hercules. It may also indicate that the system was unable to load the device handler for the specified device type.
Action
Specify a supported device type. If the device type is supported, make sure the the system can load the load modules necessary for device operations. Either use the LD_LIBRARY_PATH environment variable or use ldconfig(8) to customize the library search path.
Issued by
config.c, function attach_device

HHCCF043E
+++++++++
HHCCF043E Cannot obtain device block for device address: error
Meaning
An attempt to allocate memory for the control block describing the device with address address failed. The error is described by error. The device has not been defined.
Action
Correct the error and retry the operation.
Issued by
config.c, function attach_device

HHCCF044E
+++++++++
HHCCF044E Initialization failed for device address
Meaning
The device at address address could not be initialized. The device initialization routine has issued a message describing the problem in further detail; refer to that message for more information.
Issued by
config.c, function attach_device

HHCCF045E
+++++++++
HHCCF045E Cannot obtain buffer for device address: error
Meaning
An attempt to allocate memory for the data buffer for the device with address address failed. The error is described by error. The device has not been defined.
Action
Correct the error and retry the operation.
Issued by
config.c, function attach_device

HHCCF046E
+++++++++
HHCCF046E Device address does not exist
Meaning
An attempt was made to remove a device at address address. There is no device at that address.
Action
Choose another device address to remove, if desired.
Issued by
config.c, function detach_device

HHCCF047I
+++++++++
HHCCF047I Device address detached
Meaning
The device at address address has been successfully removed from the system.
Issued by
config.c, function detach_device

HHCCF048E
+++++++++
HHCCF048E Device address does not exist
Meaning
An attempt was made to rename a device at address address. There is no device at that address.
Action
Choose another device address to rename, if desired.
Issued by
config.c, function define_device

HHCCF049E
+++++++++
HHCCF049E Device address already exists
Meaning
An attempt was made to rename a device to address address. There is already a device at that address.
Action
Either choose another device address, or use the detach command to remove the existing device.
Issued by
config.c, function define_device

HHCCF050I
+++++++++
HHCCF050I Device oldaddr defined as newaddr
Meaning
The device which was previously defined with the address oldaddr has been changed to the address newaddr.
Issued by
config.c, function define_device

HHCCF051S
+++++++++
HHCCF051S Error in filename line lineno: verid is not a valid CPU version code
Meaning
The version code verid specified on the CPUVERID configuration statement at line number lineno of the file named filename must be exactly two digits long, and must be a valid hexadecimal number.
Action
Correct the model number and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF052S
+++++++++
HHCCF052S DIAG8CMD invalid option: option
Meaning
The argument option on the DIAG8CMD is invalid. Valid options are enable, disable, echo, and noecho,
Action
Correct the statement and restart Hercules.
Issued by
hsccmd.c, function diag8_cmd

HHCCF053E
+++++++++
HHCCF053E Incorrect second device number in device range near character c
Meaning
The 2nd argument of a device range contains an incorrect device number
Action
Correct the statement and restart Hercules.
Issued by
config.c, function parse_devnums

HHCCF054E
+++++++++
HHCCF054E Incorrect Device count near character c
Meaning
The count field in a device count specification is invalid
Action
Correct the statement and restart Hercules.
Issued by
config.c, function parse_devnums

HHCCF055E
+++++++++
HHCCF055E Incorrect device address specification near character c
Meaning
The first or only CUU in a device specification statement is invalid
Action
Correct the statement and restart Hercules.
Issued by
config.c, function parse_devnums

HHCCF056E
+++++++++
HHCCF056E Incorrect device address range. CUU1>CUU2
Meaning
The first device number of a range is greater than the last device number
Action
Correct the statement and restart Hercules.
Issued by
config.c, function parse_devnums

HHCCF057E
+++++++++
HHCCF057E CUU is on wrong channel (1st device defined on channel CC)
Meaning
At least one of the devices in a device number specification is on a different channel than a previously defined device number within the same specification. All device numbers on a single configuration line must be on a single channel (Group of 256 devices)
Action
Correct the statement and restart Hercules.
Issued by
config.c, function parse_devnums

HHCCF058E
+++++++++
HHCCF058E Some or all devices in CUU-CUU duplicate devices already defined
Meaning
At least one of the device numbers on a device specification statement defines a device number that is already specified on that same statement.
Action
Correct the statement and restart Hercules.
Issued by
config.c, function parse_devnums

HHCCF061W
+++++++++
HHCCF061W ECPS:VM Statement deprecated. Use ECPSVM instead
Meaning
The "ECPS:VM" statement was encountered. This statement is deprecated in favor of the "ECPSVM" statement.
Action
The configuration statement is still carried out, but the statement syntax should be changed as soon as possible.
Issued by
config.c

HHCCF062W
+++++++++
HHCCF062W Missing ECPSVM level value. 20 Assumed
Meaning
The "ECPSVM" statement keyword "LEVEL" was encountered, but no numeric level followed it
Action
The default level of 20 is used, and the ECPS:VM feature is made available. The statement should be corrected as soon as possible.
Issued by
config.c

HHCCF063W
+++++++++
HHCCF063W Specifying ECPSVM level directly is deprecated. Use the 'LEVEL' keyword instead
Meaning
The deprecated "ECPSVM" level syntax form (without the LEVEL keyword) was found.
Action
The ECPS:VM Level is set to the specified value. The configuration statement should be updated to include the "LEVEL" keyword.
Issued by
config.c

HHCCF064W
+++++++++
HHCCF064W Hercules set priority priority failed: error
Meaning
An attempt to change the priority of the Hercules process to priority failed. The error is described by error. The process priority has not been changed. Hercules overall performance may be impaired as a result.
Action
If performance problems are noted, correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF065I
+++++++++
HHCCF065I Hercules: tid=threadid, pid=processid, pgid=processgroupid, priority=priority
Meaning
Hercules thread id is threadid, its process id is processid, its process group id is processgroupid and its execution priority is priority.
Issued by
bldcfg.c, function build_config

HHCCF066E
+++++++++
HHCCF066E Invalid HTTPROOT: error
Meaning
The pathname specified on your HTTPROOT statement is invalid. The error is described by error.
Action
Correct the error and restart Hercules.
Issued by
httpserv.c, function http_server

HHCCF067S
+++++++++
HHCCF067S Incorrect keyword keyword for the ASN_AND_LX_REUSE statement
Meaning
The keyword specified for the ASN_AND_LX_REUSE statement is not ENABLE or DISABLE
Action
Correct the error and restart Hercules.
Issued by
hsccmd.c, function alrf_cmd

HHCCF068E
+++++++++
HHCCF068E Invalid value: value; Enter "help scsimount" for help.
Meaning
The automatic SCSI tape mount value is not "NO" nor a value between 1 and 99 seconds inclusive.
Action
Reissue the SCSIMOUNT command.
Issued by
hsccmd.c, function scsimount_cmd

HHCCF069I
+++++++++
HHCCF069I Run-options enabled for this run
          NUMCPU:           n
          ASN-and-LX-reuse: Enabled/Disabled
          DIAG8CMD:         Enabled/Disabled
Meaning
This message confirms the setting of various run-time options specified in the configuration file at startup time.
Action
None.
Issued by
bldcfg.c, function build_config

HHCCF074E
+++++++++
HHCCF074E Unspecified error occured while parsing Logical Channel Subsystem Identification
Meaning
A logic error occured while parsing the Logical Channel Subsystem Identification component of a device number or device number group.
Action
Notify hercules support. This is an error in the hercules parsing routines.
Issued by
config.c, function parse_lcss

HHCCF075E
+++++++++
HHCCF075E No more than 1 Logical Channel Subsystem Identification may be specified
Meaning
While specifying a device number or device number group, more than 1 ':' character was encountered while parsing the Logical Channel Subsystem Identification component. There can be only one Logical Channel Subsystem Identification for a device or group of devices.
Action
Correct the device number or device number group specification and either reissue the command or restart the hercules engine (depending on whether the error occured while issuing a command or while starting the engine).
Issued by
config.c, function parse_lcss

HHCCF076E
+++++++++
HHCCF076E Non numeric Logical Channel Subsystem Identification XX
Meaning
While specifying a device number or device number group, a non decimal value was encountered while parsing the Logical Channel Subsystem Identification component. The Logical Channel Subsystem Identification for a device or group of devices must be specified as a numeric value.
Action
Correct the device number or device number group specification and either reissue the command or restart the hercules engine (depending on whether the error occured while issuing a command or while starting the engine).
Issued by
config.c, function parse_lcss

HHCCF077E
+++++++++
HHCCF077E Logical Channel Subsystem Identification NN exceeds maximum of 3
Meaning
While specifying a device number or device number group, a Logical Channel Identification was encountered that exceeded the architecture maximum value of MM. The Logical Channel Subsystem Identification for a device or group of devices must be within 0 and 3 (inclusive).
Action
Correct the device number or device number group specification and either reissue the command or restart the hercules engine (depending on whether the error occured while issuing a command or while starting the engine).
Issued by
config.c, function parse_lcss

HHCCF079A
+++++++++
HHCCF079A A licensed program product operating system has been detected. All processors have been stopped.
Meaning
Hercules has detected that the operating system is a licensed program product, but the PGMPRDOS LICENSED parameter was not specified in the Hercules configuration file.
Action
Hercules enters the stopped state. To run this operating system you must obtain a license from the operating system supplier and specify the PGMPRDOS LICENSED parameter in the configuration file. If you are unable to obtain a valid license allowing you to run this operating system on your machine, you must use another operating system (such as MVS3.8J or Linux for System z) which does not require a license.
Issued by
losc.c, function losc_check

HHCCF081I
+++++++++
HHCCF081I fname Will ignore include errors .
Meaning
An ignore include_errors statement was encountered in file fname requesting that any include statements subsequently found within file fname which happen to reference include files which do not exist should simply cause a 

HHCCF084W
+++++++++
HHCCF084W warning instead of a HHCCF085S fatal error.
Action
Processing continues. This is an informational-only message.
Issued by
bldcfg.c, function build_config

HHCCF082S
+++++++++
HHCCF082S Error in fname line nnn: Maximum nesting level (nn) reached
Meaning
The maximum number of nested include statements has been exceeded. The include statement which caused the maximum nesting level of nn to be exceeded is identified as statement number nnn of file fname.
Action
This is a fatal error. Configuration file processing is immediately terminated and Hercules startup is aborted. Correct the error and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF083I
+++++++++
HHCCF083I fname1 Including fname2 at nnn.
Meaning
An include statement for file fname2 was encountered on line nnn of file fname1.
Action
Configuration file processing switches immediately to processing the statements contained in file fname2. Once all of the ststements in file fname2 have been completely processed, configuration file processing will then return to statement nnn+1 of file fname1. This is an informational-only message.
Issued by
bldcfg.c, function build_config

HHCCF084W
+++++++++
HHCCF084W fname1 Open error ignored file fname2: error
Meaning
File fname1 contained an include statement for file fname2 which could not be opened because of error.
Action
Processing continues. This is a informational warning only. Check to make sure the filename specified by fname2 was spelled correctly and restart Hercules if desired.
Issued by
bldcfg.c, function build_config

HHCCF085S
+++++++++
HHCCF085S fname1 Open error file fname2: error
Meaning
File fname1 contained an include statement for file fname2 which could not be opened because of error.
Action
This is a fatal error. Configuration file processing is immediately terminated and Hercules startup is aborted. Correct the possible misspelling of filename fname2 and restart Hercules.
Issued by
bldcfg.c, function build_config

HHCCF086S
+++++++++
HHCCF086S Error in filename: NUMCPU nn must not exceed MAXCPU mm
Meaning
The number of online CPUs nn specified in the NUMCPU configuration statement in the file named filename cannot exceed the maximum number of CPUs mm specified in the MAXCPU configuration statement.
Action
Either decrease the NUMCPU parameter, or increase the MAXCPU parameter, and restart Hercules.
Issued by
bldcfg.c, function build_config


CP CPU emulation
----------------------------------


CT Channel-to-channel adapter emulation
----------------------------------


CU CCKD utility
----------------------------------


DA DASD emulation (both CKD and FBA)
----------------------------------


DC dasdcopy
----------------------------------


DG dyngui.dll
----------------------------------


DI dasdinit
----------------------------------


DL dasdload
----------------------------------


DS dasdisup
----------------------------------


DT dasdcat
----------------------------------


DU DASD utilities common functions
----------------------------------


HD Hercules Dynamic Loader
----------------------------------


HE hetinit
----------------------------------


HG hetget
----------------------------------


HM hetmap
----------------------------------


HT HTTP server
----------------------------------


HU hetupd
----------------------------------


IF hercifc (Network interface configuration handler)
----------------------------------


IN Hercules initialization
----------------------------------


LC LCS emulation
----------------------------------


LG System Log functions
----------------------------------


PN Hercules control panel command messages
----------------------------------


PR Printer emulation
----------------------------------


PU Card punch emulation
----------------------------------


RD Card reader emulation
----------------------------------


SD Socket devices common functions
----------------------------------


TA Tape device emulation
----------------------------------


TC tapecopy
----------------------------------


TE 1052 and 3270 terminal emulation
----------------------------------


TM tapemap
----------------------------------


TS tapesplt
----------------------------------


TT TOD Clock and Timer Services
----------------------------------


TU TUN/TAP driver support
----------------------------------


VM VM/CP emulation facility
----------------------------------


