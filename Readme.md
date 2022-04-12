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

### Trnasport Layer Protocols 

**Transmission Control Protocol (TCP)**
- Connection establishment ("Three-way handshake")
- Ordering enforced using sequence numbers (streams) 
- Lost packet resent, managed by TCP itself
- Flow control, congestion control 

**User Datagram Protocol (UDP) **
- No connection establishment 
- No reordering, messages must be fully self-contained (datagrams)
- Best-effort approach, resending is application's responsiblitiy 
- Faster (no recovery, no flow control, no connection establishment) 

Why have UDP?
- To **identify the process responsible for a specific conversion
**

### Handling of Messages through NAT 

When internal client sends message to external server: 
 - Router converts **source IP to router's public IP** 
 - Router converts **source port to some available port** 
 - Router adds entry to NAT table re: conversion 
 - Each "conversation" has **one entry in NAT table **

When response comes from **external server**:
- Router finds NAT entry for destination IP/Port 
- Router changes destination IP/port to value in entry 

### NAT Forwarding Table Example 

```
=============================================================================
Internal IP | Internal Port | Remote IP | Remote Port | WLAN IP  | WLAN Port |
=============================================================================
192.168.0.2 | 9999          | 123.4.5.6 | 80          | 200.1.2.3| 12345     |
------------------------------------------------------------------------------
```

### Server on the INSIDE 

What if the initial connection comes from outside?
- Example: server is insdie the NAT </br>
- Example: connection where both hosts are inside a NAT </br>

NAT conversion will not find an entry in the table 

**Option 1: Manually add a fixed rule**

- Example add a rule that if a connection comes to port 200.1.2.3:8080, it should be forwarded to 192.168.0.2:80 

```
=============================================================================
Internal IP | Internal Port | Remote IP | Remote Port | WLAN IP  | WLAN Port |
=============================================================================
192.168.0.2 | 9999          | 123.4.5.6 | 80          | 200.1.2.3| 12345     |
------------------------------------------------------------------------------
192.168.0.2 |  80           | Any (manual/UPnP entry) | 200.1.2.3| 8080      |
------------------------------------------------------------------------------
```
**Option 2: UPnP** (Universal Plug and Play)

- Protocol that runs on the router and internal host 
- Host asks router to enter a forwarding rule (like the manual rule) 

### Applications and NAT 

Some application-level protocols advertise the IP address 
- Internal host advertise address to be used for connection 
- Example: FTP active mode 
- Example: P2P applications 

If behind NAT, how does client know which IP to use?

Solution: depends on the application
- FTP: use passive mode 
- P2P: typically require manual set up or UPnP 


## Unit 4 

### Network Structure 

Hosts 
- "Things" the users interact with: desktop computers, laptops, cell phones, etc.
- End systems or edge compoenents 

Connecting media 
- Wires, cables, radio waves 

Interconnecting hardware 
- Routers, switches, hubs, firewalls 

Network Interface components 
- Convert digital data to/from transmission signals 

### Network Metrics: Latency 

Latency: delayfrom when something is sent until it is received 
- "Something" depends on context, but must be consistent 

Examples:
- Packet Latency: From start of sending packet until completely received 
- Bit/byte Latency: From start of sending bit/byte until completely received 

### Network Metrics: RTT 

Round Trip Time (RTT): Latency for sending a packet and receiving a response 
- Latency for message + latency for response + processing time 

Easier to compute (single location for clock) </br>
Reported by ping, traceroute, etc </br>

### Network Metrics: Jitter 

Observer that not all ping times are the same </br>
Jitter: variation in latency and/ or RTT </br>
What causes jitter? </br>

### Network Metrics: Throughput 

Throughput: amount of data moved from one location to another in a given time </br>
Usually expressed in bytes per second (B/s, MB/s, etc) or bits per second (bps, Mbps, etc) 

### Network Metrics: Bandwidth 

Bandwidth: maximum rate at which data can be sent over a link
 - Througput is the rate that is actually achieved 

Throughput cannot exceed bandwidth 

### Network Metrics: Goodput 

Goodput: rate at which useful data arrives 
- Does not include headers and encoding costs 

May depend on context and application-layer protocol 

### Bottlenecks 

What is the maximum throughput possible (bandwidth) between two nodes connected by a network?
- Can traffic at maximum bandwidth in all links? 

### Causes of Delay 

- Processing delay: examine packet to decide where to direct it 
- Queueing delay: waiting time to get access to the link 
- Transmission delay: time to actually write the packet onto the medium 
- Propagation delay: time spent to move each bit from source to destination on the transmission medium 
- End to end delay: sum of all sources of delay 

### Traffic Intensity 

How much data can route handle?
- At what rate can the router process data?
- At what rate can the router forward data out?

Queueing: When a router receives data faster than it can dispose of 

### Traffic Intensity Calculation 

Traffic intensity is determined by 
- Number of packets arraving (L)
- Average packet size (a) 
- Transmission rate: rate at which bits are disposed of (R) 

Traffic intensity is, thus: La/R

### Traffic Intensity Rationale 

Traffic intensity helps us understand how busy a link is 

Queuing delay is related to the intensity 
- Queueing delay is delay caused by waiting for queue to clear 
- Packets arriving must wait for packets already there to leave 

### Traffic Intensity vs Queueing Delay 

Suppose La bits/second arrive randomly for an outgoing link in a router 
 - Sustained traffic, not bursts 

Suppose that the router can transmit R bits/second 

Draw a graph of queing delay vs Traffic intensity 
- What does La = R mean?
- What does La > R mean?
- What does La < R mean?
- WHat does La << R mean?

### Traffic Intensity vs Queuing Delay 

Assuming packets arrive at an exponential distribution, delay is given by:

**Delay = S/ 1- U**

Where: </br>
- S is average service time when server is idle
- U is server utilization (traffic intensity) 

### Some Observations 
- Routers don't have inifite buffer space
- If packets arrive faster than they can be disposed of, they may have to be dropped 
- Packets may also be corrupted in transit 
 - These packets must be discarded, since their content is no longer valid 
 - Even routing information (e.g., destination IP) may be corrupted 
- How can a transmission be considered reliable with this in mind?

## Unit 5

### Protocols 

A protocol defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event 

**Key Concepts**
- Format and order of messages 
- Actions to be taken on events 

A fully-defined protocol must provide a proper action for any event in any state 

### Basic Protocol as State Machine

![image](https://user-images.githubusercontent.com/79100627/162867500-bdde913b-7f35-44a7-93fa-3871a40a5f67.png)

### Building a Reliable Protocol 

Let's create a protocol for reliable delivery 
- Send only one packet at a time
- Identify when sending is allowable action 
- Identify when resending is required 
- Enumerate events and actions for both sender and receiver 
- Draw state machine 

### Possible Events and Actions 

Receiver 
- Packet received without problems: **Send ACK**
- Packet received corrupted: **Send NAK**

Sender 
- Data ready to send: **Send Data**
- Receive ACK: **Get ready to send more data**
- Receive NAK: **Resent data**

### Corrupt Response

What if **ACK/NAK is corrupted?**

What if:
- We ignore the corrupt ACK/NAK?
- We treat it as an ACK?
- We treat it as a NAK?

### Dealing with duplicated transfer

How can the receiver deal with a duplicate packet?

What information needs to be included to allow receiver to identify packets as duplicate?

Reminder: Scenario does not lose data, only corrupts

### Possible Events 

Receiver
- Packet 0 received without problems 
- Packet 1 received without problems 
- Receive Corrupt Packet 

Sender 
- Data ready to send
- Receive ACK0/ACK1
- Receive NAK
- Receive Corrupt Response 

### Alternate Bit Protocol 
![image](https://user-images.githubusercontent.com/79100627/162872772-861ff8ce-c04b-44a3-8fd0-c6690d6e1fe3.png)

### Alternate Bit Protocol (Without NAK)

![image](https://user-images.githubusercontent.com/79100627/162872838-2b8859f0-6856-4a87-970e-3139872630e8.png)

### What If A Packet is lost?
- What happens if a packet is lost?
- What happens if an ACK is lost?
- How to determine if a packet is lost?
 - Who determines it? Sender or receiver? 

- What changes are needed on the receiver ? 
- What changes are needed on the sender ?

### Corrupt or Lost? 
- Does it make sense to distinguish corrupt data from lost data?
 - If something is corrupt, we do not know what's corrupt
 - headers may have been corrupted too
 - The corrupt packet may not even be for you !!! 

- So, corrupt data becomes lost data 
 - Usually at link layer 

### Alternate Bit Protocol (TimeOut)

![image](https://user-images.githubusercontent.com/79100627/162873223-bc316cf3-e59c-4cfd-9b4f-3c2749085a7c.png)

### How Long Should TimeOut Be?
- Should it be the same across connections?
- Should it always be same for the same connection?
- What happens if timeout is too long?
- What happens if timeout is too short?
- What measured metric can be used to infer a proper timeout?

### Estimating Timeout
- Simple Average of RTT doesn't respond quickly enough 
  - Also doesn't capture jitter 
- Timeout value must adapt 
 - Track changes in RTT over time
 - Accomodate packet-to-packet deviations due to jitter 

### Timeout Formula 
![image](https://user-images.githubusercontent.com/79100627/162873553-b8bb0e73-48d4-4c32-93fa-40624495d6eb.png)

### Alternatvie Bit Protocol in Practice 

Assume a connection from Vancouver to Montreal 
- RTT is 30ms 
- Link Speed is 1Gbps 
- Packet size is 1000 bytes, including overhead 

How much of bandwidth are we actually using?
- Only one packet is sent at a time 
- Transmission delay, one packet: 8000/10^9 = 0.008ms 
- Utilization: 0.008 / 30 + 0.008 = 0.00027 (or 0.0027%)

How can we solve this?

### Sending multiple Packets 
- Sender can send multiple packets 
- Don't wait for each acknowledgement 
 - Assume most pacekt are successful 
- Sender needs to save sent packets to potentially resend 
 - Size is limited 

### Sender's Window
- Sender's window: range of packets that are stored for potential resend 
- Window only moves when first packet in window is acknowledged 
 - What is other ACKs are received? 
- New Packets are sent only when they "fit" in the window 

### Receiver's Window 
- What if receiver recieves packets out of order?
- Receiver's window: store packets received out of order 
 - If window is 1 packet: out of order packets are dropped 
- Once missing packets arrive, window is processed 
- Packets received beyond the window limit will be discarded 

### Problems to consider 

Sender:
- How does the sender know that data got lost?
- Can lost data be distinguished from a lost ACK?
- If we send more than one packet, how many packets can we remember?

Receiver:
- How can you tell if data is out of order or missing?
- What should be ACKed?

### Go-Back-N Strategy 

Receiver
- When pacekt is received, send ACK for last packet received in order 
- Discard arriving packet if out of order (receiver window is 1) 

Sender
- Can have a specific number of outstanding (unacknowledged) packets in memory: sender's window
- Start timer on first packet sent 
- On timeout go to last unack' ed packet and resend everyting (restart timer) 
- Received ACKs may be cumulative (restart timer on receipt) 

### Selective-Repeat Strategy 

Receiver
- Each packet is acked individually 
- Out of order packet is sotred for later: receiver's window 

Sender
- Can have a specific number of outstanding (unacknowledged) packets in memory: sender's window
- Each packet has its own timer 
- Each packet is individually resent if timeout is reached 
- ACKs received in order move the sender's window 

### Sequence Nubmer Range 

The range of possible sequence number is limited by the number of bits used for it 
- Ex: 3 bits gets numbers 0-7, 8 bits gets numbers 0-255 
- Sequences return to zero (e.g. in range of 0-7, after 7 comes another 0) 

What is the maximum sender window size for the range 0-255?
- maybe easier to compute: what about range 0-3?
- can receiver distinguish a new 0 from a resent old 0?
- Does the answer change for selective reapt vs go-back-N?

Rule: **Sender's Window size + receiver's window size <= sequence number range**

For a range with n numbers (0 to n-1):
Go-back-N
- Receiver's window size is 1
- sender's maximum window size is n-1

Selective repeat 
- any values for window sizes that add up to n is fine 
- for same szie on both sides use lower (n/2) 

### TCP Implementation

Both sides act as sender and receiver 
- All packets have both a sequence number and an ACK 
- Sequence numbers in one direction correspond to ACK numbers in opposite direction
- Sequence numbers are incremented by payloadsize 

Retranmission strategy
- ACKs correspond to first sequence number not yet received (Similar to Go-Back-N)
- Receiver stores packets in its own window (like Selective - Repeat) 

### Flow Control

Should we always send the full window size?

What if the receiving application is slow accepting new data?
- Packets will accumulate in the receiver's buffer 
- Eventually buffer will be full, packets will be dropped 
- Immediately resending this ddata does not resolve the problem 

Receiver will notify the sender how much data it can handle 
- This information is usually included in the ACK 
- Sender adjusts its window size based on this information 

### Congestion Control

What if the network can't handle a full window's worth of data?
- Packets and ACKs will be dropped by the routers 

Missing ACKs are a sign that there is congestion somewhere (in either direction)

Sender can reduce sending window once congesetion is detected
- Example: if some number of ACKs are missing in a period time 

If all packets are ACKed, we can increase the window again

### Congestion Control Strategy 

Additive increase
- Increase congestion window slowly 

Multiplicative decrease 
- If congestion detected, reduced congestion window quickly (divide by two)

Slow start 
- Increase is effectively double every RTT at start 

Fast retransmission
- Three or more ACKs with same number (when different numbers expected) trigger a retransmission without a timeout 

### Effect on throughput 

Throughput is affected by
- Bandwidth of sender's direct network connection
- Receiver's specified window size (Flow Control)
- Sender's adjusted window size (Congesetion Control)

If sender's direct connection is not the bottleneck:
- Another router will experience congestion elsewhere 
- congestion control will reduce transmission speed

### TCP Connection Establishment 

- TCP uses "three way handshake" to establish connection
- Client sends initial SYN message 
  - Initial sequence number for client->server is specified 
- Server responds with SYN/ACK message
  - Client -> Server sequence number is confirmed in ACK
  - Server -> Client initial sequence number is specified 
- Client sends an ACK message
  - Server -> Client sequence number is confirmed in ACK 

### TCP Connection Termination

Side that wants to terminate sends FIN message 
- Ohter side responds with ACK

Other side will also send a FIN message 
- It may not send it immediately since it may have more data to send 
- Also responded with an ACK

Alternative: Connection abortion (RST message)
- Usually used if other side misbehaves or too many timeouts are detected
