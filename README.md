# VMX_config

> Create a linux kernel module that queries various MSR to determine virtualization features of the CPU

## Table of contents
* [Output](#output)
* [Answers](#answers)

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
