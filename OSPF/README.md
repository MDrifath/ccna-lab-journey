Lab: OSPF v2 Configuration

🎯 Objective

A multi-area OSPF lab demonstrating routing and neighbor relationships across two OSPF areas using three routers.

🖥️ Topology

<img width="1919" height="818" alt="OSPF_topology" src="https://github.com/user-attachments/assets/b43ad9b7-7925-41f1-a6f4-d33107c2929b" />


Step-1: Assign Router-id

<img width="1919" height="1020" alt="Screenshot 2026-06-02 214909" src="https://github.com/user-attachments/assets/21f10e14-5f8b-40f5-baa8-bdd797c767e7" />

cmd:

router ospf 1 - process ID : The process ID is a locally significant number used by the router to identify an OSPF process.

Does not need to match on neighboring routers and Is only meaningful on the local router.

router-id <number> - Router ID (RID) is the unique identifier of a router in an OSPF network is used for verification 

The process ID and Router-id are configured for other two routers R2 and R3


Step-2: Configure interfaces to participate in OSPF


<img width="1919" height="1019" alt="Screenshot 2026-06-02 215602" src="https://github.com/user-attachments/assets/509904b2-f1d5-4aa4-ab60-18646d0a1fed" />


CMD:

Now we need to make interfaces participate in OSPF 

network <network-id> <wildcard-mask> area <area number>

For example:

network-id - 10.1.1.0 

network cmd specifying a network of IP addresses - basically what we are saying is if we have one more router interfaces that happen to up and belongs to this address space then

that interface going to participate in OSPF

Wildcard mask - is basically the inverse of subnet mask so according to my lab subnet mask is 255.255.255.0 inverse of this 0.0.0.255 is pur wildcard mask


Step-3: configure passsive interfaces

Do you think router R3 of interface gig 0/0/0 in area 2 need to participate in OSPF network because it is connected to switch? 

And we should receive any OSPF hello messages on this interface

To answer this question we will be using a cmd

cmd:

passive interface gig 0/1 - Basically we will not be sending those unnecessary OSPF hello messages

eventhough we make the interface as passive interface we are still going to be advertise the network we just don't want the interface to actively participate in OSPF 

neigbor Formation

OSPF v2 Verification:

<img width="1918" height="1016" alt="Screenshot 2026-06-03 130213" src="https://github.com/user-attachments/assets/2542ecb2-abab-4c84-bb07-b2212ccb8fff" />

This is the image of router R3 - we can see that there are two OSPF networks which is 172.16.1.0 and 192.168.1.0 

IA - Repesents Inter Area

Explaining the OSPF process how does it work?


<img width="1919" height="981" alt="Screenshot 2026-06-03 132029" src="https://github.com/user-attachments/assets/773e211b-d9b9-487a-9e2e-ceeffdfad7e4" />

Imagine we are connected with number of routers with one another obviosuly we want to know about each other 

1. Routers discover each other using hello message - this is called Neighborship
2. And then Routers need to form an adjaceny with other routers - this help in exchanging routing information
3. And then sends Link state Advertisements (LSAs) to routers

Each router carries different pieces of information will put together that information is in the form of LSAs those are sent between routers to educate one another.
After each router will receive thos LSAs which will be grouped together to form the map of the network and that map get stored in Link state Database 
Run the it will dijkstra shortest path first (SPF) Algorithm to determine the shortest path to a network

But we have problem here compared to neighborship, adjaceny looks like efficient but in reality it make lot of adjacencies means every router need to work more this does not scale well

To overcome this there is a process which is we need to elect DR(Designted Router) BDR(Backup Designated router)

-> what we can do is we can identify one or two routers with which everybody else is going to form an adjacency

-> Instead of exchanging router information to all the routers out there we are going to form an adjacency with Designated Router (DR) incase DR is not available we have BDR

-> If a new routing information has come in its just going to do is send those updates just to DR and BDR and they can relay the information to all other routers.


OSPF Area:

what if the network getting larger?

we need to split the OSPF speaking routers into different areas

-> A grouping of router inteface participating in OSPF that share a common view of the network much like sharing a common map of that area

Area Borer Router (ABR)

-> A router with atleast two interfaces participating in OSPF that connect to differnet areas in our case R2 is ABR where it knows about the network in Area 1 and Area 0 

-> And its going to be able to tell each area about the networks in the other area

-> we are just telling the listings of the network not the entire map of the network

<img width="1919" height="1022" alt="Screenshot 2026-06-03 145554" src="https://github.com/user-attachments/assets/c5711ccd-c105-4a85-97bc-bb32616c95f7" />


<img width="1919" height="1019" alt="Screenshot 2026-06-03 145645" src="https://github.com/user-attachments/assets/ff256826-b441-4120-ae61-a381b294072d" />

we are having 3 types of LSAs:

Form the last image we can clearly see

1. Router Link - Type 1 LSA

-> A router LSA is created by each router and contains information about that router's directly attached networks

-> Advertised within an Area

2. Net Link - Type 2 LSA

-> A Network LSA created for each tansit within an area where DR is elected

-> For type 2 LSA it has to meet 2 creteria

-> network being advertised by this type 2 LSA it interconnecting a couple of OSPF neighbors

-> Deisgnated router need to elected on this segment

3. Summary Ney link - Type3 LSA

-> Summary LSA is sent from the one area to another area and used to advertise network in the source area as well






























