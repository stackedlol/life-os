---
tags: azure
---
### physical infrastructure for azure
- starts with **data-centers** or facilities with resources arranged in racks, with dedicated power, cooling, and networking infrastructure

- data-centers are grouped into azure **regions** or **availability zones** that are designed to help you achieve resiliency and reliability for your business workloads

### regions
- is a geographical area on the planet that contains at least one, but potentially multiple data centers that are nearby and networked together with low-latency network

- azure intelligently assigns and controls the resources within each region to ensure workloads are appropriately balanced 

- some services or virtual machines (VM) features are only available in certain regions, such as VM sizes or storage types

> West US, Canada Central, West Europe, Australia East, and Japan West

### availability zones 
- physically separate data centers within an azure region 

- is made up of one or more data centers equipped with independent power, cooling, and networking 

- setup to be an **isolation boundary**... if one zone goes down, the other continues working

- are primarily used for VMs, managed disks, load balancers, and SQL databases

	- zonal services - you pint the resource to a specific zone

	- zone-redundant services - the platform replicates automatically across zones

	- non-regional services - services are always available from Azure geographies and are resilient to zone-wide outages as well as region-wide outages

### region pairs
- most azure regions are paired another region within the same geography... this allows for the replication of resources across a geography that helps reduce the likelihood of interruptions

### sovereign regions
- instances of azure that are isolated from the main instance of azure... used for compliance or legal purposes

	- US DoD central - isolated instances of azure for US government agencies and partners

	- China East/North - these regions are available thorugh a unique partnership between Microsoft and 21Vianet, where microsoft doesn't directly maintain the datacenters 