# Lab 8: Enterprise Edge Network Address Translation (NAT Overload / PAT)

## Objective
The objective of this lab was to configure Port Address Translation (PAT) on an enterprise edge router to bridge the gap between private RFC 1918 networks and the public internet. I engineered a simulation of a Public Internet Service Provider (ISP) and a public web server, then configured the corporate gateway to translate multiple private internal hosts to a single usable public IP address utilizing Layer 4 source ports.

## Topology & Architectural Modifications
During this lab, I encountered a physical port limitation on the initial Cisco 1941 router chassis (`ATL-RTR`). To accommodate a third routed interface without adding expansion modules, I upgraded the gateway to a **Cisco 2911 Integrated Services Router**, which provides three native onboard GigabitEthernet ports.

* **Inside Private LAN Subnet:** `192.168.1.0/24`
* **Public ISP Link Segment:** `203.0.113.0/30` 
  * `ATL-RTR` WAN IP (Inside Global): `203.0.113.1`
  * `ISP-RTR` Gateway IP: `203.0.113.2`
* **Simulated Public Internet Domain:** `8.8.8.0/24` (Target Google/DNS Server: `8.8.8.8`)

<img width="1506" height="557" alt="image" src="https://github.com/user-attachments/assets/b7d520b3-8898-44d2-886c-f903cd020d10" />

## Configuration Protocol
1. **Perimeter Boundaries:** Defined structural NAT orientation by binding the logical boundaries to physical interfaces:
   * `GigabitEthernet 0/0` (Internal LAN) -> `ip nat inside`
   * `GigabitEthernet 0/2` (External ISP WAN) -> `ip nat outside`
2. **Gateway of Last Resort:** Because public internet routes are not propagated via internal OSPF processes, I injected a static default route on `ATL-RTR` to direct all non-corporate traffic out to the provider:
   * Syntax: `ip route 0.0.0.0 0.0.0.0 203.0.113.2`
3. **Interesting Traffic Definition:** Configured Standard Access Control List 1 to explicitly scope the local subnet permitted to undergo translation.
4. **PAT Activation:** Tied the match criteria to the exit interface using the allocation keyword `overload` to trigger port-multiplexing:
   * Syntax: `ip nat inside source list 1 interface gigabitEthernet 0/2 overload`

## Verification & Testing Metrics
* **Outbound Path Validation:** Initiated an ICMP echo request from `PC-ATL` (`192.168.1.10`) targeting the public server (`8.8.8.8`). The packets successfully traversed the network boundary and received valid replies.
* **Header Translation Inspection:** Executed `show ip nat translations` on the edge gateway during active states. Verified that the internal private address (`Inside Local`) successfully mapped to the single assigned WAN IP (`Inside Global`) with matching unique Layer 4 port trackers.
