 🔒 Security Lab — DHCP Snooping

Objective: Configured DHCP Snooping on a Cisco switch to prevent rogue DHCP server attacks by marking the legitimate DHCP server port as trusted in Cisco Packet Tracer.

🗺️ Topology


<img width="1917" height="1016" alt="Screenshot 2026-06-28 170626" src="https://github.com/user-attachments/assets/d85112b3-7c01-45d6-b34f-e9c3dfe643bb" />


🧩 What I Did

- ✅ Enabled DHCP Snooping globally on SW1
- ✅ Enabled DHCP Snooping for VLAN 1
- ✅ Marked Fa0/2 (legitimate DHCP server port) as trusted
- ✅ All other ports remain untrusted by default
- ✅ Verified configuration using show ip dhcp snooping


📦 IP Address Plan

| Device | Interface | IP Address | Role |
|---|---|---|---|
| Victim PC | Fa0 | 192.168.1.2 | Legitimate client |
| DHCP Server | Gig0/0 | 192.168.1.1 | Legitimate DHCP server |
| Attacker PC | Fa0 | 192.168.1.3 | Rogue DHCP server |


⚙️ Configuration

Step 1 — Enable DHCP Snooping on SW1


<img width="1917" height="990" alt="image" src="https://github.com/user-attachments/assets/0111238e-928a-470d-937d-59dca73d1c2d" />



Step 2 — Mark Fa0/2 as Trusted Port


<img width="1917" height="990" alt="image" src="https://github.com/user-attachments/assets/998072f8-b3ee-4300-88a4-de92a6985c8c" />


Step 3 — Verify Using show ip dhcp snooping


<img width="1917" height="990" alt="image" src="https://github.com/user-attachments/assets/5628f815-35a4-4487-af9c-ea5660ee4f39" />




on journey — actively learning and building hands-on lab projects.*
