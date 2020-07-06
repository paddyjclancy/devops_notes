# Networking

- A network consists of two or more computers that are linked in order to share resources, exchange files, or allow electronic communications.

- May be linked through cables, telephone lines, radio waves, satellites, or infrared light beams.

1) LAN - Local Area Network
	- Restricted to small area
	- Faster speeds
	- High rate of data transfer
	- Households, offices, schools (Internal)
	- Ethernet, WiFi
2) WAN - Wide Area Network
	- Large areas
	- Slower speeds
	- Slower rate of fata transfer
	- Internet


## IP Addresses

- Public
	- Assigned to every device that connects to internet
	- Unique
	- Assigned by service provider
	- Static
		- Never changes
		- Tied to single user, device, server or website
	- Dynamic
		- Changes occasionally, such as reconnecting
	- Shared
		- Same address for group of users
- Private
	- Used by devices communicating on same network

- Unicast
	- One-to-one communication
	- Most common
	- A single identifier
- Broadcast
	- One-to-all communication
	- All possible endpoints in same subnet
	- eg TV / Radio
- Multicast
	- One-to-many
	- Opt-in
	- eg video conferencing, email alerts, subscriptions


### IPv4

- 32-bit integers, expressed in hexadecimal notation
- x.x.x.x
	- 0 >= x >= 255
- 4.2bn potential addresses
- Address exhaustion ...... IPv6


### IPv6

- 128-bit integers, expressed in hexadecimals
- Will improve performance
- Future customisability
- Data packaged
- Most computers are already capable, websites / infrastructure ARE NOT
- Not backwards compatable


### Binary

- 1s and 0s - BITS - True / False
- IP = 32-bit numbers separated into 4x8bits
- Bits converted and displayed in decimal format

---128--64--32--16--8--4--2--1
233--1---1---1---0--1--0--0--1
147--1---0---0---1--0--0--1--1


### Classes

- Somewhat uncommon now
- Mainly used 1981 - 1993
- Replaced by CIDR
- A, B, C = Unicast

A) 1-126.x.x.x
B) 128.x.x.x - 191.255.x.x
C) 192.x.x.x - 223.255.255.x
D) 224.x.x.x - 239.x.x.x
	- Reserved for multicast
E) 240.x.x.x - 255.x.x.254
	- Reserved for experimental purposes


## CDIR - Classless Inter-Domain Routing

- Classless Inter-Domain Routing
- 1993-
- Replaced classful network
- Implemented to slow rate of IPv4 exhaustion
- CIDR blocks are groups of addresses that share the same prefix and contain the same number of bits.

## Subnet / Submask

- Subdivision of IP network
- Monolith --> n-tier
- Families have an identical most significant bit group
- A subnet mask is used to divide an IP address into two parts. 
	- One part identifies the host (computer), the other part identifies the network to which it belongs

## Firewalls

- Defensive border around a network node (eg laptop)
- Monitors & controls traffic depending on set rules
- Prevent attacks eg DoS / DDoS


## Dos / DDos Attacks

- (Distributed) Denial of Service
-
