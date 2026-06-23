🌍 Project 2 — Multi-Site Company Network with OSPF

Objective: Simulated a two-branch company network (Chennai and Dubai) connected via a WAN link using OSPF dynamic routing protocol in Cisco Packet Tracer.

🗺️ Topology


<img width="1918" height="985" alt="Screenshot 2026-06-17 204239" src="https://github.com/user-attachments/assets/4f345177-4620-4a33-803c-020c443cfd7b" />


🧩 What I Built

- ✅ Designed two branch office networks — Chennai and Dubai
- ✅ Separated departments using VLANs at each site
- ✅ Configured trunk ports between switches and routers
- ✅ Connected both routers via WAN link (Gig0/0 on both routers)
- ✅ Implemented OSPF dynamic routing between both routers
- ✅ Verified full connectivity across both sites using ping

📦 IP Address Plan

Chennai Office — Router1

| Device | Interface | IP Address | Subnet Mask | Gateway | VLAN |
|---|---|---|---|---|---|
| PC1 (HR) | NIC | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 | VLAN 10 |
| PC2 (IT) | NIC | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 | VLAN 20 |
| Router1 | Gi0/1.10 | 192.168.10.1 | 255.255.255.0 | — | VLAN 10 |
| Router1 | Gi0/1.20 | 192.168.20.1 | 255.255.255.0 | — | VLAN 20 |
| Router1 | Gi0/0 | 10.0.0.1 | 255.255.255.252 | — | WAN |

Dubai Office — Router2

| Device | Interface | IP Address | Subnet Mask | Gateway | VLAN |
|---|---|---|---|---|---|
| PC3 (HR) | NIC | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 | VLAN 30 |
| PC4 (IT) | NIC | 192.168.40.2 | 255.255.255.0 | 192.168.40.1 | VLAN 40 |
| Router2 | Gi0/1.30 | 192.168.30.1 | 255.255.255.0 | — | VLAN 30 |
| Router2 | Gi0/1.40 | 192.168.40.1 | 255.255.255.0 | — | VLAN 40 |
| Router2 | Gi0/0 | 10.0.0.2 | 255.255.255.252 | — | WAN |

WAN Link

| Device | Interface | IP Address |
|---|---|---|
| Router1 | Gi0/0 | 10.0.0.1 /30 |
| Router2 | Gi0/0 | 10.0.0.2 /30 |

⚙️ Configuration Steps

Step 1 — Build Topology
- Placed 2 Routers, 2 Switches (SW1, SW2), 4 PCs in Packet Tracer
- Connected PC1 → SW1 Fa0/2, PC2 → SW1 Fa0/3
- Connected PC3 → SW2 Fa0/2, PC4 → SW2 Fa0/3
- Connected SW1 Fa0/1 → Router1 Gi0/1 (trunk)
- Connected SW2 Fa0/1 → Router2 Gi0/1 (trunk)
- Connected Router1 Gi0/0 → Router2 Gi0/0 (WAN link)

Step 2 — Configure VLANs on SW1 (Chennai)
- Created VLAN 10 (HR) and VLAN 20 (IT)
- Assigned Fa0/2 to VLAN 10 (PC1)
- Assigned Fa0/3 to VLAN 20 (PC2)
- Configured Fa0/1 as trunk port facing Router1
- Verified using `show vlan brief`
  

<img width="1918" height="1013" alt="Screenshot 2026-06-16 213413" src="https://github.com/user-attachments/assets/cb354cbe-7bf5-4307-a06f-06758e11d13c" />


<img width="1918" height="1013" alt="Screenshot 2026-06-23 122802" src="https://github.com/user-attachments/assets/f0222d8b-1f2f-41e6-a013-c5058f39965d" />


Step 3 — Configure VLANs on SW2 (Dubai)
- Created VLAN 30 (HR) and VLAN 40 (IT)
- Assigned Fa0/2 to VLAN 30 (PC3)
- Assigned Fa0/3 to VLAN 40 (PC4)
- Configured Fa0/1 as trunk port facing Router2
- Verified using `show vlan brief`
  

<img width="1918" height="1017" alt="Screenshot 2026-06-16 213712" src="https://github.com/user-attachments/assets/91c0d51b-0c9f-4d3c-9b7a-135c772088af" />


<img width="1918" height="1017" alt="Screenshot 2026-06-23 122957" src="https://github.com/user-attachments/assets/2db3fb13-4448-4715-8c41-37dfbe958db1" />


Step 4 — Configure Router1 (Chennai)
- Configured Gi0/0 as WAN interface — IP 10.0.0.1/30
- Enabled Gi0/1 physical interface for LAN
- Created subinterface Gi0/1.10 for VLAN 10 — IP 192.168.10.1
- Created subinterface Gi0/1.20 for VLAN 20 — IP 192.168.20.1
- Verified using `show ip interface brief`


<img width="1918" height="1018" alt="Screenshot 2026-06-17 105130" src="https://github.com/user-attachments/assets/1822e0c4-f8e9-4bf2-baa6-fb4f0e8efbec" />


Step 5 — Configure Router2 (Dubai)
- Configured Gi0/0 as WAN interface — IP 10.0.0.2/30
- Enabled Gi0/1 physical interface for LAN
- Created subinterface Gi0/1.30 for VLAN 30 — IP 192.168.30.1
- Created subinterface Gi0/1.40 for VLAN 40 — IP 192.168.40.1
- Verified using `show ip interface brief`


<img width="1918" height="1023" alt="Screenshot 2026-06-17 105638" src="https://github.com/user-attachments/assets/8c2f2f6d-feb9-4f82-844c-850e295cc631" />


<img width="1918" height="1012" alt="Screenshot 2026-06-23 123356" src="https://github.com/user-attachments/assets/fdeab47a-f86f-4bdc-90b9-2cdf64b2cdfa" />


Step 6 — Configure OSPF on Both Routers
- Started OSPF process 1 on both routers
- Advertised all local networks using wildcard masks
- Included WAN link network 10.0.0.0/30 in OSPF
- All networks placed in Area 0


<img width="1918" height="1018" alt="Screenshot 2026-06-17 105130" src="https://github.com/user-attachments/assets/d485222a-7c45-4fa2-8adf-661f8dba9f8f" />


<img width="1918" height="1017" alt="Screenshot 2026-06-17 105856" src="https://github.com/user-attachments/assets/185a0ce9-f58f-47aa-ad5e-941d7efb3ff7" />


Step 7 — Verify Routing Table
- Confirmed OSPF learned routes marked with "O" on both routers
- Router1 learned Dubai networks 192.168.30.0 and 192.168.40.0
- Router2 learned Chennai networks 192.168.10.0 and 192.168.20.0

<img width="1918" height="1017" alt="Screenshot 2026-06-23 123637" src="https://github.com/user-attachments/assets/c616622b-c049-443c-819a-10d5ea10fc0b" />


<img width="1918" height="1017" alt="Screenshot 2026-06-23 123708" src="https://github.com/user-attachments/assets/b5d29946-2fa9-4bf7-ba9c-9d8d2673e752" />



---

