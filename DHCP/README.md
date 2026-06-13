📘 Lab: DHCP (Dynamic Host Configuration Protocol)

🎯 Objective

To configure DHCP and DHCP Relay Agent functionality to dynamically assign IP addresses across different subnets.

🖥️ Topology

<img width="1918" height="987" alt="Screenshot 2026-06-13 140605" src="https://github.com/user-attachments/assets/b65e2ab2-87f0-4aa4-95b5-f335b40abad7" />


Step-1: Configure a DHCP server on a ciscon IOS router

-> Basically we a router to act as DHCP server and hand out the IP addresses to another cisco IOS router


<img width="1919" height="1017" alt="Screenshot 2026-06-11 231156" src="https://github.com/user-attachments/assets/38804cfb-ec24-4ae5-9a8f-b91a005b954a" />


-> Now we need to create a Pool of addresses to hand out to our clients before creating this we need to execlude some addresses

CMD:
To exclude - ip dhcp excluded-address <start-ip range> <end - ip range>

To create a pool - ip dhcp pool <name of the pool> - The pool we creating is used to hand out IP address information

To specify the network which we need to hand oout ip address - network <network id> <subnet Mask>

we also need to hand out Default gateway and DNS information those are two types that our client would need to get off its local subnet and resolve DNS



Step-2: Configure a router interface to learn IP address information from the DHCP server

-> we are going to configure its interface to request information via DHCP instead of statically configuring an IP address 


<img width="1919" height="1019" alt="Screenshot 2026-06-11 231520" src="https://github.com/user-attachments/assets/b5efb83c-6d34-4ba1-b41d-8ec6e932a729" />


-> Thsi is going to be acting as a DHCP client 

CMD:

-> pick the interface where our router is created int our case - int gig 0/0

-> assigning a IP address using DHCP rather than statically assigning an IP address - ip address dhcp

-> To bring the interface administatively up - no shutdown

However we would not get ip address information from out our interface is up and will get the IP address through DHCP but there is no ip address assigned

The reason the router r2 is discarding the discover broadcast request and broadcast cannot pass through the router in order to fix that we need to configure R2 to act

as DHCP relay agent


Step-3: Configure a DHCP Relay Agent


<img width="1919" height="1021" alt="Screenshot 2026-06-11 231732" src="https://github.com/user-attachments/assets/a5ed7137-6d54-4cc5-926f-563ab1e6174e" />


-> ISP - we are allowing them to give IP address information but once we got the IP its not going to work immediately becaues there is a router 

between our DHCP client and DHCP server - ofcourse it will block the discover broadcast sent by our DHCP client that means we are going to 

configure a DHCP relay agent to take that broadcast request

CMD:

-> First choose the interface we need to - int gig 0/0

-> to act as a relay agent - ip helper-address <ip address of the DHCP server>


Step-4 : verify DHCP operation


<img width="1900" height="959" alt="Screenshot 2026-06-12 090840" src="https://github.com/user-attachments/assets/e5efd81f-1341-4a18-b633-05cb23257498" />


-> If we go to R1 it won't recieve the ip address immdeiately we need to wait for sometime and try bouncing the interface means bring down adn bring up the interface

-> After 15-20 minutes we will get th ip address via DHCP server



