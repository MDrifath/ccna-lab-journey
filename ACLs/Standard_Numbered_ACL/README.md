Project 4.1 — Standard Numbered ACL (Access Control List)


Objective: Configured a Standard Numbered ACL to control network traffic — first verified ping works between all devices, then applied ACL to block specific traffic, demonstrating basic network security in Cisco Packet Tracer.


🗺️ Topology


<img width="1917" height="1018" alt="Screenshot 2026-06-26 171429" src="https://github.com/user-attachments/assets/127017a7-f583-459d-b4e7-b428e427123d" />



🧩 What I Built

- ✅ Built a network with two PCs and a router
- ✅ Verified full connectivity — ping works from both PCs (Phase A)
- ✅ Configured Standard Numbered ACL to block specific traffic
- ✅ Applied ACL on router interface in correct direction
- ✅ Verified ping is blocked after ACL applied (Phase B)
- ✅ Confirmed permitted traffic still works normally


📦 IP Address Plan

| Device | Interface | IP Address | Subnet Mask | Gateway |
|---|---|---|---|---
| PC1 | NIC |10.1.1.2 |255.255.255.0| 10.1.1.1|
| PC2 | NIC |10.1.1.3|255.255.255.0|10.1.1.1|
| Router | Gi0/0 |10.1.1.1|255.255.255.0| — |
| Router | Gi0/1 |192.0.2.2|255.255.255.0| — |


⚙️ Configuration Steps

Step 1 — Build Topology
- Placed Router, 2 PCs and connected all devices
- Assigned IP addresses to all devices and interfaces

Step 2 — Phase A: Test Ping Before ACL
- Pinged from PC1 to PC2 — Success ✅
- Pinged from PC2 to PC1 — Success ✅
- This confirms basic connectivity works before any ACL is applied


<img width="1917" height="1017" alt="Screenshot 2026-06-26 171023" src="https://github.com/user-attachments/assets/67d4871d-b746-46d1-99c0-414996ca2efc" />


<img width="1917" height="1016" alt="Screenshot 2026-06-26 171047" src="https://github.com/user-attachments/assets/95efc67d-361f-4e59-8f0e-a506c53f0e69" />


Step 3 — Configure Standard Numbered ACL


<img width="1917" height="1015" alt="Screenshot 2026-06-26 171142" src="https://github.com/user-attachments/assets/98605024-5b30-466a-a36b-407890289438" />


Step 4 — Apply ACL to Router Interface


<img width="1917" height="1015" alt="Screenshot 2026-06-26 171142" src="https://github.com/user-attachments/assets/487b743c-92d8-43dc-bf46-e963aba7fdfd" />



Step 5 — Verify ACL Configuration


<img width="1917" height="1015" alt="Screenshot 2026-06-26 171142" src="https://github.com/user-attachments/assets/c97798df-c230-420a-b789-5a864c1fe39f" />


Step 6 — Phase B: Test Ping After ACL
- Pinged from PC1 to PC2 — Blocked ❌
- Pinged from PC2 to PC1 — Still works ✅
- This confirms ACL is working correctly


<img width="1917" height="1017" alt="Screenshot 2026-06-26 171302" src="https://github.com/user-attachments/assets/f828c458-3cbc-4a49-a4c2-8b63791e532d" />


<img width="1917" height="1025" alt="Screenshot 2026-06-26 171247" src="https://github.com/user-attachments/assets/0152a663-ef25-481e-99c5-2ced78a53b58" />


How ACL Works — Traffic Flow

```
Phase A — Before ACL:
PC1 ——ping——→ Router ——→ PC2 ✅
PC2 ——ping——→ Router ——→ PC1 ✅

Phase B — After ACL Applied:
PC1 ——ping——→ Router → ACL checks source IP
                      → Matches DENY rule
                      → Packet dropped ❌

PC2 ——ping——→ Router → ACL checks source IP
                      → Matches PERMIT any
                      → Packet allowed ✅
```



ney — actively learning and building hands-on lab projects.*
