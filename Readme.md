# Network-Study

This is Jay Chung's Computer Network's study

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

###




