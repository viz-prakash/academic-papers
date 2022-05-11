Summary of the paper [Web-based Attacks to Discover and Control Local IoT Devices](./Web-based%20Attacks%20to%20Discover%20and%20Control%20Local%20IoT%20Devices-2018.pdf).


In this paper, Acar et al. has discussed ways to discover the and control IoT devices behind the NAT using web-based attacks.

To prepare for the attack they captured the traffic generated by few hand selected devices. They analyzed the captured traffic to discover HTTP API endpoints used by the devices and created a mapping. They end up curating a list of total 35 endpoints from 7 different devices out total 15 target devices, where endpoints were mapped to devices.

In the next step, to discover devices in the network behind NAT, they used malicous JavaScript payload delived to the victim by making them visit a TLS enabled website they control (fair assumption) and used timing based attack to discover live hosts. Detailed steps are following:

  1. The script obtains the victim’s local IP address via the WebRTC Session Description Protocol.
  2. Script sends a GET request via the Fetch API to port 81 of every IP address in the local /24 subnet (e.g., https://192. 168.1.123:81/), while measuring the timing of each response. As port 81 is rarely used, active devices are likely to immediately respond with a TCP RST packet, while the TCP connection times out for non-active IP addresses.
  3. To label a device — to every active IP address, the script sends a request using the HTML5 <audio> element for the 35 device-specific endpoints that accept GET requests. Based on the resulting MediaError error messages (as the endpoints do not host audio resources), the script infers if the responding IP address is associated with one of the seven known devices.


  To reduce the FP, they excluded a devices which responded with error messages for random paths. 

  Duration of the attack: They found that requests to IP addresses with active devices took 141 ms on average to fail with an error (i.e., due to TCP RSTs). In comparison, requests to the inactive IP addresses took approximately 3s, 21s and 76s to fail (i.e., due to timeouts) on Ubuntu, Windows and macOS respectively.

  **Limitation** of this attack included devices hosting local HTTP servers and getting a physical access to the devices to figure out the HTTP endpoints.
  
  **Countermeasures:**

  **Users:** To prevent a script from obtaining local IP address using WebRTC SDP, user can toggle a preference in their browser (e.g., media.peerconnection.enabled on Firefox), although an adversary can try to iterate over the *.1 addresses of the private IP ranges and discover an active devices.
  **Browser:** Privacy-focused browsers (or browser extensions) can limit the access to private IP ranges from web pages with public domain names. This restriction can prevent scanning of the LAN from the web, while still allowing access to web pages served from the LAN.
  **IoT vendors:** IoT vendors could configure devices with HTTP servers to respond to any HTTP GET request with the 200 OK code.

  
  First attack can identify the presence or absence of specific HTTP endpoints on devices, it cannot read any returned data due to the same origin policy(SOP). However, an attacker can circumvent the SOP with DNS rebinding. To control the devices, they used following steps:
  
  1. A victim visits http://domain.tld/ for the first time. During the DNS lookup for the domain, the authoritative name server resolves the domain to X with a short TTL (e.g., one second). The victim loads and executes the malicious JavaScript hosted at the domain.
  2. The JavaScript requests another existing resource at the attackercontrolled domain, e.g., http://domain.tld/evil-test.
  3. The local DNS caches at the victim may or may not have evicted domain.tld. If not, domain.tld still resolves to X, and the request for http://domain.tld/evil-test would still return 200 OK. In this case, the JavaScript waits a few seconds before re-attempting Step (2).
  4. If domain.tld has expired in the local DNS caches, the victim will query the attacker’s authoritative name server and resolve domain.tld again.
  5. This time, the name server returns a local IP address, Y. As the domain has been rebound to a new IP address, any request for http://domain.tld/evil-test now returns a 404 error. At this point, DNS rebinding is complete. The attack script can now send HTTP requests directly to HTTP endpoints on the device at IP address Y , and read responses, allowing the attacker to extract information from or send commands to the device.
  
  **Rebinding attack works becuase SOP is only checked for the hostname not for IP address. See  https://security.stackexchange.com/questions/189369/why-same-origin-policy-is-based-on-host-name-and-not-on-ip.**
  
  **Countermeasures for this attack:**
  **Users:** Users can install dnsmasq, a local DNS forwarder that protects against DNS rebinding by dropping RFC 1918 addresses from DNS replies, similar to dnswall. Alternatively, users can use OpenWRT routers, which use dnsmasq under the hood to drop private IPs in DNS replies.
  
  **Browsers:** They claimed browser-based defense remains as an open research problem.
  
  **IoT vendors:** Vendors can validate the Host headers of incoming requests and only allow requests that contain the device’s IP address or mDNS name in the Host header. Moreover, we propose that for- bidden header names such as the Origin header, which cannot be overwritten by web scripts, can be used to filter out requests that originate from arbitrary web pages and browsers.
  
  **DNS servers:** DNS providers can use dnswall or similar software to filter out private IPs from DNS replies.
 

**Questions:** Will WebRTC way of getting local IP address still works after Slipstream attacks?
  
  