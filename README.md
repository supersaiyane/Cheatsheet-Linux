![licence:free to use](https://img.shields.io/badge/licence-free--to--use-blue)  [![Linkedin Badge](https://img.shields.io/badge/-gurpreetsingh89-blue?style=flat&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/gurpreetsingh89/)](https://www.linkedin.com/in/gurpreetsingh89/)  [![dev.to Badge](https://img.shields.io/badge/-@gurpreetsingh-000000?style=flat&labelColor=000000&logo=dev.to&link=https://dev.to/gurpreetsingh)](https://dev.to/gurpreetsingh)

# Linux Cheat Sheet

Linux basic information unified from personal notes and bookmarks

 * [Filesystem Hierarchy Standard](#filesystem-hierarchy-standard)
 * [System Inspection Commands](#system-inspection-commands)
 * [Process Management](#process-management)
 * [systemd Service Manager](#systemd-service-manager)
 * [Working with files and folders](#working-with-files-and-folders)
 * Permissions
 * Networking
 * Packages

## [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)

| Directory | Description |
|----------------|------------------------------------------------------------------------------------------------------------|
| / | root directory of the entire file system |
| /bin | essential command binaries that need to be available in single user mode; for all users, e.g., cat, ls, cp |
| /boot | boot loader files, e.g., kernels, initrd |
| /etc | host-specific system-wide configuration files |
| /home | users' home directories, containing saved files, personal settings, etc. |
| /lib | libraries essential for the binaries in /bin and /sbin |
| /media | mount points for removable media such as CD-ROMs |
| /mnt | temporarily mounted filesystems |
| /opt | optional application software packages |
| /proc | cirtual filesystem providing process and kernel information as files |
| /root | home directory for the root user |
| /run | run-time variable data: Information about the running system since last boot |
| /sbin | essential system binaries, e.g., fsck, init, route |
| /srv | server data such as data and scripts for web servers, data offered by FTP servers |
| /sys | information about devices, drivers, and some kernel features |
| /tmp | temporary files (see also /var/tmp). Often not preserved between system reboots |
| /usr | secondary hierarchy for read-only user data; contains the majority of (multi-)user applications |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/bin | non-essential command binaries (not needed in single user mode); for all users. |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/include | standard include files |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/lib | libraries for the binaries in /usr/bin and /usr/sbin |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/local | tertiary hierarchy for local data, specific to this host |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/sbin | non-essential system binaries |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/share | architecture-independent (shared) data |
| &nbsp;&nbsp;&nbsp;&nbsp;/usr/src | source code, e.g., the kernel source code with its header files |
| /var | variable files |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/cache | application cache data |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/lib | persistent data modified by programs as they run |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/lock | lock files |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/log | log files |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/mail | mailbox files |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/opt | variable data from add-on packages that are stored in /opt |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/run | Run-time variable data |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/spool | spool for tasks waiting to be processed |
| &nbsp;&nbsp;&nbsp;&nbsp;/var/tmp | temporary files to be preserved between reboots |

## System Inspection Commands

| Command | Description |
|---------|-------------|
| uname -a | current system summary |
| lshw | system hardware |
| lscpu | cpu and processing units |
| lspci -v | pci buses and details about the devices connected to them |
| lsblk - a | all block devices |
| lsmod | loaded kernel modules |
| lsusb -v | usb devices |
| df -H | partitions, their mount points and the used and available space on each |
| fdisk -l | partition information |
| mount \| column -t | mounted file systems |
| free -m | check the amount of used, free and total amount of RAM |
| dmidecode |  SMBOIS data structures |
| ifconfig -a | network interfaces |
| cat /proc/cpuinfo |  |
| cat /proc/meminfo |  |
| cat /proc/version |  |
| cat /proc/scsi/scsi |  |
| cat /proc/partitions |  |
| cat /etc/\*-release | linux distro |
| dmesg \| less | boot information (/var/log/dmesg) |
| history \| tac \| less | bash execution history (~/.bash_history) |
| uptime | show current uptime |
| vmstat 5 10 | virtual memory statistics 10 times at 5 second intervals |
| less /etc/passwd | list users |
| find . -name "*device*" | find all files containing word device |

## Process Management

A process refers to a program in execution; it’s a running instance of a program. [Daemons](https://bash.cyberciti.biz/guide/Daemons) are special types of background processes that start at system startup and keep running forever as a service (typically in the /etc/init.d directory)

| Command | Description |
|---------|-------------|
| ps -ef | display every processes on the system |
| top | system monitoring tool |
| pstree | display a tree diagram of processes |
| w | list of all the users currently logged |
| who | same as above |
| whoami | who you are logged in as |
| kill pid | kill process id pid |
| killall proc | kill all processes named proc * |
| bg | stopped or background jobs |
| fg | brings the most recent job to foreground |
| fg n | brings job n to the foreground |

## systemd Service Manager

### [systemctl](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

| Parameters | Description |
|------------|-------------|
| start application.service | start a systemd service |
| stop application.service | stop a currently running service |
| restart application.service |  |
| reload application.service | reload configuration files without restarting |
| reload-or-restart application.service |  |
| enable application.service |  |
| disable application.service |  |
| status application.service |  |
| is-active application.service | active or inactive |
| is-enabled application.service | enabled or disabled |
| is-failed application.service |  |
| list-units --all | list loaded or attempted to load |
| list-unit-files |  |
| cat atd.service | display unit file |
| list-dependencies sshd.service | display dependencies |
| show sshd.service | show low-level properties of a unit |
| mask nginx.service | prevent the service from being started, automatically or manually |
| edit nginx.service |  |
| rescue | put the system into rescue (single-user) mode = isolate rescue.target |
| halt | halt the system |
| poweroff | initiate a full shutdown |
| reboot | system restart |

Targets are special unit files that describe a system state or synchronization point. Targets do not do much themselves, but are instead used to group other units together.

| Parameters | Description |
|------------|-------------|
| get-default | get default target |
| set-default graphical.target |  |
| list-unit-files --type=target |  |
| list-units --type=target |  |
| isolate multi-user.target |  |

### [journalctl](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs)

| Parameters | Description |
|------------|-------------|
| --utc | display the timestamps in UTC |
| -b | logs from the current boot |
| --list-boots | see the boots that journald knows about |
| -b -1 | logs for the boot n relative to the current |
| --since yesterday |  |
| --since "2015-01-10" --until "2015-01-11 03:00" |  |
| --since 09:00 --until "1 hour ago" |  |
| -u nginx.service | for a specific unit |
| \_PID=8088 | by process id |
| -k or --dmesg | kernel messages |
| -p err | priority: emerg, alert, crit, err, warning, notice, info, debug |
| -n 20 | most recent 20 logs |
| -o json-pretty | output as: cat, export, json, json-pretty, json-sse, short, short-iso, short-monotonic, short-precise, verbose |
| --no-pager |  |
| -f | actively follow the logs as they are being written |
| --disk-usage | find out the amount of space of the journal |
| --vacuum-size=1G | shrink journal by the indicated size |
| --vacuum-time=1years | remove entries beyond specified time |
| cat /etc/systemd/journald.conf | journal config |

### [udev](https://opensource.com/article/18/11/udev)

## Working with files and folders

| Command | Description |
|---------|-------------|
| pwd | show current directory |
| cd | change to home |
| cd dir | change directory to dir |
| ls | directory listing |
| ls -la | formatted listing with hidden files |
| mkdir dir | create a directory dir |
| rm file | delete file |
| rm -r dir | delete directory dir |
| rm -f file | force remove file |
| rm -rf dir | force remove directory dir |
| cp file1 file2 | copy file1 to file2 |
| cp -r dir1 dir2 | copy dir1 to dir2; create dir2 if it doesn't exist |
| mv file1 file2 | rename or move file1 to file2 |
| ln -s file link | create symbolic link link to file |
| touch file | create or update file |
| more file | output the contents of file |
| head file | output the first 10 lines of file |
| tail file | output the last 10 lines of file |
| tail -f file | output the contents of file as it grows |
| cat > file | standard input into file |

Editors

| Editor | Command | Description |
|--------|---------|-------------|
| [Vi](https://staff.washington.edu/rells/R110/) | vi file | opens file in Vi file editor |
|  | i | text mode |
|  | ESC | command mode |
|  | : | ex mode |
|  | :q | quit |
|  | :q! | force quit |
|  | :w | save |
|  | :wq or :x | save and quit |
|  | :w | save |

## File Permissions:
 * chmod octal file – change the permissions of file to octal, which can be found separately for user, group, and world by adding:
 * 4 – read (r)
 * 2 – write (w)
 * 1 – execute (x)

### Examples:
 * chmod 777 – read, write, execute for all
 * chmod 755 – rwx for owner, rx for group and world

## SSH: 
 * ssh user@host – connect to host as user
 * ssh -p port user@host – connect to host on port port as user
 * ssh-copy-id user@host – add your key to host for user to enable a keyed or passwordless login

## Searching:
 * grep pattern files – search for pattern in files
 * grep -r pattern dir – search recursively for pattern in dir
 * command | grep pattern – search for pattern in the output of command
 * locate file – find all instances of file
 
## System Info:
 * date – show the current date and time
 * cal – show this month's calendar
 * uptime – show current uptime
 * w – display who is online
 * whoami – who you are logged in as
 * finger user – display information about user
 * uname -a – show kernel information
 * cat /proc/cpuinfo – cpu information
 * cat /proc/meminfo – memory information
 * man command – show the manual for command
 * df – show disk usage
 * du – show directory space usage
 * free – show memory and swap usage
 * whereis app – show possible locations of app
 * which app – show which app will be run by default

## Compression:
 * tar cf file.tar files – create a tar named file.tar containing files
 * tar xf file.tar – extract the files from file.tar
 * tar czf file.tar.gz files – create a tar with Gzip compression
 * tar xzf file.tar.gz – extract a tar using Gzip
 * tar cjf file.tar.bz2 – create a tar with Bzip2 compression
 * tar xjf file.tar.bz2 – extract a tar using Bzip2
 * gzip file – compresses file and renames it to file.gz
 * gzip -d file.gz – decompresses file.gz back to file

## Network:
 * ping host – ping host and output results
 * whois domain – get whois information for domain
 * dig domain – get DNS information for domain
 * dig -x host – reverse lookup host
 * wget file – download file
 * wget -c file – continue a stopped download

## Installation:
 * dpkg -i pkg.deb – install a package (Debian)
 * rpm -Uvh pkg.rpm – install a package (RPM)

## Install from source:
 * ./configure
 * make
 * make install

## Shortcuts:
 * Ctrl+C – halts the current command
 * Ctrl+Z – stops the current command, resume with
 * fg in the foreground or bg in the background
 * Ctrl+D – log out of current session, similar to exit
 * Ctrl+W – erases one word in the current line
 * Ctrl+U – erases the whole line
 * Ctrl+R – type to bring up a recent command
 * !! - repeats the last command
 * exit – log out of current session
