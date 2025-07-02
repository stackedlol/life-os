---
tags: applications
---

> sets or rules or standards that define how data flows between devices or systems

### Why are protocols important?
- Protocols play a critical role in enabling communication and data exchange over the internet.
- There are a set of #standardized-protocols that allow devices and systems from varying manufacturers and vendors to communicate with each other seamlessly.

### Standardized Protocols:
1. **IP Addresses and Domain Names:**

- IP Addresses are unique identifiers assigned to each device on a network. It's used to route date to the correct destination, ensuring that information is sent to the intended recipient. (typically look like "192.168.1.1")

- Domain names, are human-readable names used to identify websites and other internet resources. Domain names are translated into IP addresses using the Domain Name System (DNS)

- DNS is a critical part of the internet infrastructure, responsible for translating domain names into IP addresses. When you enter a domain name into your web browser, your computer sends a DNS query to a DNS server, which returns the corresponding IP address. Your computer then uses that IP address to connect to the website or other resource you've requested. 


==IP AND DNS VISUAL==
![[protocols.excalidraw]]
<!--SR:!2024-04-25,1,227-->


2. **HTTP and HTTPS:** 

- Are two of the most *commonly* used protocols in internet-based applications and services. 

- #HTTP is the protocol used to transfer data between a **client** (such as a web browser) and a **server** (a website). When you visit a website, your web browser sends an HTTP request to the server, asking for the webpage or other resource you've requested. The server then sends an HTTP response back to the client, containing the requested data. 

- #HTTPS is a more *secure* version of HTTP, which encrypts the data being transmitted between the client and server using SSL/TLS (Secure Sockets Layer/Transport Layer Security) encryption. This provides an additional layer of security, helping to protect sensitive information such as login credentials, payment information, and other personal data.

- When you visit a website that uses HTTPS, your web browser will display a padlock icon in the address bar, indicating that the connection is secure. You may also see the letters "https" at the beginning of the website address, rather than "http". 


4. **Building Applications with TCP/IP:**

- The underlying communication protocol used by most internet-based applications and services. It provides a reliable, ordered, and error-checked *delivery of data* between applications running on different devices.

- Key concepts:

	- *PORTS*: are used to identify the application or service running on a device. Each application or service is assigned a unique port number, allowing data to be sent to the correct destination. 

	- *SOCKETS*: is a combination of an IP address and a port number, representing a specific endpoint for communication. Sockets are used to establish connections between devices and transfer data between applications.

	- *CONNECTIONS*: is established between two sockets when two devices want to communicate with each other. During the connection establishment process, the devices negotiate various parameters such as the maximum segment size and window size, which determine how data will be transmitted over the connection.

	- *DATA TRANSFER*: Once a connection is established, data can be transferred between the applications running on each device. Data is typically transmitted in segments, with each segment containing a sequence number and other metadata to ensure reliable delivery. 

- When building applications with TCP/IP... it is crucial to design your application with the appropriate ports, sockets, and connections.


6. **Securing Internet Communication with SSL/TLS:**

- Is a protocol used to encrypt data being transmitted over the internet. Commonly used to provide secure connections over the internet. It is commonly used to provide secure connections for applications such as web browsers, email clients, and file transfer programs. 

- Key Concepts

	- *CERTIFICATES*: SSL/TLS certificates are used to establish trust between the *client* and *server*. They contain information about the identity of the server and are signed by a trusted third party to verify their authenticity.

	- *HANDSHAKE*: During the SSL/TLS handshake process, the client and server exchange information to negotiate the encryption algorithm and other parameters for the secure connection. 

	- *ENCRYPTION*: Once the secure connection is established, data is encrypted using the agreed-upon algorithm and can be transmitted securely between the client and server.

### What are protocols similar to?
- [[api]](s) and protocols serve related purposes in facilitating communication, but are **distinct** concepts. An API is a set of rules and tools that allows *different software applications* to communicate with each other. Whereas, protocols are a set of rules that govern how data is transferred *between machines or systems*.

---

### FLASHCARDS

Why are protocols important?:: Protocols play a critical role in enabling communication and data exchange over the internet.
<!--SR:!2024-04-25,1,200-->
