🔒 Project 4.3 — Extended Named ACL (BLOCK_PC1_SERVICES)

Objective: Configured an Extended Named ACL called BLOCK_PC1_SERVICES on a router to block Telnet and HTTP access from a specific PC while allowing all other traffic — also demonstrated adding ACL rules using sequence numbers in Cisco Packet Tracer.

🗺️ Topology


<img width="1917" height="987" alt="Screenshot 2026-06-26 193809" src="https://github.com/user-attachments/assets/259ccf66-b996-4b54-877c-25afb43343b4" />


🧩 Objectives

- ✅ Ping server from both PC1 and PC2 — verify connectivity
- ✅ Create Extended Named ACL — BLOCK_PC1_SERVICES on R1
- ✅ Block PC1 from reaching server using Telnet (port 23)
- ✅ Permit all other traffic to server
- ✅ Apply ACL inbound on R1 Gi0/1
- ✅ Verify ACL using show ip access-lists
- ✅ Add sequence number 15 to block PC1 HTTP (port 80)
- ✅ Verify updated ACL with sequence number added
- ✅ Test Telnet to server using HTTPS, HTTP and Telnet ports from PC1
- ✅ Test Telnet to server using HTTPS, HTTP and Telnet ports from PC2


📦 IP Address Plan

| Device | Interface | IP Address | Subnet Mask | Gateway |
|---|---|---|---|---|
| PC1 | NIC | 10.1.1.2 | 255.255.255.0 | 10.1.1.1 |
| PC2 | NIC | 10.1.1.3 | 255.255.255.0 | 10.1.1.1 |
| Router R1 | Gi0/0 | 10.1.1.1 | 255.255.255.0 | — |
| Router R1 | Gi0/1 | 192.0.2.2 | 255.255.255.0 | — |
| Server | Fa0/0 | 192.0.2.1 | 255.255.255.0 | 192.0.2.2 |
| Server | Loopback | 203.0.113.1 | 255.255.255.255 | — |

⚙️ Configuration Steps

Step 1 — Build Topology
- Placed 2 PCs, 1 Switch (SW1), 1 Router (R1), 1 Server
- Connected PC1 → SW1 Fa0/1, PC2 → SW1 Fa0/2
- Connected SW1 Fa0/3 → R1 Gi0/0
- Connected R1 Gi0/1 → Server Fa0/0
- Assigned all IPs as per IP plan above

Step 2 — Phase A: Ping Server from Both PCs
- Verified basic connectivity before applying ACL
- PC1 ping 192.0.2.1 → ✅ Success
- PC2 ping 192.0.2.1 → ✅ Success

Step 3 — Create Extended Named ACL on R1
- Created named ACL called BLOCK_PC1_SERVICES
- Added deny rule for PC1 Telnet (port 23)
- Added permit rule for all other traffic


<img width="1917" height="1017" alt="Screenshot 2026-06-27 100646" src="https://github.com/user-attachments/assets/178b7a80-9f54-4a12-ac62-0833c7449a57" />


Step 4 — Apply ACL on R1 Gi0/1 Inbound


<img width="1917" height="1017" alt="Screenshot 2026-06-27 100646" src="https://github.com/user-attachments/assets/0a09ec56-8a54-4ee4-b5dc-006af2fb1d7f" />


Step 5 — Verify ACL After First Rule


<img width="1917" height="1017" alt="Screenshot 2026-06-27 100646" src="https://github.com/user-attachments/assets/86c11498-e92e-4506-84eb-40d3c2ebf2d9" />


Step 6 — Add Sequence Number 15 to Block HTTP
- Added new rule at sequence 15 to block PC1 HTTP (port 80)
- Sequence 15 inserts between rule 10 and rule 20 automatically


<img width="1917" height="1017" alt="Screenshot 2026-06-27 100646" src="https://github.com/user-attachments/assets/09da49dc-acc7-4208-9625-d4e5288ef4c5" />


Step 7 — Verify ACL After Sequence 15 Added


<img width="1917" height="1017" alt="Screenshot 2026-06-27 100646" src="https://github.com/user-attachments/assets/da213154-1cb0-43b4-8982-461303839011" />


Step 8 — Phase B: Test from PC1

Test using telnet command with specific port numbers:


<img width="1917" height="1020" alt="Screenshot 2026-06-27 101135" src="https://github.com/user-attachments/assets/eb2fdf5d-2daa-4d34-989c-82c01594ad42" />


Step 9 — Phase B: Test from PC2


<img width="1917" height="1018" alt="Screenshot 2026-06-27 101155" src="https://github.com/user-attachments/assets/f26d3fdd-6b37-4c5f-b1c8-8cce3e0b6efe" />


🚦 How Named ACL Works — Traffic Flow

```
PC1 tries Telnet (port 23) to Server:
PC1 ——TCP 23——→ R1 Gi0/1 inbound
ACL checks: source=10.1.1.2, TCP, port=23
Hits sequence 10 → DENY ❌ dropped

PC1 tries HTTP (port 80) to Server:
PC1 ——TCP 80——→ R1 Gi0/1 inbound
ACL checks: source=10.1.1.2, TCP, port=80
Hits sequence 15 → DENY ❌ dropped

PC1 tries HTTPS (port 443) to Server:
PC1 ——TCP 443——→ R1 Gi0/1 inbound
ACL checks: no deny match found
Hits sequence 20 → PERMIT ✅ allowed

PC2 tries anything to Server:
PC2 ——any traffic——→ R1 Gi0/1 inbound
ACL checks: source=10.1.1.3 — no deny match
Hits sequence 20 → PERMIT ✅ always allowed
```

---

