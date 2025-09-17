---
tags: cloud
---

### what is azure virtual networking
- azure virtual networks and virtual subnets enable azure resources such as VMs, web apps, and databases, to...
	- communicate with each other
	- communicate with users on the internet
	- communicate with on-prem client computers

### networking capabilities
- **isolation and segmentation** - allows you to create multiple isolated virtual networks

- **internet communications** - can enable incoming connections from the internet by assigning a public IP address to an Azure resource

- **communicate between azure resources** - virtual networks can connect to VMs and other azure resources
	- service endpoints can connect to other azure resource types... done to improve security and provide optimal routing between resources (not public)

- **communicate with on-premises resources** - enable you to link resources together in your on-premises environment and within your azure subscription

	- point-to-site virtual private network connections are from a computer outside your organization back into your corporate network 

	- site-to-site virtual private networks ink your on-premises VPN device or gateway to the Azure VPN gateway

	- azure ExpressRoute provides a dedicated private connectivity to azure that doens't travel over the internet

- **route network traffic** - routes traffic between subnets on any connected virtual networks, on-premises networks, and the internet

- **filter network traffic** - enable you to filter traffic between subnets by using the following approaches:
	- network security groups

- connect virtual networks

