# System Crashing

## Check the health of RAM

`memtest 86` tool is run in boot instead of normal operating system.

System crash log files are located in `/var/log` in linux and for windows we can look at the `Event Viewer` tool.

`strace` (system trace) can also be used in linux to find out which system call is made during the crash to identify the root cause. 

# Configuration management Cloud

Configuration management is an Automation technique which let manage computers at a large scale.

`puppet` is current industry standard for config-management.

## disk usage

To check disk usage of your system using python use

```python
import shutil
disk_usage = shutil.disk_usage("/")
print(disk_usage) 

>>usage(total=982240026624, used=45239689216, free=887029821440)
```

## cpu usage

To check cpu usage use `psutil` in python

## strace

gives the trace of  systemcalls made by any program and tell the result of each of the calls made by the program.

```shell
strace trial.py
```

```shell
mmap(NULL, 172296, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7eff145b3000
mmap(0x7eff145b6000, 110592, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7eff145b6000
mmap(0x7eff145d1000, 45056, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1e000) = 0x7eff145d1000
mmap(0x7eff145dc000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x28000) = 0x7eff145dc000
close(3)                                = 0
mprotect(0x7eff145dc000, 4096, PROT_READ) = 0
mprotect(0x7eff145e8000, 4096, PROT_READ) = 0
munmap(0x7eff145fd000, 26071)           = 0
statfs("/", {f_type=EXT2_SUPER_MAGIC, f_bsize=4096, f_blocks=239804694, f_bfree=228791752, f_bavail=216591919, f_files=60981248, f_ffree=60855621, f_fsid={val=[0x7fa55e7a, 0x8782ee03]}, f_namelen=255, f_frsize=4096, f_flags=ST_VALID|ST_RELATIME}) = 0
write(1, "usage(total=982240026624, used=4"..., 63usage(total=982240026624, used=45109010432, free=887160500224)
) = 63
rt_sigaction(SIGINT, {sa_handler=SIG_DFL, sa_mask=[], sa_flags=SA_RESTORER|SA_ONSTACK, sa_restorer=0x7eff14cc1520}, {sa_handler=0x561cf4939980, sa_mask=[], sa_flags=SA_RESTORER|SA_ONSTACK, sa_restorer=0x7eff14cc1520}, 8) = 0
munmap(0x7eff1470d000, 151552)          = 0
exit_group(0)                           = ?
+++ exited with 0 +++
```

Output shows a lot of systemcall details.

```shell
strace -o output.trace trial.py
```

This time the output of the `strace` command is stored in a trace file.

## see disk input and output

```shell
top
iotop -> show the disk usage
iostat
vmstat
ionice


iftop -> shows current traffic on network interfaces
nice -> modify the priority of a process inorder to access CPU time.
renice -> modify the priority of a running process
```

```shell
pidof jellyfin # prints the PID of the running process named jellyfin


ps ax | less # shows all the running process on computer
# less is used to scroll through the command line output
```

## Using python to interact with OS

Use `perato principle` determine which task to automate

### Some of the useful system adm function in python

- shutil.disk_usage

- `psutil` Module









## Configuration management and the Cloud

In this course we learn `puppet` which is current industry standard for configuration management.
