📘 Lab: STP (Spanning Tree Protocol)

🎯 Objective

Configured STP across three different switches to prevent Layer 2 loops and maintain a stable, loop-free network topology.

🖥️ Topology

<img width="1918" height="1017" alt="STP_toplogy" src="https://github.com/user-attachments/assets/abf64aea-d028-4220-83af-dd87c6ae7fd4" />

Step-1: Find the ROOT Bridge


<img width="1913" height="922" alt="Screenshot 2026-05-08 211313" src="https://github.com/user-attachments/assets/298ec9aa-c5f3-4430-ae0d-8f4478d25d6c" />


To find the root bridge - we need to compare the mac address and priority of all switches in topoloy

Then the switch with the lowest priority becomes the root bridge

priority + MAC Address 

The switch with the lowest brigde ID is elected as root bridge all ports on the root bridge are designated ports (FORWARDING state)

All interfaces on the root bridge are designated ports - Forwarding state

clearly we can see the image all the interfaces which is connected to the root bridge are in Forwarding state

you can ask why priority is 32769 instead of 32768? because its priority + Extended system ID ( which is our vlan number here our VLAN number is 1)

Step-2: Find the ROOT ports


<img width="1888" height="870" alt="Screenshot 2026-05-08 211337" src="https://github.com/user-attachments/assets/a7beb62a-e74a-418b-a1fa-b5f1d560f4b4" />


Each remaining switch will select one of this interface to be its root port. The interface with the lowest root cost will be the root port.

Root ports are also in a Forwarding State

Root Port selection:

1. we need to see the which root port has lowest root cost, every ethernet interface has different set of speeds
   
   In our case its Fa 0/0 - where the root cost is 19

2. If the root cost same of all the links now we need to check the interface connected to neighbor which as a lowest bridge ID - selected as root port

3. So what if the both the root cost and neighbor bridge ID are the same?

   Now we need the check which interface has the has the lowest port ID - port priority + port number


Step-3: Find the Designated(forwarding) and  Non-Designated(blocking) ports


<img width="1897" height="872" alt="Screenshot 2026-05-08 211323" src="https://github.com/user-attachments/assets/a584e1e3-98b1-4c5d-a7b1-a14f66af30ee" />


The one and only one port on each segment that is closest to root brifge in terms of cost

Each remaining collision domain will select one interface to be a designated port(forward state) 

The other port in collisio domain will be non-designated (blocking)

Designated port selection:

1. The switch with the lowest root cost will make its port designated

2. If the root cost is the same, the switch with the lowest bridge ID will make its port designated

3. The other switch will make its port non-designated (blocking)

















