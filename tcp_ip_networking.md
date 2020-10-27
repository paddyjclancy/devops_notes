# TCP/IP Based Networking

The conceptual model and set of communications protocols used in the Internet and similar computer networks.

- **TCP:**  Transmission Control Protocol
- **IP:**   Internet Protocol

## TCP

**Some major examples of utilisation:**
  - World Wide Web
  - E-mail
  - Remote administration
  - File Transfer

Provides reliable, ordered, and error-checked delivery of a stream of octets / bytes between *applications* running on *hosts* communicating through an *IP network*.

TCP uses a sequence number to identify each byte of data. The sequence number identifies the order of the bytes sent from each computer so that the data can be reconstructed in order, regardless of any packet reordering, or packet loss that may occur during transmission.

TCP is part of the *transport layer* of the TCP/IP suite, security layers (SSL) often run on top of TCP, and it is connection-orientated. This means a client-server connection must be established before any data can be sent:


![Client-server model](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Client-server-model.svg/1024px-Client-server-model.svg.png)

###### Establishing a Connection:
Before a client attempts to connect with a server, the server must first bind to and listen at a port to open it up for connections: this is called a *passive open*.

Connection established via **three-way handshake:**
  1. **SYN:**
    - The active open is performed by the client sending a SYN to the server.

    - The client sets the segment's sequence number to a random value A.

  2. **SYN-ACK:**
    - In response, the server replies with a SYN-ACK.

    - The acknowledgment number is set to one more than the received sequence number i.e. A+1, and the sequence number that the server chooses for the packet is another random number, B.

  3. **ACK:**
    - Finally, the client sends an ACK back to the server.

    - The sequence number is set to the received acknowledgement value i.e. A+1, and the acknowledgement number is set to one more than the received sequence number i.e. B+1.


## IP

###### IPv4 --2006--> IPv6

Principal communications protocol in the Internet protocol suite for relaying datagrams across network boundaries. Its routing function enables internetworking, and essentially establishes the Internet.

The Internet Protocol is responsible for addressing host interfaces, *encapsulating* data into datagrams and routing datagrams from a source host interface to a destination host interface across one or more IP networks.
  - Each datagram has two components: a header and a payload. The IP header includes source IP address, destination IP address, and other metadata needed to route and deliver the datagram. The payload is the data that is transported. This method of nesting the data payload in a packet with a header is called encapsulation.

IP has the task of delivering packets from the source host to the destination host solely based on the IP addresses in the packet headers.
  - For this purpose, IP defines packet structures that encapsulate the data to be delivered.
  - It also defines addressing methods that are used to label the datagram with source and destination information.

###### See [networking.md](https://github.com/paddyjclancy/devops_notes/blob/master/networking.md) for further info on IP addressing
