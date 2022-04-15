Chapter 2: R3, R5, R6, R7, R9, R11-20; P1, P2, P3, P4, P7-P11, P13-P15

### R3. For a communication session between a pair of processes, which process is the client and which is the server?

- The process which initiates the communication is the client; the process that waits to be contacted is the server 

### R5. What information is used by a process running on one host to identify a process running on another host?

- The IP address of the destination host and the port number of the socket in the destination process.

### R6. Suppose you wanted to do a transaction from a remote client to a server as fast as possible. Would you use UDP or TCP? Why?

- I would use UDP. With UDP, the ransaction can be completed in one roundtrip time (RTT) - the client sends the transaction request into a UDP socket, and the server sends the reply back to the client's UDP socket, with TCP, a minimum of two RTTs are needed - one to set up the TCP connection and another for the client to send the request and for the server to send back the reply 

### R7. Referring to Figure 2.4 , we see that none of the applications listed in Figure 2.4 requires both no data loss and timing. Can you conceive of an application that requires no data loss and that is also highly time-sensitive?

- One such example is remote word processing, for example, with Google docs. However, because Google docs runs over the Internet (using TCP), timing guarantees are not provided 

### R9. Recall that TCP can be enhanced with SSL to provide process-to-process security services,including encryption. Does SSL operate at the transport layer or the application layer? If the application developer wants TCP to be enhanced with SSL, what does the developer have to do?

- SSL operates at the application layer. The SSL socekt takes unencrypted data from the application layer, encrypts it and then passes it to the TCP socekt. If the application developer wants TCP to be enhanced with SSL, she has to include the SSL code in the application. 

### R11. Why do HTTP, SMTP, and POP3 run on top of TCP rather than on UDP?

- TCP is a more reliable than UDP because TCP is a connected oriented network where there is guarantee of the transmitted packet in reaching the destination 
- TCP data transmission is accurate 
- IN TCP, all the application data can be received without any gaps in a correct order but UDP does not 
- loss of data in HTTP, SMTP,FTP and POP3 cannot be affordable using the UDP protocol. 

### R12. Consider an e-commerce site that wants to keep a purchase record for each of its customers. Describe how this can be done with cookies

- When User first visits the site, the server creates a unique identification number, creates an entry in its back-end database, and returns this identification number as a cookie number. This cookie number is stored on the user's host and is managed by the browser. During each subsequent visit (and purchase), the browser sends the cookie number back to the site. Thus the site knows when this user (more precisely, this browser) is visiting the site. 

### R13. Describe how Web caching can reduce the delay in receiving a requested object. Will Web caching reduce the delay for all objects requested by a user or for only some of the objects

- Web caching reduces the response time for client request. If there is a high speed connection between the client and the cache, and if the cache has the requested object, then the cache will be able to deliver the object rapidly to the client 

### R14. Telnet into a Web server and send a multiline request message. Include in the request message the If-modified-since: header line to force a response message with the 304 Not Modified status code.

### R15. List several popular messaging apps. Do they use the same protocols as SMS?

### R16. Suppose Alice, with a Web-based e-mail account (such as Hotmail or Gmail), sends a message to Bob, who accesses his mail from his mail server using POP3. Discuss how the message gets from Alice’s host to Bob’s host. Be sure to list the series of application-layer protocols that are used to move the message between the two hosts.

Alice uses Web based e-mail account.

HTTP protocol is used to send the message from Alice browser to web-based mail server. 

From the web-based mail server, the message of the Alice is sent via SMTP 

The message is sent to Bob's mail server though the SMTP server 

From Bob's mail server, teh message is transferred to Bob browser by using POP3 Protocol in order to access the mail 

### R17. Print out the header of an e-mail message you have recently received. How many Received: header lines are there? Analyze each of the header lines in the message



### R18. From a user’s perspective, what is the difference between the download-and-delete mode and the download-and-keep mode in POP3?

In the download- and delete mode, client receives messages from a POP, then delete the messages 

In the download and keep mode, client receives messages from a POP and store messages, never deleted messages 

### R19. Is it possible for an organization’s Web server and mail server to have exactly the same alias for a hostname (for example, foo.com )? What would be the type for the RR that contains the hostname of the mail server?

- Yes, an organization can have the same alias name for both its Web server and its mail server. An MX resource record type contains the host name of the mail server. 

### R20. Look over your received e-mails, and examine the header of a message sent from a user with a .edu e-mail address. Is it possible to determine from the header the IP address of the host from which the message was sent? Do the same for a message sent from a Gmail account.

### P1. True or false?
```
a. A user requests a Web page that consists of some text and three images. For this page,
the client will send one request message and receive four response messages.
b. Two distinct Web pages (for example, www.mit.edu/research.html and
www.mit.edu/students.html ) can be sent over the same persistent connection.
c. With nonpersistent connections between browser and origin server, it is possible for a
single TCP segment to carry two distinct HTTP request messages.
d. The Date: header in the HTTP response message indicates when the object in the
response was last modified.
e. HTTP response messages never have an empty message body.
```
### P2. SMS, iMessage, and WhatsApp are all smartphone real-time messaging systems. After doing some research on the Internet, for each of these systems write one paragraph about the protocols they use. Then write a paragraph explaining how they differ.

### P3. Consider an HTTP client that wants to retrieve a Web document at a given URL. The IP address of the HTTP server is initially unknown. What transport and application-layer protocols besides HTTP are needed in this scenario?

### P4. Consider the following string of ASCII characters that were captured by Wireshark when the browser sent an HTTP GET message (i.e., this is the actual content of an HTTP GET message).The characters `<cr><lf> are carriage return and line-feed characters (that is, the italized character string <cr> in the text below represents the single carriage-return character that was contained at that point in the HTTP header). Answer the following questions, indicating where in the HTTP GET message below you find the answer

![image](https://user-images.githubusercontent.com/79100627/163495877-f5dc1da4-7552-44fa-a26b-3849549f6960.png)


### P7. Suppose within your Web browser you click on a link to obtain a Web page. The IP address for the associated URL is not cached in your local host, so a DNS lookup is necessary to obtain the IP address. Suppose that n DNS servers are visited before your host receives the IP address from DNS; the successive visits incur an RTT of Further suppose that the Web page associated with the link contains exactly one object, consisting of a small amount of HTML text. Let RTT denote the RTT between the local host and the server containing the object. Assuming zero transmission time of the object, how much time elapses from when the client clicks on the link until the client receives the object?

### P8. Referring to Problem P7, suppose the HTML file references eight very small objects on the same server. Neglecting transmission times, how much time elapses with
```
a. Non-persistent HTTP with no parallel TCP connections?
b. Non-persistent HTTP with the browser configured for 5 parallel connections?
c. Persistent HTTP?
```

### P9. Consider Figure 2.12 , for which there is an institutional network connected to the Internet. Suppose that the average object size is 850,000 bits and that the average request rate from the institution’s browsers to the origin servers is 16 requests per second. Also suppose that the amount of time it takes from when the router on the Internet side of the access link forwards an HTTP request until it receives the response is three seconds on average (see Section 2.2.5). Model the total average response time as the sum of the average access delay (that is, the delay from Internet router to institution router) and the average Internet delay. For the average access delay, use where Δ is the average time required to send an object over the access link and b is the arrival rate of objects to the access link

```
a. Find the total average response time.
b. Now suppose a cache is installed in the institutional LAN. Suppose the miss rate is 0.4.
Find the total response time
```

### P10. Consider a short, 10-meter link, over which a sender can transmit at a rate of 150 bits/sec in both directions. Suppose that packets containing data are 100,000 bits long, and packets containing only control (e.g., ACK or handshaking) are 200 bits long. Assume that N parallel connections each get 1/N of the link bandwidth. Now consider the HTTP protocol, and suppose nthat each downloaded object is 100 Kbits long, and that the initial downloaded object contains 10 referenced objects from the same sender. Would parallel downloads via parallel instances of non-persistent HTTP make sense in this case? Now consider persistent HTTP. Do you expect significant gains over the non-persistent case? Justify and explain your answer.

### P11. Consider the scenario introduced in the previous problem. Now suppose that the link is shared by Bob with four other users. Bob uses parallel instances of non-persistent HTTP, and the other four users use non-persistent HTTP without parallel downloads.

```
a. Do Bob’s parallel connections help him get Web pages more quickly? Why or why not?
b. If all five users open five parallel instances of non-persistent HTTP, then would Bob’s
parallel connections still be beneficial? Why or why not?
```
### P13. What is the difference between MAIL FROM : in SMTP and From : in the mail message itself?

### P14. How does SMTP mark the end of a message body? How about HTTP? Can HTTP use the same method as SMTP to mark the end of a message body? Explain.

### P15. Read RFC 5321 for SMTP. What does MTA stand for? Consider the following received spam e-mail (modified from a real spam e-mail). Assuming only the originator of this spam e-mail is malicious and all other hosts are honest, identify the malacious host that has generated this spam e-mail.
