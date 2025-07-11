
# CNET Project - Enterprise Network Simulation
---

## 📝 Project Overview

This project simulates a complex, multi-block enterprise network using **Cisco Packet Tracer (Instructor Version)**. It demonstrates core networking concepts and services, such as:

- Dynamic routing protocols (EIGRP, OSPF, RIP)
- Route redistribution between protocols
- VLSM-based IP addressing
- DHCP server implementation
- NAT configuration
- Access Control Lists (ACLs)
- FTP and Email service configuration

---

## 🧠 Key Objectives

- Design a realistic network topology with proper IP planning
- Configure dynamic routing using OSPF (multi-area), EIGRP, and RIP v2
- Implement route redistribution to enable communication between routing domains
- Use VLSM for efficient IP allocation across networks A to N
- Configure centralized **DHCP** for dynamic IP assignment
- Implement **NAT** using private and public IPs on edge routers
- Apply **ACLs** to restrict access to services (e.g., Web Server)
- Setup and test **FTP** and **Email servers**

---

## 🔀 Routing Protocols Used

- **EIGRP**
- **OSPF (Area 0, Area 1, etc.)**
- **RIP Version 2**

### ➕ Route Redistribution

Routing redistribution was done to interconnect different protocol zones:

```bash
router ospf 15
 redistribute eigrp 15 subnets
 redistribute rip subnets

router eigrp 15
 redistribute ospf 15 metric 10000 100 255 1 1500
 redistribute rip metric 10000 100 255 1 1500

router rip
 version 2
 redistribute eigrp 15
 redistribute ospf 15
 ```
---
🗂️ IP Addressing
---
Private IP Range: 172.16.254.15

Public IP Range: 192.168.1.57

Used VLSM for subnetting based on host requirements

Calculated subnets using: 2^n - 2

---
🌐 NAT Configuration
---
NAT was applied to simulate internet access using public IPs:

```bash
Copy
Edit
interface fa0/0
 ip nat inside
interface s0/0
 ip nat outside
ip nat inside source list 1 interface s0/0 overload
access-list 1 permit 172.16.0.0 0.0.255.255
```
---
🔐 ACL Implementation
---
Access Control Lists were used to restrict access:

Blocked one PC from Net A, one Laptop from Net E, and a phone from Net B from accessing the Web Server

Blocked all devices in Network D from the Web Server

Example ACL:

```bash
Copy
Edit
access-list 100 deny ip host 172.16.10.2 host 192.168.1.100
access-list 100 permit ip any any
```

---
🧪 DHCP Server
---
Configured to dynamically assign IPs across EIGRP, RIP, and OSPF domains:

```bash
Copy
Edit
ip dhcp pool NET_A
 network 172.16.10.0 255.255.255.0
 default-router 172.16.10.1
dns-server 8.8.8.8
```

---
📁 FTP Configuration
---
Assigned a static IP to the FTP Server

Enabled FTP service

Created login credentials for users

Only hosts in Network G can upload/download files

---
📧 Email Server
---
Hosts in Networks H and I configured with email clients

Able to send/receive messages internally using SMTP/POP3

---
📌 Summary
---
This project provided a hands-on simulation of an enterprise-grade network with:

Multiple protocols

Real-world service configurations

Traffic filtering and segmentation

Scalable IP planning using VLSM

It enhances practical skills in routing, subnetting, network services, and security.

