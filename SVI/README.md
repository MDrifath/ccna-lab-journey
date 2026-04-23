📘 Lab: SVI (Switch Virtual Interface) - Inter vlan routing

🎯 Objective

To configure SVI and enable communication between VLANs.

🖥️ Topology

<img width="1916" height="968" alt="Topology-SVI" src="https://github.com/user-attachments/assets/c0c86526-9e79-4184-9b3d-fcf620bba082" />


The moto of this lab is

vlan 10 -> ping from pc1 - vlan 20 -> pc2

During start of the lab the ping fails because we haven't created inter-vlan routing


<img width="1919" height="1017" alt="Screenshot 2026-04-19 213129" src="https://github.com/user-attachments/assets/38e52711-2346-42da-9854-983653005b0a" />


Step-1: we need to create a VLANs 

It was already created in last lab, you can view the lab by following link

https://github.com/MDrifath/ccna-lab-journey/tree/main/VLANs

Step-2: To make use of inter-vlan routing fisrt we need to create SVIs usually wokring in Multilayer switch or Layer 3 switch

cmds:

int vlan 10 -  we are creating a virtual interface for vlan 10

ip address 192.168.1.1 255.255.255.0 - we need sepecify ip address for that interface by defualt gateway and subnet mask

no shutdown - this cmd bassically make the interface up

int valn 20

ip address 192.168.1.1 255.255.255.0

no shutdown

<img width="1126" height="616" alt="SVI - creation" src="https://github.com/user-attachments/assets/a91a6598-c595-4ce8-bb54-2548e2b8429e" />

Step-3: To check whether the created Interface up or not

cmd:

show ip interface brief - using we can check whether the interface is up or not


<img width="1076" height="704" alt="Interface - UP" src="https://github.com/user-attachments/assets/a97cba0f-e789-40e5-99e2-b1cf1e7aa3de" />

At last after configuring the SVI - inter vlan routing works automatically


<img width="1142" height="650" alt="Screenshot 2026-04-20 114113" src="https://github.com/user-attachments/assets/73a5b993-e887-45e5-95e9-0f7e6756cc23" />





