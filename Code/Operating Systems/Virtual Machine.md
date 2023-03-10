When using both [[WSL]] and Virtualbox, the [[Virtual Machine]] could be running slow if the `hypervisorlaunchtype` is set to auto. To fix this run the following command and restart the system.

> bcdedit /set hypervisorlaunchtype off

When [[Docker]] uses WSL the same problem can occur. To avoid this problem we can either use a native hypervisor, like Hyper-V, or setup [[Vagrant]].