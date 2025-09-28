---
tags: linux
---

> kernel modules = small pieces of code that can be loaded/unloaded into the kernel to support hardware
### kernel modules
- depmod - builds a dependency list of kernel modules
- insmod - insert (load) a module into the kernel
- lsmod - list loaded modules
- modinfo - show details about a module
- modprobe - smarter version of insmod
- rmmod - remove (unload) a module from the kernel

can be used to add support for new hardware (like wifi-card) without rebooting the whole machine

