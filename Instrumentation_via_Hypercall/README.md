# Instrumentation_via_Hypercall

> Modify the processor instruction behavior inside KVM hypervisor

## Table of contents
* [Prerequisites](#prerequisites)
* [Answers](#answers)
* [Output](#output)
* [Technologies](#technologies)
* [References](#references)

## Prerequisites

A working KVM modification environment. Setup can be found following the installation manual at [this link](https://github.com/eccx400/Virtualization-Technologies/tree/master/KVM_Modification).


## Output

```
Output: CPUID(0x4FFFFFFF), exits= 454923, cycles spent in exit= 143924831
```

## Answers

1. I worked on the project with [Hung Le](https://github.com/HungVLe).

2. For this project, I built on the framework of the VM infrastructure in Assignment 2. To start with configuration, I first cloned the Github Repository for the Linux Kernel [here](https://github.com/torvalds/linux). After cloning to the local machine, I needed to set up the kernel by running the following commands:

    ```
    sudo bash
    apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-devuname -a
    cp /boot/config-4.15.0-112-generic ./.config
    make oldconfig
    make && make modules && make install && make modules-install
    reboot
    ```
    and then wait for a few hours for everything to compile. Check correct kernel installed with `uname -a` for newest version (5.8+).
    
    ```
    Linux eccx400-VirtualBox 5.9.0-custom #1 SMP Mon Nov 2 12:13:27 PST 2020 x86_64 x86_64 x86_64 GNU/Linux
    ```
    
    Find the files in the linux module that need changing. Access the directory in /linux/arch/x86/kvm to find cpuid.c and /linux/arch/x86/kvm/vmx to find vmx.c, which are the two main files that we need to complete this project. In cpuid.c, we will need to change the <b>kvm_emulate_cpuid</b> function mentioned in lecture 5 for managing the specific CPUID leaf function %eax=0x4FFFFFFE. 
    
    To run the program, we need to create an inner VM from which we can check for exits. We install virt-manager and other dependent files using `sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager` and then changing the <b>/etc/network/interfaces</b> file to create a connection. More instructions can be followed in the [references](#references) section below. After opening up the inner VM and making sure it works, we can continue our assignment.
    
    With the inner VM set up, we can then use it to find the number of exits using nested paging. 
    
3. The exits do not increase at a stable rate and occur more often during VM exits to the hypervisor with instructions such as I/O, HLT, and VMX instructions.
The process of a full VM boot has around 454923 exits.

4. The most frequent and least frequent exit types in the SDM are...

## Technologies
* Ubuntu on Oracle Virtualbox

## References

Here are some links for installing the Inner VM using Virtual Machine Manager which I followed:
* https://help.ubuntu.com/community/KVM/VirtManager
* https://linuxconfig.org/install-and-set-up-kvm-on-ubuntu-20-04-focal-fossa-linux

