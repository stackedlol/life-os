---
tags: linux
---

### initrd management
- intial RAM disk - temporary filesystem loaded before the full system boots.. contains drivers + tools to mount the real root filesystem

	- dracut - tool to generate/init initramfs images
	- mkinitrd - older tool for creating initrd images

- if you change hardware, you may need to rebuild initrd so the system can boot

