# Lab 4: Router-on-a-Stick (Inter-VLAN Routing)

## Objective
The goal of this lab was to establish controlled, Layer 3 inter-VLAN communication while maintaining Layer 2 broadcast isolation. I configured a "Router-on-a-Stick" (ROAS) architecture by provisioning 802.1Q trunking on a switch and deploying logical sub-interfaces on a centralized edge router.

## Topology & Architecture
* **End Devices:** 2x Windows PCs (1x HR Department, 1x IT Department)
* **Switching:** 1x Cisco 2960-24TT Switch
* **Routing:** 1x Cisco 1941 Integrated Services Router
* **Protocols:** IEEE 802.1Q (Trunking), ICMP

<img width="922" height="708" alt="image" src="https://github.com/user-attachments/assets/ac95d6e3-0202-450c-a2bd-fda21229d729" />

## Addressing & VLAN Routing Scheme
| Device | Interface / Sub-interface | VLAN / Department | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PC0** | FastEthernet0 | VLAN 10 (HR) | `192.168.10.10` | `255.255.255.0` | `192.168.10.1` |
| **PC1** | FastEthernet0 | VLAN 20 (IT) | `192.168.20.10` | `255.255.255.0` | `192.168.20.1` |
| **Router** | GigabitEthernet0/0.10 | VLAN 10 Gateway | `192.168.10.1` | `255.255.255.0` | N/A |
| **Router** | GigabitEthernet0/0.20 | VLAN 20 Gateway | `192.168.20.1` | `255.255.255.0` | N/A |

## Configuration & Troubleshooting Steps
1. **Layer 2 Provisioning:** Defined VLAN 10 (HR) and VLAN 20 (IT) on the Cisco switch, hardcoding endpoint access ports to their respective broadcast domains.
2. **Trunk Activation:** Configured the switch-to-router uplink as a multi-VLAN trunk port to allow tagged traffic to traverse a single physical wire.
3. **Layer 3 Sub-interfaces:** Activated the router's physical interface without an IP address, then generated logical sub-interfaces (`g0/0.10` and `g0/0.20`).
4. **802.1Q Encapsulation:** Bound each sub-interface to its corresponding VLAN ID using `encapsulation dot1Q` and assigned gateway IP addresses.
5. **Fault Resolution:** Initially encountered a `Destination host unreachable` error during ICMP testing. Systematically isolated the fault to the router, identified a missing sub-interface configuration for the IT gateway, applied the corrective syntax, and restored routing tables.
6. **Verification:** Successfully executed an inter-VLAN ping from PC0 to PC1, confirming that traffic was actively routing up the trunk, crossing logical boundaries at Layer 3, and successfully returning.
