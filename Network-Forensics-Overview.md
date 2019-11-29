# A Network Forensics Overview

This document will give a brief overview of certain network forensics techniques that are commonly used in the field.

### Technical Fundamentals

There are several sources that contain network based forensic evidence. These include, but not necessarily limited to:

  1. Authentication Servers
  2. Intrusion Detection Systems (IDS)/Intrusion Prevention System (IPS)
  3. Firewalls
  4. Web proxies
  5. Application Servers
  6. Central Log Servers
  
## Technical Fundamentals

There are four main principles of networking:

* Protocols
* OSI Model
* TCP/IP 
* Ports

### Protocols

Protocols are the standards implemented that allow for communication between different hardware, software and OS's across a network.
Any one protocol contains predefined rules that are set by either the manufacturing body, public standard bodies or individuals.
Network designers use TCP/IP and OSI layered standards. Depending on the function and requirementts of the protocol, layer at which the protocol operates on varies. Here are some examples for each layer of the OSI model:

    **Application Layer:**        DNS, DHCP, FTP, HTTPS
    **Presentation Layer:**       JPEG, PNG, MPEG
    **Session Layer:**            NFS, SQL, PAP
    **Transport Layer:**          TCP, UDP
    **Network Layer:**            ICMP, IPv4, IPv6, RIP
    **Data Link Layer:**          ARP, PPP, ATM
    **Physical Layer:**           Bluetooth, Ethernet, WiFi, DSL
    
Protocols are reccommended rules to enable effective communication. For a DF investigator, they can be viewed as guidelines that attackers can abuse to produce unexpected results.

### OSI Model

OSI stands for Open Systems Interconnection, and is the standard used for transferring data across a network. It is comprised of seven layers, which are Application, Presentation, Session, Transport, Network, Data Link, and Physical. 

Each layer defines a different stage that data must go through to travel from one device on a network to another. Data is encapsulated to enable transmission between each layer.

No matter what layer of the OSI model, when data is transmitted it is compromised of a header followed by data. 

![How data changes per each layer of the OSI model](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-13%20at%2022.07.51.png)

**What happens when you enter a website into a URL**

Lets say someone types in www.google.com into the URL. How does this request actually send, with respect to the OSI model?

The first thing that happens is a DNS request is sent to the local DNS server (This, surprisingly, uses the DNS protocol). The DNS protocol operates at layer seven of the OSI model - the Application Layer. This will return the IP address for the google website.

Once the IP address is known, the computer will send out a HTTP "GET" request to the web servers IP address (Also operated at Layer 7)

In order for this request to get to the web server, the host will hand down the request to the operating system. The OS will cut up the data into discrete packets and creates a TCP (Transmission Control Protocol) header (TCP operates at layer 4 - the Transport Layer).
Information contained in this packet includes the source port of the host and the destination port that the hosts expects the web server to be listening on (Usually port 80).

Next, the Operating System will prepend an IP header (Layer 3 - Network Layer) which describes the source and destination endpoint IP addresses - that is the IP address of the host an the IP address of the web server. This way the traffic can be properly routed from network to network across the internet.

Each packet is then given, in the case of a wireless router being used, 802.11 (WiFi) infromation for transmission across the LAN (Layer 2 - Data Link)

Finally, the frame is translated into RF and sent out. (Layer 1 - Physical Layer)

Next, the WAP (Wireless Application Protocol - Layer 2) will transmit the entire frame over a copper wire (Layer 1) to the next hop address. The data then continues hopping until it reaches its final destination.

Once the destination is reached, the process works in reverse. So the destination physically receives the data, the Data Link headers are stripped, the recepient of the data is then acknowledged (Network layer - source IP address).

The transport layer then validates the ports that the packet came from (source port).

The TCP header is then removed and the get request is handed to the web server at Layer 7 - the application layer.

The process would be repeated every time over the network

## TCP/IP
