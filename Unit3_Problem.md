
Chapter 2: P19, P20, P21
Chapter 3: R2, R3, R4, R5, R6

### P19. In this problem, we use the useful dig tool available on Unix and Linux hosts to explore the hierarchy of DNS servers. Recall that in Figure 2.19 , a DNS server in the DNS hierarchy delegates a DNS query to a DNS server lower in the hierarchy, by sending back to the DNS client the name of that lower-level DNS server. First read the man page for dig, and then answer the following questions. 
a. Starting with a root DNS server (from one of the root servers [a-m].root-servers.net), initiate a sequence of queries for the IP address for your department’s Web server by using dig. Show the list of the names of DNS servers in the delegation chain in answering your query.
b. Repeat part (a) for several popular Web sites, such as google.com, yahoo.com, or amazon.com.

### P20. Suppose you can access the caches in the local DNS servers of your department. Can you propose a way to roughly determine the Web servers (outside your department) that are most popular among the users in your department? Explain.

- We can periodically take a snapshot of the DNS caches in the local DNS servers. The Web server that appears most frequently in the DNS caches is the most popular server. This is because if more users are intrested in a Web Server, then DNS requests for that server are more frequently sent by users 

### P21. Suppose that your department has a local DNS server for all computers in the department. You are an ordinary user (i.e., not a network/system administrator). Can you determine if an external Web site was likely accessed from a computer in your department a couple of seconds ago? Explain.

- Local DNS (Domain Naming Server) resolver 
- The key functionality of the DNS resolver is to resolve (translate) the DNS name to the DNS name to the respective IP (Internet Protocol) address. 
- The DNS resolver cache in the client will store the records of the recent DNS lookups 
- The command "ipconfig/displaydns" helps to view the records stored in the cache of the DNS resolver

Process to identify, if an external Web site is accessed from a computer by accessing local DNS server, the (ipconfig /displaydns) will show the partial list of DNS records that are stored in the cache of the DNS resolver. By examing the record, it is possible to identify that an external website is accessded from computer in the department or not 

### R2. Consider a planet where everyone belongs to a family of six, every family lives in its own house, each house has a unique address, and each person in a given house has a unique name. Suppose this planet has a mail service that delivers letters from source house to destination house. The mail service requires that (1) the letter be in an envelope, and that (2) the address of the destination house (and nothing more) be clearly written on the envelope. Suppose each family has a delegate family member who collects and distributes letters for the other family members. The letters do not necessarily provide any indication of the recipients of the letters.
- a. Using the solution to Problem R1 above as inspiration, describe a protocol that the delegates can use to deliver letters from a sending family member to a receiving family
 member.
      - For sending a letter, the family member is required to give the delegate the letter itself, the address of the destination house, and the name of the recipient. The delegate clearly writes the recipient's name on the top of the letter. The delegate then puts the letter in an envelope and writes the address of the destination house on the envelope. The delegate then gives the letter to the planet's mail service. At the receiving side, the delegate receives the letter from the mail service, takes the letter out of the envelope, and takes note of the recipient name written at the top of the letter. The delegate then gives the letter to the family member with this name.
- b. In your protocol, does the mail service ever have to open the envelope and examine the letter in order to provide its service?
  - No, the mail service does not have to open the envelope; it only examines the address on the envelope

### R3. Consider a TCP connection between Host A and Host B. Suppose that the TCP segments traveling from Host A to Host B have source port number x and destination port number y. What are the source and destination port numbers for the segments traveling from Host B to Host A?

- Source is y and Destination x 

### R4. Describe why an application developer might choose to run an application over UDP rather than TCP.

- Transmission Control Protocol (TCP): Transmission Control Protocol is a connection oriented protocol that establishes the connections between the computers before sending the data 

- User Datagram Protocol (UDP): User Datagram Protocol is a connectionless protocol in while data is sent to destination computer without checking whether the system is ready to receives the data or not 

- The reasons why an application developer chooses to run an application over UDP rather than TCP are as follows:
  - At the time of congestion, the TCP's congestion control suffocates the application's sending rate. Thus, many application developers don't want their applications to use TCP's congestion control. 
  - When application runs over UDP, many more active clients can be supported by the server which is devoted to a particular application 
  - Eventhough data transfer by TCP is reliable, some applications do not need reliable TCP data transfer. Therefore, application developers prefer UDP.
  - Generally, designer of IP video conference applications and IP telephony run their applications over UDP to avoid TCP congestion control 

### R5.  Why is it that voice and video traffic is often sent over TCP rather than UDP in today’s Internet? (Hint: The answer we are looking for has nothing to do with TCP’s congestion-control mechanism.)

- Most firewalls are configured to block UDP traffic, using TCP for video and voice traffic lets the traffic though the firewalls. So, that voice and video traffic is often sent over TCP rather than UDP in today's interent 

