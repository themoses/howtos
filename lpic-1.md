# LPIC 1
### Learning Bank: https://testbanks.wiley.com/WPDACE/Dashboard
- [x] Assessment Test (19.00/30) :-(
- [ ] Chapter 1 - Command Line Tools

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

Continue at page 28
##### 103.4 Search text files using RegEx
