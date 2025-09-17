---
tags: cloud
---


### what are virtual machines?
- VMs provide [[iaas]] in the form of a virtualized server and can be used in many ways
	- take control over the operating system
	- the ability to run custom software
	- use custom hosting configurations

### virtual machine scale sets
- virtual machine scale sets let you create and manage a group of identical, load-balanced VMs
- can build large-scale services for areas such as compute, big data, and container workloads

### virtual machine availability sets 
- are designed to ensure that VMs stagger updates and have varied power and network connectivity, preventing you from losing all your VMs with a single network or power failure

	- **update domain**: the update domain groups VMs that can be rebooted at the same time

	- **fault domain**: groups VMs by common power source and network switch

### when to use virtual machines
- during testing and development
- when running applications in the cloud
- extending your datacenter to the cloud

### virtual machine resources
- size (purpose, number of processor cores, and amount of RAM)
- storage disks (hard disk drives, solid state drives, etc)
- networking (virtual network, public IP address, and port config)