📘 Lab: NAT (Network Address Translation)

🎯 Objective

Configuring Static NAT

🖥️ Topology

<img width="1919" height="1018" alt="Screenshot 2026-06-10 221450" src="https://github.com/user-attachments/assets/f6423f15-1676-4792-8d84-d505eee962ee" />


Step-1: Enable NAT on Inside and Outside Interfaces

<img width="1919" height="1019" alt="Screenshot 2026-06-09 230117" src="https://github.com/user-attachments/assets/99b47f2c-ca93-40cc-8fcc-6449044ac73b" />

-> we are going to configure the static NAT on Router R1

-> pc1 inside of the network it has the private IP address and we want to transalte into a publicly routable IP address to get out the internet

-> Now we define which interface the inside local of the network and Inside global of the network

CMD:

int gig 0/0 - Inside Local interface

ip nat inside - we are telling that that this interface will act as inside local

int gig 0/1 - Inside Global interface

ip nat outside - we are telling that that this interface will act as Inside Global


Step-2: create a static mapping between a inside local and inside global address

CMD:

ip nat inside source static <Inside local address> <Inside Global address>

-> Basically we are mapping the inside local address to inside global address

Step-3: Verify NAT Translation:

<img width="1919" height="1017" alt="Screenshot 2026-06-09 230151" src="https://github.com/user-attachments/assets/932b3e65-79df-4c07-8ee0-48d1de3ca81a" />


<img width="1919" height="1018" alt="Screenshot 2026-06-09 230559" src="https://github.com/user-attachments/assets/5f82e015-d167-4d42-a801-c959198312db" />


-> From the image we can clearly see that the ip address got translated 







