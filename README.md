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
## 📌 Overall Network Architecture
This is the **Enterprise Office Network Architecture**, which consists of **three floors**, each equipped with a **Layer 2 switch** and **wireless access point** to support both wired and wireless devices.

### 📷 Network Topology Diagram
![Enterprise Office Network](https://github.com/Prajwal-Manjunath/OfficeSpaceNetworkDesign/blob/main/OfficeNetwork.png)

### 🏢 Network Overview
- **First Floor:** Reception, Store, and Logistics departments.
- **Second Floor:** Finance, HR, and Sales departments.
- **Third Floor:** Administration and IT departments.

### 🔗 Interconnectivity
- **Three Routers** form the core network backbone.
- **Connected via Serial DCE Cables** for inter-router communication.
- **Each floor has a dedicated switch** for VLAN-based segmentation.
- **Access Points (APs) on each floor** enable Wi-Fi connectivity for mobile devices.

### Detail Explanation

## 📡 Router Interconnections 

| Network       | Subnet          | Router Interfaces |
|--------------|----------------|------------------|
| `10.10.10.0/30` | `255.255.255.252` | R1 ↔ R2 |
| `10.10.10.4/30` | `255.255.255.252` | R2 ↔ R3 |
| `10.10.10.8/30` | `255.255.255.252` | R3 ↔ R1 |

##  Router Configurations

### **Router 2 Configuration**
```bash
en 
conf t
int se0/3/0
no sh

int se0/3/1
no sh

int gig0/0
no sh

int se0/3/0
clock rate 64000

int se0/3/1
clock rate 64000
do wr

### **Router 1 Configuration**
en 
conf t 

int se0/3/0
no sh

int se0/3/1
no sh

do wr

### **Router 3 Configuration**
en
conf t

int se0/3/0 
no sh

int se0/3/1
no sh

do wr


```

## 🖧 Configuring VLAN in Switches

Switch 1 configuration
```bash
en
conf t
int range fa0/2-3
switchport mode access
switchport access VLAN 80

int range fa0/4-5
switchport mode access
switchport access VLAN 70

int range fa0/6-8
switchport mode access
switchport access VLAN 60
int range fa0/1
switchport mode access
switchport mode trunk
do wr

Switch 2 configuration

en
conf t
int range fa0/2-3
switchport mode access
switchport access VLAN 50

int range fa0/4-5
switchport mode access
switchport access VLAN 40

int range fa0/6-8
switchport mode access
switchport access VLAN 30

int range fa0/1
switchport mode access
switchport mode trunk
do wr

switch 3 Configuration

en
conf t
int range fa0/2-3
switchport mode access
switchport access VLAN 20

int range fa0/4-6
switchport mode access
switchport access VLAN 10
int range fa0/1
switchport mode access
switchport mode trunk
do wr
```

## Router IP configuration as per table

```bash
router 1

en
conf t
in se0/3/0
ip address 10.10.10.1 255.255.255.252

in se0/3/1
ip address 10.10.10.5 255.255.255.252
do wr

router 2

en
conf t
in se0/3/0
ip address 10.10.10.2 255.255.255.252

in se0/3/1
ip address 10.10.10.9 255.255.255.252
do wr

router 3

en
conf t
in se0/3/0
ip address 10.10.10.6 255.255.255.252

in se0/3/1
ip address 10.10.10.10 255.255.255.252

do wr
```
## Inter VLAN Routing

```bash
Router 1

int gig0/0.80
encapsuation dot1Q 80
ip address 192.168.8.1 255.255.255.0

int gig0/0.70
encapsuation dot1Q 70
ip address 192.168.7.1 255.255.255.0

int gig0/0.60
encapsuation dot1Q 60
ip address 192.168.6.1 255.255.255.0
do wr

DHCP Server Configuration

service dhcp
ip dhcp pool reception
network 192.168.8.0 255.255.255.0
default-router 192.168.8.1
dns-server 192.168.8.1

ip dhcp pool store
network 192.168.7.0 255.255.255.0
default-router 192.168.7.1
dns-server 192.168.7.1

ip dhcp pool Logistics
network 192.168.6.0 255.255.255.0
default-router 192.168.6.1
dns-server 192.168.6.1

do wr

Router 2

int gig0/0.50
encapsuation dot1Q 50
ip address 192.168.5.1 255.255.255.0

int gig0/0.40
encapsuation dot1Q 40
ip address 192.168.4.1 255.255.255.0

int gig0/0.30
encapsuation dot1Q 30
ip address 192.168.3.1 255.255.255.0
do wr

DHCP Server Configuration

service dhcp
ip dhcp pool finance
network 192.168.5.0 255.255.255.0
default-router 192.168.5.1
dns-server 192.168.5.1

ip dhcp pool HR
network 192.168.7.0 255.255.255.0
default-router 192.168.4.1
dns-server 192.168.4.1

ip dhcp pool Sales
network 192.168.3.0 255.255.255.0
default-router 192.168.3.1
dns-server 192.168.3.1

do wr

Router 3

int gig0/0.20
encapsuation dot1Q 20
ip address 192.168.2.1 255.255.255.0

int gig0/0.10
encapsuation dot1Q 10
ip address 192.168.1.1 255.255.255.0


DHCP Server Configuration

service dhcp
ip dhcp pool Admin
network 192.168.2.0 255.255.255.0
default-router 192.168.2.1
dns-server 192.168.2.1

ip dhcp pool IT
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 192.168.1.1

do wr

```
## Inter Routing Protocol Configuration (OSPF Configuration)

```bash
Router 1

en
conf t
router ospf 10
network 10.10.10.0 255.255.255.252 area 0
network 10.10.10.4 255.255.255.252 area 0
network 192.168.8.0 255.255.255.0 area 0
network 192.168.7.0 255.255.255.0 area 0
network 192.168.6.0 255.255.255.0 area 0
do wr

Router 2

en
conf t
router ospf 10
network 10.10.10.4 255.255.255.252 area 0
network 10.10.10.0 255.255.255.252 area 0
network 10.10.10.8 255.255.255.252 area 0
network 192.168.5.0 255.255.255.0 area 0
network 192.168.4.0 255.255.255.0 area 0
network 192.168.3.0 255.255.255.0 area 0

do wr

Router 3

en
conf t
router ospf 10
network 10.10.10.8 255.255.255.252 area 0
network 10.10.10.4 255.255.255.252 area 0
network 192.168.2.0 255.255.255.0 area 0
network 192.168.1.0 255.255.255.0 area 0
do wr
```

## Configuring SSH on routers for remote login 
```bash
Router 1 
en
conf t
hostname f1-router
ip domain-name poffice
username poffice password poffice
crypto key generate rsa
line vty 0 15
transport input ssh
do wr

Router 2
en
conf t
hostname f2-router
ip domain-name poffice
username poffice password poffice
crypto key generate rsa
line vty 0 15
transport input ssh
do wr

Router 3
en
conf t
hostname f3-router
ip domain-name poffice
username poffice password poffice
crypto key generate rsa
line vty 0 15
transport input ssh
do wr
