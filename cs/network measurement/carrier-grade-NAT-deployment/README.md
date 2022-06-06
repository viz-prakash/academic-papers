Summary of paper [A Multi-perspective Analysis of Carrier-Grade NAT Deployment](./carrier-grade-NAT-deployment.pdf).

In this paper authors have studied the deployment of Carrier-Grade NAT deployment. Different from NAT, carrier grade NAT
puts various independent and disparate endpoints under NAT to solve the IP address exhaustion inside an ISP network.

They have used two methodologies to conduct this study. First, they used a unique technique of BitTorrent Distributed
Hash Table (DHT) to find the deployment of C-NATs. BitTorrent protocol uses internal assigned IPs of nodes in the DHT
which helped then in finding out existance of NAT between two different end points inside the same ISP network. Second
technique they used relied on Netalyzer, which is a tool users volunteerly install on their machine. Netalyzer collects
information about the machine and sends it to the server controlled by the authors, which gives them idea if there is a
C-NAT in between.

This paper have a detialed definition of different kind of NAT deployments and is must read for understanding advanced
concepts of NAT.

