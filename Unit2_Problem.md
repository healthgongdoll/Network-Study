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

### P7. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the following forwarding table

![image](https://user-images.githubusercontent.com/79100627/162335209-fd67198b-9a7b-47be-8a6c-97c5b68c0449.png)

For each of the four interfaces, give the associated range of destination host addresses and the
number of addresses in the range

### P8. Consider a router that interconnects three subnets: Subnet 1, Subnet 2, and Subnet 3. Suppose all of the interfaces in each of these three subnets are required to have the prefix 223.1.17/24. Also suppose that Subnet 1 is required to support at least 60 interfaces, Subnet 2 is to support at least 90 interfaces, and Subnet 3 is to support at least 12 interfaces. Provide three network addresses (of the form a.b.c.d/x) that satisfy these constraints

### P11. Consider a subnet with prefix 128.119.40.128/26. Give an example of one IP address (of form xxx.xxx.xxx.xxx) that can be assigned to this network. Suppose an ISP owns the block of addresses of the form 128.119.40.64/26. Suppose it wants to create four subnets from this block, with each block having the same number of IP addresses. What are the prefixes (of form a.b.c.d/x) for the four subnets?

### P16. Consider the network setup in Figure 4.25 . Suppose that the ISP instead assigns the router the address 24.34.112.235 and that the network address of the home network is 192.168.1/24. 

- a. Assign addresses to all interfaces in the home network.
- b. Suppose each host has two ongoing TCP connections, all to port 80 at host 128.119.40.86. Provide the six corresponding entries in the NAT translation table
