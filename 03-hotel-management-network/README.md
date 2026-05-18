# Project 3: Vic Modern Hotel Management Network

## Project Overview
This project involves the design and implementation of an enterprise-grade network for **Vic Modern Hotel**. The architecture spans three floors, each housing distinct operational departments. The network emphasizes logical segmentation using VLANs, dynamic IP allocation, secure remote management (SSH), physical layer security (Port Security), and dynamic routing using OSPF to ensure full inter-departmental and inter-floor connectivity.

## Network Topology
The topology utilizes a multi-router core connected via Serial DCE cables, with each router managing the inter-VLAN routing (Router-on-a-Stick) and DHCP services for its respective floor.

![Vic Modern Hotel Topology](./topologi.png)

### Hardware Architecture
* **Routers:** 3x Cisco 2901 (F1-Router, F2-Router, F3-Router) connected in a triangle topology via Serial DCE interfaces.
* **Switches:** 3x Cisco 2960-24TT (One per floor handling Access and Trunking).
* **Wireless:** Access Points deployed on every floor to service mobile devices (Laptops, Smartphones, Tablets).
* **End Devices:** PCs, Network Printers (per department), and a dedicated Test-PC for IT Administration.

---

## IP Addressing & VLAN Schema

### WAN Links (Serial Connections)
| Link | Network Address | Subnet Mask |
| :--- | :--- | :--- |
| **F1-Router ↔ F2-Router** | `10.10.10.0/30` | `255.255.255.252` |
| **F2-Router ↔ F3-Router** | `10.10.10.4/30` | `255.255.255.252` |
| **F3-Router ↔ F1-Router** | `10.10.10.8/30` | `255.255.255.252` |

### Floor 1 Deployment
| Department | VLAN ID | Network Address | Subnet Mask |
| :--- | :---: | :--- | :--- |
| **Logistics** | VLAN 60 | `192.168.6.0/24` | `255.255.255.0` |
| **Store** | VLAN 70 | `192.168.7.0/24` | `255.255.255.0` |
| **Reception** | VLAN 80 | `192.168.8.0/24` | `255.255.255.0` |

### Floor 2 Deployment
| Department | VLAN ID | Network Address | Subnet Mask |
| :--- | :---: | :--- | :--- |
| **Sales** | VLAN 30 | `192.168.3.0/24` | `255.255.255.0` |
| **HR** | VLAN 40 | `192.168.4.0/24` | `255.255.255.0` |
| **Finance** | VLAN 50 | `192.168.5.0/24` | `255.255.255.0` |

### Floor 3 Deployment
| Department | VLAN ID | Network Address | Subnet Mask |
| :--- | :---: | :--- | :--- |
| **IT** | VLAN 10 | `192.168.1.0/24` | `255.255.255.0` |
| **Admin** | VLAN 20 | `192.168.2.0/24` | `255.255.255.0` |

---

## Key Configurations

### 1. Dynamic Routing (OSPF)
OSPF is configured on all routers to advertise local VLAN subnets and the point-to-point serial links, ensuring full reachability across the hotel network.

```bash
F3-Router(config)# router ospf 1
F3-Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
F3-Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
F3-Router(config-router)# network 10.10.10.4 0.0.0.3 area 0
F3-Router(config-router)# network 10.10.10.0 0.0.0.3 area 0
```
*(Similar OSPF configurations are applied to F1-Router and F2-Router for their respective networks).*

### 2. Remote Access (SSH Setup)
To secure remote management, SSH is configured on all routers, disabling unencrypted Telnet access.

```bash
R3(config)# ip domain-name gtech
R3(config)# username gtech password gtech
R3(config)# crypto key generate rsa 
# (Set modulus to 1024 bits when prompted)
R3(config)# line vty 0 15
R3(config-line)# login local
R3(config-line)# transport input ssh
```

### 3. Layer 2 Security (Port Security)
To protect the IT Department's infrastructure, strict port security is applied to `fa0/1` on the Floor 3 Switch. It binds the MAC address of the **Test-PC** to the port dynamically and shuts down the port if an unauthorized device connects.

```bash
S3(config)# interface fa0/1
S3(config-if)# switchport mode access
S3(config-if)# switchport port-security
S3(config-if)# switchport port-security maximum 1
S3(config-if)# switchport port-security mac-address sticky
S3(config-if)# switchport port-security violation shutdown
```

### 4. DHCP Server Configuration
Each router is configured to act as the DHCP server for the VLANs operating on its specific floor. 

```bash
# Example: IT Department Pool on F3-Router

# Exclude Default Gateway Addresses
F3-Router(config)# ip dhcp excluded-address 192.168.1.1
F3-Router(config)# ip dhcp excluded-address 192.168.2.1

# DHCP Pool for IT (VLAN 10)
F3-Router(config)# ip dhcp pool IT
F3-Router(dhcp-config)# network 192.168.1.0 255.255.255.0
F3-Router(dhcp-config)# default-router 192.168.1.1
F3-Router(dhcp-config)# dns-server 192.168.1.1
F3-Router(dhcp-config)# exit

# DHCP Pool for Admin (VLAN 20)
F3-Router(config)# ip dhcp pool Admin
F3-Router(dhcp-config)# network 192.168.2.0 255.255.255.0
F3-Router(dhcp-config)# default-router 192.168.2.1
F3-Router(dhcp-config)# dns-server 192.168.2.1
F3-Router(dhcp-config)# exit
```

---

## Testing & Verification
1. **DHCP Validation:** All wired PCs, wireless laptops, tablets, and smartphones successfully receive IP configurations dynamically.
2. **End-to-End Connectivity:** Cross-floor pings succeed (e.g., Reception PC on Floor 1 can ping the IT Test-PC on Floor 3), proving OSPF and Inter-VLAN routing are functioning correctly.
3. **SSH Verification:** Using the Test-PC in the IT department, successful remote login to F1-Router, F2-Router, and F3-Router is achieved via SSH.
4. **Port Security Test:** Disconnecting Test-PC and attaching an unauthorized rogue laptop to `fa0/1` on the F3-Switch immediately transitions the port to an `err-disabled` (shutdown) state, verifying MAC spoofing protection.
