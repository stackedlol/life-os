---
tags: azure
---

### azure subscriptions
- are a unit of management, billing, and scale
- logically organize your [[management-infrastructure]] or resource groups and facilitate billing

### the structure of subscriptions
- azure requires an azure subscription... providing authenticated and authorized access to azure products and services

	- billing boundary: this subscription type determines how an azure account is billed for using azure

	- access control boundary: azure applies access-management policies at subscription level, allowing you to manage and control access to resources that users provision with specific subscriptions

> choosing additional subscriptions for resource or billing management purposes...

1. **environments** - you can choose to create subscriptions  to set up separate environments for development and testing, security, or to isolate data for compliance reasons

2. **organizational structures** - you can create subscriptions to reflect different organizational structures
	- limit one team to lower-cost resources
	- allowing IT department full range

3. **billing** - you can create additional subscriptions for billing purposes 

### management groups
- resources are gathered in resource groups and resource groups are gathered into subscriptions

- for many subscriptions, you might need a way to efficiently manage access, policies, and compliance for those subscriptions

- management groups apply governance conditions to the management groups
