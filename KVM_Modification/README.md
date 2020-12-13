# KVM_Modification

> Modify the CPUID emulation code in KVM to report back additional information when a special CPUID “leaf function” is called.

## Table of contents
* [Answers](#answers)
* [Output](#output)
* [Technologies](#technologies)

## Output

```
Output: CPUID(0x4FFFFFFF), exits= 454923, cycles spent in exit= 143924831
```

## Answers

1. I did the project myself.

2. For this project, I built on the framework of the VM infrastructure in Assignment 1. To start with configuration, I first cloned the Github Repository for the Linux Kernel [here](https://github.com/torvalds/linux). After cloning to the local machine, I needed to set up the kernel by running the following commands:

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
    
    Find the files in the linux module that need changing. Access the directory in /linux/arch/x86/kvm to find cpuid.c and /linux/arch/x86/kvm/vmx to find vmx.c, which are the two main files that we need to complete this project. In cpuid.c, we will need to change the <b>kvm_emulate_cpuid</b> function mentioned in lecture 5 for managing the specific CPUID leaf function %eax=0x4FFFFFFF. 
    
    In vmx.c we modify the atomic counter so that the number of exits can be calculated to store in the registers in cpuid.c. We set a u64 timer, and then whenever we encounter an exit we subtract that from rdtsc() and store it in `exit_time`. After compiling the code with make again, which shouldn't take as long as before, following which I use gcc to run the test program and get the output.
    
3. The exits do not increase at a stable rate and occur more often during VM exits to the hypervisro with instructions such as I/O, HLT, and VMX instructions.
The process of a full VM boot has around 454923 exits.

## Technologies
* Ubuntu on Oracle Virtualbox
