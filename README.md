<h1>Enterprise Office Network Design and Implementation Using Cisco Packet Tracer</h1>

<h2>Description</h2>
The Enterprise Office Network Design and Implementation Project focuses on designing a scalable, secure, and high-performance network infrastructure for a multi-floor corporate office. The network is structured to support departmental segmentation, secure interconnectivity, dynamic IP allocation, and wireless access while ensuring network security, redundancy, and efficiency.
This enterprise network consists of three core routers forming the backbone infrastructure, three Layer 2 switches providing VLAN segmentation per floor, and Wi-Fi access points enabling mobility for employees. The network uses OSPF (Open Shortest Path First) routing for efficient inter-floor and inter-department communication. DHCP services are also deployed to manage IP allocation dynamically.
<br />


<h2>Objectives</h2>

- <b>Hierarchical Network Architecture: Structuring the network using core (routers), distribution (switches), and access layers (end devices)</b> 
- <b>VLAN Segmentation: Implementing logical network segmentation to isolate departmental traffic.</b>
- <b>Dynamic Routing with OSPF: Ensuring inter-VLAN and inter-floor routing for efficient communication.</b>
- <b>DHCP Configuration: Automating IP address allocation across VLANs.</b>
- <b>Enterprise Security Measures: Enforcing SSH-based remote management </b>

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (21H2)
## VLAN and Subnet Assignments

| VLAN ID   | Department          | Subnet           |
|-----------|---------------------|------------------|
| **VLAN 80** | Reception         | `192.168.8.0/24` |
| **VLAN 70** | Inventory         | `192.168.7.0/24` |
| **VLAN 60** | Logistics         | `192.168.6.0/24` |
| **VLAN 50** | Finance           | `192.168.5.0/24` |
| **VLAN 40** | HR                | `192.168.4.0/24` |
| **VLAN 30** | Sales & Marketing | `192.168.3.0/24` |
| **VLAN 20** | Administration    | `192.168.2.0/24` |
| **VLAN 10** | IT Department     | `192.168.1.0/24` |

<h2>Implementation</h2>

