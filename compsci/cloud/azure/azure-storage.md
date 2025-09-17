---
tags: azure
---

### types of azure storage
- locally redundant storage (LRS)
	- 3 copies of your data
	- all in one datacenter
	- *protects against hardware failures*

- geo-redundant storage (GRS)
	- 6 copies total
	- 3 copies in your main region + 3 copies in a far away region
	- *protects against regional outage*

- read-access geo redundant storage (RA-GRS)

- zone redundant storage (ZRS)
	- 3 copies of your data
	- spread across 3 different zones in one region
	- *protects against a whole zone going down*

- geo-zone redundant storage (GZRS)
	- best of both worlds
	- ZRS inside your main region + extra copies a second region
	- *protects against zone AND region failures*

- read-access geo-zone-redundant storage (RA-GZRS)