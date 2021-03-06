# LPIC 1

### Learning Bank: <https://testbanks.wiley.com/WPDACE/Dashboard>

- [x] Assessment Test (19.00/30) :-(
- [x] Chapter 1 - Command Line Tools (17/20) :-| (85%)
- [ ] Chapter 2 - Managing Software

#### Chapter 1 - Command Line Tools

##### 103.1 Work on the command line

###### Bash Basics

```bash
time ls

aur  Desktop  Downloads
ls  0.00s user 0.00s system 83% cpu 0.001 total
```

```bash
set --> show all settings
'!'=0
'#'=0
'$'=6543
'*'=(  )
-=569BJXZims
0=/bin/zsh
'?'=0
@=(  )
ARGC=0
CDPATH=''
COLORTERM=truecolor
COLUMNS=81
CPUTYPE=x86_64
DBUS_SESSION_BUS_ADDRESS='unix:path=/run/user/1000/bus'
DESKTOP_AUTOSTART_ID=1060acfdeed34b555e155293683288317900000007100002
DESKTOP_SESSION=mate
DISPLAY=:0.0
EGID=1000
EUID=1000
FIGNORE=''
...
```

```bash
type pwd
pwd is a shell builtin

type -a pwd
pwd is a shell builtin
pwd is /usr/bin/pwd
pwd is /bin/pwd
```

- Use CTRL+G to cancel reverse search in shell
- Use CTRL+T to shift a letter to the right
- Use ESC and T to change to words
- Use ESC and U to UPPERCASE a word
- Use ESC and L to lowercase

Standard Bash Profile: /etc/profile
User Profile: .bashrc

###### Environment

```bash
env
XDG_SESSION_ID=820
HOSTNAME=XXXXX
TERM=xterm
SHELL=/bin/bash
HISTSIZE=1000
SSH_CLIENT=XXXXXXXX
QTDIR=/usr/lib64/qt-3.3
...
```

```bash
echo $TERM
xterm
```

```bash
echo $PS1
[\u@\h \W]\$ --> PROMPT: [user@host workingdirectory]
```

```bash
export VARNAM="VALUE" to set an env variable
unset $VARNAME to unset an env variable
```

###### Man pages

- SPACE to move forward a page
- ESC and V to go back a bage

```bash
man -P /bin/vim uname
--> opens man page in vim
```

```bash
man -k "system information"
dumpe2fs (8)         - dump ext2/ext3/ext4 filesystem information
...
uname (1)            - print system information
```

- Man page numbers go from 1 to 9

| Number | Description                            |
| ------ | -------------------------------------- |
| 1      | executable programs and shell commands |
| 2      | system calls                           |
| 3      | library calls                          |
| 4      | device files /dev                      |
| 5      | file formats                           |
| 6      | games                                  |
| 7      | misc                                   |
| 8      | sysadmin commands                      |
| 9      | kernel routines                        |

- info is the same as man --> info info
- help pages for bash builtins help pwd

##### 103.3 Use streams, pipes and redirects

###### File descriptors

- Input and output are streams and can be handled as files

| Type | Description |
| --- | --- |
| Standard Input | STDIN - in most cases the keyboard - file descriptor 0 |
| Standard Output | STDOUT - in most cases the screen/terminal - file descriptor 1 |
| Standard Error | STDERR - in most cases the same as STDOUT - file descriptor 2|

- programs use file descriptors as files and can be redirected

Redirect STDOUT with 1>

Redirect STERR with 2>

Redirect STDOUT and STDERR with &>

Append with >>

< /path/to/fileorprogram to use as STDIN

```bash
echo $PATH | tee path.txt
--> cat path.txt == STDOUT
```

###### Pipes and substitution

```bash
find . -iname *.log | xargs rm --> rm all results from find
```

```bash
rm $(find . -iname *.log) --> spawns subshell. Dont use backticks
```

##### 103.2 Process text streams, pipes and redirects

```bash
cat first.txt second.txt > combined.txt
```

- cat -E shows Line Ends
- cat -n shows line number --> make an alias for this
- cat -T shows tabs an
- join merges matching fields in files --> comparable to SQL SELECT * FROM 1,2 WHERE 1.username == 2.username
- expand -t 2 converts tabs to 2 spaces --> unexpand -t 2 does the reverse
- od shows octal dump / hex values with -x

```bash
 od -x test
0000000 2023 ... 766e
0000020 6e65 ... 4c53
0000040 5345 ... 6b2e
....
0000430
```

```bash
ls -al | sort -k 5 -n --> sort ls by file size (numeric)
```

- split --> by bytes, lines
- translate --> ???
- uniq --> get rid of duplicates lines
- fmt --> cleans up files, -width CHARSINONELINE
- nl == cat -n but with way more options
- pr --> prepare for printing, shows header, footer, etc --> lpr for actually printing --> genscript for postscript

```bash
ifconfig eth0 | grep HWaddr | cut -d " " -f 11
00:0C:76:96:A3:73
```

```bash
 wc repoindex.xml
 2  5 63 --> LINES WORDS CHARS
```

##### 103.4 Search text files using RegEx

##### grep

```bash
ip addr sh eth0 | grep -i ETHER
    link/ether 00:50:56:8d:2d:76 brd ff:ff:ff:ff:ff:ff --> case insensitive

ip addr sh eth0 | grep -ic ETHER
1 --> count lines

ip addr sh eth0 | grep -ic -f FILENAME
0 --> matches expr in filename
```

- grep -r PATTERN --> find PATTERN in files recursively
- grep -E "REGEX" --> for more complex regex

###### sed

- modifies a files contents and shows changes at STDOUT

```bash
sed a\text test.txt --> append text to file
sed i\text test.txt --> insert text to file
sed 's\regex\replacement\g' --> replace all occurencys of regex with replacement
sed c\text test.txt --> replace range of lines with text

sed r filename test.txt --> append text from filename to file
sed w filename test.txt --> write pattern into file
sed q --> quit script
sed Q --> quit script without printing the current pattern
```

#### Chapter 2 - Managing Software

##### 102.3 - Managed shared libraries

Package management consists of mainly the following components:

- Package: tarball containing the necessary binaries
- Database: List of installed files on the computer
- Dependencies: List of which packages rely on each other
- Checksum: Hashes to prove the integrity of the packages

It offers you:

- Installation/Upgrades/Removal of packages
- Package building

###### RPM

RPM Package Manager usually has the convention of packagename-a.b.c.-x.arch.rpm which translates to name-version.number-buildnumber.architecture.rpm
You can use RPM packages on all RPM distros (like SUSE) - it's not recommended, though. The RPM utilities could be different, dependencies like to be named differently, different init systems etc.

```bash
rpm -i/U packagename --> install/upgrade a package
rpm -qi packagename --> query if a package is installed (with i for more information)
rpm -e packagename --> remove a package
rpm --rebuilddb --> rebuild the rpm db
```

Yum and dnf are most commonly used. No need to download rpm packages manually, just install them out of a repo

```bash
yum install/update/remove/list/check-update/clean --> pretty self explanatory
```

Repos are stored in /etc/yum.repos.d/REPONAME

Yum itself ist configured by editing the /etc/yum.conf file.

###### Building Packages

Building packages is often done when compiling a program from source to use special compiler flags to improve performance with CPU flags and still manage the program with the package manager. Packages out of a repo are generally compiled to maximize support to the underlying operating system architecture.

###### Debian Packages

.deb Packages are manipulated with dpkg

```bash
dpkg -i --> install
dpkg -r --> remove
dpkg -P --> purge (including config files)
dpkg -p --> print information on installed package
dpkg -l PATTERN --> list all matched packages
```

Like yum, there exists apt to handle package downloading and upgrades for you from a repo. it works pretty much the same way:

```bash
apt install/remove/update/upgrade/clean
```

Repos are stored in /etc/apt/sources.list

Packages often comen with an initial configuration. This config can be altered by running dpkg-reconfigure
PACKAGENAME

Deb packages consist of a source tarball, a patch file to modify the source code and a signature.
Binary packages are created with the debian package tools like .

Overall, debian based distribution have a higher compatibility of packages than RPM based distros.

Config file for apt lies in /etc/apt/apt.conf and uses BIND server config file layout.

The program alien makes it possible to convert packages from deb to RPM and vice versa.
Compiling from source or building a package on your own might be a better choice here.

###### Libraries

Libraries are shared across multiple programs to reduce space on local storage devices and RAM as well.
These Shared libraries are called dynamic libraries and usually end with .so which stands for shared object.
Static libraries used by linkers to include them in their program use to have .a as filename extension.

Libraries with major upgrades are installed alongside their older versions. See libc.so.5 libc.so.6 etc.

Paths to libraries are maintained in either /etc/ld.so.conf or /etc/ld.so.conf.d/
and can be placed there with NAME.conf. The content is a LDPATH variable??

After changing a library's path, `ldconfig` has to be run.

LD_LIBRARY_PATH env variable specifies additional locations on your filesystem to look for libraries for example:

```bash
export LD_LIBRARY_PATH=/home/username/testlib:/opt/newlib
```

Linker version mismatches can be resolved using symlinks:

```bash
ln -s examplelib.so.5.2 examplelib.so.5
ldconfig
```

###### Library Management

`ldd /bin/ls` displays shared library dependencies
ldconfig also rebuilds /etc/ld.so.cache when adding/removing entries to /etc/ld.so.conf

#### Process Management

Understanding uname

| Name | Description |
| --- | --- |
| Node Name | -n shows hostname |
| Kernel Name | -s shows kernel name (linux/darwin) |
| Kernel Version | -v shows kernel build date and time |
| kernel Release | -r shows release version |
| Machine | -m shows architecture |
| Processor | -p shows maufacturer, speed, model or unknown |
| Hardware Platform | -i shows information or unknown |
| OS Name | -o shows os name (GNU/Linux) |
| All | -a prints all above information |

To gain information about processes use `ps` with it's most common parameters - mostly without dashes (BSD legacy)

```bash
ps faux --> all processes, extra information, as process tree
ps u USERNAME --> processes owned by USERNAME
username 2498 0.0 0.8 1860 1044 pts/1 S 16:17 0:00 bash
```

The output gives you the username, process id, parent process id, cpu time, memory use, tty, command

`top` can also be used and takes multiple keystrokes, for example `M` / `P` to sort by memory consumption/CPU time
or `k` to kill a process.

##### fg and bg

`CTRL+Z`pauses the program and sends it to the background of the terminal. `fb` gets it back to the foreground.
Run commands with space and ampersand at the end to launch them in bg directly (`cat file.txt &`).

Process priorities can be managed by their niceness. To set the niceness when launching a program the `nice` command is prepended (`nice -n 12 programname`) or `renice -15 -p PID` if the process already launched. -20 is the highest priority an 19 the lowest.

###### Killing Processes

`kill -s signal PID` while signal is usually the SIGKILL signal (also known as 9). 
Other signals such as SIGHUP and SIGTERM can be sent as well
(Kill process and reload config / kill process and close opened files)

You can run a program after logging out/terminating your session with `nohup program` so the 
program will ignore any signals received by the kernel.

### Configuring Hardware

#### 101.1 Determine and configure hardware settings

##### Configuring the firmware and core hardware

Most computers use UEFI, many VMs still use BIOS. This firmware is produced by the hardware's manufacturer.
It gets all the devices in the computer ready and performs basic checking. Once Linux boots, it uses own drivers to communicate with the hardware.

##### Interrupts

Interrupt requests or IRQ is a signal sent to the CPU to stop current activity and handle a certain event.
There exist multiple interrupts to handle mouse or keyboard events etc. Interrupts are listed in `/proc/interrupts`

Using IRQs requires a driver for a certain device (network, videocard, etc). Devices should not use the same IRQ to prevent conflicts.

##### I/O Addresses

I/O Addresses are unique locations in memory, reserved for CPU and hardware communication. Like IRQs, they should not be shared.
The I/O adresses can be checked by running `cat /proc/ioports` which - for example - delivers 0060-006f for the keyboard

##### DMA Adresses

Direct memory addressing can be use alternatively to communicate to I/O ports but does not rely on the CPU as a transport medium and can hereby improve the system's performance.
DMA are visible in `/proc/dma`. Like IRQ and I/O addresses, they should not be shared.

#### 102.1 Design hard disk layout

##### Boot Disks and Geometry Settings

BIOS uses a boot sector (first sector of the disk) and executes the code written in there. EFI uses a specific partition called ESP. EFI is more flexible since this partition could be present in NVRAM.

Hard disks use a CHS geometry (cylinder/head/sector). Each head uses a track (circle on the platter). All tracks combined make up the cylinder. Tracks consist of sectors, so each sector is addressable by telling which cylinder number, head number and sector number you need.

Nowadays, the values presented to the BIOS are not a representation of the real sectors on the disk. LBA (logical block addressing is the replacement for CHS. It assigns a unique number to each sector and the disk firmware handles the correct head and cylinder.

##### Cold- and Hotplugging

Coldplug devices can only be attached if the computer is turned off, hotplug devices can be added while the computer is running.

Multiple components handle hotplugging:

- sysfs virtual filesystem at `/sys` exports device information, similar to `/proc`.
- HAL Daemon (Hardware Abstraction Layer) provides information about available hardware
- D-Bus provides hardware information like hald but enables processes to be notified by events like a plugged in USB stick
- udev is a virtual filesystem at `/dev` and creates dynamic device files --> configurable by `/etc/udev/rules`

##### Configuring Expansion Cards

Devices require an IRQ, I/O port and DMA address set to function. The PCI Bus enables devices to configure themselves automatically. It is possible to manipulate how they are detected and list them with `lspci`

- linux kernel options --> if you are compiling the kernel yourself.
- firmware pci options
- particular ressources can be needed by the device, so enable the modules or set a boot option to load them
- use `setpci` to query and adjust values directly --> dangerous

To load modules you'll need use `modprobe`/`insmod` and `lsmod` to list them. Insmod inserts a single module into the kernel and requires all all modules it is depending on to be loaded beforehand. Modprobe loads all dependencies and the module itself. Modprobe -r removes a module but there exists `rmmod` to do this.

##### USB Devices

Use `lsmod` to list usb devices.

usbmgr and hotplug exist but are usually not shipped with a distro.

##### PATA

PATA vs SATA vs SCSI vs NVME

PATA uses a parallel interface and are configured as master/slave and an IDE cable meaning that there can be two devices at one cable. They are typically identified as `/dev/hda` and so on. This applies for optical drives as well but these are mostly symlinked to `/dev/dvd`

##### SATA

Sata is a serial bus but are attached one by one to the motherboard. It is faster than PATA and the kernel handles them as SCSI drives.

##### SCSI

SCSI is a parallel bus but Serial Attached SCSI (SAS) is a serial bus. SCSI devices are named `/dev/sda` and so on with optical drives as `/dev/sra`. USB sticks are mapped as SCSI devices as well.

#### 104.1 Create partitions and filesystems

##### Hard Disk Layout

###### Partitions
Partitioning is needed for:

- Multiple OS Support - different FS for each OS
- Filesystem Choice - different use cases require different FS
- Disk Space Management - use disk partition as quota
- Disk Error Protection - protect data on other partitions
- Security - use read-only mode and advanced mount options
- Backup - simplify backups with whole partitions

###### MBR

MBR stores data in first sector of disk (512 byte) but is limited to 2TiB. It supports 4 primary partitions, extended partitions and logical partitions (within an extended partition). Other OS must boot from primary partition (Windows).

Primary partitions are labeled 1-4 and logical partition 5 and up. Gaps are allowed in primary partitions but not in logical partitions (i.e. 1,3,5,6 for primary).

The MBR holds the primary BIOS boot loader and is thus vulnerable to damage.

###### GPT

GPT is part of the EFI specification and uses a protective MBR as well as additional data to define partitions. It support up to 128 partitions, gaps are allowed and disks larger than 2TiB are supported. It supports partition type codes like MBR.

#### Mount Points

The OS needs a way to access data on the partition (for example drive letters in Windows). Linux uses the mount points in the unified directory tree. Partitions can be mounted anywhere in the file system. Common partitions are the following

| Partition (mount point) | Typical Size | Use |
| --- | --- | --- |
| Swap | 1-2 * RAM size | slower RAM extension or suspended data|
| /home | 200MiB - 3TiB | users data files. Isolation keeps user data after system upgrades |
| /boot | 100-1000MiB | Boot files. Some Kernels can't boot off partitions of 504MiB and bigger |
| /usr | 500MiB-25GiB | Most Linux program and data files. Seldomely separate partition |
| /usr/local | 100MiB-3GiB | Linux program data and files that are compiled by the user |
| /opt | 100MiB-3GiB | Third party packages and data, mostly commercial ones |
| /var | 100MiB-3TiB | Miscellaneous files that are variable like logs |
| /tmp | 100MiB-20GiB | Temporary files, usually wiped on reboot or after a specific time range |
| /mnt | N/A | not a separate partition but used as a mount point for removable media |
| /media | N/A | like /mnt |

#### 104.2 Maintain the integrity of filesystems


#### 104.3 Control mounting and unmounting of filesystems
