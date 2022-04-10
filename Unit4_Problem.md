R11, R16 - R21
P10, P13 - P16

### R11. Suppose there is exactly one packet switch between a sending host and a receiving host. The transmission rates between the sending host and the switch and between the switch and the receiving host are R and R , respectively. Assuming that the switch uses store-and-forward packet switching, what is the total end-to-end delay to send a packet of length L? (Ignore queuing, propagation delay, and processing delay.)

- L/R1 + L/R2

### R16. Consider sending a packet from a source host to a destination host over a fixed route. List the delay components in the end-to-end delay. Which of these delays are constant and which are variable?

- Process Delay - Processing delay is fixed. Processing delay depends on several factors such as time taken to check the packet header, time taken to check errors in the packet 
- Queuing Delay - may be variable. It is the time spent waiting in the queue to be transmitted onto the link
- Propagation Delay - It is fixed, it is the time taken to travel from the beginning of the link to router B
- Transmission Delay - It is fixed. it is the time taken to transmit all of the bits of packet into the link 

### R17. Visit the Transmission Versus Propagation Delay applet at the companion Web site. Among the rates, propagation delay, and packet sizes available, find a combination for which the sender finishes transmitting before the first bit of the packet reaches the receiver. Find another combination for which the first bit of the packet reaches the receiver before the sender finishes transmitting

### R18. How long does it take a packet of length 1,000 bytes to propagate over a link of distance 2,500 km, propagation speed m/s, and transmission rate 2 Mbps? More generally, how long does it take a packet of length L to propagate over a link of distance d, propagation speed s, and transmission rate R bps? Does this delay depend on packet length? Does this delay depend on transmission rate?

Propagation Delay = Distance / Speed of light = 2500 km (2500000) / 2.5 * 10^8 m/s = 0.01 s

Transmission Delay = Length/Rate = 1000 bytes / 2Mbps =  0.004 s

Total = 0.014 s 

Delay depend on packet length is not true

Delay depend on transmission rate is not true 

### R19. Suppose Host A wants to send a large file to Host B. The path from Host A to Host B has three links, of rates R1 = 500 kbps, R2= 2Mbps and R3 = 1Mbps
- a. Assuming no other traffic in the network, what is the throughput for the file transfer?
      - 500 kbps is the throughput Why? because it is the bootleneck of the link 
- b. Suppose the file is 4 million bytes. Dividing the file size by the throughput, roughly how long will it take to transfer the file to Host B?

      - 4 000000 * 8 = 32 000 000 bits 
      - 32 000 000 / 500 000 = 64 seconds
- c. Repeat (a) and (b), but now with R reduced to 100 kbps. 
  - 100 kbps is the bottleneck 
  -  32 000 000 / 100 000 = 320 seconds

### R20. Suppose end system A wants to send a large file to end system B. At a very high level, describe how end system A creates packets from the file. When one of these packets arrives to a router, what information in the packet does the router use to determine the link onto which the packet is forwarded? Why is packet switching in the Internet analogous to driving from one city to another and asking directions along the way?

- Suppose system A want to sent packet to system B steps involvedin this process are given below1.System A first breaks large file into small pieces generallyknown as chunks.2.It adds separate headers for each chunks so that each chunkappers like separate packet.3.Header file in chunks contain ip address of receiver heresystem B.4.Switch system uses IP present in header to determine link todestination .When we travel from one city to another and we don’t knowthe path then we ask for path and go on that which is same likepacket switching process

### P10. Consider a packet of length L that begins at end system A and travels over three links to a destination end system. These three links are connected by two packet switches. Let d, s , and R denote the length, propagation speed, and the transmission rate of link i, for . The packet switch delays each packet by d . Assuming no queuing delays, in terms of d, s , Ri, (i=1,2,3), and L, what is the total end-to-end delay for the packet? Suppose now the packet is 1,500 bytes, the propagation speed on all three links is the transmission rates of all three links are 2 Mbps, the packet switch processing delay is 3 msec, the length of the first link is 5,000 km, the length of the second link is 4,000 km, and the length of the last link is 1,000 km. For these values, what is the end-to-end delay?

```
Known Facts:

A --------------Sw1-----------Sw2------------D
      5000 km        4000 km        1000km 
      
End to End delay = Processing Delay + Queueing Delay + Propagation Delay + Transmission Delay 

Processing Delay = 3 msec 

Queueing Delay = 0

Propagation Delay (i=1,2,3) 

i = 1 = 5000 000 / 2.5 * 10^8 =0.02  = 20 ms
i = 2 = 4000 000 / 2.5 * 10^8 = 0.016 = 16 ms 
i = 3 = 1000 000 / 2.5 * 10^8 = 0.004 = 4 ms 

Transmission Dealy (i=1,2,3) 
i = 1 = 1500 bytes / 2Mbps = 0.006 seconds
i =2 = 1500 bytes / 2Mbps = 0.006
i = 3 = 1500 bytes / 2Mpbs = 0.006 seconds

End to End delay = 6 *3 + 20 + 16 + 4 + 3 + 3 = 64 msec
```

### P13.
- a. Suppose N packets arrive simultaneously to a link at which no packets are currently
being transmitted or queued. Each packet is of length L and the link has transmission
rate R. What is the average queuing delay for the N packets?
- b. Now suppose that N such packets arrive to the link every LN/R seconds. What is the
average queuing delay of a packet?

```
The first packet queuing delay = 0
The second packet queuing delay = L/R
The thrid queuing delay = 2 (L/R) 
...

(N-1) L/(2R)

```
### P14. Consider the queuing delay in a router buffer. Let I denote traffic intensity; that is, I= La/R.Suppose that the queuing delay takes the form for IL/R(1-l) for I<1.
- a. Provide a formula for the total delay, that is, the queuing delay plus the transmission delay.
- b. Plot the total delay as a function of L/R

```
(La/R)L/R(1-I) + L/R 
```

### P16. Consider a router buffer preceding an outbound link. In this problem, you will use Little’s formula, a famous formula from queuing theory. Let N denote the average number of packets in the buffer plus the packet being transmitted. Let a denote the rate of packets arriving at the link. Let d denote the average total delay (i.e., the queuing delay plus the transmission delay) experienced by a packet. Little’s formula is . Suppose that on average, the buffer contains 10 packets, and the average packet queuing delay is 10 msec. The link’s transmission rate is 100 packets/sec. Using Little’s formula, what is the average packet arrival rate, assuming there is no packet loss?
