---
title:  "Kernel-based Virtual Machine (KVM)"
search: true
categories: 
  - Linux
  - KVM
last_modified_at: 2018-01-08T08:05:34-05:00
header:
  teaser: /assets/images/blog/kernel-based-virtual-machine/kernel-based-virtual-machine.png
---
![simple-home-automation](/assets/images/blog/kernel-based-virtual-machine/kernel-based-virtual-machine.png)

# Introduction

I first installed Windows, when I was in 7th standard. It was Windows XP. That time, I really loved to use different operating systems. But, during those days I didn't know how to use multiple operating systems as virtual machines until I reached by the 11th standard. That time, I was using Windows 7 ultimate and I wanted to use Windows Vista for knowing the experience and Windows XP for feeling the nostalgia. I started surfing the internet for solutions. One of the solutions was to use VirtualBox. I installed VirtualBox and installed both the operating systems and started using both of them. It was going well at first. But after a few days, I started noticing lags and graphics issues. I went along till my BCA first year. When I got my first Laptop (Lenovo Y50-70), I started searching for alternatives for VirtualBox and came across VMWare. VMWare fixed many of the issues, but it was a trail pack and had to pay money to use it. So, I switched back to VirtualBox. It went on till my MCA. During my first year of MCA, I uninstalled Windows 10 completely and installed Fedora. I installed VirtualBox for Virtualization. I was then suggested by my senior, [Ashwin Babu Karuvally](https://karuvally.github.io/) that KVM is better than VirtualBox. I started surfing the internet for KVM and I solved many issues that I faced while using VirtualBox.

# What is KVM?

Kernel-based Virtual Machine is an open source virtualization technology built into Linux. KVM is an alternative for using VirtualBox or VMWare. KVM helps to convert the Linux host system (Your machine) into a hypervisor that can run multiple operating systems as individual and independent virtual environments. These virtual environments are called guest machines or virtual machines. To understand how KVM works, we need to know what KVM is and how it works?

# What is Hypervisor?

 The hypervisor can be a software or hardware that can run virtual machines. The hypervisor provides a virtual operating environment for running the operating systems. Using hypervisor, a user can run any operating system on the host system. There are mainly 2 types of hypervisors:-
1. Type-1: Bare-metal hypervisors
2. Type-2: Hosted hypervisors

![Types-of-hypervisor](/assets/images/blog/kernel-based-virtual-machine/type-hypervisor.png)

A type-1: Bare-metal hypervisor is a type of hypervisor communicates directly with the host's hardware. That is, the guest machine's hardware directly communicates with the host's machine. This type of hypervisors are fast and have least delay time. When the user triggers a command in guest operating system, it sends the command to the hypervisor and the hypervisor sends the command to the host's hardware. Kernel-based Virtual Machine (KVM), Red Hat Enterprise Virtualization (RHEV), XenServer, Microsoft Windows Server 2012 Hyper-V and VMware vSphere are examples of this type of hypervisors.

A type-2: Hosted hypervisor is a type of hypervisor communicates using the host operating system. A hosted hypervisor creates each running instance of the guest machine as a process in the host operating system. So for every request from the guest operating system goes to the host operating system and from there to the hardware. This communication takes time to execute each request. These kinds of hypervisors are not efficient in terms of performance. This type of hypervisor is also called hosted hypervisors. Oracle VirtualBox, VMWare Workstation and Windows Virtual PC are examples of this type of hypervisor.

# Why KVM
1. Free and open source software.
2. Secure as it uses sVirt (Secure virtualization) and SELinux for securing and isolating every guest operating system.
3. Wide hardware support
4. Efficient memory management
5. Scalable

# Requirements before installing KVM

Make sure to enable Intel Virtualization Technology (INTEL VT) or AMD-V Technology for Client Virtualization. This setting can be enabled through the system's BIOS settings.

# Installing KVM
## Ubuntu 18.04
1. Lets install KVM and virtual machine manager.
```
$ sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager
```

2. Next we need to find the name of the network interfaces. It will be like enp8s0 or something like that.
```
$ ip a
```

3. Now, we have to edit the network interface's configuration file to create a network bridge. This bridge will provide internet to all the virtual machines (VM). The file will be empty.
```
$ sudo nano /etc/network/interfaces
```
4. Add the following line.
```
auto lo br0
iface lo inet loopback
iface enp8s0 inet manual
iface br0 inet dhcp
  bridge_ports enp8s0
```

5. Now we will add the user to appropriate group, so that he can open any KVM without need for root access.
```
$ sudo adduser username libvirt
$ sudo adduser username libvirt-qemu
```

6. Reboot your system.
```
$ sudo reboot
```

## Fedora 29

1. Install KVM
```
$ sudo dnf install @virtualization
```

2. Let's start the service.
```
$ sudo systemctl start libvirtd
$ sudo systemctl enable libvirtd
```


Here, no need to setup network bridge because during installation, the installer will automatically do that.

# Other Methods to use KVM
If you want to use KVM on your home server. That is, if you have a server that is used for virtualization only. You can use Proxmox server. Proxmox was first suggested by my senior, [Tharun P Karun](https://www.tharunpkarun.com/). I used proxmox server for my virtualization server. Learn more about proxmox server from [this link](https://www.proxmox.com/en/).
