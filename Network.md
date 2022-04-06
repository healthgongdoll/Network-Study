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
 Data flows need to be "multiplexed"
- Multiple input streams must share the medium 
- It must be possible to "demultiplex" at the destimation 

Multiple Methods 
- Time division multiplexing (time quotas) 
- Frequency division multiplexing (different frequencies) 
- Code division multiplexing (different representations of data) 
- Orthogonal multiplexing (combination of techniques) 

Problems
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

Application <------------->  Application
Transport   <------------->  Transport
Network     <---Network--->  Network 
  Link <---> Link<-->Link <---> Link
Physical Medium        Physical Medium 

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
