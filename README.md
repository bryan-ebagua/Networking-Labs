# Network Engineering & Simulation Labs

##  Repository Overview
This repository contains a progression of network engineering labs built using **Cisco Packet Tracer**. The purpose of this project is to demonstrate hands-on understanding of network architecture, routing protocols, subnetting, and enterprise security configurations. 

Through these labs, I am actively translating theoretical networking concepts (OSI Model, TCP/IP) into functional, configured topologies.

---

##  Technologies & Protocols Explored
* **Simulation Environment:** Cisco Packet Tracer
* **Layer 2 (Switching):** VLANs, 802.1Q Trunking, Spanning Tree Protocol (STP), MAC Addressing
* **Layer 3 (Routing):** IPv4/IPv6 Subnetting, Static Routing, OSPF (Dynamic Routing), Inter-VLAN Routing (Router-on-a-Stick)
* **Network Services:** DHCP, DNS, NAT / PAT (Network Address Translation)
* **Security & Edge:** Standard/Extended Access Control Lists (ACLs), Site-to-Site IPsec VPNs, Firewalls

---

##  Lab Index & Progression

### Building the Foundation
* **[Lab 1: The Simple LAN](./Lab-01)** 
  * *Objective:* Configure static IPv4 addressing, connect end devices via Layer 2 switching, and verify ICMP connectivity.
* **[Lab 2: SOHO Wireless Setup](./Lab-02)** 
  * *Objective:* Deploy a wireless router, configure internal DHCP scopes, and establish WPA2 Wi-Fi security for end devices.
* **[Lab 3: Creating and Isolating VLANs](./Lab-03)**
  * *Objective:* Segment a physical switch into multiple logical broadcast domains (VLANs) and verify network isolation.
  * 
### Routing & Security
* **[Lab 4: Inter-VLAN Routing (Router-on-a-Stick)](./Lab-04)** 
  * *Objective:* Configure 802.1Q trunking and sub-interfaces on a router to allow communication between isolated VLANs.
* **[Lab 5: Static and Default Routing](./Lab-05)** 
  * *Objective:* Manually configure routing tables across multiple routers to establish end-to-end paths across different networks.
* **[Lab 6: Dynamic Routing with OSPF](./Lab-06)** 
  * *Objective:* Automate routing table updates using Single-Area OSPF and observe dynamic path convergence.
* **[Lab 7: Traffic Filtering with ACLs](./Lab-07)** 
  * *Objective:* Write and apply Standard and Extended Access Control Lists to restrict traffic based on IP addresses and specific port protocols (HTTP, ICMP).

### Advanced Enterprise Architecture
* **[Lab 8: NAT & PAT (Network Address Translation)](./Lab-08)** - `[Not Started]`
  * *Objective:* Configure NAT Overload (PAT) to allow private internal networks to access the public internet using a single public IP, and Static NAT for web server hosting.
* **[Lab 9: Site-to-Site IPsec VPN](./Lab-09)** - `[Not Started]`
  * *Objective:* Establish a secure, encrypted tunnel over a simulated public internet between two remote corporate branch routers.
* **[Lab 10: The Ultimate Capstone Network](./Lab-10)** - `[Not Started]`
  * *Objective:* Combine all previous concepts into a cohesive enterprise topology featuring Core/Access layers, VLANs, OSPF routing, a secure DMZ, and NAT internet breakout.

---

## 📝 Methodology
For each lab, the documentation includes:
1. **Topology Diagram:** Visual layout of the configured network.
2. **Addressing Scheme:** The IP subnets, masks, and gateways utilized.
3. **Verification Logs:** CLI outputs proving successful routing, pings, or security enforcements.
