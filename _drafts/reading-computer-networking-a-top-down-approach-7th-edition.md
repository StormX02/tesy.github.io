---
title: "Reading \"Computer Networking: A Top-Down Approach, 7th Edition\""
categories: [Notes, Reading, Computer]
tags: [computer networks]
---

Here are some notes I took while I was reading [*Computer Networking: A Top-Down Approach*, 7th Edition](https://www.amazon.com/dp/0133594149/) (2016) by [James Kurose](https://www-net.cs.umass.edu/personnel/kurose.html) and [Keith Ross](https://www.nyu.edu/projects/keithwross/).

![front cover](https://images-na.ssl-images-amazon.com/images/I/51xp1%2BoDRML._SX402_BO1,204,203,200_.jpg){: .align-right width="25%" }

This book is divided into 9 chapters:

1. Computer Networks and the Internet
2. Application Layer
3. Transport Layer
4. Network Layer: Data Plane
5. Network Layer: Control Plane
6. The Link Layer and LANs
7. Wireless and Mobile Networks
8. Security in Computer Networks
9. Multimedia Networking

The first chapter presents a broad overview of computer networks and the Internet. They are two different ideas -- the Internet is a network of computer networks.

Chapters 2 to 6 are the core part of this book and organized around the top four layers of the five-layer Internet protocol.

## Chapter 1. Computer Networks and the Internet

## Chapter 2. Application Layer

### Principles of Network Applications

Two predominant architectural paradigms used in modern network applications:

- The client-server architecture
- The peer-to-peer (P2P) architecture

Network applications involve communications between different *processes* running on different hosts. We define the process that initiates the communication as the *client*, and the process that waits to be contacted to begin the session is the *server*. This definition is suitable for both client-server architecture and P2P architecture. In the P2P architecture, a process can be both a client and a server.

A network application sends and receives messages through a *socket*, that's an interface between the application layer and the transport layer. Application developers have fewer controls on the transport layer; They can only choose transport protocols and fix a few transport-layer parameters such as the maximum buffer and maximum segment sizes.

If a process needs to send some messages into another process on another host, it must locate the host and the process. We use an *IP address* to locate the host, and use a *port number* to identify the process. A list of well-known port numbers for all Internet standard protocols can be found at [www.iana.org](https://www.iana.org/).

How to choose a transport protocol? We can broadly classify the possible services provided by transport protocols along four dimensions:

- *Reliable data transfer*

    Packets can get lost within a computer network. For example, a packet can overflow a buffer in a router or can be discarded by a host or router after having some of its bits corrupted. If a protocol provides a guarantee to send packets without loss, it is said to provide reliable data transfer.

- *Throughput*

    Some transport protocols can ensure that the available throughput is always at least r bits/sec.

- *Timing*

    Some transport protocols can ensure that every bit that the sender pumps into the socket arrives at the receiver’s socket no more than a specific time.

- *Security*

    For example, in the sending host, a transport protocol can *encrypt* all data transmitted by the sending process, and in the receiving host, the transport-layer protocol can *decrypt* the data before delivering the data to the receiving process.

The Internet (TCP/IP networks) makes two transport protocols available to applications, *TCP* and *UDP*.

- TCP services
  - *Connection-oriented service*: TCP has the client and server exchange transport-layer control information with each other before the application-level messages begin to flow.
  - *Reliable data transfer service*.
  - *Congestion-control mechanism*. It throttles a sending process (client or server) when the network is congested between the sender and receiver.
- UDP services
  - *Connectionless*. There is no handshaking before the two processes start to communicate.
  - *Unreliable data transfer*.
  - *Without the congestion-control mechanism*.

Neither TCP nor UDP provide any encryption. There is an application layer called *Secure Sockets Layer (SSL)* (An upgrade version is called *[Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security)*). It is an enhancement for TCP, provides critical process-to-process security services, including encryption, data integrity, and end-point authentication.

### The Web and HTTP