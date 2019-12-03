# Tips and Tools

## Binary bits

Looking at an Ethernet frame, you can tell a large amount of information such as the source mac address, destination macaddres, IP addresses and the protocols used.

Just because Wireshark says that an protocol si one thing, does not mean that this is neccessarily true. To find out the correct protocol, the IP header section of the ethernet frame can be viewed, whcih stores the IP address. 

  1. Red - Ethernet Header
  2. Green - IP header
  3. Gold - Protocol header
  4. Purple - Payload (Optional)

![The makeup of an ethernet frame](https://github.com/Av3rageJoe/Digital-Forensics/blob/master/Images/Screenshot%202019-12-03%20at%2009.24.24.png)

To find the bytes that store the protocol, the byte 9 in the IP header must be viewed. A point to note is that the bytes start counting from byte 0. 

To further verify the protocols being used, the ports that the data is being sent to can be viewed. These can be found in the protocol header, with the source address coming from byte 0 and 1, and the destination port at bytes 2 and 3.

To identify the source IP address being used, the 12th to 15th bytes of the IP header can be viewed. the destination port comes from the 16th - 19th bytes.

## tshark

tshark is a command line network protocol analyser. tshark is capable of reading from a live network or from previously captured packets. With no options set, tshark will work similar to a tcpdump. With the -r option set, tshark will perform actions similar to a tcpdump on a specified pcap file. It will read packets from the file and display a summary line on the standard output for each packet. 

***-T and -e***

The -T option and -e option can be used to show only specific fields
Example: tshark -2 -r evidence01.pcap -X lua_script:oft-tsk.lua -Y "oft" -n -T fields -e "oft.filename" -e oft.totsize

## ngrep 

ngrep is a command line tool used to grep pcap files. it works in the exact same way as grep does, except when using a pacap file, the -I option must be specified.

The output will show all of the packets with the keyword and what IP addresses sent the packets

## Filter traffic between IP addresses

ip.addr==<IP ADDRESS>

# Procedure

1. Check what protocols have been transmitted and make a list of them. 
2. Attempt to identify any IP addresses that could be submitting suspicious traffic
3. Investigate said IP addresses further - checking the identified protocol is correct, checking who the source IP address belongs to etc.
4. Follow any suspicious TCP streams to try and identify any obvious suspicious content
5. If suspicious activity is found between two IP addresses, filter the traffic to only show exchanges between the two addresses, then extract them for closer analyses


