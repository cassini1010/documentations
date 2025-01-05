# Command Prompt Tricks

###### 

###### Open CMD as an Administrator and run below command to open Environment Variable window.

> `rundll32.exe sysdm.cpl,EditEnvironmentVariable`

###### `control` command opens control panel window.

###### `wmic`command can be used as below to uninstall programs from CMD

```shell
Run "wmic" command
Run "product get name" to list out the applications.
Run "product where name='Python 3.9.13 Standard Library (64-bit)' call uninstall" command
```

# VS-CODE error in Power shell : Cannot be loaded because running scripts is disabled on this system

Run the following command and confirm with ‘Y’ 

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
```
