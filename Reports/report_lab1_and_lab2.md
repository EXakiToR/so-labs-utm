Search the "Observe" questions by ctrl+f

LAB 1
"Before you start" part:
Part 1. Files and directories

Observe:

(1) Who owns the files you just created, and which group?

&#x20;- owner root, group root

(2) What do the ten characters at the start of `ls -l` mean for note.txt after chmod 600?

&#x20;- read and write permissions
(3) Name two directories directly under / and say, in one line each, what they hold.

&#x20;- /bin directory holds all the binaries (executable) for the system
 - /dev directory holds all devices as files, since in Linux everything is a file

Part 2. Processes

Observe:
(1) What is the PID of process number 1, and what is it (look it up)?

&#x20;- first process' PID is 41, and it is a sleep job
(2) Roughly how many processes were running on your idle VM? 
 - 8
(3) From /proc/<pid>/status, what does the "State:" line say for your sleeping process?

&#x20;- State: S (sleeping)
Part 3. Memory

Observe:
(1) How much total RAM does the VM have, and how much is free?
 - total 7.4 GB, free 7.0 GB
(2) What is swap, and how much is configured?

&#x20;- swap is a support file in case machine runs out of RAM, it will use the space of the swap file. It is configured to 2.0GB
(3) How much resident memory (VmRSS) does a bare `sleep` process use, and does that surprise you?

&#x20;- 4kB, surprising, why such a simple process uses that much memory? (a question in my head)
Part 4. Devices and storage
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

