Search the "Observe" questions by ctrl+f

LAB 1
"Before you start" part:
A315:\~# mkdir -p \~/os-lab1 \&\& cd \~/os-lab1

A315:\~/os-lab1# whoami

root

A315:\~/os-lab1# uname -a

Linux A315 5.15.167.4-microsoft-standard-WSL2 #1 SMP Tue Nov 5 00:21:55 UTC 2024 x86\_64 Linux

A315:\~/os-lab1# uptime

&#x20;13:41:19 up 5 min,  0 users,  load average: 0.03, 0.02, 0.00

Part 1. Files and directories
1. 
A315:\~/os-lab1# pwd

/root/os-lab1

A315:\~/os-lab1# ls -la /

total 20704

drwxr-xr-x   20 root     root          4096 Sep 28 13:35 .

drwxr-xr-x   20 root     root          4096 Sep 28 13:35 ..

drwxr-xr-x    2 root     root          4096 Apr 18  2025 bin

drwxr-xr-x   11 root     root          3080 Sep 28 13:35 dev
…
drwxr-xr-x    7 root     root          4096 Feb 18  2025 usr

drwxr-xr-x   12 root     root          4096 May 22  2024 var
A315:\~/os-lab1# ls -la \~

total 20

drwx------    4 root     root          4096 Sep 28 13:38 .

drwxr-xr-x   20 root     root          4096 Sep 28 13:35 ..

\-rw-------    1 root     root            80 Sep 28 14:03 .ash\_history

drwxr-xr-x    3 root     root          4096 Apr 18  2025 .docker

drwxr-xr-x    2 root     root          4096 Sep 28 13:38 os-lab1
A315:\~/os-lab1# cd /etc \&\& ls | head

alpine-release

apk

...

group

hostname

A315:/etc#
2.

A315:/etc# cd \~/os-lab1

A315:\~/os-lab1# mkdir demo \&\& cd demo

A315:\~/os-lab1/demo# echo "hello operating systems" > note.txt

A315:\~/os-lab1/demo# cp note.txt copy.txt

A315:\~/os-lab1/demo# mv copy.txt renamed.txt

A315:\~/os-lab1/demo# ls -l

total 8

\-rw-r--r--    1 root     root            24 Sep 28 14:05 note.txt

\-rw-r--r--    1 root     root            24 Sep 28 14:05 renamed.txt

A315:\~/os-lab1/demo# rm renamed.txt

A315:\~/os-lab1/demo# ls -l

total 4

\-rw-r--r--    1 root     root            24 Sep 28 14:05 note.txt

A315:\~/os-lab1/demo#
3.
A315:\~/os-lab1/demo# chmod 600 note.txt

A315:\~/os-lab1/demo# ls -l note.txt

\-rw-------    1 root     root            24 Sep 28 14:05 note.txt

A315:\~/os-lab1/demo# chmod 644 note.txt

A315:\~/os-lab1/demo# ls -l note.txt

\-rw-r--r--    1 root     root            24 Sep 28 14:05 note.txt

A315:\~/os-lab1/demo#

Observe:

(1) Who owns the files you just created, and which group?

&#x20;- owner root, group root

(2) What do the ten characters at the start of `ls -l` mean for note.txt after chmod 600?

&#x20;- read and write permissions
(3) Name two directories directly under / and say, in one line each, what they hold.

&#x20;- /bin directory holds all the binaries (executable) for the system
 - /dev directory holds all devices as files, since in Linux everything is a file
Part 2. Processes
4.
Mem: 424788K used, 7318724K free, 2720K shrd, 948K buff, 80312K cached

CPU:   0% usr   0% sys   0% nic  99% idle   0% io   0% irq   0% sirq

Load average: 0.00 0.00 0.00 2/159 36

&#x20; PID  PPID USER     STAT   VSZ %VSZ CPU %CPU COMMAND

&#x20;   1     0 root     S     2784   0%   2   0% {init(docker-des} /init

&#x20;   9     8 root     S     2784   0%   5   0% {Relay(10)} /init

&#x20;   8     1 root     S     2784   0%   3   0% {SessionLeader} /init

&#x20;   5     1 root     S     2776   0%   3   0% {init} plan9 --control-socket

&#x20;  10     9 root     S     1696   0%   0   0% -sh

&#x20;  36    10 root     R     1624   0%   3   0% top

A315:/# ps aux | head

PID   USER     TIME  COMMAND

&#x20;   1 root      0:00 {init(docker-des} /init

&#x20;   5 root      0:00 {init} plan9 --control-socket 6 --log-level 4 --server-fd 7 --pipe-fd 9 --log-truncate

&#x20;   8 root      0:00 {SessionLeader} /init

&#x20;   9 root      0:00 {Relay(10)} /init

&#x20;  10 root      0:00 -sh

&#x20;  37 root      0:00 ps aux

&#x20;  38 root      0:00 head

A315:/# ps aux | wc -l

8

5\.
A315:/# sleep 300 \&

A315:/# jobs

\[1]+  Running                    sleep 300

A315:/# ps -ef | grep sleep

&#x20;  41 root      0:00 sleep 300

A315:/# kill 41

A315:/#

\[1]+  Terminated                 sleep 300

6\.
A315:/# sleep 300 \&

A315:/# PID=$!

A315:/# ls /proc/$PID/

arch\_status      fdinfo           oom\_adj          stack

...

exe              net              smaps

fd               ns               smaps\_rollup

A315:/# cat /proc/$PID/status | head -20   # state, memory, threads

Name:   sleep

Umask:  0022

State:  S (sleeping)

Tgid:   44

Ngid:   0

Pid:    44

PPid:   10

TracerPid:      0

Uid:    0       0       0       0

Gid:    0       0       0       0

FDSize: 64

Groups: 0 0 1 2 3 4 6 10 11 20 26 27

NStgid: 44

NSpid:  44

NSpgid: 44

NSsid:  10

VmPeak:     1612 kB

VmSize:     1612 kB

VmLck:         0 kB

VmPin:         0 kB

A315:/# kill $PID

A315:/#

\[1]+  Terminated                 sleep 300

Observe:
(1) What is the PID of process number 1, and what is it (look it up)?

&#x20;- first process' PID is 41, and it is a sleep job
(2) Roughly how many processes were running on your idle VM? 
 - 8
(3) From /proc/<pid>/status, what does the "State:" line say for your sleeping process?

&#x20;- State: S (sleeping)
Part 3. Memory
A315:/# free -h

&#x20;             total        used        free      shared  buff/cache   available

Mem:           7.4G      314.1M        7.0G        2.7M       99.1M        6.9G

Swap:          2.0G           0        2.0G

A315:/# cat /proc/meminfo | head -6

MemTotal:        7743512 kB

MemFree:         7320128 kB

MemAvailable:    7239380 kB

Buffers:            1044 kB

Cached:            80380 kB

SwapCached:            0 kB

A315:/# sleep 300 \& PID=$!

A315:/# grep VmRSS /proc/$PID/status

VmRSS:         4 kB

A315:/# kill $PID

A315:/#

\[1]+  Terminated                 sleep 300

A315:/#

Observe:
(1) How much total RAM does the VM have, and how much is free?
 - total 7.4 GB, free 7.0 GB
(2) What is swap, and how much is configured?

&#x20;- swap is a support file in case machine runs out of RAM, it will use the space of the swap file. It is configured to 2.0GB
(3) How much resident memory (VmRSS) does a bare `sleep` process use, and does that surprise you?

&#x20;- 4kB, surprising, why such a simple process uses that much memory? (a question in my head)
Part 4. Devices and storage
A315:/# df -h

Filesystem                Size      Used Available Use% Mounted on

none                      3.7G         0      3.7G   0% /lib/modules/5.15.167.4-microsoft-standard-WSL2

none                      3.7G      4.0K      3.7G   0% /mnt/host/wsl

drivers                 207.5G     96.7G    110.8G  47% /usr/lib/wsl/drivers

/dev/sdc               1006.9G     56.7M    955.6G   0% /

none                      3.7G     80.0K      3.7G   0% /mnt/host/wslg

/dev/sdc               1006.9G     56.7M    955.6G   0% /mnt/host/wslg/distro

none                      3.7G         0      3.7G   0% /usr/lib/wsl/lib

none                      3.7G         0      3.7G   0% /dev

none                      3.7G         0      3.7G   0% /run

none                      3.7G         0      3.7G   0% /run/lock

none                      3.7G         0      3.7G   0% /run/shm

none                      3.7G         0      3.7G   0% /dev/shm

none                      3.7G         0      3.7G   0% /run/user

tmpfs                     3.7G         0      3.7G   0% /sys/fs/cgroup

none                      3.7G    100.0K      3.7G   0% /mnt/host/wslg/versions.txt

none                      3.7G    100.0K      3.7G   0% /mnt/host/wslg/doc

none                      3.7G     80.0K      3.7G   0% /tmp/.X11-unix

C:\\                     207.5G     96.7G    110.8G  47% /mnt/host/c

D:\\                     254.7G     56.4G    198.3G  22% /mnt/host/d

A315:/# lsblk

NAME MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS

sda    8:0    0 388.4M  1 disk

sdb    8:16   0     2G  0 disk \[SWAP]

sdc    8:32   0     1T  0 disk /mnt/host/wslg/distro

&#x20;                              /

A315:/# du -sh \~/os-lab1

12.0K   /root/os-lab1

A315:/# ls -l /dev | head

total 0

crw-r--r--    1 root     root       10, 235 Sep 28 13:35 autofs

drwxr-xr-x    2 root     root            40 Sep 28 13:35 block

drwxr-xr-x    2 root     root           100 Sep 28 13:35 bsg

crw-------    1 root     root       10, 234 Sep 28 13:35 btrfs-control

drwxr-xr-x    3 root     root            60 Sep 28 13:35 bus

crw-------    1 root     root        5,   1 Sep 28 13:35 console

crw-------    1 root     root       10, 125 Sep 28 13:35 cpu\_dma\_latency

crw-------    1 root     root       10, 203 Sep 28 13:35 cuse

drwxr-xr-x    2 root     root            80 Sep 28 13:35 dri

A315:/# mount | head

none on /lib/modules/5.15.167.4-microsoft-standard-WSL2 type overlay (rw,nosuid,nodev,noatime,lowerdir=/modules,upperdir=/lib/modules/5.15.167.4-microsoft-standard-WSL2/rw/upper,workdir=/lib/modules/5.15.167.4-microsoft-standard-WSL2/rw/work)

none on /mnt/host/wsl type tmpfs (rw,relatime)

drivers on /usr/lib/wsl/drivers type 9p (ro,nosuid,nodev,noatime,dirsync,aname=drivers;fmask=222;dmask=222,mmap,access=client,msize=65536,trans=fd,rfd=8,wfd=8)

/dev/sdc on / type ext4 (rw,relatime,discard,errors=remount-ro,data=ordered)

none on /mnt/host/wslg type tmpfs (rw,relatime)

/dev/sdc on /mnt/host/wslg/distro type ext4 (ro,relatime,discard,errors=remount-ro,data=ordered)

none on /usr/lib/wsl/lib type overlay (rw,nosuid,nodev,noatime,lowerdir=/gpu\_lib\_packaged:/gpu\_lib\_inbox,upperdir=/gpu\_lib/rw/upper,workdir=/gpu\_lib/rw/work)

rootfs on /init type rootfs (ro,size=3868264k,nr\_inodes=967066)

none on /dev type devtmpfs (rw,nosuid,relatime,size=3868264k,nr\_inodes=967066,mode=755)

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,noatime)

Observe: 
(1) Which device is your root filesystem "/" mounted on?

&#x20;- /dev/sdc 
(2) Give one entry from /dev and say what real thing it stands for.

&#x20;- entry "console" stands for /dev/tty0, /dev/tty1
(3) In one sentence: what does "everything is a file" mean, based on what you saw?

&#x20;- even usb ports are considered files, as well as drives, cpu, any hardware that is on the machine.

Closing sentences:
The OS manages files and directories, processes, memory and devices and storage.
Commands which let us see them:
Files and directories — ls -la

Processes — ps aux

Memory — free -h

Devices and storage — lsblk

LAB 2
Part 1. Build it and boot it (done)

Part 2. Use xv6 as the Unix it is

Observe: 

Three xv6 programs: ls, cat, echo.

Two OS features needed for a pipe: processes and inter-process communication (IPC).

Shell comparison: The xv6 shell is a small Unix-like shell with basic features similar to the Linux shell, such as commands and pipes.

Part 3 — Observe
System calls used by user/cat.c:

read() — asks the kernel to read data.

write() — asks the kernel to write data.

exit() — asks the kernel to terminate the process.

sys_read implementation: It is in kernel/sysfile.c, at the line containing uint64 sys_read(void) (the exact line number can vary between xv6 versions).

Difference between kernel/ and user/: kernel/ contains privileged OS code that manages hardware and system resources, while user/ contains ordinary programs that run on top of the OS.

