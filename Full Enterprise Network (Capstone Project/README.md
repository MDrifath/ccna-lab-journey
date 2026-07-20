🏢 Project 5 — Full Enterprise Network (Capstone Project)

Objective:
Designed and implemented a complete enterprise network in Cisco Packet Tracer combining all CCNA concepts — VLANs, EtherChannel, STP, DHCP relay, OSPF, Named ACL, NAT/PAT, Default Route and SSH — simulating a real company network with centralized services and internet access.


Topology

<img width="1917" height="982" alt="image" src="https://github.com/user-attachments/assets/74240433-e16c-47b0-8784-7cb85a253863" />


🧩 What I Built

- ✅ Designed complete enterprise network with 1 router, 3 switches, 4 PCs and 1 server
- ✅ Configured VLANs (10, 20, 99) across all switches for department segmentation
- ✅ Implemented EtherChannel (PAgP) between core and access switches for redundancy
- ✅ Configured STP with SW1 as designated root bridge to prevent loops
- ✅ Set up centralized DHCP server on VLAN 99 with pools for VLAN 10 and VLAN 20
- ✅ Configured DHCP relay using ip helper-address on router subinterfaces
- ✅ Implemented Named ACL to restrict inter-department traffic
- ✅ Configured NAT/PAT with default route for internet access simulation
- ✅ Enabled SSH on all network devices replacing Telnet


📋 IP Address Plan

Router R1 — Subinterfaces

| Interface | IP Address | Subnet Mask | Purpose |
|---|---|---|---|
| Gi0/0 | 203.0.113.1 | 255.255.255.252 | NAT Outside — Internet |
| Gi0/1.10 | 192.168.10.1 | 255.255.255.0 | VLAN 10 Gateway — HR |
| Gi0/1.20 | 192.168.20.1 | 255.255.255.0 | VLAN 20 Gateway — IT |
| Gi0/1.99 | 192.168.80.1 | 255.255.255.0 | VLAN 99 Gateway — Server |

Internet Router

| Interface | IP Address | Purpose |
|---|---|---|
| Gi0/0 | 203.0.113.2 | Connects to R1 |
| Loopback 0 | 8.8.8.8 | Simulates internet/Google DNS |

End Devices

| Device | IP Address | Gateway | VLAN | How Assigned |
|---|---|---|---|---|
| PC1 | 192.168.10.2 | 192.168.10.1 | VLAN 10 | DHCP Auto |
| PC2 | 192.168.20.2 | 192.168.20.1 | VLAN 20 | DHCP Auto |
| PC3 | 192.168.10.x | 192.168.10.1 | VLAN 10 | DHCP Auto |
| PC4 | 192.168.20.x | 192.168.20.1 | VLAN 20 | DHCP Auto |
| Server | 192.168.99.5 | 192.168.99.1 | VLAN 99 | Static |


Step 1 — Configure VLANs on All Switches

```
! On SW1, SW2, SW3 — create all VLANs
vlan 10
name HR
exit
vlan 20
name IT
exit


! SW2 — Access ports
interface fa0/1
switchport mode access
switchport access vlan 10
exit
interface fa0/2
switchport mode access
switchport access vlan 20
exit

! SW3 — Access ports
interface fa0/1
switchport mode access
switchport access vlan 10
exit
interface fa0/2
switchport mode access
switchport access vlan 20
exit

```

<img width="1917" height="1020" alt="Screenshot 2026-06-30 112011" src="https://github.com/user-attachments/assets/4ab0ffb9-3978-4830-93be-a48dc45fd945" />


<img width="1917" height="1013" alt="Screenshot 2026-06-30 112523" src="https://github.com/user-attachments/assets/965675c7-354b-4ae2-8688-2ccdd5c5861a" />


Step 3 — Configure EtherChannel (PAgP)

```
! SW1 — towards SW2
interface range fa0/1 - 2
channel-group 1 mode desirable
exit
interface port-channel 1
switchport mode trunk
exit

! SW1 — towards SW3
interface range fa0/3 - 4
channel-group 2 mode desirable
exit
interface port-channel 2
switchport mode trunk
exit

! SW2 — towards SW1
interface range fa0/23 - 24
channel-group 1 mode auto
exit
interface port-channel 1
switchport mode trunk
exit

! SW3 — towards SW1
interface range fa0/23 - 24
channel-group 1 mode auto
exit
interface port-channel 1
switchport mode trunk
exit
```

<img width="1917" height="1015" alt="Screenshot 2026-06-30 123921" src="https://github.com/user-attachments/assets/3e0c74a6-5827-48e0-80ab-58134ffeec93" />


<img width="1917" height="1015" alt="Screenshot 2026-06-30 124757" src="https://github.com/user-attachments/assets/34a1b63c-d755-4392-8016-8cedeb30d7ec" />


<img width="1917" height="1020" alt="Screenshot 2026-06-30 125557" src="https://github.com/user-attachments/assets/b7367e1b-6056-4a64-98ff-bd32dc465e22" />


<img width="1917" height="1015" alt="Screenshot 2026-06-30 124930" src="https://github.com/user-attachments/assets/2eb01d00-97ed-4c2a-8b3a-414aed814051" />


<img width="1917" height="1015" alt="Screenshot 2026-06-30 131045" src="https://github.com/user-attachments/assets/92ff153c-970c-42a0-927e-9d7ac035233b" />


<img width="1917" height="1018" alt="Screenshot 2026-06-30 131250" src="https://github.com/user-attachments/assets/885787d6-7c76-4b2e-a88b-06dfe7e280d5" />



Step 4 — Configure STP Root Bridge


<img width="1917" height="1025" alt="image" src="https://github.com/user-attachments/assets/9928f3c8-d5e6-49a3-8b09-f4fa6eccfa55" />


Step 5 — Configure Trunk — SW1 to Router

```
! SW1
interface fa0/24
switchport mode trunk
exit
```

Step 6 — Configure Router R1 Subinterfaces + DHCP Relay

```
enable
configure terminal

interface gi0/1
no shutdown
exit

interface gi0/1.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
ip helper-address 192.168.99.5
exit

interface gi0/1.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0
ip helper-address 192.168.99.5
exit

interface gi0/1.99
encapsulation dot1q 99
ip address 192.168.99.1 255.255.255.0
exit

interface gi0/0
ip address 203.0.113.1 255.255.255.252
no shutdown
exit
```

<img width="1916" height="1020" alt="Screenshot 2026-06-30 140737" src="https://github.com/user-attachments/assets/8a2ade27-ecd0-48dc-ad22-6b318d021d40" />


<img width="1917" height="1015" alt="Screenshot 2026-06-30 141242" src="https://github.com/user-attachments/assets/3db4b98e-d7c6-4aa6-a9e8-62efe414502b" />


Step 7 — Configure DHCP Server

On Server → Services → DHCP:

| Pool | Gateway | DNS | Start IP | Subnet |
|---|---|---|---|---|
| VLAN10_POOL | 192.168.10.1 | 192.168.99.5 | 192.168.10.10 | 255.255.255.0 |
| VLAN20_POOL | 192.168.20.1 | 192.168.99.5 | 192.168.20.10 | 255.255.255.0 |


<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/d34e2953-6af4-451b-87ef-83fb068e1247" />


Step 8 — Configure NAT + Default Route

```
! R1
ip route 0.0.0.0 0.0.0.0 203.0.113.2

access-list 1 permit 192.168.0.0 0.0.255.255

ip nat inside source list 1 interface gi0/0 overload

interface gi0/1
ip nat inside
exit

interface gi0/0
ip nat outside
exit
```

<img width="1917" height="1021" alt="Screenshot 2026-06-30 142800" src="https://github.com/user-attachments/assets/242741f6-d12d-4e51-b035-4dc44788815c" />


<img width="1917" height="1015" alt="Screenshot 2026-06-30 143738" src="https://github.com/user-attachments/assets/931ab12f-936a-48d7-815f-dae18993cf62" />


Step 9 — Configure Named ACL

```
! Block IT department from accessing HR subnet
ip access-list extended BLOCK_IT_TO_HR
deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
permit ip any any
exit

interface gi0/1.20
ip access-group BLOCK_IT_TO_HR in
exit
```

<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/42b2d60c-a77f-4065-88c4-b97914b21a1e" />


<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/7fe83d02-0256-4233-8ca3-7eb72d4a047b" />



Step 11 — Configure Internet Router

```
interface gi0/0
ip address 203.0.113.2 255.255.255.252
no shutdown
exit

interface loopback 0
ip address 8.8.8.8 255.255.255.255
exit

ip route 192.168.0.0 255.255.0.0 203.0.113.1
```

<img width="1917" height="1018" alt="Screenshot 2026-06-30 210504" src="https://github.com/user-attachments/assets/e21e3fcb-b678-46f1-a67d-edfdb48d1536" />


<img width="1917" height="1018" alt="Screenshot 2026-06-30 210635" src="https://github.com/user-attachments/assets/1119e839-effd-4994-a97f-58f05b4a2e68" />



✅ Test Plan and Results

| Test | Command | Expected Result |
|---|---|---|
| PC1 gets IP automatically | ipconfig | 192.168.10.x via DHCP ✅ |
| PC2 gets IP automatically | ipconfig | 192.168.20.x via DHCP ✅ |
| Same VLAN connectivity | ping PC3 from PC1 | ✅ Success |
| Inter-VLAN routing | ping PC2 from PC1 | ✅ Via router |
| ACL blocking | ping PC1 from PC2 | ❌ Blocked by ACL |
| Internet simulation | ping 8.8.8.8 from PC1 | ✅ Via NAT |
| NAT verification | show ip nat translations | ✅ Entries appear |
| EtherChannel | show etherchannel summary | ✅ SU — active |
| STP root bridge | show spanning-tree | ✅ SW1 is root |
| SSH access | ssh -l admin 192.168.10.1 | ✅ Secure login |

> 📸 *(Screenshot — Full ping test results)*
> 📸 *(Screenshot — show ip nat translations)*
> 📸 *(Screenshot — show etherchannel summary)*
> 📸 *(Screenshot — show spanning-tree)*


🔧 Troubleshooting I Did

- PCs not getting DHCP IP → Fixed by adding VLAN 99 on SW2 and SW3 so DHCP traffic could pass through
- EtherChannel not forming → Fixed by ensuring both sides configured — desirable on SW1, auto on SW2/SW3
- NAT not working → Fixed by correct ip nat inside on Gi0/1 and ip nat outside on Gi0/0
- SSH not connecting → Fixed by generating RSA keys and setting transport input ssh on VTY lines

---

## 💬 What I Would Say in an Interview

> "Project 5 is my capstone project where I combined all CCNA concepts into one complete enterprise network. I used EtherChannel with PAgP between core and access switches for bandwidth aggregation and redundancy. STP was configured with SW1 as root bridge to prevent loops. A centralized DHCP server on VLAN 99 served multiple VLANs through relay agents configured with ip helper-address on router subinterfaces. NAT/PAT with a default route simulated internet access. A Named ACL restricted IT department from accessing HR subnet. SSH was enabled on all devices replacing insecure Telnet. This project demonstrates I can design and configure a complete enterprise network from scratch."

---

## 📁 Files in This Repository

```
Project5-FullEnterpriseNetwork/
├── README.md                          ← This file
├── topology-screenshot.png            ← Full topology image
├── vlan-config.png                    ← show vlan brief output
├── etherchannel-summary.png           ← show etherchannel summary
├── spanning-tree.png                  ← show spanning-tree output
├── dhcp-server-config.png             ← DHCP server pool settings
├── router-ip-interface.png            ← show ip interface brief
├── nat-translations.png               ← show ip nat translations
├── acl-output.png                     ← show ip access-lists
├── ssh-test.png                       ← SSH connectivity test
├── ping-test-results.png              ← Full ping test results
├── sw1-config.txt                     ← SW1 full configuration
├── sw2-config.txt                     ← SW2 full configuration
├── sw3-config.txt                     ← SW3 full configuration
└── router-r1-config.txt               ← Router R1 full configuration
```

---

## 🚀 Part of My CCNA Lab Portfolio

| Project | Topic | Status |
|---|---|---|
| Project 1 | Small Office Network — VLANs + Inter-VLAN Routing | ✅ Done |
| Project 2 | DHCP Server + Relay Agent + Client Setup | ✅ Done |
| Project 3 | Multi-Site Network with OSPF | ✅ Done |
| Project 4 | Network Security — ACLs + DHCP Snooping + Port Security | ✅ Done |
| Project 5 | Full Enterprise Network — Capstone | ✅ Done |

---

*Built as part of my CCNA certification journey — actively learning and building hands-on lab projects.*
