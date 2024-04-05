# System Crashing

## Check the health of RAM

`memtest 86` tool is run in boot instead of normal operating system.

System crash log files are located in `/var/log` in linux and for windows we can look at the `Event Viewer` tool.

`strace` (system trace) can also be used in linux to find out which system call is made dering the crash to identify the root cause. 

# Configuration management Cloud

Configuration management is an Automation technique which let manage computers at a large scale.

`puppet` is current industry standard for config-management.

    
