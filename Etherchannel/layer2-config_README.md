📘 Lab: Etherchannel

🎯 Objective

To configure Etherchannel between 2 switches.

🖥️ Topology


<img width="1918" height="988" alt="layer2-Etherchannel_topology" src="https://github.com/user-attachments/assets/fb11377a-7c8e-4824-843b-ecd8062c9112" />


Step-1: Creating a Layer-2-Etherchannel and creating a trunk over a EtherChannel fro SW1 and SW2


<img width="1918" height="1017" alt="Screenshot 2026-05-10 221028" src="https://github.com/user-attachments/assets/51a3f21e-5027-421c-90c2-2f31fad10537" />


<img width="1918" height="1012" alt="Screenshot 2026-05-10 221705" src="https://github.com/user-attachments/assets/446abd64-628c-473c-9e0d-9e150a4b8f25" />


In this topology we have couples of links between switches SW1 and SW2 we need to logically bond together two physical links into an EtherChannel

we are just creating a virtual interface represents the etherchannel also called as Port-Channel interface

Before configuring Etherchannel we need to check whether both the switches has the same setting meaning in terms of speed and duplex

cmd:

int range - basically we need to specify what are all the ports belong to etherchannel

channel-group <number> <mode> - we are creating a channel for those two interfaces

number - based on our conveint

mode - For PAgp we have different and more LACP we do have different only the nameing convention is different other than that working principles are same

For PAgP:

desirable - Initiates to send PAgP frames to other end

Auto - It will not Initaites but it will waits for PAgP frames if someoen send the PAgP frames it will form Etherchannel

For LACP:

Active - Initiates to send LACP frames to other end

Passive - It will not Initaites but it will waits for LACP frames if someone send the LACP frames it will form Etherchannel

If the mode is hust ON  it will enable etherchannel it will intiate or accept anything if other end is also on if the configuration mathces to will form a
Etherchannel


Switchport mode trunk - Basically this is used to carry multiple VLANs over a single interface

Same mirror configuration should be on SW3 switch

Step-2: Now we can look into the load-balance and bandwidth


<img width="1918" height="1012" alt="Screenshot 2026-05-10 224628" src="https://github.com/user-attachments/assets/303523e5-e26b-4588-b8d2-175aedc3dc15" />


We can clearly that our bandwidth got increased basically we have combined two ethernet port Fa 0/1 -2 (Fast Ethernet)

Fast Ethernet speed is 100 Mbps so we have two links total is 200 Mbps - In switch is calculated as Kbps so it becomes 200000

Load balance - Its actually running a load balancing algorithm that is going to select mathematically which link to use for a particular packet

and these are actaully several algorithm we can select from and we get to choose the one we want 

Now we will be having a doubt how it will etherchannel makes a single logical link where as we have two physical links which it will choose to flow?

STP would see multiple separate links

It would block some ports

EtherChannel hides the multiple links from STP by presenting them as:

-> one logical interface

But internally:

-> all physical interfaces still work.

If one flow only uses one physical link, then why does bandwidth become 200 Mbps?

The total EtherChannel bandwidth is shared across MULTIPLE traffic flows, not one single flow.

Example:

Fa0/1 = 100 Mbps
Fa0/2 = 100 Mbps

Etherchannel - Port-Channel1 = 200 Mbps logical bandwidth

One single conversation/flow:

PC1 → Server1

This flow will use ONLY:

Fa0/1

So this single flow is still limited to:
100 Mbps

NOT 200 Mbps

where does 200 Mbps come from?

When MULTIPLE flows exist.

Example:

PC1 → Server1 = Fa0/1
PC2 → Server2 = Fa0/2

Now BOTH links are being used simultaneously.

Total:

100 + 100 = 200 Mbps

EtherChannel does NOT increase speed for one single transfer it increases TOTAL available bandwidth for multiple traffic flows.









