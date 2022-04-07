Textbox Exercises and Problems

Chapter 4: R21, R22, R24, R26, R27, R29, P5-P12, P16-P18
Chapter 5: R10-R13, P12-P14, P19
Chapter 6 R2 (just think about it. The answer might not be what you think.), R10, R11, R12, P14, P15, P16, P21, P22


### R21. Do routers have IP addresses? If so, how many?

### R22. What is the 32-bit binary equivalent of the IP address 223.1.3.27?

### R24. Suppose there are three routers between a source host and a destination host. Ignoring fragmentation, an IP datagram sent from the source host to the destination host will travel over how many interfaces? How many forwarding tables will be indexed to move the datagram from the source to the destination?

### R26. Suppose you purchase a wireless router and connect it to your cable modem. Also suppose that your ISP dynamically assigns your connected device (that is, your wireless router) one IP address. Also suppose that you have five PCs at home that use 802.11 to wirelessly connect to your wireless router. How are IP addresses assigned to the five PCs? Does the wireless router use NAT? Why or why not?

### R27. What is meant by the term “route aggregation”? Why is it useful for a router to perform route aggregation?

### R29. What is a private network address? Should a datagram with a private network address ever be present in the larger public Internet? Explain

### P5. Consider a datagram network using 32-bit host addresses. Suppose a router has four links numbered 0 thorugh 3, and packets are to be forwarded to the link interfaces as floows

![image](https://user-images.githubusercontent.com/79100627/162333589-22557d7a-c1f2-4048-b3c8-53a914760e2d.png)

- Provide a forwarding table that has five entries, uses longest prefix matching, and forwards packets to the correct link interfaces 
- describe how your forwarding table determines the appropriate link interface for datagrams with destination addressses

### P6. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the following forwarding table:
![image](https://user-images.githubusercontent.com/79100627/162335011-050a1d30-7d08-4136-9891-01df07d0e5db.png)

### P7. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the following forwarding table

![image](https://user-images.githubusercontent.com/79100627/162335209-fd67198b-9a7b-47be-8a6c-97c5b68c0449.png)

For each of the four interfaces, give the associated range of destination host addresses and the
number of addresses in the range

### P8. Consider a router that interconnects three subnets: Subnet 1, Subnet 2, and Subnet 3. Suppose all of the interfaces in each of these three subnets are required to have the prefix 223.1.17/24. Also suppose that Subnet 1 is required to support at least 60 interfaces, Subnet 2 is to support at least 90 interfaces, and Subnet 3 is to support at least 12 interfaces. Provide three network addresses (of the form a.b.c.d/x) that satisfy these constraints

### P11. Consider a subnet with prefix 128.119.40.128/26. Give an example of one IP address (of form xxx.xxx.xxx.xxx) that can be assigned to this network. Suppose an ISP owns the block of addresses of the form 128.119.40.64/26. Suppose it wants to create four subnets from this block, with each block having the same number of IP addresses. What are the prefixes (of form a.b.c.d/x) for the four subnets?


