🔒 Security Lab — Port Security

Objective: Configured Port Security on a Cisco switch to prevent unauthorized devices from connecting to the network — restricting port access based on MAC address in Cisco Packet Tracer.

🗺️ Topology


<img width="1916" height="1021" alt="Screenshot 2026-06-28 182109" src="https://github.com/user-attachments/assets/edbac656-bebf-4cb6-8f93-ae3bc64eb016" />


🧩 What I Did

- ✅ Connected authorized PC to SW1 Fa0/2
- ✅ Configured port security on Fa0/2
- ✅ Set maximum MAC addresses to 1
- ✅ Set violation mode to shutdown
- ✅ Used sticky MAC to automatically learn authorized PC's MAC
- ✅ Verified using show port-security commands

📚 Key Concepts — Port Security

### What is Port Security?
Port Security is a **Layer 2 switch feature** that restricts which devices can connect to a specific switch port based on their **MAC address**. It prevents unauthorized devices from accessing the network through the switch.

Port Security Maximum
```
switchport port-security maximum 1
```
- Defines how many MAC addresses are allowed on the port
- Default is **1**
- If a second MAC address is detected → violation is triggered
- Can be increased to allow multiple devices (e.g. IP phones + PC)

Violation Modes
There are 3 violation modes when an unauthorized MAC is detected:

| Mode | What Happens | Port Status | Sends Alert |
|---|---|---|---|
| **Shutdown** | Port immediately disabled | err-disabled ❌ | Yes — sends SNMP trap |
| **Restrict** | Drops unauthorized frames | Still up ✅ | Yes — increments counter |
| **Protect** | Drops unauthorized frames | Still up ✅ | No alert sent |

> **Shutdown** is the most secure and most commonly used in real networks

Sticky MAC Address
```
switchport port-security mac-address sticky
```
- Switch **automatically learns** the first MAC address that connects
- Saves it into running config as a secure MAC
- No need to manually type the MAC address
- If different MAC connects later → violation triggered

⚙️ Configuration

Step 1 — Configure Port Security on Fa0/2

```
enable
configure terminal

interface fa0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security violation shutdown
switchport port-security mac-address sticky
exit

write memory
```

<img width="1917" height="1018" alt="Screenshot 2026-06-28 180827" src="https://github.com/user-attachments/assets/be5a454c-b7e2-40d0-a6a5-32dd9cb077eb" />


Step 2 — Verify Port Security

```
show port-security
```

<img width="1917" height="1016" alt="Screenshot 2026-06-28 181827" src="https://github.com/user-attachments/assets/24cdf63a-a18d-49c6-a111-b79a5e1b87ad" />


Step 3 — Verify Port Security on Specific Interface

```
show port-security interface fa0/1
```

Expected output:
```
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Security Violation Count   : 0
```


<img width="1917" height="1018" alt="Screenshot 2026-06-28 202008" src="https://github.com/user-attachments/assets/dddf4a7b-b66b-4755-bf60-b03e40e650eb" />


🚦 How Port Security Works

```
Authorized PC connects to Fa0/1
            ↓
Switch learns MAC automatically (sticky)
            ↓
MAC saved into running config
            ↓
Port status → Secure-up ✅

If unauthorized device tries to connect:
Different MAC detected on Fa0/1
            ↓
Violation mode = shutdown
            ↓
Port Fa0/1 → err-disabled ❌
```

---

