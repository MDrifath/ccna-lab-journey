<img width="1917" height="1012" alt="Screenshot 2026-04-26 115026" src="https://github.com/user-attachments/assets/369755f0-cb1d-4899-9715-86c232538a6b" />Lab: Trunking Configuration

🎯 Objective

The ping should work between devices in the same VLAN across switches. For example, a device in VLAN 10 on SW1 can successfully ping a device in VLAN 10 on SW2 through a trunk port.

🖥️ Topology

<img width="1905" height="955" alt="Trunk_topology" src="https://github.com/user-attachments/assets/82832b2b-3b2b-4bbe-9556-3e1351e478a9" />

Step-1: Will check from  one of the pc from sw1 where able to ping the pc on the sw2 as trunk port is configured yet we can't able to ping

<img width="1917" height="1014" alt="Screenshot 2026-04-25 232331" src="https://github.com/user-attachments/assets/3ddd6a95-cfe7-41fa-9a0d-0b81c067ae70" />

Step-2: We need to configure the trunk ports where interace of sw1 is connected to sw2

cmd:

int fa 0/1 - so this interface of the sw1 is connected 

switchport mode trunk - so now interface is no longer will be on mode access, now it can able to make traffic flow from on sw1 to sw2

show interface trunk - this cmd shows whether the trunk is configured properly

<img width="1917" height="1012" alt="Screenshot 2026-04-26 114925" src="https://github.com/user-attachments/assets/7d07c36a-9c79-4aad-b85b-91b3678d5909" />


<img width="1917" height="1012" alt="Screenshot 2026-04-26 115026" src="https://github.com/user-attachments/assets/c4ba4691-d562-4d7d-bb37-fa22eba186a4" />

Step-3: Verify now the whether we can able to ping - Now ping is successfull

<img width="1919" height="1022" alt="Screenshot 2026-04-26 115108" src="https://github.com/user-attachments/assets/10015caf-1c13-43e3-9c9b-e3de1234fbc7" />


Other than this we have we have other modes as well

DTP(Dynamic Trunking Protocol) - A cisco proprietary protocol that allows a switchport to dynamically negotiate the formation of trunk etween two switches

cmd: 

switchport mode dynamic desirable - Initiates the negotiation of a trunk

switchport mode dynamic auto - passively waits for the remote swithc to initiate the negotiation of a trunk

The trunk mode and dynamic desirable mode these two modes will initiate the sending of the DTP frames to the other side

If dynamic mode and auto port receives the DTP frames from the other side it knows that other side of this link wants to be trunk

And also one more thing we also decide of which vlans need to be in trunk - you can check in allowed vlans







