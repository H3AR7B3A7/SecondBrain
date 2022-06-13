
# Windows Subsystem for Linux (WSL)
The Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most command-line tools, utilities and applications -- directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup. It does not provide a linux desktop, but allows the user to use [[Unix]]-like commands and run bash-scripts within the [[Windows]] OS.

[What is Windows Subsystem for Linux | Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/about)
[Install WSL | Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install)
[WSL | Ubuntu](https://ubuntu.com/wsl)

## Activation
- Turn Windows features on or off:
	- Windows Subsystem for Linux
	- Virtual Machine Platform
- Reboot
- Install distribution(s)

## Some commands
List:
> wsl -l -v

Set default version:
> wsl --set-default-version 2

Set distribution / version:
> wsl --set-version DistributionName VersionNumber

Terminate distribution:
> wsl -t DistributionName

Version:
> cat /proc/version

Access files on the hard drive:
> cd /mnt/c/   (...)

## What is WSL 2?
Includes a lightweight virtual machine based on Hyper-V with a Real Linux Kernel, allowing to run things like Docker.

## Docker with WSL 2
> curl -fsSL https://get.docker.com -o get-docker.sh
> sh get-docker.sh

For details about using Docker Desktop with WSL 2, visit:
[Docker documentation on WSL 2](https://docs.docker.com/go/wsl2/)

Make sure you have wsl_update_x64.msi or higher:
[Manual installation steps for older versions of WSL | Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)

In Docker settings:
Resources > WSL Integration > Toggle distribution(s)

To grant the user permissions to use docker in in the kernel:
>  sudo chmod 666 /var/run/docker.sock




---
#WSL