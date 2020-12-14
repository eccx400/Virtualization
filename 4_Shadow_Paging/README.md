# Shadow_Paging

> Compare performance between nested paging (EPT) and shadow paging (non-EPT) inside KVM hypervisor

## Table of contents
* [Prerequisites](#prerequisites)
* [Answers](#answers)
* [Technologies](#technologies)
* [Contributors](#contributors)

## Prerequisites

A working KVM modification environment with nested paging. Setup can be found following the installation manual at [this link](https://github.com/eccx400/Virtualization-Technologies/tree/master/3_Instrumentation_via_Hypercall).

## Answers

1. I worked on the project with [Hung Le](https://github.com/HungVLe). I focused on researching how the project should be implemented, dependency files, answering the questions, and preparing the documentation of the project. Hung focused on setting up the Virtual Machine and the inner VM, updating the cpuid.c and vmx.c modules, making sure the implementation was correct and produced the right output.

2. Implementation steps:
    - With the inner VM set up, we can then use it to find the number of exits using nested paging. Before removing the modules (Nested Paging), total count for each type of exit handled by KVM. This done done using the same steps as [assignment 3](https://github.com/eccx400/Virtualization-Technologies/tree/master/3_Instrumentation_via_Hypercall). Use repeated calls to cpuid at leaf 0x4FFFFFFE to record the total exit count information; this completes the nested paging steps. 

    ![](./nested_paging.jpeg)

    -  After turning off the kernel, we want to remove the current kvm-intel module from the running kernel. This is done by running the commands `rmmod kvm-intel` and `rmmod kvm`. After running the code segment, check to make sure the kvm-intel module is properly removed:

    ![](./rmmod.jpeg)

    - To make program run shadow paging instead of nested paging, we must turn the EPT option off by removing kvm and the kvm-intel modules. This is done by running the command `insmod /lib/modules/5.10.0-rc2+/kernel/arch/x86/kvm/kvm-intel.ko ept=0;` at the path directory /lib/modules/XXX/kernel/arch/x86/kvm, where XXX is the current kernel version after running make install. Refer to [assignment 2](https://github.com/eccx400/Virtualization-Technologies/tree/master/2_KVM_Modification) for more instructions. After running the code segment, the EPT option should be set to 0 and disabled. Check to make sure it is properly turned off:

    ![](./insmod.jpeg)

    - Now because the EPT value is set to 0, the kernel is forced to use shadow paging instead of neested paging. After reloading the kvm-intel modules with insmod (Shadow Paging), we can count total count for each type of exit handled by KVM using shadow paging.

    ![](./shadow_paging.png)

    - Reboot the inner VM and record total exit count.
    
3. When running the Virtual Machine with Extended Page Tables turned off, we can clearly see that the number of exits increased. This is within our expections, since shadow paging relies on the page fault exiting in order the Shadow Page Table and the TLB to be updated. Running shadow paging requires many types of exits to be turned on, including Load CR3, #PF, Write to CR3, Read from CR3, TLB flushing for free(), etc.  Nested paging eliminates the overhead by having a page table translating from the guest PA to the host PA which acts as the final translation, while the guest page table can be updated with anything. Thus the number of exits, especially by exit number 1 is significantly higher in shadow paging than in nested paging (69866 for EPT vs 142139 for non-EPT).

4. The main reasons for the differences between running Nested Paging (EPT) vs Shadow Paging(non-EPT) are listed above. In summary, the structure of shadow paging requires many more exit types to be turned on, since every translation is managed by the hypervisor using the nested page table.

## Technologies
* Ubuntu on Oracle Virtualbox

## Contributors

| Contributors | GitHub Link                 |
|--------------|-----------------------------|
| Eric Cheng   | https://github.com/eccx400/ |
| Hung Le      | https://github.com/HungVLe  |
