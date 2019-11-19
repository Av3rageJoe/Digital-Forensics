# Network Intrusion Detection and Analysis

If there is no piece of hardware or software in place used to detect abnormal activity on a network then it will often go undetected. This is the purpose of Intrusion Detection Systems and Intrusion Prevention Systems.

## IDS vs IPS, What's the difference?

IPS systems are defined to have the ability to act when an intrusion is detected. This means that they are capable of spotting suspicious packets and dropping them. IDS's on the other hand, by default, are only able to detect (as the name suggests) abnormal behaviour, and not do anything about it except alert the system administrator. However, they can be configured to act upon abnormal behaviour if desired. Therefore, there is not much of a difference.

## IDS/IPS

**HI(D/P)S - Host-based Intrusion Detection/Prevention System**

This system monitors system events and alert of any suspicious system activity

**NI(D/P)S - Network-based Intrusion Detection/Prevention System**

These systems monitor network traffic and alert of any suspicious network activity.

### Functionality

IDS/IPS's are rule based systems. They describe how to compare a packet or stream against known malicious traffic.

They issue alerts of suspicious packets and streams and can be configure to capture suspicious packet sequences.

### Sniffing

Sniffing a network is the process of inspecting each packet in a networks traffic. It involves mutliple layer inspection, protocol awareness and protocol reassembly.
If the system is set to log and drop packets, then this process si time critical and thus must be done quickly. However, if the system is only set to log the packets, then offline analysis and alerting would be tolerable. 
NIDS/NIPSs also have the ability to use deep packet analysis. For example, firewalls can see traffic on port 80, however the intrusion systems may have rules to read the HTTP packet and make rules on if the packet is malicious or not. 

### Modes of Detection

**Signature Based Analysis**

This method compares things like headers and packet content against a databse that contains known malicious byte sequences. However, in some cases malicious activity may be spread across multiple packets which would hinder the effectiveness of this method. 

**Protocol Analysis**

Does the traffic being receievd comply with what would be normal protocol standards?

**Behavioural analysis**

The system will elarn what would be classed as normal behaviour and flag any packets that do not follow this 'normal' behaviour. E.g. traffic volume

### Placement

There are two options for placement of an IDS/IPS: In-line and Siphon/Mirrored.

In-line is when the systems is placed directly on the line, an can act on malicious traffic. It is commonly found in enterprise networks. A downside of this method is that it could potentially slow down the network traffic.

![In-line placement of an IDS/IPS](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.02.57.png)

Siphon/Mirrored is when the system has been placed to passively montior the network and not interfere.

![Siphon/Mirrored placement of an IDS/IPS](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.05.27.png)

The deployment of the IDS/IPS may determine what type of packets are logged and the type of alerts that will be sent. Additionaly, the placement of the system will often determine whether the packet will ro will not be available for further analysis. 

**Outside perimeter firewall**

By placing the IDS outside of the firewall, it will be able to detect any incoming attacks, however, it will also receive a high false positive rate. These systems are normally configured to only log data and not act upon it. 

![An IDS placed outside of a firewall](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.14.06.png)

**Inside perimeter firewall**

Using this placement, the system will be able to detect incoming and outgoing attacks and protect the DMZ. It is typically configured to use low to moderate alert rules with some packet capture. 

![IDS placed inside of the perimeter](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.17.06.png)

**Inside Internal Firewall**

Using this placement the IDS can detect internal and outgoing attacks and protect the internal network. It is usually configured to use moderate to high alert rules with in-detail packet captures. 

![IDS placed inside the internal network](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.20.24.png)

## Evidence Acquisition
