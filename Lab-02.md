# Lab 2: SOHO Wireless & Automated DHCP Deployment

##  Objective
The goal of this lab was to implement a Small Office/Home Office (SOHO) network that automates IP address provisioning and enforces wireless security protocols. I deployed a wireless gateway, activated automated dynamic host configurations, and established secure endpoint access parameters.

##  Topology & Architecture
* **End Devices:** 1x Wired PC, 1x Wireless Laptop (Upgraded with a WPC300N 2.4GHz wireless NIC)
* **Intermediary Device:** 1x Cisco Wireless Home Router
* **Cabling:** Copper Straight-Through (LAN ports to PC) & 802.11n Wireless 

<img width="1866" height="766" alt="image" src="https://github.com/user-attachments/assets/bd8269cd-0ddd-477c-b0d2-ea382f82c95d" />


##  Addressing Scheme
| Device Name | Connection Type | IP Assignment | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Home Router** | Management Interface | `192.168.0.1` (Static) | `255.255.255.0` | N/A |
| **PC0** | Wired (FastEthernet0) | `192.168.0.100` (DHCP) | `255.255.255.0` | `192.168.0.1` |
| **Laptop0** | Wireless (Wireless0) | `192.168.0.101` (DHCP) | `255.255.255.0` | `192.168.0.1` |

##  Configuration & Verification Steps
1. **Hardware Modification:** Swapped the laptop's default wired RJ-45 module for a WPC300N wireless network interface card to support local radio frequency links.
2. **DHCP Activation:** Toggled client network interfaces to DHCP mode, successfully requesting lease assignments automatically from the router's internal scope pool.
3. **Wireless Hardening:** Accessed the router's graphical user interface (GUI) to broadcast a custom Service Set Identifier (SSID) named `LabNetwork`. 
4. **Encryption Enforcement:** Enforced **WPA2-Personal (AES)** security over the wireless domain using a secure pre-shared key.
5. **Connectivity Verification:** Authenticated the laptop to the secured wireless network and verified network functionality via a successful ICMP ping from the wired PC to the wireless laptop interface.


