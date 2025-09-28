---
tags: linux
---

### basic boot process

i. BIOS or UEFI
- lives on motherboard
- it's the very first code that runs when you press the power button
- check that the hardware works
- find a bootable device (hard drive, usb, network)
- hand control over to the bootloader

1. **Bootloader**
	- small program that starts the OS
	- lives within the /boot folder ([[file-system-hierarchy]])
	- reads config files to know which kernel to load
	- like GRUB

2. **Kernel**
	- core of linux (manages CPU, memory, and hardware)
	- wakes up the computer parts and tells them how to work together

3. **Initrd** (Initial RAM Disk)
	- before the full system is ready, linux needs a few tools (like drivers for disks)

4. **Initramfs**
	- temporary, compressed file system loaded into memory
	- modern method compared to initrd
	- faster and simpler

5. **Init System**
	- start services
	- mounts additional file systems
	- hands you a login prompt

6. **PXE** (Preboot Execution Environment)
	- boot a system over a network (no local disk)
	- used in big data centers or thin clients
