# *Wireless Forensics*

Wireless traffic makes use of different protocols on layer 2. The majority of data transport is encrypted if they use modern protocols. By investigating wireless traffic, a huge amount of information can be recovered.

## 802.11 details

Nowadays, numerous devices that are wireless. These include, but are not limited to:

    1. AM/FM radios
    2. Cordless Phones
    3. Mobile phones
    4. Bluetooth Headsets
    5. Infrared devices (e.g. TV remotes)
    6. Wireless Doorbells
    7. Smart home devices
    8. Wi-Fi (802.11) LAN networking over RF
    
### Wireless Network Architecture

*Stations*
All components that connect into a wireless medium in a network are called stations. Naturally, all stations are also equipped with wireless network interface controllers as a result.
Wireless stations fall into one of two categories: Access Points (AP) or Clients

Wireless Access Points (WAPs) which are usually routers in a domestic setting, are used as base stations to allow access to the wireless network (WLAN). These WAPs emit and receive radio frequencies for wireless enabled devices. 

*Service Set ID (SSID)*
The SSID acts as an identifier of a wireless network broadcasted. In other words, it is the name associated with a wireless network, such as your routers name.

*Basic Service Set (BSS)*
The BSS is a set or group of stations that are able to communicate with one another 
Every BSS has an ID, known as the BSSID. This ID is the MAC address of the access point servicing the BSS

*Forensics cases involving wireless*

There are numerous cases that use wireless forensics to come to a conclusion. However, to name just a few:

    1. Recover a stolen laptop - The laptop could be found by tracking it on the wireless network
    2. Identify rogue WAPs - They may have been installed by insiders for convenience or to bypass enterprise security
    3. Investigate malicious or inappropriate activity - This activity may be occurring or seen on the wireless network
    4. Investigate attacks on the wireless networks itself - These types of attack could include DoS, encryption cracking or authentication bypass.
    
*IEEE Layer 2 protocol series*

Protocols on layer 2 typically belong to the 802 series. For example, Ethernet runs on 802.3, LAN based authentication runs on 802.1X and Wi-Fi runs on 802.11

## 802.11 Frame Types

### Management Frames

Management Frames govern communications between different stations (except for flow control)
Management frames are also knowns as Type 0.
Management frames coordinate communications. They have several uses for forensics, and these are: 

    1. They are not encrypted
    2. Store the Mac Addresses
    3. Store the BSSID
    4. Store the Service Set Identifiers (SSID)
    5. their subtypes (an area stored in the packet) indicate basic activities
    
Their subtypes are as follow:

* 0x0 — Association Request
* 0x1 — Association Response (if the Status Code is 0x0000 then the response is successful)
* 0x2 — Reassociation Request
* 0x3 — Reassociation Response
* 0x4 — Probe Request
* 0x5 — Probe Response
* 0x6 — Reserved
* 0x7 — Reserved
* 0x8 — Beacon frame
* 0x9 — Announcement Traffic Indication Map (ATIM)
* 0xA — Disassociation
* 0xB — Authentication
* 0xC — Deauthentication
* 0xD — Action
* 0xE — Reserved
* 0xF — Reserved

How can these be useful though?

Well, management frames can be a point of attack for WEP cracking, and Evil Twin

### Control Frames

Control frames supper flow control over a variably medium, such as RF

Control frames are also knowns as Type 1.

This frame controls the flow of traffic across a network. However, there is a problem with hidden nodes for this method.

On an ethernet network, every node can see one another and therefore talk directly to each other. The same cannot be said for wireless networks. Although it is possible for a node to be able to see all other nodes on the wireless network, it is not guaranteed.

Instead every node can send RTS (Request to Send) frames and search for the corresponding CTS (Clear to Send) or ACK frames.
This method was created in order to avoid the hidden node problem. If a node sends out a RTS frame and receives a CTS frame back, then it knows it is capable and able to send the following packet. It also allows the availability and reception of transmission to be tested.

This frame provides very little information for forensic investigators, besides the timing station MAC addresses.

### Data Frames

The data frame encapsulates the Layer 3+ data that moves between stations that are actively engaged in communication on a wireless network.

Data frames are also known as Type 2. 

This is the frame that includes the actual data. Every IP packet that is sent across a wireless network is part of the payload of an 802.11 data frame.

Some subtype examples:
    
    If the subtype is 4, then it indicates a null function where no data is transmitted.
    If the subtype is 0, then it indicates that data has been transmitted with the packet.
    
Using packet analysis techniques, unencrypted or decrypted data frames can be analysed at layer 3 and above.

Encrypted data frames may only be useful for statistical flow analysis.

## Endianness

There are three types of endianness - Big endian, little endian and mixed endian.

Big endian has the most significant bit transmitted first
Little endian has the least significant bit translated first
Mixed endian uses a combination of the two.

Depending on which protocol is used, stations can be configured to transmit the bits in different orders.

## WAPs

### Wired Equivalent Privacy

This is a security protocol. It is designed to provide a WLAN with a level of security that is not usually found on a normal LAN.
If the WEP key is broken, then a brute force attack can be performed on the shared encryption key. If WEP can be found, then the 13th byte of a frame header will be set to 1. However, WEP has become outdated and is now a part of legacy.

### WPA
Wireless protected Access is another security standard. It makes use of key rotation - Temporal Key Integrity Protocol (TKIP)
It was used as a temporary fix for WEP until 802.11i was approved. WPA was able to run on existing hardware without any new hardware being needed. However, it is also now broken!

### WPA2
WPA2 used Counter Mode with CBC-MAC Protocol (CCMP) mode of Advanced Encryption Standard. 
With WPA2, stations need to communicate their ability to be able to confirm to the new WPA2 specifications.
In recent years, WPA2 has also proven to be vulnerable. 

### WPA3
WPA3 is the most recent and up to date member of the WPA family. It makes use of the CCM mode of Advanced Encryption Standard.

WAPs are a layer 2 device that can aggregate end point stations into a LAN. All stations have access to these signals and they make interception of traffic easy. Anyone who is within the range of the RF signal can intercept the signals. 
The majority of Enterprise WAP solutions are capable of logging traffic. Some consumer WAPs are getting more sophisticated too.

### Why investigate WAPs?

* Wireless access points could potentially locally contain stored logs of connection attempts, authentication successes and failures, and other local WAP activity.
* WAP logs can help you track the physical movements of a wireless client throughout a building or campus. 
* The WAP configuration may contain information about how an attacker gained access to the network.
* The WAP configuration may have been modified by an unauthorised party as part of the attack.
* The WAP itself may be compromised

## Gathering Evidence

There are several different types of evidence that can be gathered from WAPs. These can be split into two categories - Persistent and Volatile, where persistent evidence stays stored on the WAP, but volatile evidence can be lost at any point.

Persistent evidence:

    1. Operating System image
    2. Boot Loader
    3. Start-up Configurations
    
Volatile Evidence:

    1. History of connections by MAC addresses
    2. List of IPs associated with MACs
    3. Historical logs of wireless events (access requests, key rotation etc)
    4. History of client signal strength (can help identify geographic location)
    5. routing tables
    6. Stored packets before they are forwarded
    7. Packet counts and statistics
    8. ARP table (MAC address to IP address mappings)
    9. Flow data and related statistics
    
### Passive evidence acquisition

In order for the wireless card to be able to gather evidence it must have a Monitor mode. Alternatively, a separate device can be used for monitoring, such as the AirPcap USB. This USB will monitor layer 2 wifi. It runs on windows and can be used to decrypt WEPs.
Information that can be gathered through a monitoring device are the broadcast SSIDs, WAP MAC addresses, supported encryption/authentication algorithms and associated client MAC addresses

### Efficient analysis

* Are there any beacons in the wireless traffic? A beacon is a management frame which is transmitted periodically to announce the presence of a wireless WAN
* Are there any probe repsonses? When a probe request is made, a machine is asking for information from a specific access point, or all access points. The access points then send out a probe response 
* Can all of the BSSIDs/SSIDs be found from the associated/authenticated network traffic?
* Can you find the malicious traffic? If so, what does it look like?
* Is the captured traffic encrypted using WPA/WEP? If so, is anyone trying to break it?

In order to find WAPs, there are several things to look for in the network traffic:

* Beacon frames - management frames with subtype 0x08
* Probe response frames - management frames with subtype 0x05
* WAPs set ESS to 1 and IBSS to 0 when broadcasting these frames. An ESS is one or more interconnected BSSs. An IBSS is a single (or independent) BSS

## Types of Attacks

### Common types of attacks

* Sniffer
    - This is when an attacker eavesdrops on the network and gathers/monitors its traffic
* Rogue Wireless Access Points
    - Theres are unauthorised wireless devices that extend the LANs, norally for an end users convenience. This requires an insider to perform.
* The Evil Twin Attack
    - An attacker sets up a WAP with the same SSID as a legitimate one. Usually they will then DoS the legitimate one. This way a users device will try and reconnect to the 'Evil Twin'
* WEP Cracking
    - An attacker attempts to recover the WEP encryption key to gain unathorised acces to a WEP-encrypted network

## Rogue WAP evasion techniques 

You can change the channel. WAPs broadcast on channels, but can be configured to broadcast an alternative channels to evade detection.

You can use Greenfield mode. This is when you limit the AP to only accept 802.11ac/n channels.

Another method is Wireless Port Knocking. This is when a rogue WAP must receive a packet with a preconfigured SSID. Once this packet is received, it awakens and sets itself to master mode. When it is not in master mode, it is silent and therefore cannot be detected by common wireless scanning tools.

## WEP Cracking

WEP cracking occurs when there are flaws in the protocol and encryption method. Using ARP packets, the attacker gathers several thousand packets of network traffic and then uses these packets to guess the WEP key.
