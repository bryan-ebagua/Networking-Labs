# Lab 7: Hardening Perimeters with Extended Access Control Lists (ACLs)

## Objective
The objective of this lab was to implement stateless firewall filtering using an Extended Named Access Control List. I configured the edge router to enforce enterprise security policies by selectively permitting web traffic (HTTP) while explicitly blocking network reconnaissance traffic (ICMP/Ping) from reaching a sensitive server subnet.

## Topology & Additions
Building upon the convergent OSPF network from Lab 6, I introduced a dedicated server node to simulate a corporate data center environment:
* **Atlanta LAN Domain:** `192.168.1.0/24` (Host `PC-ATL`: `192.168.1.10`)
* **New York LAN Domain:** `192.168.2.0/24`
* **Target Web Server (NY-SRV):** `192.168.2.100` (Connected via the New York Switch)
* **WAN Routing Link:** `10.0.0.0/30` running dynamic OSPF

<img width="892" height="322" alt="image" src="https://github.com/user-attachments/assets/50623188-71f9-4dbc-a781-057208b677b3" />


## Security Policy Enforcement Logic
Extended ACLs permit granular filtering based on source/destination IPs, Layer 4 protocols, and logical port numbers. I implemented a named extended ACL called `SECURE_PERIMETER` on `ATL-RTR` using the following top-down sequential rules:
1. **Rule 1 (Deny ICMP):** `deny icmp host 192.168.1.10 host 192.168.2.100`  
   *Blocks ping verification attempts to prevent network mapping and discovery.*
2. **Rule 2 (Permit HTTP):** `permit tcp host 192.168.1.10 host 192.168.2.100 eq 80`  
   *Allows the host to establish standard TCP port 80 handshakes to view the hosted webpage.*
3. **Rule 3 (Permit IP Any Any):** `permit ip any any`  
   *Overrides the default implicit deny at the bottom of the ACL to preserve normal traffic flows for the rest of the enterprise.*

## Placement & Application
To maximize efficiency and conserve WAN bandwidth, I applied the ACL as close to the traffic source as possible. I mapped the rule sequence to the **inbound** direction of the Atlanta local gateway interface:
```text
interface gigabitEthernet 0/0
 ip access-group SECURE_PERIMETER in
