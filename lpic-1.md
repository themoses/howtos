# LPIC 1
### Learning Bank: https://testbanks.wiley.com/WPDACE/Dashboard
- [x] Assessment Test (19.00/30) :-(
- [x] Chapter 1 - Command Line Tools (17/20) :-| (85%)
- [ ] Chapter 2 - Managing Software

#### Chapter 1 - Command Line Tools
##### 103.1 Work on the command line
###### Bash Basics
```
time ls

aur  Desktop  Downloads
ls  0.00s user 0.00s system 83% cpu 0.001 total
```
```
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
```
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
```
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
```
echo $TERM
xterm
```
```
echo $PS1
[\u@\h \W]\$ --> PROMPT: [user@host workingdirectory]
```
```
export VARNAM="VALUE" to set an env variable
unset $VARNAME to unset an env variable
```
###### Man pages
- SPACE to move forward a page
- ESC and V to go back a bage
```
man -P /bin/vim uname
--> opens man page in vim
```
```
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

```
echo $PATH | tee path.txt
--> cat path.txt == STDOUT
```
###### Pipes and substitution
```
find . -iname *.log | xargs rm --> rm all results from find
```
```
rm $(find . -iname *.log) --> spawns subshell. Dont use backticks
```

##### 103.2 Process text streams, pipes and redirects
```
cat first.txt second.txt > combined.txt
```
- cat -E shows Line Ends
- cat -n shows line number --> make an alias for this
- cat -T shows tabs an
- join merges matching fields in files --> comparable to SQL SELECT * FROM 1,2 WHERE 1.username == 2.username
- expand -t 2 converts tabs to 2 spaces --> unexpand -t 2 does the reverse
- od shows octal dump / hex values with -x
```
 od -x test
0000000 2023 ... 766e
0000020 6e65 ... 4c53
0000040 5345 ... 6b2e
....
0000430
```
```
ls -al | sort -k 5 -n --> sort ls by file size (numeric)
```
- split --> by bytes, lines
- translate --> ???
- uniq --> get rid of duplicates lines
- fmt --> cleans up files, -width CHARSINONELINE
- nl == cat -n but with way more options
- pr --> prepare for printing, shows header, footer, etc --> lpr for actually printing --> genscript for postscript

```
ifconfig eth0 | grep HWaddr | cut -d " " -f 11
00:0C:76:96:A3:73
```
```
 wc repoindex.xml
 2  5 63 --> LINES WORDS CHARS
```

##### 103.4 Search text files using RegEx
##### grep
```
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

```
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

```
rpm -i/U packagename --> install/upgrade a package
rpm -qi packagename --> query if a package is installed (with i for more information)
rpm -e packagename --> remove a package
rpm --rebuilddb --> rebuild the rpm db
```

Yum and dnf are most commonly used. No need to download rpm packages manually, just install them out of a repo
```
yum install/update/remove/list/check-update/clean --> pretty self explanatory
```
Repos are stored in /etc/yum.repos.d/REPONAME

###### Building Packages

Building packages is often done when compiling a program from source to use special compiler flags to improve performance with CPU flags and still manage the program with the package manager. Packages out of a repo are generally compiled to maximize support to the underlying operating system architecture.

###### Debian Packages

.deb Packages are manipulated with dpkg

```
dpkg -i --> install
dpkg -r --> remove
dpkg -P --> purge (including config files)
dpkg -p --> print information on installed package
dpkg -l PATTERN --> list all matched packages
```

Like yum, there exists apt to handle package downloading and upgrades for you from a repo. it works pretty much the same way:

```
apt install/remove/update/upgrade/clean
```

Repos are stored in /etc/apt/sources.list
