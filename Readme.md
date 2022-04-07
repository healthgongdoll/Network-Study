# Network-Study

This is Jay Chung's Computer Network's study note

- Unit1 : Design of Internet 
- Unit2 : The Internet Protocol
- Unit3 : DNS, NAT and Multiplexing
- Unit4 : Performance
- Unit5 : Reliable Transfer and TCP
- Unit6 : Application Layer Protocol
- Unit7 : Security

## Unit1

### Introduction 

Laptops, smartphones, tablets, TVs, gamming consoles, home seucirty systems and more are being connected to the Interent, we call **hosts** or **end systems**. 

End systems are connected together by a network of **communication links** and **packet switches**

Different links can transmit data at different rates with **Transmission rate** of a link measured in bits/second. When one end system has data to send to another end system, the sending end system segments the data and adds header bytes to the each segment. The resulting packages of information are known as **Packets**

Today's Internet are **Routers** and **Link-Layer Switches**. Link Layer switches are typically used in access networks, while routers are typically used in the network core. 

End systems access Internet through **Internet Service Providers (ISPs).** Each ISP is in itself network of packet switches and communication links. ISPs provide a variety of types of network access to the end systems, including residential braodband access such as cable modem or DSL, high speed local area network acess and mobile wireless access. 

### How Data is sent?

#### Circuit switching
- Dedicated route between source and destination
- Single stream of bytes per route 
- TDM/FDM/CDM multiplexing

#### Packet switching
 - Data is divided in packets that are sent individually 
 - Medium is occupied only during the transmission of the packet 
 - Statistical multiplexing 
 - **Packet** is a unit of data moved through the Internet 
 - Each Packet is **self-contained** (Contains source and destination address / Independently routed from source to destination) 
 - Failure handled by **Best Effort** approach

### Multiplexing 
 **Data flows need to be "multiplexed"**
- Multiple input streams must share the medium 
- It must be possible to "demultiplex" at the destimation 

**Multiple Methods** 
- Time division multiplexing (time quotas) 
- Frequency division multiplexing (different frequencies) 
- Code division multiplexing (different representations of data) 
- Orthogonal multiplexing (combination of techniques) 

**Problems**
- Not efficient for dynamic flows 
- Complex interaction of new data sources 

### IP Address 
Every Machine reachable on the Interent has at least one IP address
- Technically, each interface has at least one 

Internally, each IP address is a sequence of 32 bits (IPv4)

For easier human recognition, represented as 4 8-bit unsigned integer: a.b.c.d (0-255)

Some addresses are reserved. 

### Packet switching and Routers

To get a packet to its recipient, each machine sends it to the router that is believed to be closet to the destination 
- Similar to a road interaction 

Router looks up destination IP address in a forwarding table to determine next hop.

There may be several possible path to take 

### Protocols 
- Roles of communicating entities 
- Format of messages
- Order of messages
- Actions taken on the transmission, receipt of a message, or other event 

A fully-defined protocol must provide a proper action for any event in any state 

### Request-Response Protocols 
Many protocols on the Inernet are request-response protocols
- Requestor (**usually client**) sends a request 
- Receiver (**usually server**) sends a response 
- Well-defined rules for whose turn it is 

Some rules can be complicated 
- Server is slow to respond 
- Size of request or response can vary

### Protocol Stack 
```
=======================
|     Application     |   HTTP, Email, File Transfer, Multimedia
=======================
|     Trnasport       |   TCP, UDP
=======================
|      Network        |   IP
=======================
|       Link          |   Ethernet
=======================
|      Physical       |  802.11b/g/n 1000 BASE-T
=======================
```

### Sending Data Through The Task 
```
Application <------------->  Application
Transport   <------------->  Transport
Network     <---Network--->  Network 
  Link <---> Link<-->Link <---> Link
Physical Medium        Physical Medium 
```
### Protocol Stack Responsiblities 

Transport Layer 
- Identifies process on machine (Resources within process. e.g., browser tab)
- Ensure data arrives in order (if required) 
- Recovers lost data (if required) 

Network Layer 
- Routes packet through routers to destination machine 

Link Layer
- Routes frames to adjacent machines ("direct" connection) 

Physical Layer
- Encodes data appropriately for the physical medium 

### Traceroute 

Traceroute (or **tracert**) is a tool used to determine a path taken to a destination
- sends a packet it hopes no one will use 
- interested in the errors, not the packet itself

Returning errors can tell
- Which router returned it 
- How long it took to return it 

Does not always work: relies on routers that may decided not to send answers 

May find multiple routes to same host 

## Unit2

### Interent Organization Structure 
Organized into entities called **Autonomous System (ASs)** 
- Remnant of old private networks 

Each Autonomous System:
- is assigned **a range/ collection of IP addresses**
- is responsible for **Routing to address it owns**
- is reponsible for **Routing to addresses that are not its responsibility
- uses address ranges represented in **CIDR form**

### Who Controls an AS?
- Some compnaies do the end systems 
- Some companies do long haul line (backbones) 
  - within a country or region
  - around the world 
- Some do a mix of both 
- Some companies are consortiums 
- Networks often connect to each other at Internet Exchanges 
- Routers need to know how to get to each possible destination 

### Autonomous Systems

```
=======                                                       =========
| SFU |                                                ______ |  UofT |
======= =======                       ========        |       =========
   |    | UBC |                       |GTAnet| _______|       =========
   |    =======                       ========        |______ | YorkU |
   |_______|__________                  |                     =========
                      |                 |
                   ===========          |
                   | Canarie | _________|
                   ===========
                   
```
Each of AS handles several range of IP addresses 

### Classes Inter-Domain Routing (CIDR)
AS recieves a **range of addresses**
All routing from outside the AS only need to reach the AS that contains it 
- Routing table **does not need to list** every single IP address 
- Routing information propagation is also compacted 
- **AS takes care of internal routing**

### CIDR Prefix Matching 
How can we represent a range of addresses?
- Example: 123.123.96.16/19 
  - Represented by some address in range, followed by a number of fixed bits 
  - All addresses in range have the same fixed bits (first 19 bits)
- Fixed bits are called **network address** (19 bits)
- Unfixed bits are called **host address** (32-19 = 13 bits) 

### CIDR Prefix Example
CIDR Address: 123.123.96.16/19

01111011 01111011 01100000 00010000

**01111011** **01111011** **011**00000 00010000 (**19 Network address** 13 Host address) 

### Alternavtive Format: NETMASK
CIDR Address: 123.123.96.16/255.255.224.0

**11111111 11111111 111**00000 00000000    (**1: Network Address**, 0: Host Address)

255      255      224       0

### Computing The Network Address

```
CIDR Address: 192.168.45.24/255.255.240.0
192.168.45.24  = 11000000 10101000 00101101 00011000
255.255.240.0  = 11111111 11111111 11110000 00000000
Net address    = 11000000 10101000 00100000 00000000

Destination IP is 192.168.49.104
192.168.49.104 = 11000000 10101000 00110001 01101000
255.255.240.0  = 11111111 11111111 11110000 00000000
Net address    = 11000000 10101000 00110000 00000000
```
### CIDR Prefix Matching
The first and last addresses are never used for an actual host
- Generally the first address is used to **represent the network **
- The last address in range is used for **broadcast **

### Address Range Division
How to divide an address range into two?

Set **first unfixed bit** as fixed bit in two ranges 
 - One range has that bit as 0, the other has that bit as 1
 - Repeat if multiple ranges required 

### Address Range Division Example 

![image](https://user-images.githubusercontent.com/79100627/162079633-7ebe5b31-c97e-47d7-bf67-58c3599921af.png)

### Address Range Aggregation
Ranges can be aggregated if, when combined:
 - All ranges being aggregated are covered
 - New range does not include groups not being aggregated

Useful for collapsing range information 
- Example: when **advertising network ranges** 

### Address Range Aggregation 
![image](https://user-images.githubusercontent.com/79100627/162080048-ff2fbf4b-da49-41a0-a03a-696d9160ca04.png)

### Address Rnage Aggregation Can't Aggregate 
![image](https://user-images.githubusercontent.com/79100627/162080284-0fc85d4b-f021-429d-9cbe-d31b5b528bf1.png)

### Forwarding Table 
Each Router keeps a forwarding table linking, for each IP range, the link and next hop to be used

Formally, the Forwarding Information Base (FIB)

Built from aggregating information retrieved from other routers (routing table, or RIB)

### Longest Prefix Matching 

If more than one range match an IP in the table the **most specific entry** is used

Since ranges are prefixes, the longest prefix is the most specific 

Hence, longest prefix match 

Example: **192.168.35.0/24** is more specific than **192.168.0.0/16**

### Routing: What do we know?

Internet is organized into ASs

Each AS is responsible for some collection of IP addresses 

Each AS must tell other ASs
 - Which addresses it can handle 
 - which addresses it is willing to route to 

### External Routing EBGP

Advertise Prefixes. Each prefix include:
- AS number
- AS path (prevents looping by allowing receiver to look for itself) 
- Next hop to take 

Receiver of advertisement builds forwarding table based on:
- AS management decisions
- Shortest route 
- Closest connecting router (hot potato routing) 

### Routing within an AS 

Internal BGP: communication between external routers about external routes 

Interior Gateway Protocols: routing between hosts in the same network 
- OSPF (Open Shortest Path First): link-state routing, based on network topology
- RIP (Routing Information Protocol): distance-vector routing, based on advertised hop counts 

### AS Agreements 

**Peering agreement**
- Two ASs (e.g. ISPs) pass traffic between each other's customers 

**Transit agreement**
- AS passes traffic from source AS to get to a different AS 

### IP Address Assignment
When Company **"joins"** an ISP it may receive an IP address/range

Alternative: You can get it through different means and tell ISP 
- E.g. Keep your IP from previous ISP 
- ISP will then announce your prefix as reachable through them 
- Usually charged differently 
- ISP gets it (maybe indirectly) from an RIR (Regional Interent Registry) 
  - US/Canada: ARIN
- RIRs get address from IANA (Internet Assigned Numbers Authority) 

### Assigning Individual Addresses 

Network administrators may divide network in smaller subnets 
 - Usually for specific areas or purposes (e.g. departments, labs, etc) 

Severs and desktop computers may be assigned fixed IP addresses manually 

### Assigning Addresses - Problems 

What if the address for several computers needs to change?
- rearrangement of subnets 

Laptops and mobile devices: do they need to change addresses in different networks?

Solution: what if computers asked a central authrotiy for an IP address when connecting to a network?

### DHCP (Dynamic Host Configuration Protocol)

A host that needs an IP address requests one from a server
- What server should a host contact?

Solution: send a broadcast request 

### DHCP Steps 

**DHCP Discover**: client asks server for an IPaddress
**DHCP Offer**: server provides a possible IP address to client 
**DHCP Request**: client accepts the offer and requests to be assigned the IP address
**DCHP ACK**: server acknowledges request and assigns new IP address to client


![image](https://user-images.githubusercontent.com/79100627/162100221-fd17a3bc-3cb1-48ef-a251-2351b1f4714d.png)

### DHCP Offer/ACK includes

- Unique IP Address for client 
- Netmask for local network 
- Lease time
  - How long can you use the IP address before renewing (in seconds)
- Routing information 
  - Usually IP address for only one catch-all router (default gateway) is provided
- Host name, domain name 
- Name server

### After DHCP
The computer got an IP what is next?
- It knows the address range of the local network 
- It knows the router(s) to use for other IPs 

Computer can build the IP datagram

Computer knows IP of the next hop
- Either the destination or the router

But what about the link-layer address?

### Link Layer Address

Each network interface card typically has **one MAC address**

Addresses are, in theory, **globally unique**
 - Usually, if you use the MAC provided with your card, it is 

Assigned by manufacturer 
- First 24 bits: identifies the manufactuer
- Last 24 bits: uniquely set by the manufacturer

## UNIT3

### Naming and Network Structure 

How do we know which destination IP to use? </br>
Problems:
- Humans have hard time remembering numbers
- Addresses can change 

Solution: Map user-freindly names to IP addresses (**This is called DNS Domain Name Service**)
- Names are easier to remember 
- Names can mask address changes 

### implementing a Name Service 
What are Pros and Cons of using 
- **A single centralized server**
  - Pros: easier to synchronize
  - Cons: single point of failure, high congestion and latency
- **A replicated set of server**
  - Pros: Stop the single point of failure
  - Cons: Cost and synchronization problem

### DNS Hierarchy

DNS uses a hierarchy of servers 
 - some machines in hierarchy may be replicated but they don't need to be 

Root name servers are known by most DNS implementations 
- 13 servers 

Load is distribued

Name ownership is distributed 

### DNS Design Challenges 

Performance 
 - OpenDNS alone servers about 100 billion request per day (over 1 million per second) 

Which server contains "the answer" ?
- Does any other server contain a copy?


### Answer to a Regular Query 

```
;; QUESTION SECTION:
;ca.prairielearn.com.       IN       A

;;ANSWER SECTION: 
ca.prairielearn.com   60    IN       A    15.222.173.100
ca.prairielearn.com   60    IN       A    3.96.69.126
```

### ANYCAST 

Some DNS server use a technique called **anycast** </br>
Same IP address is served by multiple hosts </br>
- Each host advertises its IP (or range) to its neighbours </br>
Requestor reach the cloest server 

### ANYCAST LIMITATION

Only stateless UDP-based protocols can be used </br>
- Example: DNS

All host must be able to provide same (or equivalent) data </br>
- Root nameserver's information doesn't change often 

### Limited Number of IP Address

We are running out of IP addresses </br>
Do you actually need a globally unique address? </br>
What would other hosts need your address for? </br>
- Do ohter hosts initiate a connection to your host? </br>
Can several hosts share an IP address? </br>

### NON-Routable IP Address

Some addresses were put in place that can never be advertised publically 
 - Initially used only for local communication (no Interent Connection) 

**Networks:**
- 10.0.0.0/8 (16 million addresses)
- 172.16.0.0/12 (1 million addresses) 
- 192.168.0.0/16 (65,536 addresses) 
- Carrier-grade NAT: 100.64.0.0/10 (4 million addresses) 

### Sharing an Address 

Can several hosts share an IP address?
- If they share an address, how do you distinguish incoming messages?

Solution: NAT **(Network Address Translation)**
- NAT Router gets a **public IP address** 
- All other hosts in the network get a **private network address **

### NAT Router Configuation 

```
===============
| 192.168.0.2 | __
===============   |
                  |
                  |
===============   |        ===============        ===========
| 192.168.0.3 | _________  | 192.168.0.1 | ROUTER |200.1.2.3| _____
===============   |        ===============        ===========
                  |        
                  |
===============   |
| 192.168.0.4 | __|
===============
```

### Connection Multiplexing 
How can you Identify if two messages are part of the same conversation?

### Identifying a Connection

IP address: Local and remote 
 - For incoming messages, local is receiver, remote is sender 
 - For outgoing messages, local is sender, remote is receiver 

Transport-Layer Protocl 
- Typically TCP or UDP 

Transport-Layer **"Address"**
- Port Number 
- Local port and remote port 






