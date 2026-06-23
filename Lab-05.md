# Lab 5: Multi-Network Static Routing

##  Objective
The goal of this lab was to establish point-to-point Wide Area Network (WAN) connectivity between two geographically isolated corporate offices (simulated as Atlanta and New York) and manually manipulate the routing tables using static IP routes.

##  Topology & Architecture
* **Atlanta LAN Domain:** `192.168.1.0/24`
* **New York LAN Domain:** `192.168.2.0/24`
* **Point-to-Point WAN Link:** `10.0.0.0/30` (Utilizing a `/30` mask to conserve addressing space, provisioning exactly 2 usable host endpoints).
* **Hardware Simulated:** 2x Cisco 1941 ISR Routers, 2x Cisco 2960 Switches, 2x Endpoint PCs.

<img width="1913" height="727" alt="image" src="https://github.com/user-attachments/assets/f0399c4b-c503-44ad-ba3b-b93d6b6eb063" />

##  Routing Table Blueprint
| Device | Interface | Network Segment Purpose | Assigned IP Address | Subnet Mask |
| :--- | :--- | :--- | :--- | :--- |
| **ATL-RTR** | Gi0/0 | Atlanta Local Gateway | `192.168.1.1` | `255.255.255.0` |
| **ATL-RTR** | Gi0/1 | Cross-Country WAN Link | `10.0.0.1` | `255.255.255.252` |
| **NY-RTR**  | Gi0/0 | New York Local Gateway | `192.168.2.1` | `255.255.255.0` |
| **NY-RTR**  | Gi0/1 | Cross-Country WAN Link | `10.0.0.2` | `255.255.255.252` |

##  Configuration & Execution Breakdown
1. **Interface Provisioning:** Activated the administrative state of all physical interfaces (`no shutdown`) and bound IPs according to the point-to-point allocation scheme.
2. **Static Route Injection:** Because neither router inherently possesses situational awareness of networks beyond their directly connected interfaces, I manually programmed static directional maps:
   * **ATL-RTR Syntax:** `ip route 192.168.2.0 255.255.255.0 10.0.0.2`
   * **NY-RTR Syntax:** `ip route 192.168.1.0 255.255.255.0 10.0.0.1`
3. **End-to-End Verification:** 
   * Executed a `show ip route` verification on both nodes to confirm the manual path injection, validated by an **`S`** flag inside the routing tables.
   * Successfully validated end-device pathing via cross-network ICMP echo replies from `PC-ATL` to `PC-NY`.
