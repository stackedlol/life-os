---
tags: cloud
---

### benefits of high availability and scalability in the cloud 
- when building or deploying a [[cloud-computing]] application, two of the biggest considerations are...
	- **uptime** (==availability==)
	- **handling demand** (==scalability==)

### high availability
- **SLA**: formal agreement between service provider and customer
- provides information on **uptime** and **downtime** and **credit** if SLA is not met
- [[azure]] SLA's are represented as a percentage (higher percentage = less downtime)

### scalability
- refers to the ability to adjust resources to meed demand
- doesn't let you overpay for services, thanks to consumption based model

	1. **vertical** - is focused on increasing or decreasing capabilities of resources
		- add more or lower CPU's or RAM to the virtual machine to meed demand

	2. **horizontal** - adding or or subtracting the number of resources
		- adding or subtracting additional virtual machines or containers

### reliability
- the ability of a system to recover from failures  and continue to function
- the cloud enables you to have resources deployed in regions around the world


### predictability
- focused on
	- performance predictability
	-  cost predictability

### performance
- focused on predicting the resources needed to deliver a positive experience for customers
	- **autoscaling** - auto deploying additional resources to meed demand
	- **load balancing** - help redirect some of the overload to less stressed areas
	- **high availability** - amount of uptime and downtime



