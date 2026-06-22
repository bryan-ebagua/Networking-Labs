# Lab 3: Logical Network Segmentation via VLANs

## 📌 Objective
The goal of this lab was to implement Virtual Local Area Networks (VLANs) on a Cisco enterprise switch to achieve Layer 2 network segmentation. By dividing a single physical switch into distinct logical broadcast domains, I established strict traffic isolation between departments sharing the same IP subnet framework.

## 🏗️ Topology & Architecture
* **End Devices:** 4x Windows PCs (2x HR Department, 2x IT Department)
* **Intermediary Device:** 1x Cisco 2960-24TT Switch
* **Cabling:** Copper Straight-Through (FastEthernet)

<img width="908" height="752" alt="image" src="https://github.com/user-attachments/assets/401a53cd-e4cd-48fc-8a59-68a8f27cb59e" />
<img width="732" height="260" alt="image" src="https://github.com/user-attachments/assets/0cd28f90-d8ca-45bd-a892-397a0fc5ffb7" />

## 🗺️ Addressing & VLAN Assignment Scheme
| Device Name | Switch Port | Department / Access VLAN | IP Address | Subnet Mask |
| :--- | :--- | :--- | :--- | :--- |
| **PC0** | FastEthernet 0/1 | VLAN 10 (HR) | `192.168.1.10` | `255.255.255.0` |
| **PC1** | FastEthernet 0/2 | VLAN 10 (HR) | `192.168.1.11` | `255.255.255.0` |
| **PC2** | FastEthernet 0/3 | VLAN 20 (IT) | `192.168.1.20` | `255.255.255.0` |
| **PC3** | FastEthernet 0/4 | VLAN 20 (IT) | `192.168.1.21` | `255.255.255.0` |

## 🚀 Configuration & Verification Steps
1. **Baseline Testing:** Verified that all 4 devices could ping each other initially while residing within the switch's default, unsegmented broadcast domain (`VLAN 1`).
2. **VLAN Creation:** Accessed the Cisco Switch CLI via privileged EXEC mode to define and name two distinct logical networks: `VLAN 10 (HR)` and `VLAN 20 (IT)`.
3. **Port Provisioning:** Configured specific interface ranges to operate in access mode, permanently binding `Fa0/1-2` to VLAN 10 and `Fa0/3-4` to VLAN 20.
4. **Isolation Verification:** * Initiated an intra-VLAN ping from PC0 to PC1; traffic **succeeded**, confirming normal operations within the same logical domain.
   * Initiated an inter-VLAN ping from PC0 to PC2; traffic **failed** (request timed out), successfully demonstrating hard Layer 2 data link layer isolation despite sharing the identical `192.168.1.0/24` subnet.


