# Pre Security
## Module 1 - Introduction to Cyber Security

### Offensive Security Intro

- To find hidden URLs, we will use a tool called dirb. This tool uses a brute-force approach, by taking a list of potential page names and testing one by one if they exist in your website. This approach works because people use predictable names a lot of times.

- Command -> [[dirb]]

- Offensive security = red team

- Offensive security involves breaking into computer systems, exploiting software bugs, and finding loopholes in applications to gain unauthorized access. The goal is to understand hacker tactics and enhance our security defenses. 

### Defensive Security Intro

- Defensive security = blue team

- Blue Team's two main tasks are preventing intrusions from occurring and detecting intrusions when they do occur and responding properly.

- Some tasks for blue team include cyber security awareness, documenting & managing assets, preventative security, logging & monitoring, and Frameworks, Policies, & Procedures.

- SOC -> Security Operations Center: isa  team of cyber security professionals that monitors the network and its systems to detect malicious cyber security events. Some main interests are: Trends & Vulnerability Awareness, Policy Violations, Unauthorized & Illegal Activity, and Intrusion & Breach Detection.

- Digital Forensics is the application of traditional forensic science processes to digital devices. Digital forensics is used to preserve and analyze digital evidence to aide in the investigation of incidents, such as a breach. This may involve looking at information from: File System, System Memory, System Logs, and Network Logs

- Incident response is how organizations manage security events such as breaches, data leaks and cyber attacks. An incident response process is a defined set of stages to minimize damage, contain the threat and recover fast. The process looks like this: Preparation -> Detection & Analysis -> Containment, Eradication, and Recovery -> Post-Incident Activity
 <img width="1140" height="497" alt="image" src="https://github.com/user-attachments/assets/3360d5f2-0080-4cdb-a957-bbfd05cea3bf" />

- Preparation: Creating the necessary resources and frameworks to handle an incident.

- Detection & Analysis: Using tooling and processes to detect incidents and assess their scope (reach) and severity. Logs can be analyzed for suspicious events.

- Containment, Eradication, and Recovery: Limiting the impact of the incident, such as preventing a virus from spreading and eliminate the cause and restore affected systems.

- Post-Incident Activity: Review the incident overall, how it was handled and could've been prevented. What were the learning points throughout the process?

- SIEM = Security Information and Event Management tool, gathers security-related information and events from various sources and presents them in one dashboard.

### Careers in Cyber

- Security analysts - responsibilities:
    - Work with various stakeholders to analyze the cyber security throughout the company.
    - Compile ongoing reports about the safety of networks, documenting security issues and measures taken in response.
    - Develop security plans, incorporating research on new attack tools and trends, and measures needed across teams to maintain data security.

- Security Engineer - responsibilities:
    - Testing and screening security measures across software.
    - Monitor networks and reports to update systems and mitigate vulnerabilities.
    - Identify and implement systems needed for optimal security.

 - Incident Responder - responsibilities:
    - Developing and adopting a thorough, actionable incident response plan.
    - Maintaining strong security best practices and supporting incident response measures.
    - Post-incident reporting and preparing for future attacks, considering learning and adaptations to take from incidents.

- Digital Forensics Examiner - responsiblities:
    - Collect digital evidence while observing legal procedures.
    - Analyze digital evidence to find answers related to the case.
    - Document your findings and report on the case.

 - Malware Analyst - responsibilities:
    - Carry out static analysis of malicious programs, which entails reverse-engineering.
    - Conduct dynamic analysis of malware ssamples by observing their activities in a controlled evironment.
    - Document and report all findings.

- Penetration Tester - responsibilites:
    - Conduct tests on computer systems, networks, and web-based applications.
    - Perform security assessments, audits, and analyze policies.
    - Evaluate and report on insights, recommending actions for attack prevention.

- Red Teamer - responsibilities:
    - Emulate the role of a threat actor to uncover exploitable vulnerabilities, maintain access and avoid detection.
    - Assess organization's security controls, threat intelligence, and incident response procedures.
    - Evaluate and report on insights, with actionable data for companies to avoid real-world instances.

## Module 2 - Network Fundamentals

### What is Networking?

- Networks are simply things connected. Can be formed by anywhere from 2 devices to billions.

- The internet is one giant network that consists of many, many small networks within itself.

- The first iteration of the Internet was within the ARPANET project in the late 1960s. This project was funded by the U.S. Defense Department and was the first documented network in action. However, it wasn't until 1989 when the Internet as we know it was invented by Tim Berners-Lee by the creation of the World Wide Web (WWW). It wasn't until this point that the Internet started to be used as a repository for storing and sharing information, just like it is today.

- A network can be one of two type: 1) A private network, 2) a public network

- Devices have two means of identification, with one being permeable. These are: 1) An IP Address and 2) A Media Access Control (MAC) Address - think of this as being similar to a serial number.

- An IP Aaddress (or Internet Protocol) address can be used as a way of identifying a host on a network for a period of time, where that IP address can then be associated with another device without the IP address changing.

<img width="1140" height="487" alt="image" src="https://github.com/user-attachments/assets/cb0913a3-39c2-47dc-8199-c8fc4c1371d5" />

- An IP address is a set of numbers that are divided into four octets. The value of each octet will summarise to be the IP address of the device on the network. This number is calculated through a technique known as IP addressing & subnetting.

- An IP address can change from device to device but cannot be active simultaneously more than once wihtin the same network.

- IP Addresses follow a set of standards known as protocols.

- A public address is used to identify the device on the Internet, whereas a private address is used to identify a device amongst other devices.

- Public IP addresses are given by your Internet Service Provider (ISP) at a montly fee (your bill!).

- IPv4 uses a numbering system of 2^32 IP addresses (4.29 billion)

- IPv6 is a new iteration of the Internet Protocol addressing scheme to help tackle the shortage of addresses for IPv5. IPv6 supports up to 2^128 of IP addresses (340 trillion-puls) and is more efficient due to new methodologies.

<img width="736" height="177" alt="image" src="https://github.com/user-attachments/assets/4f0ef524-c522-4db7-924c-45646c45e2ea" />

- MAC Addresses - Devices on a network will all have a physical network interface, which is a microchip board foudn on the device's motherboard. This network interface is assigned a unique address at the factory it was built at, called a MAC (Media Access Control) address. The MAC address is a twelve-character hexadecimal number (a base sixteen numbering system used in computing to represent numbers) split into two's and separatedby a colon. These colons are considered separators. For example, a4:c3:f0:85:ac:2d. The first six characters represent the company that made the network interface, and the last six is a unique number.

<img width="1140" height="669" alt="image" src="https://github.com/user-attachments/assets/c065dd33-b3b5-4ff8-a563-e9f8de4a6280" />

- Ping (ICMP) - Ping is one of hte most fundamental network tooks available to us. Ping uses ICMP (Internet Control Message Protocol) packets to determine the performance of a connection between devices, for example, if the connection exists or is reliable

- The syntax to do a simple ping is ping IP address or website URL

### Intro to LAN

- Local Area Network (LAN)

- Topology - referring to the design or look of the network at hand.

- Star Topology - Devices are individually connected via a central networking device such as a switch or hub. This topology is most commonly found today becasue of its reliability and scalability - despite the cost. Any informatiion sent to a device in this topology is sent via the central device which it connects. Because more cabling and the purchase of dedicated networking equipment is required for this topology, it is more expensive than any other topologies. However, this topology is much more scalable in nature, which means that it is very easy to add more devices as the demand for the network increases. Unfortunately, the more the network scales, the more maintenance is required to keep the network functional.

<img width="1140" height="669" alt="image" src="https://github.com/user-attachments/assets/85be1a2e-4286-4d57-8efd-d3a47142167a" />

- Bus Topology - This type of connection relies upon a single connection which is known as a backbone cable. this type of topology is similar to the leaf off of a tree in the sense that devices (leaves) stem from where the branches are on this cable. Because all data is destined for each deivce travels along the same cable, it is very quickly prone to becoming slow and bottlenecked if devices within teh topology simultaneously requesting data. This bottleneck also results in very difficult troubleshooting because it quickly becomes difficult to identify which device is experiencing issues with data all travelling along the same route. Bus topologies are one of the easier and more cost-efficient topologies to set up because of their expenses, such as cabling or dedicated networking equipment used to connect these devices. Lastly, another disadvantage fo the bus topology is that there is little redundancy in place in case of failures.

<img width="1140" height="801" alt="image" src="https://github.com/user-attachments/assets/9501d4b1-92c2-4f56-9e9b-d2e51a87d666" />

- Ring Topology - The ring topology (also known as token topology) boasts some similarities. Devices such as computers are connected directly to each other to form a loop, meaning there is little cabling required and less dependence on dedicated hardware such as within a star topology. A ring topology works by sending data across the loop until it reaches the destined device, using other devices along the loop to forward the data. Interestingly, a device will only send received data from another device in this topology if it does not have any to send itself. If the device happnes to have data to send, it will send its own data first before sending data from another device. Becasue there is only one direction for data to travel across this topology, it is fairly eaasy to troubleshoot any faults that arise. However, this is a double-edged sword because it isn't an efficient way of data travelling across a network, as it may have to visit multiple devices before reaching the intended device. Lastly, ring topologies are less prone to bottlenecks, such as within a bus topology, as large amounts of traffic are not travlling across the network at any one time.

<img width="878" height="801" alt="image" src="https://github.com/user-attachments/assets/06d9ecef-6ad2-4a20-921f-c14d28a01aaa" />

- What is a Switch? Switches are dedicated devices within  network that are designed to aggregate multiple other devices such as computers, printers, or any other networking-capable device suing ethernet. These various devices plug into a switch's port. Switches are usually found in larger networks such as busineses, schools, or similar-sized networks, where there are many devices to connect to the network. Swithches can connect a large number of devices by having ports of 4, 8, 16, 24, 32, and 64 for devices to plug into. Switches are much more efficient than their lesser counterprt (hubs/repeaters). Switches keep track of what device is connected to which port. This way, when they receive a packet, instead of repeating that packet to every port like a hub would do, it just sends it to the intended target, thus reducing network traffic.

<img width="1409" height="801" alt="image" src="https://github.com/user-attachments/assets/9efc286b-48c8-4e6a-b589-de174a1a4fed" />

- Both siwtches and routers can be connected to one another.

- What is a Router? It's a routers job to connect networks and pass data between them. It does this by using routing (hence the name router!). Routing is the label given to the process of data travelling across networks. Routing involves creating a patth between networks so that this data can be successfully delivered. Routing is useful when devices are connected by many paths.

<img width="1140" height="390" alt="image" src="https://github.com/user-attachments/assets/cacbf02d-2435-4a6d-b7bb-93beacd0f371" />

- Subnetting is the term given to splitting up a network into smaller, minature networks within itself.

<img width="908" height="801" alt="image" src="https://github.com/user-attachments/assets/b50c8769-b527-45a5-9837-4f4a3843822e" />

- Network administrators use subnetting to categorize and assign specific parts of a network to reflect this. Subnetting is achieved by splitting up the number of hosts that can fit within the network, represented by a number called a subnet mask. As we can recall, an IP address is made up of four sections called octets. The same goes for a subnet mask, which is also represented as a number of four bytes (32 bits), ranging from 0 to 255 (0 - 255). Subnets use IP addresses in three different ways: 1) Identify the network address, 2) Identify the host address, 3) identify the default gateway. Default gateways usually use either the first or last host address in a network (.1 or .254).

- Address Resolution Protocol (ARP), is the technology that is responsible for allowing devices to identify themselves on a network. Simply, ARP allows a device to associate its MAC address with an IP address on the network. Each device on a network will keep a log of the MAC address associated with other devices. When devices wish to communicate with another, they will send a broadcast to the entiere network searching for the specific device. Devices can use ARP to find the MAC address (and therefore the physical identifier) of a device for communication.

- How does ARP work? Each device within a network has a ledger to store information on, which is called a cache. In the context of ARP, this cache stores the identifiers of other devices on the network. In order to map these two identifiers together (IP address and MAC address), ARP sends two type of messages: 1) ARP Request & 2) ARP Reply. When an ARP request is sent, a message is broadcasted on the network to other devices asking, "What is the mac address that owns this IP address?" When the other device receives that message, they will only respond if they own that IP address and will send an ARP reply with its MAC address. The requesting device can now remember this mapping and store it in its ARP cache for future use.

<img width="823" height="864" alt="image" src="https://github.com/user-attachments/assets/fc799cd9-65cc-407e-a4b6-e496c9c6b05b" />

- IP addresses can be assigned either manually, by entering them physically into a device, or automatically and most commonly by using a DHCP (Dynamic Host Configuration Protocol) server. When a device connects to a entwork, if it has not already been manually assigned an IP address, it sends out a request (DHCP Discover) to see if any DHCP servers are on the network. The DHCP server then replies back with an IP address the device could use (DHCP Offer). The device then sends a reply confirming it wants the offered IP Address (DHCP Request), and then lastly, the DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address (DHCP ACK).

<img width="636" height="870" alt="image" src="https://github.com/user-attachments/assets/fe591d4a-0603-4ebd-9d12-ca69f1ae090d" />

- OSI (Open Systems Interconnection) Model

- The OSI model is an essential model used in networking. This critical model provides a framework dictating how all networked devices will send, receive, and interpret data. One of the main benefits of the OSI model is that devices can have different functions and designs on a network while communicating with other devices. Data sent across a network that follows the uniformity of the OSI model can be understood by other devies. The OSI model consist of seven layers. Each layer has a different set of responsibilites and is arranges from Layer 7 to Layer 1. At every individual layer that data travels through, specific processes take place, and pieces of information are added to this data.

<img width="1077" height="800" alt="image" src="https://github.com/user-attachments/assets/8ca3ceec-3718-40c0-83bd-90ab95eeee32" />

- Layer 1 - Physical: This layer references  the physical components of the hardware used in networking and is the lowest layer that you will find. Devices use electircal signals to transfer data between each other in a binary numbering system (1's and 0's).

- Layer 2 - Data Link: The data link layer focuses on the physical addressing of the transmission. It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical MAC (Media Access Control) address of the receiving endpoint. Inside every network-enabled computer is a Network Interface Card (NIC) which comes with a unique MAC address to identify it. MAC addresses are set by the manufacturer and literally burnt into the card; they can't be changed - although they can be spoofed.

- Layer 3 - Network: The third layer of the OSI model (network layer) is where the magic of routing & re-assembly of data takes place (from these small chunks to the larger chunk). Firstly, routing simply determines the most optimal path in which these chunks of data should be sent. Some protocols at this layer determine exactly what is the "optimal" path that data should take to reach a device. OSPF (Open Shortest Path First) and RIP (Routing Information Protocol). At this layer, everythign is dealt with via IP addresses. Devices such as routers capable of delivering packets using IP addresses are known as Layer 3 devices - becaus they are capable of working at the third layer of the OSI model.  

- Layer 4 - Transport: Layer 4 of the OSI model plays a vital part in transmitting data across a network and can be a little bit difficult to grasp. When data is sent between devices, it follows one of two different protocols that are decided upon several factors: TCP or UDP.
    - Transmission Control Protocol (TCP) is designed with reliability and guarantee in mind. This protocol reserves a constant connection between the two devies for the amount of time it takes for the data to be sent and received. Not only this, but TCP incorporates error checking into its design. Error checking is how TCP can guarantee htat data is sent from the small chunks in the session layer (Layer 5) has been received and reassembled in the same order. TCP is used for situations such as file sharing, internet browsing or sending an email. This usage is because services require the data to be accurate and complete.
    - User Datagram Protocol (UDP) is not nearly as advances as the TCP protocol. It doesn't boast the many features offered by TCP, such as error checking and reliability. In fact, any data that gets sent via UDP is sent to the computer whether it gets there or not. There is no synchronization between the two devices or guarantee; just hope for the best, and fingers crossed. UDP is useful in situations where there are small pieces of data being sent. For example, protocols used for discovering devices (ARP & DHCP) or larger files such as video streaming (where it is oky if some part of hte vidwo is pixelated).

 - Layer 5 - Session: Once data has been correctly translated or formatted from the presentation layer (Layer 6), the session layer (Layer 5) will begin to create and maintain the connection to other computer which the data is destined. When a connection is established, a session is created. Whils this conneciton is active, so is the session. Teh session layer is also responsible for closing the connection if it hasn't been used in a while or if it is lost. What is worth of noting is that sessions are unique - meaining that data cannot travel over different sessions, but in fact, only accross each session instead.

 - Layer 6 - Presentation: Layer 6 of the OSI model is the layer in which standardization starts to take place. Because software developers can develop any software such as an email client differently, the data still needs to be handled in the same way - no matter how the software works. This layer acts as a translator for data to and from the application layer (Layer 7). Security features such as data encryption (like HTTPS) occur at this layer.

 - Layer 7 - Application: The application layer of the OSI model is the layer that you will be most familiar with. This familiarity is because the application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received. Everyday applications such as email clients, browsers, or file server browing software such as FileZilla proved a friendly, Graphical User Interface (GUI) for users to interact with data sent or received. Other protocols include DNS (Domain Name System), which is how website addresses are translated into IP addresses.

### Packets & Frames

- A packet is a piece of data from Layer 3 (Network Layer) of the OSI model, containing information such as an IP header and payload.

- A frame, however, is used at Layer 2 (Data Link) of the OSI model, which, encapsulates the packet and adds additional information such as MAC addresses.

- A packet using the Internet Protocol will have a set of headers that contain additional pieces of information to the data that is being sent across a network. Some notable headers include:
   - Time to Live - This field sets an expiry timer for the packet to not clog up your network if it never manages to reach a host or escape!
   - Checksum - This field provides integrity checking for protocols such as TCP/IP. If any data is changed, this value will be different from what was expected and therefore corrupt.
   - Source Address - The IP address of the device that the packet is being sent from so that data knows where to return to.
   - Destination Address - The device's IP address the packet is being sent to so that data knows where to travel next.

 - TCP/IP protocol conists of four layers and is arguably just a summarized version of the OSI model. These layers are: 1) Application, 2) Transport, 3) Internet, and 4) Network Interface.

 - Very similar to how the OSI model works, information is added ot each layer of the TCP model as the piece of data (or packet) traverses it.

 - TCP guarantees that any data sent will be received on the other end. This process is named the three-way handshake.

 - TCP packets contain various sections of information known as headers that are added from encapsulation.
     - Source Port - This value is the port opened by the sender to send the TCP packet from. This value is chosen randomly (out of the ports from 0 - 65535 that aren't already in use at that time).
     - Destination Port - This value is the port nubmer that an application or service is running on the remote host (the one receiving data); for example a webserver running on port 80. Unlike the source port, this value is not chosen at random.
     - Source IP - This is the IP address of the device that is sending the packet.
     - Destination IP - This is the IP address of the device that the packet is destined for.
     - Sequence Number - When a connection occurs, the first piece of data transmitted is given a random number.
     - Acknowledgement Number - After a piece of data has been given a sequence number, the number for the next piece of data will have the sequence number +1.
     - Checksum - This value is what gives TCP integrity. A mathematical calculation is made where the output is remembered. When the receiving device performs the mathematical calculation, the data must be corrupt if the output is different from what was sent.
     - Data - This header is where the data, i.e. bytes of a file that is being transmitted is stored.
     - Flag - This header determines how the packet should be handled by either device during the handshake process. Specific flags will determine specific behaviours.
  
- Thre-way handshake - the term given for the process used to establish a connection between two devices. The Three-way handshake communicates using a few special messages. Below are some of the main ones:
   - 1 - SYN - A SYN message is the initial packet sent by a client during the handshake. This packet is used to initiate a conneciton and synchronize the two devices together.
   - 2 - SYN/ACK - This packet is sent by the receiving device (server) to acknowledge the synchronization attempt from the client.
   - 3 - ACK - The acknowledgement packet can be used by either the client or server to acknowledge that a series of messages/packets have been successfully recieved.
   - 4 - DATA - Once a connection has been established, data (such as bytes of a file) is sent via the "DATA" message.
   - 5 - FIN - This packet is used ot cleanly (properly) close the conneciton after it has been complete.
   - \# - RST - This packet abruptly ends all communication. This is the last resport and indicates there was a problem during the process. For example, if the service or application is not working correctly, or the system has faults such as low resources.
 
<img width="981" height="949" alt="image" src="https://github.com/user-attachments/assets/03011fab-cd5b-41b4-a796-9e803d623793" />

-  Any sent data is given a random number sequence and is reconstructed using this number sequence and incrementing by 1. Both computers must agree on the same number sequence for data to be sent in the correct order. This order is agreed upon during three steps.
   - 1 - SYN - Client: Here's my Initial Sequence Number (ISN) to SYNchronize with (0).
   - 2 - SYN/ACK - Server: Here's my Initial Sequence Number (ISN) to SYNchronize with (5,000), and I ACKnowledge your initial number sequence (0).
   - 3 - ACK - Client: I ACKnowledge your Initial Sequence Number (ISN) of (5,000), here is some data that is in my ISN+1 (0+1).
 
- TCP Closing a Connection - First, TCP will close a connection once a device has determined that the other device has successfullly received all of the data. To initiate the closure of a TCP connection, the device will send a "FIN" packet to the other device. Of course, with TCP, the other device will also have to acknowledge this packet.   

<img width="981" height="949" alt="image" src="https://github.com/user-attachments/assets/ed939f8f-41a5-4f8f-ab27-ccc9ac1ac8c4" />

### Extending Your Network

- Port forwarding is an essential component in connecting applications and services to the Inernet. Without port forwarding, applications and services such as web servers are only available to devices within the same direct network.

- Port forwarding is configured at the router of the network.

- A firewall is a device within a network responsible for determining what traffic is allowed to enter and exit. Think of a firewall as border security for a network.

- Sateful Firewall: This type of firewall uses the entire information from a connection; rather than inspecting an individual packet, this firewall determines the behavior of a device based upon the entire connection. This firewall type consumes many resources in comparison to stateless firewalls as the decision making is dynamic. If a connection from a host is bad, ti will block the entire device.

- Stateless Firewall: This firewall type uses a static set of rules to determine whether or not individual packets are acceptable or not. For example a device sending a bad packet will not necessarily mean that the entire device is then blocked. Whilst these firewalls use much fewer resources than alternatives, they are much dumber. If a rule is not exactly matched, it is effectively useless. However, these firewalls are great when receiving large amounts of traffic froma  set of hosts (such as a DDoS attack).

- Virtual Private Network (VPN): Is a technology that allows devices on separate networks to communicate securely by creating a dedicated path between each other over the Internet (known as a tunnel). Devices connected within this tunnel form their own private network.

- VPN allows networks in different goegraphical locations to be connectted, offers privacy, and offers anonymity.

- VPN technology has improved over the years. Existing VPN technologies are:
    - PPP - this technology is used by PPTP to allow for authentication and provide encryption of data. VPNs work by using a private and public certificate. A private key and certificate must match for you to connect. This technology is not capable of leaving a network by itself (non-routable).
    - PPTP - The Point-to-Point Tunneling Protocol (PPTP) is a technology that allows th data from PPP to travel and leave a network. PPTP is very easy to set up and is supported by many devices. It is, however, weakly encrypted in comparison to alternatives.
    - IPSec - Internet Protocol Security (IPsec) encrypts data using the existing Internet Protocol (IP) framework. IPSec is difficult to set up in comparison to alternatives; however, if successful, it boasts strong encryption and is also supported on many devices.
 
- Router - A router's job is to connect networks and pass data between them. It does this by using routing (hence the name router!).

- Routers operate at Layer 3 of the OSI model.

- Switch - A switch is a dedicated networking device responsible for providing a means of connecting to multiple devices. Switches can facilitate many devices (from 3 to 63) using Ethernet cables.

- Switches can operate at both layer 2 and layer 3 of the OSI model. However, these are exclusive in the sense that Layer 2 switches cannot operate at Layer 3.

- VLAN (Virtual Local Area Network) allows specific devices within a network to be virtually split up. This split meas they can all benefit from things such as an Internet connection but are treated separately. 

## Module 3 - How The Web Works
### DNS in Detail

- DNS (Domain Name System) provides a simple way for us to communicate with devices on the internet without remember complex numbers.

- Domain Hierarchy
![[Pasted image 20260213094759.png]]

- TLD (Top-Level Domain): A TLD is the righthand part of a domain name. So, for example, the tryhackme.com TLD is .com. There are two types of TLD, gTLD (Generic Top Level) and ccTLD (CountryCode Top Level Domain). Historically a gTLD was meant to tell the user the domain name's purpose; for example, a .com would be for commercial purposes, .org for organization, .edu for education and .gov for government. And a ccTLD was used for geographical purposes, for example, .ca for sites based in Canada, .co.uk for sites based in the United Kingdom and so on.

- Second-Level Domain: Taking tryhackme.com as an example, the .com part is the TLD, and tryhackme is the Second Level Domain. When registering a domain name, the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens.

- Subdomain: A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it; for example, in the name admin.tryhackme.com the admin part is the subdomain. A subdomain name has the same creation restrictions as a Second-Level Domain, being limited to 63 characters and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens). You can use multiple subdomains split with periods to create longer names, such as jupiter.servers.tryhackme.com. But the length must be kept to 253 characters or less.

- DNS Record Types:
    - A Record: These records resolve to IPv4 addresses, for example 104.26.10.229.
    - AAAA Record: These records resolve to IPv6 addresses, for example 2606:4700:20::681a:be5
    - CNAME Record: These records resolve to another domain name, for example, TryHackMe's online shop has the subdomain name store.tryhackme.com which returns a CNAME record shops.shopify.com. Another DNS request would then be made to shops.shopify.com to work out the IP address.
    - MX Record: These records resolf to the address of the servers that handle the email for the domain you are querying, for example an MX record response for tryhackme.com would look something like alt1.aspmx.l.google.com. These records also come with a priority flag. This tells the cliend in which order to try the servers, this is perfort for if the main server goes down and emai lneeds to be sent to a backup server.
    - TXT Record: TXT records are free text fields where any text-based data can be stored. TXT records have multiple uses, but some common ones can be to list servers that have the authority to send an email on behalf of the domain (this can ehlp in the battle against spam and spoofed email. They can also be used to verify ownership of the domain name when signing up for third party services.

- What happens when you make a DNS request?
    - 1 - When you request a domain name, your computer first checks its local cache to see if you've previously looked up the address recently; if not, a request to your Recursive DNS Server will be made.
    - 2 - A Recursive DNS Server is usually provided by your ISP, but you can also choose your own. This server also has a local cache of recently looked up domain names.
    - 3 - The root servers act as the DNS backbone of the internet; thier job is to redirect you to the correct Top Level Domain Server, depending on your request. If, for exmple, you request www.tryhackme.com, the root server will recognize the Top Level Domain of .com and refer you to the correct TLD server that deals with .com addresses.
    - 4 - The TLD server holds records for where to find the authoritative server to answer the DNS request. The authoritative server is also known as the nameserver for the domain.
    - 5 - An athoritative DNS server is the server that is responsible for storing the DNS records for a particular domain name and where any updates to your domain name DNS records would be made. Depending on the record type, the DNS record is then sent back to the Recursive DNS Server, where a local copy will be cached for future requests and then relayed back to the original client that madde the request. DNS records all come with a TTL (Time To Live) value. 

![[Pasted image 20260213094819.png]]
### HTTP in Detail
- HTTP (HyperText Transfer Protocol)
- HTTP is what's used whenever you view a website, developed by Tim Berners-Lee and his team between 1989 - 1991. 
- HTTPS (HyperText Transfer Protocol Secure)
- HTTPS is the secure version of HTTP. HTTPS data is encrypted so it not only stops people from seeing the data you are receiving and sending, but it also gives you assurances that you're talking to the correct web server and not something impersonating it.
- What is a URL? (Uniform Resource Locater)
![[Pasted image 20260213095238.png]]

	- **Scheme:** This instructs on what protocol to use for accessing the resource such as HTTP, HTTPS, FTP (File Transfer Protocol).
	- **User:** Some services require authentication to log in, you can put a username and password into the URL to log in.
	- **Host:** The domain name or IP address of the server you with to access.
	- **Port:** The Port that you are going to connect to, usually 80 for HTTP and 443 for HTTPS, but this can be hosted on any port between 1  65535.
	- **Path:** The file name or location of the resource you are trying to access.
	- **Query String:** Extra bits of information that can be sent to the requested path. For example, /blog?id=1 woudl tell the blog path that you wish to receive the blog article with the id of 1.
	- **Fragment:** This is a reference to a location on the actual page requested. this is commonly used for pages with long content and can have a certain part of the page directly linked to it, so it is viewable to the user as they access the page. 
- It's possible to make a request to a web server with just one line **GET /HTT/1.1**
- HTTP methods are a way for the client to show their intended action when making an HTTP request.
	- GET Request: This is used for getting information from a web server.
	- POST Request: This is used for submitting data to a web server and potentially creating new records.
	- PUT Request: This is used for submitting data to a web server to update information.
	- DELETE Request: This is used for deleting information/records from a web server. 
- HTTP Status Codes [[HTTP Status Codes]]:

| 100-199 - Information Response | These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common. |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200-299 - Success              | This range of status codes is used to tell the client their request was successful.                                                                                                    |
| 300-399 - Redirection          | These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.                                      |
| 400-499 - Client Errors        | Used to inform the client that there was an error with their request.                                                                                                                  |
| 500-599 - Server Errors        | This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handing the request.                                               |
- Common HTTP Status Codes:

| 200 - OK                     | The request was completed successfully.                                                                                                                                                                                       |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 201 - Created                | A resource has been created (for example a new user or new blog post).                                                                                                                                                        |
| 301 - Move Permanently       | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.                                                                                |
| 302 - Found                  | Similar to the above permanent redirect, bat as the name suggests, this is only a temporary change and it may change again in the near future.                                                                                |
| 400 - Bad Request            | This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send. |
| 401 - Not Authorized         | You are not currently allowed to view this resource until you have authorized with the web application, most commonly with a username and passwod.                                                                            |
| 403 - Forbidden              | You do not have permission to view this resource whether you are logged in or not.                                                                                                                                            |
| 404 - Page Not Found         | The page/resource you requested does not exist.                                                                                                                                                                               |
| 405 - Method Not Allowed     | The resource does not allow this method request, for example, you send a GET request to the resource/create-account when it was expecting a POST request instead.                                                             |
| 500 - Internal Service Error | The server has encountered some kind of error with your request that it doesn't know how to handle properly.                                                                                                                  |
| 503 - Service Unavailable    | This server cannot handle your request as it's either overloaded or down for maintenance.                                                                                                                                     |
- Headers are additional bits of data you can send to the web server when making requests.
- Common Request Headers:
	- **Host:** Some web servers host multiple websites so by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the server.
	- **User-Agent:** This is your browser software and version number, telling the web server your browser software helps it format the website properly for your browser and also some elements of HTML, JavaScript, and CSS are only available in certain browsers.
	- **Content-Length**: When sending data to a web server such as in a form, the content length tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.
	- **Accept-Encoding:** Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.
	- **Cookie:** Data sent to the server to help remember your information.
- Common Response Headers:
	- **Set-Cookie:** Information to store which gets sent back to the web server on each request.
	- **Cache-Control:** How long to store the content of the response in the browser's cache before it requests it again.
	- **Content-Type:** This tells the client what type of data is being returned, i.e., HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content-type header the browser then knows how to process the data.
	- **Content-Encoding:** What method has been used to compress the data to make it smaller when sending over the internet.
### How Websites Work
- There are two major components that make up a website:
	1. Front End (Client-Side) - the way your browser renders a website.
	2. Back End (Server-Side) - a server 



### Module 4 - Linux Fundamentals

## Module 5 - Windows Fundamentals
- The Windows operating system has a long history dating back to 1985, and currently, it is the dominant operating system in both home use and corporate networks. Because of this, Window has always been targeted by hackers & malware writers.
![[Pasted image 20260213085644.png]]
- The above screenshot is an example of a typical Windows Desktop. Each component that makes up the GI is explained below.
	1. The Desktop
	2. Start Menu
	3. Search Box (Cortana)
	4. Task View
	5. Taskbar
	6. Toolbars
	7. Notification Area
- The file system used in modern versions of Windows is the New Technology File System or simply NTFS.
- Before NTFS, there was FAT16/FAT32 (File Allocation Table) and HPFS (High Performance File System).
- You still see FAT partitions in use today. For example, you typically see FAT partitions in USB devices, MicroSD cards, etc. but traditionally not on personal Windows computers/laptops or Windows Servers.
- NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.
- NTFS addresses many limitations of previous file systems; such as:
	1. Supports files larger than 4GB
	2. Set specific permissions on folders and files
	3. Folder and file compression
	4. Encryption (Encryption File System or EFS)
- On NTFS volumes, you can set permissions that grant or deny access to files and folders. The permissions are:
	1. Full control
	2. Modify
	3. Read & Execute
	4. List folder contents
	5. Read
	6. Write
![[Pasted image 20260213090917.png]]
- Another feature of NTFS is Alternate Data Streams (ADS).
- Alternate Data Streams (ADS) is a file attribute specific to Windows NTFS (New Technology File System). 
- Every file has at lease one data stream ($DATA), and ADS allows files to contain more than one stream of data. Natively Windows Explorer doesn't display ADS to the user.
- The Windows folder (C:\Windows) is traditionally known as the folder which contains the Windows operating system.
- The system variables for the Windows directory is %windir%. 
- Per Microsoft, "*Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders*".
- There are many folders within the "Windows" folder. One of the many is **System32**.
- The **System32** folder holds the important files that are critical for the operating system. You should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within the System32 can render the Windows OS not operational. 
- User accounts can be one of two types on a typical local Windows system: Administrator & Standard User.
- The user account type will determine what actions the user can perform on that specific Windows system.
	- An Administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc. 
	- A Standard user can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.\
- When a user account is created, a profile is created for the user. The location for each user profile folder will fall under is C:\Users.
- Each user profile will have the same folders; a few of them are:
	- Desktop
	- Documents
	- Downloads
	- Music
	- Pictures
- Another way to access this information, and then some, is using the Local User and Group Management. Right-click on the Start Menu and click **Run**. Type *Lusrmgr.msc*. 
- To protect the local user with high (elevated) privileges, Microsoft introduced **User Account Control** (UAC). UAC (by default) doesn't apply for the built-in local administrator account. How does UAC work? When a user with an account type of administrator logs into a system, the current session doesn't run with elevated privileges. When an operation requiring higher-level privileges needs to execute, the user will be prompted to confirm if they permit the operation to run. 
- **Task Manager** provides information about the applications and processes currently running on the system. Other information is also available, such as how much CPU and RAM are being utilized, which falls under **Performance**. 