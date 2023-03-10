When using both WSL and VM and the VM is running slow, the problem could be with Hypervisor. To fix this run the following command and restart the system.

> bcdedit /set hypervisorlaunchtype off

