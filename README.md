# Networking Lab Portfolio

Welcome to my networking lab portfolio! This collection showcases hands-on experience in network design, configuration, and troubleshooting using Cisco Packet Tracer. Each project demonstrates progressive complexity and mastery of enterprise networking concepts.

---

## 📋 Projects Overview

### [Project 1: Simple Networking Project](./01-simple-networking-project/)
**Focus:** Network Fundamentals & Subnetting

A foundational network design featuring two departments (Accounts & Delivery) connected through a central router using **VLSM subnetting**. This project demonstrates the ability to:
- Design efficient IP addressing schemes using subnetting
- Configure router interfaces and gateways
- Implement inter-subnet routing
- Verify end-to-end connectivity with ping tests

**Key Technologies:**
- Subnetting (/25 netmask)
- Static IP configuration
- Router-based inter-departmental communication
- Network troubleshooting & ICMP testing

---

### [Project 2: SOHO Network Design (XYZ Company Branch)](./02-soho/)
**Focus:** VLAN Segmentation, Router-on-a-Stick, DHCP & Wireless Integration

An enterprise branch network for XYZ Company supporting three departments (Admin/IT, Finance/HR, Customer Service) with **VLAN segmentation** and **Router-on-a-Stick (ROAS)** architecture. This project introduces:
- VLAN configuration and trunk port setup
- Inter-VLAN routing using router sub-interfaces
- Dynamic IP allocation via DHCP with multiple pools
- Wireless integration with departmental access points
- Network scalability and logical segmentation

**Key Technologies:**
- VLANs (VLAN 10, 20, 30)
- Router-on-a-Stick (ROAS) architecture
- DHCP server configuration
- 802.1Q trunking
- Wireless access points per department
- Sub-interface configuration

---

### [Project 3: Hotel Management Network (Vic Modern Hotel)](./03-hotel-management-network/)
**Focus:** Enterprise Multi-Router Topology, OSPF Routing, SSH Security & Port Security

A sophisticated enterprise network spanning three floors with dynamic routing, remote access security, and Layer 2 protection. This project demonstrates advanced capabilities including:
- Multi-router core network connected via Serial DCE links
- **OSPF dynamic routing** for automatic route discovery
- **SSH remote management** with encrypted access
- **Port Security** with MAC address binding
- Distributed DHCP services across multiple routers
- Complex VLAN spanning multiple floors

**Key Technologies:**
- OSPF dynamic routing protocol
- Multi-router topology (Triangle configuration)
- Serial DCE point-to-point links
- SSH encryption & remote access
- Layer 2 port security with violation handling
- Distributed VLAN architecture
- Wireless access points per floor

---

## 🎯 Technical Skills Demonstrated

### Networking Protocols & Concepts
✓ IP Addressing & Subnetting (VLSM)  
✓ Router Configuration (Static Routes, Dynamic Routes)  
✓ VLANs and Logical Segmentation  
✓ Inter-VLAN Routing (Router-on-a-Stick)  
✓ Dynamic Routing (OSPF)  
✓ DHCP (Dynamic Host Configuration Protocol)  
✓ Wireless Networking  
✓ Network Security (SSH, Port Security)  

### Cisco Devices & Commands
✓ Cisco Routers (2901, 2911)  
✓ Cisco Switches (2960-24TT)  
✓ Cisco IOS CLI Configuration  
✓ Router Interface Configuration  
✓ VLAN & Trunk Configuration  
✓ Sub-interface Setup  
✓ Access Point Management  

### Network Design & Analysis
✓ Topology Design & Documentation  
✓ Addressing Schema Planning  
✓ Network Troubleshooting (Ping, Traceroute)  
✓ Connectivity Verification  
✓ Multi-floor Enterprise Design  
✓ Security Implementation  

---

## 📈 Progression of Complexity

| Aspect | Project 1 | Project 2 | Project 3 |
|--------|-----------|----------|----------|
| **Routers** | 1 | 1 | 3 |
| **Switches** | 2 | 1 | 3 |
| **IP Subnets** | 2 | 3 | 8 |
| **VLAN Count** | — | 3 | 8 |
| **Routing Type** | Static | Static (ROAS) | Dynamic (OSPF) |
| **DHCP Pools** | — | 3 | 6+ |
| **Security Features** | — | — | SSH + Port Security |
| **Wireless Integration** | — | ✓ | ✓ |

---

## 🚀 How to Use This Repository

1. **Review individual project READMEs** for detailed configurations and verification results
2. **Open `.pkt` files in Cisco Packet Tracer** to explore and modify network designs
3. **Follow the configuration logic sections** to understand CLI commands and network setup
4. **Study the connectivity testing sections** to learn troubleshooting approaches

---

## 💡 Key Learnings

- **From Project 1:** Understanding subnetting and basic routing is the foundation of network design
- **From Project 2:** VLANs and dynamic IP allocation enable scalable, manageable enterprise networks
- **From Project 3:** Dynamic routing protocols and security measures are essential for complex, multi-site networks

---

## 📝 Files & Structure

```
networking-lab/
├── README.md (this file)
├── 01-simple-networking-project/
│   ├── 01-simple-networking-project.pkt
│   └── README.MD
├── 02-soho/
│   ├── 02-soho.pkt
│   └── README.md
└── 03-hotel-management-network/
    ├── 03-hotel-management-network.pkt
    └── README.md
```

---

## 🔧 Tools & Software

- **Cisco Packet Tracer** - Network simulation and design platform
- **Cisco IOS CLI** - Device configuration and management

---
