🔒 Project 4.2 — Extended Numbered ACL (Block Telnet for Specific Host)

Objective: Configured an Extended Numbered ACL to block Telnet access from a specific PC while allowing all other traffic including ping — demonstrating granular traffic filtering in Cisco Packet Tracer.

🗺️ Topology

<img width="1917" height="987" alt="Screenshot 2026-06-26 193809" src="https://github.com/user-attachments/assets/0bf3326b-bf46-49c4-b9db-1f0b2e8ec8d1" />


🧩 What I Built

- ✅ Built network with 2 PCs, 1 Switch, 1 Router and 1 Server
- ✅ Verified ping and telnet work from both PCs — Phase A
- ✅ Configured Extended Numbered ACL 100 to block telnet from PC1 only
- ✅ Applied ACL on Router Gi0/0 inbound direction
- ✅ Verified PC1 telnet blocked, PC2 telnet still works — Phase B
- ✅ Verified PC1 ping to server still works after ACL applied


📦 IP Address Plan

| Device | Interface | IP Address | Subnet Mask | Gateway |
|---|---|---|---|---|
| PC1 | NIC | 10.1.1.2 | 255.255.255.0 | 10.1.1.1 |
| PC2 | NIC | 10.1.1.3 | 255.255.255.0 | 10.1.1.1 |
| Router R1 | Gi0/0 | 10.1.1.1 | 255.255.255.0 | — |
| Router R1 | Gi0/1 | 192.0.2.2 | 255.255.255.0 | — |
| Server | Fa0/0 | 192.0.2.1 | 255.255.255.0 | 192.0.2.2 |
| Server | Loopback | 203.0.113.1 | 255.255.255.255 | — |


🔑 ACL Plan

| ACL Number | Type | Action | Source IP | Protocol | Port | Applied On | Direction |
|---|---|---|---|---|---|---|---|
| 100 | Extended | Deny | 10.1.1.2 (PC1) | TCP | 23 (Telnet) | Gi0/0 | Inbound |
| 100 | Extended | Permit | Any | Any | Any | Gi0/0 | Inbound |



⚙️ Configuration Steps

Step 1 — Build Topology
- Placed 2 PCs, 1 Switch (SW1), 1 Router (R1), 1 Server
- Connected PC1 → SW1 Fa0/1, PC2 → SW1 Fa0/2
- Connected SW1 Fa0/3 → R1 Gi0/0
- Connected R1 Gi0/1 → Server Fa0/0
- Assigned all IP addresses as per IP plan above

Step 2 — Phase A: Test Before ACL

**Ping Test:**
- PC1 ping 192.0.2.1 (Server) → ✅ Success
- PC2 ping 192.0.2.1 (Server) → ✅ Success

**Telnet Test:**
- PC1 telnet 192.0.2.1 → ✅ Success
- PC2 telnet 192.0.2.1 → ✅ Success


<img width="1917" height="1018" alt="Screenshot 2026-06-26 185014" src="https://github.com/user-attachments/assets/5d8c1e50-c4a0-4210-8379-742ec9ed92f8" />


<img width="1917" height="1015" alt="Screenshot 2026-06-26 184950" src="https://github.com/user-attachments/assets/0497c154-dcab-4171-a65f-e82e2bfb7474" />


Step 3 — Configure Extended Numbered ACL 100
- Denied TCP telnet (port 23) traffic from PC1 only
- Permitted all other traffic


<img width="1917" height="1020" alt="Screenshot 2026-06-26 192948" src="https://github.com/user-attachments/assets/5cd9dccb-0911-411b-8edb-98c23bcdc40c" />


Step 4 — Apply ACL on Router R1 Interface
- Applied ACL 100 inbound on Gi0/0 (facing PCs)
- Extended ACLs placed closest to SOURCE


<img width="1917" height="1020" alt="Screenshot 2026-06-26 192948" src="https://github.com/user-attachments/assets/b136bbc5-42e5-4f6c-842f-aedae299dae4" />


Step 5 — Verify ACL Configuration


<img width="1917" height="1020" alt="Screenshot 2026-06-26 192948" src="https://github.com/user-attachments/assets/852aa64c-d00a-4428-bd33-80494f13c1b2" />


Step 6 — Phase B: Test After ACL

**Ping Test (should still work):**
- PC1 ping 192.0.2.1 → ✅ Still works (ping not blocked)
- PC2 ping 192.0.2.1 → ✅ Still works

**Telnet Test (PC1 blocked, PC2 allowed):**
- PC1 telnet 192.0.2.1 → ❌ Blocked by ACL
- PC2 telnet 192.0.2.1 → ✅ Still works


<img width="1917" height="1020" alt="Screenshot 2026-06-26 193606" src="https://github.com/user-attachments/assets/7559657f-4696-4314-82ac-73a62d3d565f" />


<img width="1917" height="1016" alt="Screenshot 2026-06-26 193705" src="https://github.com/user-attachments/assets/a694b852-245e-4b98-bdd6-1ae1ca31c0db" />


🚦 How Extended ACL Works — Traffic Flow

```
Phase A — Before ACL:
PC1 ——telnet——→ Router Gi0/0 ——→ Server ✅
PC2 ——telnet——→ Router Gi0/0 ——→ Server ✅
PC1 ——ping——→  Router Gi0/0 ——→ Server ✅

Phase B — After ACL 100 Applied on Gi0/0 inbound:

PC1 telnet attempt:
PC1 ——TCP port 23——→ Router Gi0/0
ACL checks: source=10.1.1.2, protocol=TCP, port=23
Matches rule 10 → DENY ❌ packet dropped

PC2 telnet attempt:
PC2 ——TCP port 23——→ Router Gi0/0
ACL checks: source=10.1.1.3, protocol=TCP, port=23
No deny match → hits rule 20 → PERMIT ✅

PC1 ping attempt:
PC1 ——ICMP——→ Router Gi0/0
ACL checks: source=10.1.1.2, protocol=ICMP
No TCP deny match → hits rule 20 → PERMIT ✅
```

---

