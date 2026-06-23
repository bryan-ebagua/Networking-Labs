# Lab 6: Dynamic Routing with Single-Area OSPF

## Objective
In the previous lab, I manually configured static routes to establish WAN connectivity. The goal of this lab was to replace those static routes with a dynamic routing protocol. I configured Single-Area OSPF (Open Shortest Path First) to allow the routers to automatically discover each other, share their connected networks, and build their routing tables dynamically.

## Topology & Addressing
I used the same physical topology as Lab 5, consisting of two branch networks connected by a point-to-point WAN link.
* **Atlanta LAN:** `192.168.1.0/24`
* **New York LAN:** `192.168.2.0/24`
* **WAN Link:** `10.0.0.0/30`
* **Hardware:** 2x Cisco 1941 Routers, 2x Cisco 2960 Switches, 2x PCs

<img width="936" height="745" alt="image" src="https://github.com/user-attachments/assets/47a03b4b-3ead-4d2c-98ab-2df1f8c190dd" />

## Configuration Steps
1. **Removing Static Routes:** Before configuring OSPF, I had to remove the manual static routes from both `ATL-RTR` and `NY-RTR` using the `no ip route` command. This ensured that the traffic would only be routed using OSPF.
2. **Enabling OSPF:** I entered global configuration mode on both routers and initialized OSPF using process ID 1 (`router ospf 1`).
3. **Advertising Networks:** I used the `network` command to tell OSPF which interfaces to include in the routing process. This required converting the standard subnet masks into wildcard masks and assigning them to the backbone area (Area 0).
   * **ATL-RTR:** Advertised `192.168.1.0 0.0.0.255` and `10.0.0.0 0.0.0.3`
   * **NY-RTR:** Advertised `192.168.2.0 0.0.0.255` and `10.0.0.0 0.0.0.3`

## Verification & Testing
* **Adjacency Check:** After applying the network statements, I watched the console for the syslog message confirming that the neighbor state moved from `LOADING to FULL`, indicating a successful OSPF handshake.
* **Neighbor Table:** I ran `show ip ospf neighbor` to verify that both routers recognized each other across the `10.0.0.0/30` WAN link.
* **Routing Table:** I used `show ip route` to check the routing tables. I successfully located the newly injected routes marked with an **`O`**, which confirmed that the routers learned the remote networks dynamically.
* **End-to-End Connectivity:** I sent an ICMP ping from the Atlanta PC (`192.168.1.10`) to the New York PC (`192.168.2.10`). The replies were successful, proving the OSPF convergence was functioning correctly.
