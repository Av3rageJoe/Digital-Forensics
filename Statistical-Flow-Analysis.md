# **Statistical Flow Analysis**

This document contains information about statistical flow analysis.

A network is like a roadmap. There are several destinations with several common areas that traffic passes through. As a car travels around the network, it collects and drops off information (in the form of packets). If a bad man manages to get a car on the network and cause damage, plus steal information from areas of the network. If this was to happen, then investigators will want to know what damage was done and what was stolen. This is the purpose of statistical flow analysis - to help unveil what damage was done on the network.

## What is a flow record?

A flow record is a subset of information about a flow. 
Normally a flow record contains:
     
     1. The source and destination IP address
     2. The source and destination port
     3. The protocol
     4. The date
     5. The time
     6. The amount of data transmitted in each flow

## Purpose of Recording flows

Flow charts can be helpful to identify any compromised hosts. Typically, a compromised host will:

      1. Send out more traffic than normal
      2. Use unusual ports
      3. Communicate with known malicious systems
      
They can confirm and/or disprove data leakage. The amount of data that is exported is usually a good indicator of this

Individual profiling of an account can also give an indicator of malicious activity.
A flow will reveal
      
      1. Normal working hours
      2. Periods of inactivity
      3. Source of entertainment/inappropriate activity

In addition to these individual profiling will also show who regularly shares data with each other. 

## Flow Record Processing System

Flow record processing systems have four main components:
      
      1. Sensor
            A sensor is a device used to monitor the flow of traffic on any given segment. It can be used to extract important pieces of information to a flow record
      2. Collector
            A collector is one or more servers that are configured to listen on the network for flow record data and then store it to a hard drive.
      3. Aggregator
            If multiple collectors are used, an aggregator is used to aggergate the data on on central server which can be used for analysis.
      4. Analysis
            Once the flow record has been exported and stored, it can be analysed using several tools of the investigators choosing.
            
## Sensor Types

Many networks have their own solutions to support the creation of flow records, such as Cisco, SonicWall and Juniper
If the network does not have their own solution then standalone appliances can be used. This could come in the form of a software based sensor. Network administrators can then route traffic via the sensors so that the data can be investigated. 

## Where to place a sensor

When setting up a network infrastructure, it should be set up with flow monitoring in mind. However, this is often not the case. 

The following factors should be considered when placing a sensor:
        
        1. The duplication of logs is bad practice and should be minimised
        2. Time synchronisation is crucial (all devices and the sensor should be using the same time). Therefore, it is reccommended that the Network Time Protocol (NTP) is used where ever possible. 
        3. Most flow records are collected on external devices such as firewalls. However, the internal traffic of the network should not be ignored as this could prove valuable too.
        4. Do not overload the network capacity

## Collection and Aggregation

Factors that should be considered during placement for these devices should be:
        
        1. Congestion
              When flow records are created, they generate network traffic which can cause congestion
        2. Security 
              * Can records be sniffed or modified in transit?
              * Export flow records on seperate VLAN if possible
              * Isolate physical cables
              * Encrypt
        3. Reliability
              * Traditionally uses UDB, consider using TCP
        4. Capacity
              * Is there only one sensor or many?

## Anaylsis

Once the flow records have been obtained, the analysis of them can begin. 

Analysis is typically used for forensics. The data gathered can store a summary of information about the traffic that flows across the network. Flow analysis will allow a forensic investigator to form the "When", "Who", and "How"s of an  incident.

### Analysis Techniques

During analysis, an investigator will want to identify the IP address of compromised or malicious machines, the time frame of suspect activity, any known ports of suspect activity and specific flow which indicate abnormal or unexplained activity.

**Filtering** </br>
  Filtering is the process of narrowing down a large pool of evidence into a subset on forensically interesting activities. 
  Any This process should start by isolating activity relating to specific IP addresses.
  
  
**Baselining** </br>
  Identifying what is normal traffic given the context of the environment
  The investigator should build a profile of what "normal" traffic looks like on the network
  General trends over a period of time can eb used to establish this.
  When baselining an individual, the historical pattern can be sued to identify any anomalous behaviour. Most flow patterns will change dramatically if a host is compromised or under attack
  
  
**Dirty Values** </br>
  There might be an unusual port that is not often used. Or a port claiming to be of a different protocol than ti actually is
  Dirty values could include:
  
        1. IP addresses
        2. Ports
        3. Protocols
     
**Activity Pattern Matching** </br>
  Might indicate the behaviour of an already known malware or attack
  Things to check during pattern matching:
  
        1. IP Address
          Does the IP belong internally or is it from a WAN?
          What is the counrty of Origin?
          Who are they registered to?
        2. Ports
          Are the ports assigned and/or well known (linked to specific applications)
          Is the system scanning or being scanned?
        3. Protocols and Flags
          Layer 3 and 4 are often tracked in flow record data.
               Connection attemps
               Successful port scans
               Data transfers
        4. Directionality
          Is data coming in (downloaded) or going out (uploaded)?
        5. Volume of data transferred
          Lots of small packets can indicate port scanning
          Large amounts of data usually cause for concern
          
          
## Simple Patterns

Simple patterns and devices/attacks which use such patterns

* Many-to-one IP addresses
     DDoS attack
     "Drop box" sata repository on destination IP
     Email server (at destination)

* One-to-many IP addresses
     Web server
     Email server (at source)
     Spam bot
     Network port scanning

* Many-to-many IP addresses
     Peer-to-peer file sharing
     Widespread port scanning
     
* One-to-one IP addresses
     Targeted attack
     Routine Server communication
     
## Complex patterns

This is the process of matching complex flow record patterns to specific activities.

For example:

     * TCP SYN port scan
     
          * One source IP address
     
          * One or more destination IP addresses
          * Destination port numbers increase incrementally
          * Volume of packets surpass a specified value within a given period of time
          * TCP protocol
          * Outbound protocol flags set to "SYN"
               * No full TCP connections
