📘 Lab: NAT (Network Address Translation)

🎯 Objective

Configuring Dynamic NAT

🖥️ Topology

<img width="1919" height="942" alt="Screenshot 2026-06-09 232243" src="https://github.com/user-attachments/assets/31092c4a-dcdf-44bb-8fef-0b7c8470e688" />

-> we are going to configure NAT thats where we going to translate the inside local addresses on the inside of our network into a pool of inside 

global addresses this is where the multiple addresses that can be routed on the public internet 

Step-1: Enable nat on Inside and Outside Interfaces

<img width="1919" height="1019" alt="Screenshot 2026-06-09 232219" src="https://github.com/user-attachments/assets/cb9de9f7-4149-48b4-a58e-843fb2aca1ac" />

-> similary we need to follow the same step that we had did in static NAT


Step-2: Create an ACL to match the inside network

-> This ACL is not mean to allow or deny traffic but ACL can also be used for match the traffic

-> This ACL is going to match any IP address that belongs to our inside network

CMD:

access-list 1 permit <Inside Local Address> <Wilcard Mask> - Basically we are telling this access-list number 1 and permit in this context we are just matching the ip address that belongs

to inside addresses(netwokr id) with local mask

-> This ACL going to identify out inside local addresses


Step-3: Creating a Pool of inside global Addresses

-> We are going to translate the those inside local addresses to inside global addresses that belong to pool of publicy routable IP addresses

CMD:

ip nat pool <NAME> <RANGE OF IP ADDRESSED > netmask <SUBNET MASK>

-> We are Just created the pool of addressed that represents out inside global addresses

Step-4:  Map IP addresses defined by the ACL into a Pool of inside global Addresses

-> Now we are going to map if the source IP address is matched by this ACL we want to translate into that in to one of the IP address that belongs to the pool

CMD:

ip nat inside source list 1 pool POOL -> this the dynamic NAT

list 1 -  l is the belong access list that we created during the creation of the inside local addres

pool POOL - we are telling the name of the pool by using its name


Step-4: Verifying NAT Translations

<img width="1919" height="1021" alt="Screenshot 2026-06-09 232344" src="https://github.com/user-attachments/assets/3c1bb5ad-e2ef-4774-a779-1396e489d024" />


<img width="1919" height="1019" alt="Screenshot 2026-06-09 232418" src="https://github.com/user-attachments/assets/db452dd3-35a3-4100-b548-664abe10d6cd" />


<img width="1919" height="1020" alt="Screenshot 2026-06-09 232633" src="https://github.com/user-attachments/assets/fc45037c-1822-4c25-b26a-2eafff5177af" />







