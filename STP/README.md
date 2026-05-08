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



Step-3: Find the Designated ports


Every link has a designated port even if we're not carrying traffic over a link to prevent that loop one end is still active it's designated while the other end is blocking.


Step-4: Find the Non-Designated(blocking) ports

















