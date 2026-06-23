🖥️ Project 3 — DHCP Server, Relay Agent & Client (3 Router Setup)

Objective: Simulated a real-world DHCP scenario using 3 routers in Cisco Packet Tracer — one acting as DHCP Server, one as DHCP Relay Agent, and one as DHCP Client receiving IP automatically.

🗺️ Topology


<img width="1915" height="988" alt="Screenshot 2026-06-23 131220" src="https://github.com/user-attachments/assets/288c1ef8-aa71-473b-8430-96c4c9a774ec" />


🧩 What I Built

- ✅ Configured R3 as DHCP Server with a pool for client subnet
- ✅ Configured R2 as DHCP Relay Agent using ip helper-address
- ✅ Configured R1 as DHCP Client — receives IP automatically
- ✅ Verified DHCP binding on server using show ip dhcp binding
- ✅ Tested full connectivity across all 3 routers

📦 IP Address Plan

| Device | Interface | IP Address | Subnet Mask | Role |
|---|---|---|---|---|
| R1 | Gi0/0 | Auto (192.168.1.10) | 255.255.255.0 | DHCP Client |
| R2 | Gi0/0 | 192.168.1.1 | 255.255.255.0 | Relay — facing R1 |
| R2 | Gi0/1 | 192.168.2.1 | 255.255.255.0 | Relay — facing R3 |
| R3 | Gi0/0 | 192.168.2.5 | 255.255.255.0 | DHCP Server |


⚙️ Configuration Steps

Step 1 — Build Topology
- Placed 3 Routers (R1, R2, R3) in a line in Packet Tracer
- Connected R1 Gi0/0 → R2 Gi0/0 (client subnet)
- Connected R2 Gi0/1 → R3 Gi0/0 (server subnet)
- Used straight-through copper cables


Step 2 — Configure R3 as DHCP Server
- Assigned static IP 192.168.2.5 on Gi0/0
- Created DHCP pool named CLIENT_POOL
- Set network, default gateway and DNS server in pool
- Excluded R2's IP from being assigned to clients


<img width="1919" height="1017" alt="Screenshot 2026-06-11 231156" src="https://github.com/user-attachments/assets/dcb8374d-3419-40db-bbfc-a0073f0feb96" />


 Step 3 — Configure R2 as DHCP Relay Agent
- Assigned IPs on both interfaces Gi0/0 and Gi0/1
- Added ip helper-address on Gi0/0 (facing R1)
- This forwards DHCP broadcasts from R1 to R3 server


<img width="1919" height="1021" alt="Screenshot 2026-06-11 231732" src="https://github.com/user-attachments/assets/b9676ac8-41f4-421d-9839-5156d44a1d8e" />


Step 4 — Configure R1 as DHCP Client
- Set Gi0/0 to receive IP automatically using ip address dhcp
- R1 sends DHCPDISCOVER broadcast
- R2 relays it to R3 which assigns IP from pool


<img width="1919" height="1019" alt="Screenshot 2026-06-11 231520" src="https://github.com/user-attachments/assets/c55bc3a6-a2f2-4140-934b-c28c2b4cc387" />



Step 5 — Verify DHCP Assignment on R1
- Checked if R1 received IP automatically from server


<img width="1900" height="959" alt="Screenshot 2026-06-12 090840" src="https://github.com/user-attachments/assets/f3d82020-5c39-48a0-be97-7d31b83c3c6b" />


#Step 6 — Verify DHCP Binding on R3
- Confirmed R3 recorded the IP assignment for R1


<img width="1918" height="1020" alt="Screenshot 2026-06-23 152121" src="https://github.com/user-attachments/assets/45702313-8bbb-4d1a-9c6e-5e0f54ca3e0d" />


