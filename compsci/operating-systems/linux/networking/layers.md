---
tags: networking
---
### 1. physical layer
- the actual hardware + signals
	- like cables (ethernet & fiber), wifi radio waves, voltage, etc
	- it's about moving the information across a medium

### 2. data link layer
- how devices identify each other on a local network
	- uses MAC addresses (unique Ids burned into NICs)
	- switches operate here
	- ethernet + wifi protocols live here

### 3. network layer
- routing packets between networks
	- uses IP addresses
	- routers operate here
	- decides where the packet goes

### 4. transport layer
- reliability + port numbers
	- 22 = SSH
	- 80 = [[HTTP]]
	- 443 = HTTPS

### 5. session layer
- maintains a connection between apps
	- handles sessions, authentication, keep-alive
	- logging into a website, stay logged in

### 6. presentation layer
 - data formatting and encryption

### 7. application layer
- what the user actually interacts with
	- web browsers
	- email client 
	- APIs + SaaS apps


