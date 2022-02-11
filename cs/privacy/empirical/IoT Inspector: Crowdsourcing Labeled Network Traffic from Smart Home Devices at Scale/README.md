Summary of [IoT Inspector: Crowdsourcing Labeled Network Traffic from Smart Home Devices at Scale](./IoT%20Inspector:%20Crowdsourcing%20Labeled%20Network%20Traffic%20from%20Smart%20Home%20Devices%20at%20Scale-2020.pdf)

In this paper, Huang et al. have presented a new tool to study the smart home research. They developed and released IoT Inspector, an open-source tool that allows users to observe the traffic from smart home devices on their own home networks. Using this tool they crowdsourced the largest known dataset of labeled network traffic from smart home devices from within real-world home networks, while respecting the privacy of the volunteers. 

They have pointed out scaling and labelling challenges in studying the smart home networks. Most of the studies so far has been in the small lab setup which didn't represent the grander picture of smart home networks as there were more than 8 billion IoT devices in the world at the time of this study. Previous study of smart home networks consisting of IoT devices from Internet scans provide limited and often not correct view because of difficulty in accurately labeling the IoT devices. They solved this challenge by crowdsourcing the data from real world home networks at large scale where user can label the devices. 

IoT inspector uses ARP scanning to scan for devices in the local network, and after user marks a device for inspection it uses ARP spoofing to capture the traffic going through the device. Limitations of the IoT inspector was ARP spoofing only captured traffic between monitored devices and the router. However, smart home devices could be communicating with one another. Capturing the traffic between devices was marked as future work.

IoT inspector runs on a computer in the local network and captures the traffic going to and from the devices marked for monitoring. IoT inspector is built using python library Scapy. It parses the relevant information from collected traffic from the devices and upload them to the database server every 5 second. Exact information capture by IoT inspector on a device after it's marked for monitoring while respecting the user's privacy are:
- SHA-256 hashes of device MACaddresses, using a secret salt
- Mnaufacturer of network chipset from MAC address (i.e. OUI)
- DNS request and response
- Remote IP address and port
- Aggregate flow statistics on transport layer
- Data related to device identities, including SSDP/mDNS/UPnP messages, HTTP User-Agent strings, and hostnames from DHCP Request packets, that are useful for validating device identity labels entered by users
- TLS Client Hello messages
- Timezone of the computer running IoT Inspector

Finally, IoT Inspector uploaded the device labels along with the network traffic data to a central database hosted at author's institution. To keep the users engaged IoT inspector present the finding to user in real time with the goal that users to learn new insights about their devices, such as what third parties a device communicates with and when devices send and receive data.

To involve the users in this study, authors have spread word about IoT inspectory by shouting on Twitter and getting coverage on news outlets. 

As with crowdsourced data, the user-entered device name, category, and vendor labels are likely inconsistent and may be prone to mistakes. In order to correctly label smart home device because of typographical error or multiple naming of same device they used Levenshtein distance and human knowledge. To validate this labeling they used following ways:
- Commong top domain visited by the devices. If a device of a given vendor communicated with the common domain, we consider the vendor label as Validated.
- Vendor as substring in the domain. For example, Philips devices tend to communicate with “philips.com,” based on our in-lab observations.
- IoT Inspector regularly scans the user’s network with Netdisco, an open-source library that discovers smart home devices on the local network using SSDP, mDNS, and UPnP protocols.
- Extract the OUI from the first three octets of a device’s MAC address. We translate OUIs into English names of manufacturers based on the IEEE OUI database.

With this strategy, 6,776 devices across 81 vendors have their vendor labels validated using at least one of the methods. They only used 6,776 devices for the study.

They made the assumption that traffic over port 80 is likely unencrypted HTTP traffic. Of the 6,776 devices they obtained 3,462 devices (51.1%) communicated with an Internet endpoint over port 80. These devices are associated with 69 vendors, out of a total of 81 validated vendors. They also analyzed TLS ClientHello messages in the dataset and found 375 devices across 26 vendors (e.g., smart TVs from Amazon, TCL, and Panasonic, along with Neato vacuum cleaners) used outdated TLS versions, i.e., SSL 3.0 and TLS 1.0.

Limitations:
- volunteers in the study didn't run the IoT inspector for long period of time.
- current method of validating device labels may be limited, as our four validation methods may introduce false negatives, e.g., correct vendor labels but not being marked as Validated because of missing data.
- while IoT Inspector helps users identify potential security and privacy issues in their smart homes, the ultimate goal is for users to take actions, e.g., upgrading their device firmware, isolating devices on a separate network, or even unplugging devices when not in use. The current dataset collected does not produce any insight on whether, how, and why users changed their behaviors after using IoT Inspector, and whether they are comfortable letting IoT Inspector influence their behaviors

Questions: To categorize the unencrypted traffi authors assumed traffic on port 80 is HTTP because it's the IANA port, but further research like LZR have suggested the devices might not be running only HTTP on port 80. Is there a way to confirm this assumption?








