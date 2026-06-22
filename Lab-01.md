# Lab 1: The Simple Local Area Network (LAN)

## 📌 Objective
The goal of this lab was to establish foundational Layer 1 (Physical), Layer 2 (Data Link), and Layer 3 (Network) connectivity. I configured a simple Local Area Network (LAN) by connecting two end devices to a central switch, applying static IPv4 addressing, and verifying bidirectional communication.

## 🏗️ Topology & Architecture
* **End Devices:** 2x Windows PCs
* **Intermediary Device:** 1x Cisco 2960-24TT Switch
* **Cabling:** Copper Straight-Through (FastEthernet)


<img width="1192" height="451" alt="image" src="https://github.com/user-attachments/assets/41fb98c9-588c-4925-8bc6-f3f08e6ed358" />

## 🗺️ Addressing Scheme
| Device Name | Interface | IP Address | Subnet Mask |
| :--- | :--- | :--- | :--- |
| **PC0** | FastEthernet0 | `192.168.1.10` | `255.255.255.0 (/24)` |
| **PC1** | FastEthernet0 | `192.168.1.11` | `255.255.255.0 (/24)` |

## 🚀 Configuration & Verification Steps
1. **Physical Connections:** Patched PC0 and PC1 into the Cisco 2960 switch using straight-through cables. Waited for Spanning Tree Protocol (STP) to transition ports from learning to forwarding state (amber to green).
2. **Logical Addressing:** Assigned static IPv4 addresses within the same `/24` broadcast domain so the devices could communicate locally without a router.
3. **Connectivity Verification:** Ran an ICMP ping test from PC0 to PC1 (`ping 192.168.1.11`).
4. **Packet Analysis:** Utilized Packet Tracer's Simulation Mode to track the ICMP echo requests and replies traversing the switch, confirming successful Layer 2 frame forwarding and Layer 3 packet delivery. 

## ✅ Status: Completed

