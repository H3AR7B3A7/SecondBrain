# Vagrant

Vagrant is an open-source software product for building and maintaining portable virtual software development environments, e.g., for VirtualBox, KVM, Hyper-V, Docker containers, VMware, Parallels, and AWS.

It tries to simplify the software configuration management of virtualization in order to increase development productivity. Vagrant is written in the Ruby language, but its ecosystem supports development in a few other languages.

- [Download](https://developer.hashicorp.com/vagrant/downloads) and install vagrant

```
choco install vagrant
```

## Create an external switch via Hyper-V Manager, follow these steps:

1.  Open Hyper-V Manager on your host machine.
2.  Click on the "Virtual Switch Manager" option in the Actions pane on the right-hand side of the window.
3.  In the Virtual Switch Manager window, select "External" from the list of switch types.
4.  Click "Create Virtual Switch" to start the creation wizard.
5.  Give the switch a name and select the network adapter you want to use for the switch from the drop-down menu.
6.  Choose whether or not to allow the management operating system to share this network adapter.
7.  Click "OK" to create the external switch.

## Use the Hyper-V Provider

> vagrant box add hashicorp/bionic64 --provider hyperv

> vagrant up --provider hyperv

## Edit vagrant file

> vagrant init

	Vagrant.configure(2) do |config|
    config.vm.box = "hashicorp/bionic64"
    config.vm.provider "hyperv"
    config.vm.network "public_network"
    end

_Comment out or remove the line that is not in comments._

## SMBv1

You can check if SMBv1 is enabled with this PowerShell Cmdlet:

> Get-SmbServerConfiguration

If you can live without synced folders, here's the line to add to the vagrant file to disable the default synced folder.

`config.vm.synced_folder ".", "/vagrant", disabled: true`

## Nifty Hyper-V Features

- virtualization extensions, which allow nested virtualization
- differencing disks

	config.vm.provider "hyperv" do |h|
		h.enable_virtualization_extensions = true
		h.linked_clone = true
	end

## Vagrant Cloud

Find [Hyper-V Compatible Boxes](https://app.vagrantup.com/boxes/search?provider=hyperv) on the vagrant cloud.

## Default Provider

You can set your default provider on a user level by using the VAGRANT_DEFAULT_PROVIDER environmental variable. Here's how to set the user-level environment variable in PowerShell:

`[Environment]::SetEnvironmentVariable("VAGRANT_DEFAULT_PROVIDER", "hyperv", "User")`

## Ubuntu

[Discover Vagrant Boxes](https://app.vagrantup.com/boxes/search)

Cmd:

```
vagrant box add bento/ubuntu-20.04
```

```
vagrant init bento/ubuntu-20.04
vagrant up
```

Vagrant file:

```
Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"
  config.vm.network "private_network", ip: "192.168.33.10"
end
```

```
vagrant ssh
sudo apt install nginx -y
sudo service nginx start
ifconfig
```

_Default password: vagrant_

System 'hosts' file:

```
192.168.33.10    box1.com
```


---
