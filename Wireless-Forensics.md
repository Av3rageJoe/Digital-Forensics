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
Wireless stations fall into one of two catagories: Access Points (AP) or Clients

Wireless Access Points (WAPs) which are usually routers in a domestic setting, are used as base stations to allow access to the wireless network (WLAN). These WAPs emit and receive radio frequencies for wireless enabled devices. 

*Service Set ID (SSID)*
The SSID acts as an identifier of a wireless network broadcasted. In other words, it is the name assosciated with a wireless network, such as your routers name.

*Basic Service Set (BSS)*
The BSS is a set or group of stations that are able to communicate with oneanother 
Every BSS has an ID, known as the BSSID. This ID is the MAC address of the access point servicing the BSS

*Forensics cases involving wireless*

There are numerous cases that use wireless forensics to come to a conclusion. However, to name just a few:

    1. Recover a stolen laptop - The laptop could be found by tracking it on the wireless network
    2. Identify rogue WAPs - They may have been installed by insiders for convenience or to bypass enterprise security
    3. Investigate malicious or inappropraite activity - This activity may be occurring or seen on the wireless network
    4. Investigate attacks on the wireless networks itself - These types of attack could include DoS, encryption cracking or authentication bypass.
    
*IEEE Layer 2 protocol series*

Protocols on layer 2 typically belong to the 802 series. For example, Ethernet runs on 802.3, LAN based authentication runs on 802.1X and Wi-Fi runs on 802.11

## 802.11 Frame Types

### Management Frames

Management Frames govern communications between different stations (except for flow control)

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

### Data Frames

