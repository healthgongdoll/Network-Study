Textbox Exercises and Problems

Chapter 4: R21, R22, R24, R26, R27, R29, P5-P12, P16-P18 </br>
Chapter 5: R10-R13, P12-P14, P19 </br>
Chapter 6 R2 (just think about it. The answer might not be what you think.), R10, R11, R12, P14, P15, P16, P21, P22</br>


### R21. Do routers have IP addresses? If so, how many?
  
  They have one address for **each interface** 

### R22. What is the 32-bit binary equivalent of the IP address 223.1.3.27?

  11011111.0000001.0000011.00001111

### R24. Suppose there are three routers between a source host and a destination host. Ignoring fragmentation, an IP datagram sent from the source host to the destination host will travel over how many interfaces? How many forwarding tables will be indexed to move the datagram from the source to the destination?

```
Source ----- R1 -------R2 ------R3 ------ Destination
```

For the interfaces: Source (1) R1 (2) R2 (2) R3 (2) Destination (1) -> we need 8 interfaces </br>
For the forwarding table: 3 forwarding table is needed </br>


### R26. Suppose you purchase a wireless router and connect it to your cable modem. Also suppose that your ISP dynamically assigns your connected device (that is, your wireless router) one IP address. Also suppose that you have five PCs at home that use 802.11 to wirelessly connect to your wireless router. How are IP addresses assigned to the five PCs? Does the wireless router use NAT? Why or why not?

Typically the wireless router includes a DHCP server. DHCP is used to assign IP addresses to the 5 PC and to the router interfaces. Also wireless router also uses NAT as it obtains only one IP address from the ISP. 

### R27. What is meant by the term “route aggregation”? Why is it useful for a router to perform route aggregation?

Routing aggregation is a method of aggregating multiple specific routes and summarizing themm into a single general route </br>
In route aggregation the network address are arranged in a hierarchical manner and each interent service provider is assigned with a contiguous block of IP addresses. </br>

This service provider can further subnet the addresses and assign them to organizations in hierarchical manner.</br>

Route aggregation reduces the number of routes used to acess the network. It also reduces the size of the routing tables, thus avoiding depletion of routes and over usuage of routers to acess the network 

### R29. What is a private network address? Should a datagram with a private network address ever be present in the larger public Internet? Explain

Private network has its own private addresses assigned by the internet service provideers, these addresses can be assigned to a particular organization or a LAN or an Individual. A range of addresses are assigned to a private network and all the devices in the network do not directly connect to the internet, they are connected to a router or a network address translator </br>

- Message can not be published over the interent because router seperates the network address and internet address 

### P5. Consider a datagram network using 32-bit host addresses. Suppose a router has four links numbered 0 thorugh 3, and packets are to be forwarded to the link interfaces as floows

![image](https://user-images.githubusercontent.com/79100627/162333589-22557d7a-c1f2-4048-b3c8-53a914760e2d.png)

- Provide a forwarding table that has five entries, uses longest prefix matching, and forwards packets to the correct link interfaces 

Since we have to provide the forwarding table using longest prefix match 

```
Forwarding table will be like this 

===========================================
|  Prefix Match    |     Link Interface   |
===========================================
| 11100000 00      |          0           | -> because since it's longest prefix match 11100000 0000... ~ 11100000 00111111 
-------------------------------------------
| 11100000 01000000|          1           | -> 11100000 01000000 000... ~ 11100000 01000000 111... 
-------------------------------------------
| 11100000         |          2           | -> 11100000 01000001 ~ 11100000 01111111 111...  
-------------------------------------------
| 11100000   1     |          3           |
-------------------------------------------
| OTHERWISE        |          3           |
-------------------------------------------
```
- describe how your forwarding table determines the appropriate link interface for datagrams with destination addressses

```
11001000 10010001 01010001 01010101
11100001 01000000 11000011 00111100
11100001 10000000 00010001 01110111
Prefix match for first address is 5th entry: link interface 3
Prefix match for second address is 3nd entry: link interface 2
Prefix match for third address is 4th entry: link interface 3
```

### P6. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the following forwarding table:
![image](https://user-images.githubusercontent.com/79100627/162335011-050a1d30-7d08-4136-9891-01df07d0e5db.png)

```
00000000  ~ 00111111-> 0
01000000  ~ 01011111-> 1
01100000  ~ 10111111-> 2
11000000  ~ 11111111-> 3
```

### P7. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the following forwarding table

![image](https://user-images.githubusercontent.com/79100627/162335209-fd67198b-9a7b-47be-8a6c-97c5b68c0449.png)

For each of the four interfaces, give the associated range of destination host addresses and the
number of addresses in the range

```
10000000 ~ 11111111 -> 0
10000000 ~ 10111111 -> 1
11100000 ~ 11111111 -> 2
else 
```

### P8. Consider a router that interconnects three subnets: Subnet 1, Subnet 2, and Subnet 3. Suppose all of the interfaces in each of these three subnets are required to have the prefix 223.1.17/24. Also suppose that Subnet 1 is required to support at least 60 interfaces, Subnet 2 is to support at least 90 interfaces, and Subnet 3 is to support at least 12 interfaces. Provide three network addresses (of the form a.b.c.d/x) that satisfy these constraints

```
Subnet 1 = 60 addresses = 2^6 = 223.1.17.0 / 25
Subnet 2 = 90 addresses = 2^7 = 223.1.17.128 / 26
Subnet 3 = 12 addresses = 2^4 = 223.1.17.192 / 26
```

### P11. Consider a subnet with prefix 128.119.40.128/26. Give an example of one IP address (of form xxx.xxx.xxx.xxx) that can be assigned to this network. Suppose an ISP owns the block of addresses of the form 128.119.40.64/26. Suppose it wants to create four subnets from this block, with each block having the same number of IP addresses. What are the prefixes (of form a.b.c.d/x) for the four subnets?

### P16. Consider the network setup in Figure 4.25 . Suppose that the ISP instead assigns the router the address 24.34.112.235 and that the network address of the home network is 192.168.1/24. 

- a. Assign addresses to all interfaces in the home network.
- b. Suppose each host has two ongoing TCP connections, all to port 80 at host 128.119.40.86. Provide the six corresponding entries in the NAT translation table

### R10. Define and contrast the following terms: subnet, prefix, and BGP route.

- Subnet: sub protion of larger network which does not contain router (No router) 
- Prefix: is the portion of the network CIDR address, CIDR generalizes the notion of subnet addressing (Routers invovled) 
- BGP route: BGP messages along with the TCP connection sent over a link is called BGP session (Routers involved)
  
### R11. How does BGP use the NEXT-HOP attribute? How does it use the AS-PATH attribute?

- BGP protocol (Border Gateway Protocol) is an Inter-AS routing protocol that uses the attributes for routing the paths between the Autonomous System (AS's). 
  - it **obtains the subnet reachability** information from neighboring AS 
  - it **propagates the reachability information to all routers** within an AS 
  - the peers determine the routes to each other AS systems 

- AS-PATH
   - The advertisement passed for the prefix values contains the AS's in the AS-PATH 
   - When the **value of prefix is passed into an AS, it adds the ASN (Autonomous System Number) to the AS-PATH attribute** 
   - The router uses the AS-PATH attribute for detecting and preventing the loop advertisements. When the router finds the AS is already present in the list, the advertisement is rejected by the router 
   - The routers also uses AS-PATH attribute in order to choose among the multiple paths with the same prefix 

- Next-Hop 
  - The next hop is the router interface that initiates the AS PATH 
  - The attribute is necessary in providing the ciritical link between the Inter - AS routing and Intra-AS routing protocols 

### R12. Describe how a network administrator of an upper-tier ISP can implement policy when configuring BGP.

  - Let us assume Assumethe three ISPs such as ISP A, ISP B, ISP C
  - Take ISP B does not carry between ISP A and ISP C 
  - Then ISP A and ISP C have ISP B as their BGP peers 
  - ISP B does not promote to ISP A, which authorization through ISP C

### R13. True or false: When a BGP router receives an advertised path from its neighbor, it must add its own identity to the received path and then send that new path on to all of its neighbors.

  - False, A BGP router can **choose not to add its own identity to the received path** and then send that new path on to all of its neighbors, as BGP is a policy based routing protocol. This can happen in the following scenario. The destination of the received path is some other AS, instead of the BGP router's AS and the BGP router does not want to work as a transit router. 

### P12. Describe how loops in paths can be detected in BGP

  - BGP advertisements contain complete paths showing the AS's the path passes thorugh, and so a router can easily identify a loop because an AS will appear two or more times 

### P13. Will a BGP router always choose the loop-free route with the shortest ASpath length?
  
  - Generally, the router may c**ontain more than one path to any one prefix **
  - In this case, the BGP can apply the some elimination rules to catch the one route 
  - These elimination rules obtained **from the AS_PATH**. it is an inter domain routing. Then choose the loop-free route with the shortest AS_Path Length 

### P14. Consider the network shown below. Suppose AS3 and AS2 are running OSPF for their intra-AS routing protocol. Suppose AS1 and AS4 are running RIP for their intra-AS routing protocol. Suppose eBGP and iBGP are used for the inter-AS routing protocol. Initially suppose there is no physical link between AS2 and AS4. 
- a. Router 3c learns about prefix x from which routing protocol: OSPF, RIP, eBGP, or iBGP? **eBGP**
- b. Router 3a learns about x from which routing protocol? **iBGP**
- c. Router 1c learns about x from which routing protocol? **eBGP**
- d. Router 1d learns about x from which routing protocol? **iBGP**

![image](https://user-images.githubusercontent.com/79100627/162472460-244c0a02-18f2-4ca6-93ca-0a594d845b08.png)

### P19. In Figure 5.13 , suppose that there is another stub network V that is a customer of ISP A. Suppose that B and C have a peering relationship, and A is a customer of both B and C. Suppose that A would like to have the traffic destined to W to come from B only, and the traffic destined to V from either B or C. How should A advertise its routes to B and C? What AS routes does C receive?

 ![image](https://user-images.githubusercontent.com/79100627/162481484-b63c0c84-6721-4a48-9d7e-ab392f9d8c17.png)

```
Number of provider networks=3 (A, B and C).

Number of customer networks=4 (W, V, X and Y ).

Autonomous system AS A  collect the information only from AS B.

Autonomous system AS V A  collect the information only from AS B and AS C.

To decide the information as AS W, need to transfer from AS A to AS B at the AS-PATH. The peering relationship contains AS B and AS C. Then AS C route the packets to AS B to AS A. Thus, AS C follows the AS-PATH CBAW.

So, the route to be advertised by A for B to reach A is AS-PATH AW. The path used by C to reach W is AS-PATH CBAW
```

### R2. If all the links in the Internet were to provide reliable delivery service, would the TCP reliable delivery service be redundant? Why or why not?

- No even if all the individual links were completely reliable, this would not guarantee that the end-to-end communication between hosts was reliable. To provide end-to-end reliability between two arbitrary hosts requires a higher layer service 


### R10. Suppose nodes A, B, and C each attach to the same broadcast LAN (through their adapters). If A sends thousands of IP datagrams to B with each encapsulating frame addressed to the MAC address of B, will C’s adapter process these frames? If so, will C’s adapter pass the IP datagrams in these frames to the network layer C? How would your answers change if A sends frames with the MAC broadcast address?

- C adapter will process the frames but the adapter will not pass the datagrams up to the protocol stack. If the LAN broadcast address is used, then C's adapter will both process the frames and pass the datagrams up the protocol stack

### R11. Why is an ARP query sent within a broadcast frame? Why is an ARP response sent within Problems a frame with a specific destination MAC address?

- An ARP Query is sent in a braodcast frame because the querying host does not which adapter address corresponds to the IP address in qeustion. For the response, the sending node knows the adapter address to which the response should be sent, so there is no need to send a broadcast frame (which would have to be processed by all the other nodes on the LAN). 

### R12. For the network in Figure 6.19 , the router has two ARP modules, each with its own ARP table. Is it possible that the same MAC address appears in both tables?


### P14. Consider three LANs interconnected by two routers, as shown in Figure 6.33 .
- a. Assign IP addresses to all of the interfaces. For Subnet 1 use addresses of the form 192.168.1.xxx; for Subnet 2 uses addresses of the form 192.168.2.xxx; and for Subnet 3 use addresses of the form 192.168.3.xxx.
- b. Assign MAC addresses to all of the adapters.
- c. Consider sending an IP datagram from Host E to Host B. Suppose all of the ARP tables are up to date. Enumerate all the steps, as done for the single-router example in Section 6.4.1 .
- d. Repeat (c), now assuming that the ARP table in the sending host is empty (and the other tables are up to date).

### P15. Consider Figure 6.33 . Now we replace the router between subnets 1 and 2 with a switch S1, and label the router between subnets 2 and 3 as R1.

![image](https://user-images.githubusercontent.com/79100627/162473195-1d359efe-8724-492b-8776-ee5355a86b40.png)

- a. Consider sending an IP datagram from Host E to Host F. Will Host E ask router R1 to help forward the datagram? Why? In the Ethernet frame containing the IP datagram, what are the source and destination IP and MAC addresses?
- b. Suppose E would like to send an IP datagram to B, and assume that E’s ARP cache does not contain B’s MAC address. Will E perform an ARP query to find B’s MAC
poll address? Why? In the Ethernet frame (containing the IP datagram destined to B) that is delivered to router R1, what are the source and destination IP and MAC addresses?
- c. Suppose Host A would like to send an IP datagram to Host B, and neither A’s ARP cache contains B’s MAC address nor does B’s ARP cache contain A’s MAC address. Further suppose that the switch S1’s forwarding table contains entries for Host B and router R1 only. Thus, A will broadcast an ARP request message. What actions will switch S1 perform once it receives the ARP request message? Will router R1 also receive this ARP request message? If so, will R1 forward the message to Subnet 3? Once Host B receives this ARP request message, it will send back to Host A an ARP response message. But will it send an ARP query message to ask for A’s MAC address? Why? What will switch S1 do once it receives an ARP response message from Host B?

### P16. Consider the previous problem, but suppose now that the router between subnets 2 and 3 is replaced by a switch. Answer questions (a)–(c) in the previous problem in this new context.

### P21. Consider Figure 6.33 in problem P14. Provide MAC addresses and IP addresses for the interfaces at Host A, both routers, and Host F. Suppose Host A sends a datagram to Host F.Give the source and destination MAC addresses in the frame encapsulating this IP datagram as the frame is transmitted (i) from A to the left router, (ii) from the left router to the right router, (iii) from the right router to F. Also give the source and destination IP addresses in the IP datagram encapsulated within the frame at each of these points in time.

### P22. Suppose now that the leftmost router in Figure 6.33 is replaced by a switch. Hosts A, B, C, and D and the right router are all star-connected into this switch. Give the source and destination MAC addresses in the frame encapsulating this IP datagram as the frame is transmitted (i) from A to the switch, (ii) from the switch to the right router, (iii) from the right router to F. Also give the source and destination IP addresses in the IP datagram encapsulated within the frame at each of these points in time




