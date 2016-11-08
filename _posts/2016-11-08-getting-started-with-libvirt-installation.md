---
layout: post
title: Getting started with libvirt
---

Very recently I have been working on a platform to orchestrate VM creation and lifecycle management across a cluster of nodes with capacity, metadata, storage and network management. I was exploring stuff like [KVM](http://www.linux-kvm.org/) + QEMU and [XEN](https://www.xenproject.org/) when I read about [libvirt](http://libvirt.org) and found it perfectly suiting my needs.

To start off with, KVM (Kernel-based Virtual Machine) is a virtualization infrastructure for the Linux kernel that turns it into a hypervisor, a software which enables us to run Virtual Machines on top of a host machine. XEN is another such hypervisor.

libvirt, on the other hand is an abstraction layer on top of the various hypervisor platforms with a nice API available to manage virtualization. We can choose to use any of the hypervisor backends that libvirt supports to create and manage virtual machines. The list of hypervisors supported by libvirt are listed below:

- [lxc](https://linuxcontainers.org/)
- [openvz](https://github.com/OpenVZ)
- [KVM / QEMU](http://www.linux-kvm.org/)
- [XEN](https://www.xenproject.org/)
- [User Mode Linux](http://user-mode-linux.sourceforge.net/)
- [VirtualBox](https://www.virtualbox.org/)
- [VMWare ESX](http://www.vmware.com/products/esxi-and-esx.html) and GSX
- [VMWare workstation](http://www.vmware.com/products/workstation.html) and [Player](http://www.vmware.com/products/player/playerpro-evaluation.html)
- [Hyper V](https://www.microsoft.com/en-us/cloud-platform/virtualization)
- [PowerVM](http://www-03.ibm.com/systems/power/software/virtualization/)
- [Parallels Workstation](http://www.parallels.com/)
- [Bhyve](http://bhyve.org/)

[Source: Wikipedia](https://en.wikipedia.org/wiki/Libvirt)

libvirt has an API in [C](https://libvirt.org/html/index.html) for development. It also has bindings in other languages like [python](https://libvirt.org/python.html), [perl](http://search.cpan.org/dist/Sys-Virt/), [ocaml](http://libvirt.org/ocaml/), [ruby](http://libvirt.org/ruby/), [java](https://libvirt.org/java.html), [Go](https://github.com/rgbkrk/libvirt-go), [PHP](https://libvirt.org/php.html) and [C#](https://libvirt.org/csharp.html).

Let's start off with installing libvirt first. Since the workstations I use are ArchLinux and OSX, I will stick to these two platforms only (the installation instructions for other platforms are easily available).

On ArchLinux, you can install libvirt with a KVM backend by installing the following packages

```
sudo pacman -S libvirt qemu ebtables dnsmasq bridge-utils openbsd-netcat
```

By default, KVM is the default driver enabled.

On OSX, you can install libvirt by running

```
brew install libvirt
```

To ensure that the libvirt daemon is running, run the following command

```
sudo systemctl status libvirtd
```

Once the libvirt daemon is running you can use the command line client `virsh` which comes included in the libvirt package to connect to the daemon.

Once inside the `virsh` client, you can run a bunch of commands to consume the API.

- Getting the hypervisor hostname

```
virsh # hostname
playstation
```

- Getting the node information

```
virsh # nodeinfo 
CPU model:           x86_64
CPU(s):              4
CPU frequency:       1800 MHz
CPU socket(s):       1
Core(s) per socket:  2
Thread(s) per core:  2
NUMA cell(s):        1
Memory size:         8066144 KiB
```


- Getting the version

```
virsh # version
Compiled against library: libvirt 2.3.0
Using library: libvirt 2.3.0
Using API: QEMU 2.3.0
Running hypervisor: QEMU 2.7.0
```

You can use the help command to get a list of all available commands.

In the next post in the libvirt series, I'll start off with programmatically consuming the libvirt APIs.
