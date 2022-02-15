Summary of paper [All Things Considered: An Analysis of IoT Devices on Home Networks](./All%20Things%20Considered-%20An%20Analysis%20of%20IoT%20Devices%20on%20Home%20Networks-2019.pdf)

In this paper, Kumar et al. discuss the IoT ecosystem across different geographical regions — how
diverse and fragmented they are across regions; what are some most common categories of IoT devices
across them; vendor diversity; and finally security posture in the premise of default username and
password used in FTP and telnet services.

Authors have collaborated with Avast antivirus to make tool call Avast Wi-Fi Inspector. It performs
internal network scans to do device identification, look weak default credentials, and
vulnerability to recent CVEs.

It first generates a list of scan candidates from entries in the local ARP table as well through
active ARP, SSDP, and mDNS scans. It then probes targets in increasing IP order over ICMP and
common TCP/UDP ports to detect listening services. 

Further they use various methods to classify IoT devices in 14 different device categories. First
WiFi Inspector uses expert rules — regular expressions that parse out simple fields (e.g., telnet
banner or HTML title) — to label hosts that follow informal standard practices for announcing their
manufacturer and model. They ~1000 rules generated over 3 years period. This helps them categorize
60% of devices.

For remaining devices, they used supervised ML algorithm. WiFi Inspector leverages an ensemble of
four supervised learning classifiers that individually classify devices using network layer-data,
UPnP responses, mDNS responses, and HTTP data. The network classifier is built using a random
forest, which aggregates the following network features of a device:

1. MAC address
2. Local IP address
3. Listening services
4. Application layer responses on each port
5. DHCP class_id and hostname

The UPnP, mDNS and HTTP classifiers leverage raw text responses. The classifier treats each
response as a bag-of-words representation, and uses TF-IDF to weight words across all responses.
This representation is fed as input to a Naïve Bayes classifier.

This final classifier gives them coverage on 92% of devices with accuracy of 96%.

For ethical purpososes authros didn't receive individual data about the users, they only got
aggregated data by device manufacturer, region, and device type, and all the scans were initiated
by users.

Finally, they scanned 15.5 million homes spanning across 83 million devices in 11 geographic
regions. From this data they found out 66%, 53%, and 8.7% of devices in North America, Western EU,
and South Asia have IoT devices respectively. Avg. number of devices per home for those regions
were 7,4, and 2.

In North America, contrary to normal assumption of widespread usage of Voice assistant and home
automation, highest percent of devices were Media(43%), Work Appliance (e.g. printer) (33%), Gaming
console(16%), Voice assistants (10%).

They found out that different regions have different device type preferences.

Vendors distribution was also very spread out with long tail to cover all the devices, but 90% of
devices were covered by less than 100 manufacturers in all regions. They also found our that vendor
diversity depends on device type, for e.g., voice assistants are dominated by few vendors.

They also looked for weak credentials used on services hosted on discovered IoT devices, servies
were FTP and Telnet and found that spread of weak credentials is dependent on device preference in
that region. 


**Question:** Data is skewed towards the Avast users, which mean they are already security minded
folks, would the actual distribution of IoT devices across the world differ?

Author suggested that this is the lower bound of security, actual issues might be worse because
other users might not consider security as the top priority.
