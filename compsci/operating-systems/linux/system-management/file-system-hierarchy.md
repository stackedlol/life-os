---
tags: operating-system
---

### directories within linux operating system

---
#### home directories

**/home** - user home directories
- where regular user accounts live
- store files, documents, config files, dot-files, downloads etc

**/root** - root user's home directory (top)
- contains root's personal scripts, logs, ssh keys

---
#### user system resources

> things needed once the system is up and running

**/usr** - things not needed for single user mode
- general user programs, libraries, documentation

**/usr/bin** - most command binaries
- most of the user command binaries (ls, cat, grep, nano)
- general purpose tools available for all users

**/usr/lib** - libraries for most commands
- shared code that programs rely on
- the C standard library

---

#### local-specific directories

> software you install manually on the specific machine

**/usr/local** - stuff specific to this computer
- root of local-only software
- anything you build from source usually goes here

**/usr/local/bin** - binaries for this computer (scripts)
- locally installed command binaries
- if you compile and install "htop" from source

---

#### boot & system essentials

**/boot** - boot loader and kernel files
- kernel images
- initrd/initamfs (temporary filesystem for boot)
- GRUB bootloader config and binaries

**/bin** - essential binaries
- essential user commands required for single-user/emergency

**/sbin** - essential system administration binaries
- for root level tools used to bring up the system

**/lib** - libraries for /sbin and /bin 
- think of them like DLLs on windows

---

#### configuration & add-ons

**/etc** - text config files... all text based
- like /etc/hosts or /etc/ssh/sshd_config

**/opt** - add-on software packages
- optional/add-on-software installed outside the normal package manager
- often commercial use software like chrome

---

#### mounting & media

**/media** - removable media mount location
- when you plug in a usb stick

**/mnt** - temp mounted file systems
- temporary mount point for manually mounted filesystems
- mounting an external drive or ISO image

----

### temporary storage

**/tmp** - temp files, usually deleted on reboot
- used by apps for short-lived files
- web browser cache, session files

**/var/tmp** - temp files NOT deleted during reboot
- used when an app needs to persist temp between restarts

---
#### variable data

**/var** - files that change a lot

---






