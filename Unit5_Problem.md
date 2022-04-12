R9 - R13
P6 - P25, P31 (Don't compute the TCP time-out interval), P37


### R9. In our rdt protocols, why did we need to introduce sequence numbers?
### R10. In our rdt protocols, why did we need to introduce timers?
### R11. Suppose that the roundtrip delay between sender and receiver is constant and known to the sender. Would a timer still be necessary in protocol rdt 3.0 , assuming that packets can be lost? Explain.
### R12. Visit the Go-Back-N Java applet at the companion Web site.
- a. Have the source send five packets, and then pause the animation before any of the five packets reach the destination. Then kill the first packet and resume the animation. Describe what happens.
- b. Repeat the experiment, but now let the first packet reach the destination and kill the first acknowledgment. Describe again what happens.
- c. Finally, try sending six packets. What happens?

### R13. Repeat R12, but now with the Selective Repeat Java applet. How are Selective Repeat and Go-Back-N different?
### P6. Consider our motivation for correcting protocol rdt2.1 . Show that the receiver, shown in Figure 3.57 , when operating with the sender shown in Figure 3.11 , can lead the sender and receiver to enter into a deadlock state, where each is waiting for an event that will never occur.

![image](https://user-images.githubusercontent.com/79100627/162992113-6b421602-97a6-4bcc-8dcf-ca2f4a29f9d6.png)
 ![image](https://user-images.githubusercontent.com/79100627/162992197-5681de82-2dd3-4af5-ba87-81b69f293798.png)

### P7. In protocol rdt3.0 , the ACK packets flowing from the receiver to the sender do not have sequence numbers (although they do have an ACK field that contains the sequence number of the packet they are acknowledging). Why is it that our ACK packets do not require sequence numbers?

![image](https://user-images.githubusercontent.com/79100627/162992635-f511bb3d-3d7a-4cb2-b101-20c179d2fdd3.png)

### P8. Draw the FSM for the receiver side of protocol rdt3.0
![image](https://user-images.githubusercontent.com/79100627/162992764-604db1a2-594d-49e9-9865-7968b01d8ba4.png)

### P9. Give a trace of the operation of protocol rdt3.0 when data packets and acknowledgment packets are garbled. Your trace should be similar to that used in Figure 3.16

### P10. Consider a channel that can lose packets but has a maximum delay that is known. Modify protocol rdt2.1 to include sender timeout and retransmit. Informally argue why your protocol can communicate correctly over this channel.

### P11. Consider the rdt2.2 receiver in Figure 3.14 , and the creation of a new packet in the self-transition (i.e., the transition from the state back to itself) in the Wait-for-0-from-below and the Wait-for-1-from-below states: sndpkt=make_pkt(ACK, 1, checksum) and sndpkt=make_pkt(ACK, 0, checksum) . Would the protocol work correctly if this action were removed from the self-transition in the Wait-for-1-from-below state? Justify your answer. What if this event were removed from the self-transition in the Wait-for-0-from-below state? [Hint: In this latter case, consider what would happen if the first sender-to-receiver packet were corrupted.]

### P12. The sender side of rdt3.0 simply ignores (that is, takes no action on) all received packets that are either in error or have the wrong value in the acknum field of an acknowledgment packet. Suppose that in such circumstances, rdt3.0 were simply to retransmit the current data packet. Would the protocol still work? (Hint: Consider what would happen if there were only bit errors; there are no packet losses but premature timeouts can occur. Consider how many times the nth packet is sent, in the limit as n approaches infinity.)

### P13. Consider the rdt 3.0 protocol. Draw a diagram showing that if the network connection between the sender and receiver can reorder messages (that is, that two messages propagating in the medium between the sender and receiver can be reordered), then the alternating-bit protocol will not work correctly (make sure you clearly identify the sense in which it will not work correctly). Your diagram should have the sender on the left and the receiver on the right, with the time axis running down the page, showing data (D) and acknowledgment (A) message exchange. Make sure you indicate the sequence number associated with any data or acknowledgment segment.

### P14. Consider a reliable data transfer protocol that uses only negative acknowledgments. Suppose the sender sends data only infrequently. Would a NAK-only protocol be preferable to a protocol that uses ACKs? Why? Now suppose the sender has a lot of data to send and the endto-end connection experiences few losses. In this second case, would a NAK-only protocol be preferable to a protocol that uses ACKs? Why?

### P15. Consider the cross-country example shown in Figure 3.17 . How big would the window size have to be for the channel utilization to be greater than 98 percent? Suppose that the size of a packet is 1,500 bytes, including both header fields and data

### P16. Suppose an application uses rdt 3.0 as its transport layer protocol. As the stop-and-wait protocol has very low channel utilization (shown in the cross-country example), the designers of this application let the receiver keep sending back a number (more than two) of alternating ACK 0 and ACK 1 even if the corresponding data have not arrived at the receiver. Would this application design increase the channel utilization? Why? Are there any potential problems with this approach? Explain

### P17. 
```
Consider two network entities, A and B, which are connected by a perfect bi-directional
channel (i.e., any message sent will be received correctly; the channel will not corrupt, lose, or
re-order packets). A and B are to deliver data messages to each other in an alternating manner:
First, A must deliver a message to B, then B must deliver a message to A, then A must deliver a
message to B and so on. If an entity is in a state where it should not attempt to deliver a
message to the other side, and there is an event like rdt_send(data) call from above that
attempts to pass data down for transmission to the other side, this call from above can simply be
ignored with a call to rdt_unable_to_send(data) , which informs the higher layer that it is
currently not able to send data. [Note: This simplifying assumption is made so you don’t have to
worry about buffering data.]
Draw a FSM specification for this protocol (one FSM for A, and one FSM for B!). Note that you
do not have to worry about a reliability mechanism here; the main point of this question is to
create a FSM specification that reflects the synchronized behavior of the two entities. You should
use the following events and actions that have the same meaning as protocol rdt1.0 in Figure
3.9 : rdt_send(data), packet = make_pkt(data) , udt_send(packet),
rdt_rcv(packet) , extract (packet, data), deliver_data(data) . Make sure your
protocol reflects the strict alternation of sending between A and B. Also, make sure to indicate
the initial states for A and B in your FSM descriptions.
```
### P18.
```
P18. In the generic SR protocol that we studied in Section 3.4.4 , the sender transmits a
message as soon as it is available (if it is in the window) without waiting for an acknowledgment.
Suppose now that we want an SR protocol that sends messages two at a time. That is, the
sender will send a pair of messages and will send the next pair of messages only when it knows
that both messages in the first pair have been received correctly.
Suppose that the channel may lose messages but will not corrupt or reorder messages. Design
an error-control protocol for the unidirectional reliable transfer of messages. Give an FSM
description of the sender and receiver. Describe the format of the packets sent between sender
and receiver, and vice versa. If you use any procedure calls other than those in Section 3.4 (for
example, udt_send() , start_timer() , rdt_rcv() , and so on), clearly state their
actions. Give an example (a timeline trace of sender and receiver) showing how your protocol
recovers from a lost packet.
```
### P19.
```
 Consider a scenario in which Host A wants to simultaneously send packets to Hosts B and
C. A is connected to B and C via a broadcast channel—a packet sent by A is carried by the
channel to both B and C. Suppose that the broadcast channel connecting A, B, and C can
independently lose and corrupt packets (and so, for example, a packet sent from A might be
correctly received by B, but not by C). Design a stop-and-wait-like error-control protocol for
reliably transferring packets from A to B and C, such that A will not get new data from the upper
layer until it knows that both B and C have correctly received the current packet. Give FSM
descriptions of A and C. (Hint: The FSM for B should be essentially the same as for C.) Also,
give a description of the packet format(s) used.
```
### P20. 
```
 Consider a scenario in which Host A and Host B want to send messages to Host C. Hosts
A and C are connected by a channel that can lose and corrupt (but not reorder) messages.
Hosts B and C are connected by another channel (independent of the channel connecting A and
C) with the same properties. The transport layer at Host C should alternate in delivering
messages from A and B to the layer above (that is, it should first deliver the data from a packet
from A, then the data from a packet from B, and so on). Design a stop-and-wait-like error-control
protocol for reliably transferring packets from A and B to C, with alternating delivery at C as
described above. Give FSM descriptions of A and C. (Hint: The FSM for B should be essentially
the same as for A.) Also, give a description of the packet format(s) used.
```

### P21.
```
Suppose we have two network entities, A and B. B has a supply of data messages that will
be sent to A according to the following conventions. When A gets a request from the layer above
to get the next data (D) message from B, A must send a request (R) message to B on the A-to-B
channel. Only when B receives an R message can it send a data (D) message back to A on the
B-to-A channel. A should deliver exactly one copy of each D message to the layer above. R
messages can be lost (but not corrupted) in the A-to-B channel; D messages, once sent, are
always delivered correctly. The delay along both channels is unknown and variable.
Design (give an FSM description of) a protocol that incorporates the appropriate mechanisms to
compensate for the loss-prone A-to-B channel and implements message passing to the layer
above at entity A, as discussed above. Use only those mechanisms that are absolutely
necessary.
```
### P22.
```
P22. Consider the GBN protocol with a sender window size of 4 and a sequence number range
of 1,024. Suppose that at time t, the next in-order packet that the receiver is expecting has a
sequence number of k. Assume that the medium does not reorder messages. Answer the
following questions:
a. What are the possible sets of sequence numbers inside the sender’s window at time t?
Justify your answer.
b. What are all possible values of the ACK field in all possible messages currently
propagating back to the sender at time t? Justify your answer.
```

###  P23. Consider the GBN and SR protocols. Suppose the sequence number space is of size k. What is the largest allowable sender window that will avoid the occurrence of problems such as that in Figure 3.27 for each of these protocols?

### P24. Answer true or false to the following questions and briefly justify your answer:
- a. With the SR protocol, it is possible for the sender to receive an ACK for a packet that falls outside of its current window.
- b. With GBN, it is possible for the sender to receive an ACK for a packet that falls outside of its current window.
- c. The alternating-bit protocol is the same as the SR protocol with a sender and receiver window size of 1.
- d. The alternating-bit protocol is the same as the GBN protocol with a sender and receiver window size of 1

### P25. We have said that an application may choose UDP for a transport protocol because UDP offers finer application control (than TCP) of what data is sent in a segment and when.
- a. Why does an application have more control of what data is sent in a segment?
- b. Why does an application have more control on when the segment is sent?


