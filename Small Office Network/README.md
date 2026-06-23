# 🏢 Project 1 — Small Office Network

Objective: Simulated a small company network with two departments separated by VLANs and connected using Inter-VLAN routing (Router-on-a-Stick) in Cisco Packet Tracer.

🗺️ Topology

<img width="1918" height="992" alt="Screenshot 2026-06-23 104556" src="https://github.com/user-attachments/assets/0b1a403a-9669-4afb-892f-ceba63c388db" />


🧩 What I Built

- ✅ Designed a 2-department office network (HR and IT)
- ✅ Separated departments using VLANs for security
- ✅ Configured trunk ports between switches and router
- ✅ Implemented Inter-VLAN routing using Router-on-a-Stick
- ✅ Verified connectivity using ping across departments


📦 IP Address Plan

| Device | IP Address | Subnet Mask | Gateway | VLAN |
|---|---|---|---|---|
| PC1 | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 | VLAN 10 |
| PC2 | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 | VLAN 10 |
| PC3 | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 | VLAN 20 |
| PC4 | 192.168.20.3 | 255.255.255.0 | 192.168.20.1 | VLAN 20 |
| Router Gi0/0.10 | 192.168.10.1 | 255.255.255.0 | — | VLAN 10 |
| Router Gi0/0.20 | 192.168.20.1 | 255.255.255.0 | — | VLAN 20 |



⚙️ Configuration Steps

Step 1 — Build Topology
- Placed 1 Router, 2 Switches, 4 PCs in Packet Tracer
- Connected devices using straight-through copper cables

Step 2 — Configure VLANs on Switches
- Created VLAN 10 (HR) and VLAN 20 (IT) on both switches
- Assigned access ports to correct VLANs
- Configured trunk ports between switches and router
- 

<img width="1918" height="1017" alt="Screenshot 2026-06-14 215752" src="https://github.com/user-attachments/assets/9d4f5eb8-d6a9-4089-997f-5ed0a03a00bf" />


<img width="1918" height="1018" alt="Screenshot 2026-06-14 215950" src="https://github.com/user-attachments/assets/0590d202-abb5-4c13-99d7-5d6805a2eb57" />


Step 3 — Configure Trunk Ports
- Set Fa0/24 as trunk on both switches facing the router
- Set Fa0/23 as trunk on Switch1 facing Switch2
- Verified using `show interfaces trunk`


<img width="1918" height="1020" alt="Screenshot 2026-06-23 105329" src="https://github.com/user-attachments/assets/5414eed3-7460-4b49-9cbf-70a0f3995697" />


<img width="1918" height="1021" alt="Screenshot 2026-06-23 105426" src="https://github.com/user-attachments/assets/8bba3d2d-781c-4eda-b411-6910a7d37b06" />



Step 4 — Configure Router (Router-on-a-Stick)
- Enabled Gi0/0 physical interface
- Created subinterface Gi0/0.10 for VLAN 10 with IP 192.168.10.1
- Created subinterface Gi0/0.20 for VLAN 20 with IP 192.168.20.1
- Used `encapsulation dot1q` on each subinterface


<img width="1918" height="1018" alt="Screenshot 2026-06-14 220209" src="https://github.com/user-attachments/assets/e8c920e6-abb1-4f2f-ada8-dae058cde95f" />


Step 5 — Test Connectivity

- Pinged PC1 from PC4 (different VLAN via router) ✅
  

<img width="1918" height="1016" alt="Screenshot 2026-06-14 221442" src="https://github.com/user-attachments/assets/1a6eb5b6-e071-4d57-b863-a12aa8f8c433" />






