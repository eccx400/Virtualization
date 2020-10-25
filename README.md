# VMX_config

> Create a linux kernel module that queries various MSR to determine virtualization features of the CPU

## Table of contents
* [Output](#output)
* [Answers](#answers)
* [Technologies](#technologies)

## Output

```
[ 2540.184764] CMPE 283 Assignment 1 Module Start
[ 2540.184769] Pinbased Controls MSR: 0x3f00000016
[ 2540.184770]   External Interrupt Exiting: Can set=Yes, Can clear=Yes
[ 2540.184771]   NMI Exiting: Can set=Yes, Can clear=Yes
[ 2540.184772]   Virtual NMIs: Can set=Yes, Can clear=Yes
[ 2540.184773]   Activate VMX Preemption Timer: Can set=No, Can clear=Yes
[ 2540.184774]   Process Posted Interrupts: Can set=No, Can clear=Yes
[ 2766.129359] CMPE 283 Assignment 1 Module Exits
[ 2829.936486] CMPE 283 Assignment 1 Module Start
[ 2829.936491] Pinbased Controls MSR: 0xf7b9fffe0401e172
[ 2829.936492]   External Interrupt Exiting: Can set=No, Can clear=Yes
[ 2829.936493]   NMI Exiting: Can set=Yes, Can clear=Yes
[ 2829.936494]   Virtual NMIs: Can set=Yes, Can clear=No
[ 2829.936495]   Activate VMX Preemption Timer: Can set=Yes, Can clear=No
[ 2829.936496]   Process Posted Interrupts: Can set=Yes, Can clear=Yes
[ 2878.119228] CMPE 283 Assignment 1 Module Exits
[ 2881.885742] CMPE 283 Assignment 1 Module Start
[ 2881.885750] Pinbased Controls MSR: 0x104d00000000
[ 2881.885752]   External Interrupt Exiting: Can set=Yes, Can clear=Yes
[ 2881.885753]   NMI Exiting: Can set=Yes, Can clear=Yes
[ 2881.885754]   Virtual NMIs: Can set=No, Can clear=Yes
[ 2881.885756]   Activate VMX Preemption Timer: Can set=Yes, Can clear=Yes
[ 2881.885757]   Process Posted Interrupts: Can set=No, Can clear=Yes
[ 2921.027295] CMPE 283 Assignment 1 Module Exits
[ 2923.957893] CMPE 283 Assignment 1 Module Start
[ 2923.957896] Pinbased Controls MSR: 0x33efff00036dff
[ 2923.957897]   External Interrupt Exiting: Can set=Yes, Can clear=No
[ 2923.957898]   NMI Exiting: Can set=Yes, Can clear=No
[ 2923.957898]   Virtual NMIs: Can set=Yes, Can clear=No
[ 2923.957899]   Activate VMX Preemption Timer: Can set=Yes, Can clear=No
[ 2923.957899]   Process Posted Interrupts: Can set=Yes, Can clear=No
[ 2952.529937] CMPE 283 Assignment 1 Module Exits
[ 2954.953592] CMPE 283 Assignment 1 Module Start
[ 2954.953597] Pinbased Controls MSR: 0x93ff000011ff
[ 2954.953598]   External Interrupt Exiting: Can set=Yes, Can clear=No
[ 2954.953600]   NMI Exiting: Can set=Yes, Can clear=No
[ 2954.953601]   Virtual NMIs: Can set=Yes, Can clear=No
[ 2954.953602]   Activate VMX Preemption Timer: Can set=Yes, Can clear=No
[ 2954.953603]   Process Posted Interrupts: Can set=Yes, Can clear=No
```

## Answers

1. I did the project myself.

2. For this project, start by setting up the Virtualization environment. For this project, you need to set up a Virtualization environment where the VMX nested virtualization feature is enabled. In Virtualbox on an Intel machine, that requires the use of VBoxManage in order to check the nested virtualization checkbox in the VM settings. Configurations can be found [here](https://youtube.com/watch?v=JMT2qimlL9Q&ab_channel=DavidBombal). You can check if the setup is correct by running `<section>cat /proc/cpuinfo | more</section>`, and if you see <b>vmx</b> under flags the setup is correct. Next, download the cmpe283-1.c and the Makefile to your documents. For this project you will change the MSR index in the cmpe283-1.c file in the line `<section>#define IA32_VMX_PINBASED_CTLS</section>`. Each change in the MSR index will generate a different output for kernel info. The table for the MSR indexes used are listed below:

| MSR Name                         | MSRIndex | Notes                                                             |
|----------------------------------|----------|-------------------------------------------------------------------|
| IndexNotesIA32_VMX_PINBASED_CTLS | 0x481    | Use this MSR for pinbased controls if no true controls capability |
| IA32_VMX_PROCBASED_CTLS          | 0x482    | Use this MSR for procbased controls if no truecontrols capability |
| IA32_VMX_PROCBASED_CTLS2         | 0x48B    | Use this MSR for secondary procbased controls, if available       |
| IA32_VMX_EXIT_CTLS               | 0x483    | Use this MSR for exit controls if no true controls capability     |
| IA32_VMX_ENTRY_CTLS              | 0x484    | Use this MSR for entry controls if no true controls capability    |


## Technologies
* Ubuntu on Oracle Virtualbox

