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

Sniffing a network is the process of inspecting each packet in a networks traffic. It involves multiple layer inspection, protocol awareness and protocol reassembly.
If the system is set to log and drop packets, then this process is time critical. However, if the system is only set to log the packets, then offline analysis and alerting would be tolerable. 
NIDS/NIPSs also have the ability to use deep packet analysis. For example, firewalls can see traffic on port 80, however the intrusion systems may have rules to read the HTTP packet and make rules on if the packet is malicious or not. 

### Modes of Detection

**Signature Based Analysis**

This method compares things like headers and packet content against a database that contains known malicious byte sequences. However, in some cases malicious activity may be spread across multiple packets which would hinder the effectiveness of this method. 

**Protocol Analysis**

Does the traffic being received comply with what would be normal protocol standards?

**Behavioural analysis**

The system will learn what would be classed as normal behaviour and flag any packets that do not follow this 'normal' behaviour. E.g. traffic volume

### Placement

There are two options for placement of an IDS/IPS: In-line and Siphon/Mirrored.

In-line is when the systems is placed directly on the line and can act on malicious traffic. It is commonly found in enterprise networks. A downside of this method is that it could potentially slow down the network traffic.

![In-line placement of an IDS/IPS](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.02.57.png)

Siphon/Mirrored is when the system has been placed to passively monitor the network and not interfere.

![Siphon/Mirrored placement of an IDS/IPS](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-11-19%20at%2012.05.27.png)

The deployment of the IDS/IPS may determine what type of packets are logged and the type of alerts that will be sent. Additionally, the placement of the system will often determine whether the packet will or will not be available for further analysis. 

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

There are some issues that may affect gathering evidence. One of these issues is the configuration of the IDS. The configuration of each sensor is very important. Depending on the placement in the network, some sensors will require different rules. The location of the sensor within each network is also an important aspect. 

The rule set that a sensor has is of high importance. If the sensor has not been configured correctly to alert upon a specific event, then the absence of that event would mean nothing.

### Types of data

**Alert data**

The format of this data may include email messages, text messages or a nicely formatted GUI

**Packet header and/or Flow record info**

This information will typically include the location, destination and pattern of the activity. As well as which rule/pattern triggered the event.

**Packet payloads**

Some systems may have been configured to capture the full packet from these triggering alerts. This information is useful for malware carving. 

### Issues with comprehensive logging

To capture all packets all the time, a massive amount of storage space would be required. They would also be very difficult to archive due to the amount of packets captured. Lots of processing time would be required and there is potential for a large security risk if access is gained to the several from a malicious attacker. It is therefore best to use alerts with other sources rather than storing the full network.

## SNORT

SNORT is the most widely used IDS on the market. It is an open-rule language that is extremely versatile. It comes with commercial support and a community/commercial business model.

### SNORT Architecture

SNORT used libpcap to capture packets on the network. It passes through 4 pre-processors which can roughly be aligned with the OSI model. 

  1. Layer 3 - reassembles fragments
  2. Layer 4 - Reassembles streams
  3. Layer 5 - Reassembles sessions
  4. Layer 6 - Reassembles transactions
  
SNORT can issue an alert at any layer. Using rule-detection, it can detect and reassemble any anomalies in the network. The information would be handed to the alerting engine and the subsequent related packets can be marked for capture.

### SNORT Configuration

The location of the global SNORT files can be found under /etc/snort/snort.conf. This file stores the various network addresses, location of rules and location of services.

The home of the actual rules can be found under /etc/snort/rules

Lastly, the SNORT logs can be found under /var/log/snort

## Conclusion

In conclusion, NIPS/NIDS's are usually the cause that triggers an investigation into the network. They provide crucial data for the investigation and aid with the problem of 'finding the needle in a haystack'
