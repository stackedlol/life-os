---
tags: cloud
---

### what are virtual private networks
- deployed to connect two or more trusted private networks to one another over an untrusted network
- traffic is encrypted while traveling over the untrusted network to prevent eavesdropping on other attacks

### VPN gateways
- is a type of virtual network gateway... enables this
	- connect on-premises data centers to virtual networks through a site-to-site connection
	- connect individual devices to virtual networks through a point-to-site connection
	- connect virtual networks to other virtual networks

> can deploy only one VPN gateway in each virtual network... HOWEVER you can use one gateway to connect multiple locations

- setting up a VPN gateway... which route needs encryption

	- **policy based** - specify the statically the IP address of packets that should be encrypted through each tunnel

	- **route-based** - IPSec tunnels are modeled as a network interface or virtual tunnel interface
		- connections between virtual networks
		- point-to-site connections
		- multisite connections
		- coexistence with azure ExpressRoute gateway