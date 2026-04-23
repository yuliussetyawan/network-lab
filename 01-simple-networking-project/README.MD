## Project Overview
This project showcases a functional network topology designed in **Cisco Packet Tracer**. It implements a segmented architecture to connect the **Accounts** and **Delivery** departments, ensuring secure and efficient data flow between specialized workgroups using Subnetting.

## Network Topology
The design features a star topology within each department, linked via a central router to enable inter-subnet communication.

- **Router:** Cisco 2911 (Router0)
- **Switches:** 2x Cisco 2960-24TT (ACCOUNTS & DELIVERY)
- **End Devices:** - **Accounts:** 2 PCs (PC0, PC1) and 1 Network Printer (Printer0).
  - **Delivery:** 2 PCs (PC2, PC3) and 1 Network Printer (Printer1).
- **Cabling:** Copper Straight-Through cables used for all Ethernet connections.

## IP Addressing Schema
The network utilizes the `192.168.40.0` address space, partitioned into two subnets using a `/25` mask (255.255.255.128) to accommodate up to 126 hosts per department.

### Subnet 1: Accounts Department
| Detail | Value |
| :--- | :--- |
| **Network Address** | 192.168.40.0/25 |
| **First Usable Host (Gateway)** | 192.168.40.1 |
| **Last Usable Host** | 192.168.40.126 |
| **Broadcast Address** | 192.168.40.127 |

### Subnet 2: Delivery Department
| Detail | Value |
| :--- | :--- |
| **Network Address** | 192.168.40.128/25 |
| **First Usable Host (Gateway)** | 192.168.40.129 |
| **Last Usable Host** | 192.168.40.254 |
| **Broadcast Address** | 192.168.40.255 |

## Configuration Logic

### 1. Router Interface Configuration
The router (Router0) acts as the default gateway for both departments. 

```bash
Router> enable
Router# configure terminal

# Configuring Accounts Gateway
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.40.1 255.255.255.128
Router(config-if)# no shutdown

# Configuring Delivery Gateway
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.40.129 255.255.255.128
Router(config-if)# no shutdown


### 2. End Device Assignment
Each PC and Printer is assigned a static IP address within its respective range. To ensure communication outside their local subnet, the Default Gateway for every device points to the respective Router0 interface.

| Device | Department | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **PC0** | Accounts | 192.168.40.2 | 255.255.255.128 | 192.168.40.1 |
| **PC1** | Accounts | 192.168.40.3 | 255.255.255.128 | 192.168.40.1 |
| **Printer0** | Accounts | 192.168.40.4 | 255.255.255.128 | 192.168.40.1 |
| **PC2** | Delivery | 192.168.40.130 | 255.255.255.128 | 192.168.40.129 |
| **PC3** | Delivery | 192.168.40.131 | 255.255.255.128 | 192.168.40.129 |
| **Printer1** | Delivery | 192.168.40.132 | 255.255.255.128 | 192.168.40.129 |

---

## Connectivity Testing & Verification

Verification was conducted by performing cross-departmental pings to ensure the Router is correctly routing traffic between the two subnets.

### Test Scenario: Inter-Departmental Ping
**Source Device:** PC3 (Delivery Department)  
**Destination Device:** PC0 (Accounts Department)

**The Packet Path:**
1. **Source:** PC3 generates an ICMP request. Since the destination IP (`192.168.40.2`) is on a different subnet, the packet is sent to the Default Gateway.
2. **Local Switch:** The Delivery Switch forwards the frame to the Router0 `GigabitEthernet 0/1` interface.
3. **Routing:** Router0 checks its routing table, identifies that the `192.168.40.0/25` network is directly connected to its `GigabitEthernet 0/0` interface.
4. **Switching:** The packet is forwarded through the Accounts Switch.
5. **Destination:** PC0 receives the ICMP request and sends an ICMP reply back through the same logical path.

**Result:** `Pinging 192.168.40.2 with 32 bytes of data:`  
`Reply from 192.168.40.2: bytes=32 time<1ms TTL=127`  
`Reply from 192.168.40.2: bytes=32 time<1ms TTL=127`

**Status:** ✅ **Successful.** The routing table on Router0 correctly identifies the direct routes to both the `192.168.40.0/25` and `192.168.40.128/25` networks.

---

## Technical Skills Demonstrated
* **VLSM/Subnetting:** Efficient use of the 192.168.40.0/24 address space.
* **Router Configuration:** Setting up Gateways and enabling interfaces via Cisco IOS CLI.
* **Network Troubleshooting:** Verifying end-to-end connectivity across Layer 3 boundaries.
* **Topology Documentation:** Clearly mapping out network flow and addressing.

---