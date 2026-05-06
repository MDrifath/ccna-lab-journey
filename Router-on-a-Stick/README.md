Lab: Router-on-a-Stick(ROAS) / Router-on-a-Trunk Configuration

🎯 Objective

To configure and verify inter-VLAN routing using the Router-on-a-Stick method, where a single switch connects multiple VLANs (VLAN 10 and VLAN 20) to a router, enabling communication between devices in different VLANs through a trunk link.

🖥️ Topology

<img width="1919" height="970" alt="R-O-A-S_topology" src="https://github.com/user-attachments/assets/4b258ee5-3821-4e44-a441-a0bcef6b21a1" />

Step-1: In the router we need to configure subinterfaces in order to carry vlan traffic from the switch

<img width="1919" height="1016" alt="Screenshot 2026-05-06 133421" src="https://github.com/user-attachments/assets/647edff5-15cd-4488-90f4-d6f9dc1479da" />

cmd:

First we need to switch to global config mode

int gig 0/0 - First we need to choose the interface which is connected to switch

no shudown - will up the interface

int gig 0/0.10 - now I am configuring the subinterface for the vlan 10

int gig 0/0.20 - similar to above

encapsulation dot1q 10 - we are mentioning that we need to use dot1q standard tagging for the trunk and we are mentioning our vlan 10

ip address - now we need to specify the ip address and subnet mask of the network

we need to configure for the both the subinterfaces then we carry multiple vlans through trunk link

Step-2: Now we need to configure the switch for the trunk link

<img width="1919" height="1010" alt="Screenshot 2026-05-06 133748" src="https://github.com/user-attachments/assets/328b5ab9-53f9-4e4e-97b5-3b2da508b884" />

cmd:

int fa 0/5 - this is the interface which is directly connected to the router - so we need make this as a trunk port

switchport mode trunk - This will enable the port to behave as trunk port instead of access port(only applies to only one vlan)

show interface trunk - now we can clearly see that out interface is trunk now and we can see the different det of vlans to make inter vlan routing




