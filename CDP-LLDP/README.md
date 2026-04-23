 Lab: CDP and LLDP Configuration
🎯 Objective

To understand how CDP and LLDP work between a router and a switch.

🖥️ Topology

<img width="1919" height="1028" alt="Topology" src="https://github.com/user-attachments/assets/fcd6d3a7-ad3e-4037-a0f7-dbe414c44db0" />


In this lab, I connected one router and one switch using a cable.

Step-1: Use CDP to verify Layer 2 adjacent Cisco Devices and View and Intrepret Detailed Information

CDP is enabled by default on Cisco devices.

I verified it using:

cmd - show cdp neighbors

To get the detailed informtion about the neighbors

cmd - show cdp neighbors detail

From SW1 to R1

<img width="1913" height="921" alt="CDP view-1" src="https://github.com/user-attachments/assets/f205abad-543a-4597-9412-28ea1c106d62" />

From R1 to SW1

<img width="1919" height="920" alt="CDP view-2" src="https://github.com/user-attachments/assets/1908bf38-ec74-4a82-8837-678fa44c0e83" />


Step-2: Disable CDP on an Interface

Router

cmds:

int gig 0/0 - we are going to disable cdp on a particlular interface which is gig 0/0

no cdp disable - this will disable the CDP on this interface

<img width="1841" height="704" alt="CDP enable - disable" src="https://github.com/user-attachments/assets/b2f8e7dd-f752-49db-bed1-5bef24b1b5f6" />


Step-3: Disable CDP globally

cmds:

no cdp run - meaning we disabling the CDP for all the interfaces in switch or router and run basically we are appending the changes to runnig-config

cdp run - will enable the CDP protocol for the interfaces

<img width="841" height="284" alt="CDP globally enable-disable" src="https://github.com/user-attachments/assets/4ebb4a28-6f7c-4dcc-a3af-fc5f47d1e7a1" />


LLDP Demos

Step-1: Use LLDP to verify Layer 2 adjacent Devices and View and Intrepret Detailed Information 

LLDP is not enabled by default on Layer 2 devices.

To enable the LLDP protocol:

cmd - lldp run 

To get the detailed informtion about the neighbors

cmd - show lldp neighbors detail

<img width="1225" height="491" alt="LLDP - View-1" src="https://github.com/user-attachments/assets/4b227219-422c-4e80-bcc5-13aca3dfe267" />


Step-2: Disable LLDP on an Interface

Router

If Transmit is OFF → your device won’t send info

If Receive is OFF → your device won’t learn neighbors

cmds:

int gig 0/0 - we are going to disable lldp on a particlular interface which is gig 0/0

no lldp receive - this will disable the LLDP on this interface

<img width="1101" height="736" alt="LLDP - disable recieve" src="https://github.com/user-attachments/assets/b9fec8dd-2002-4ab1-9307-4ea28043ac11" />


Step-3: Enable LLDP on an Interface

cmd:

lldp receive -  this will enable the LLDP on this interface

Step-4: Disable LLDP Globally

cmd:

no lldp run - this will globally turn off the lldp protocol 















