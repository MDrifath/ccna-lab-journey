Lab: VLAN Configuration 

🎯 Objective

To configure VLANs.

🖥️ Topology


<img width="1904" height="980" alt="image" src="https://github.com/user-attachments/assets/f817e83b-d7e2-48be-a3f8-eca0d155321e" />


Step-1: First need to check the VLAN information

cmd:

show vlan brief


<img width="1586" height="460" alt="VLAN-info" src="https://github.com/user-attachments/assets/814ad536-20eb-4210-ade5-991b4acf32c4" />


Step-2: Create the VLANs and assign the names to the VLANs

VLAN 10 and VLAN 20 are created

cmds:

vlan 10 - To create the VLAN

name Engineering - we can assign the name to the VLAN

vlan 20

name HR

<img width="1411" height="692" alt="VLAN creation" src="https://github.com/user-attachments/assets/83f3f4c6-2cf6-44e0-bd29-02b0cab27199" />


Step-3: We need to assign some of the interfaces for the respective vlans

cmds:

int gig 0/0 - for single interface

int range fa 0/1-2 - we can list of interfaces at a single time

switchport access vlan 10 - This is basically we are telling that this can access only one VLAN meaning we can able to send traffic to another VLAN (LAN)

int range gig 0/3-4 - we can list of interfaces at a single time

switchport access vlan 20


<img width="1364" height="805" alt="VLAN interface assignment" src="https://github.com/user-attachments/assets/598b5a3e-e39e-4394-98f7-ee10c1d8c346" />


Step-3: We can also delete a VLAN

cmd:

no vlan 10 - we are just deleting a VLAN 10


<img width="1136" height="525" alt="VLAN deletion" src="https://github.com/user-attachments/assets/4f9e5e16-4ba2-4d81-a255-183cda311a70" />







