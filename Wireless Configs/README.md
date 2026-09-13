Wireless LAN Controller (WLC) Based Enterprise Wireless Network

Objective: To design and configure a centralized wireless network using a Wireless LAN Controller (WLC), a network switch, and multiple Access Points (APs), enabling wireless clients to securely connect to the network and access network resources.

🗺️ Topology

<img width="1917" height="965" alt="Screenshot 2026-09-13 113443" src="https://github.com/user-attachments/assets/71d8c71f-cef7-4a94-b8bc-a452b8247c28" />


🧩 What I Built

-> Designed and implemented a Layer 3 enterprise wireless network.
-> Configured a Layer 3 switch as the core network device.
-> Integrated a Cisco Wireless LAN Controller (WLC) with the network.
-> Connected and managed two Access Points (APs) through the WLC.
-> Configured wireless connectivity for end-user devices.
-> Implemented Layer 3 routing and IP connectivity between the network components.
-> Verified end-to-end connectivity between wireless clients and network resources.

Step 1 — Configuring the Layer 3 Switch

-> Configured the Layer 3 switch as the DHCP server for the wireless network.
-> Excluded a range of IP addresses from the DHCP pools to reserve addresses for network infrastructure and management purposes.

<img width="1917" height="815" alt="image" src="https://github.com/user-attachments/assets/60d4076c-e1e5-4180-9331-e28aa7534675" />

-> Created a DHCP pool for VLAN 10, which is used to provide IP addresses to the Access Points (APs) and PC1, which is used to access the WLC management GUI.
-> Configured DHCP Option 43 in the VLAN 10 DHCP pool to provide the WLC management IP address to the APs.
-> DHCP Option 43 enables the APs to discover the WLC during the initial boot and join the controller using CAPWAP. This is particularly useful when the WLC and APs are not on the same Layer 2 network.4
-> Created separate DHCP pools for VLAN 100 (Internal SSID) and VLAN 200 (Guest SSID) to dynamically assign IP addresses to wireless clients.

<img width="1917" height="1020" alt="image" src="https://github.com/user-attachments/assets/66f81321-ac4a-4402-aa3a-7705341fd403" />

-> Configured the switch ports and uplinks with the appropriate access and trunk modes to carry the required VLAN traffic between the Layer 3 switch, WLC, and Access Points.
-> Verified the DHCP assignments, VLAN connectivity, and WLC/AP communication using the switch's running configuration and connectivity tests.

<img width="1917" height="1015" alt="image" src="https://github.com/user-attachments/assets/79275e85-7024-4ec9-b7c9-2ce0420751ef" />


Step 2 — Getting Familiar with the WLC

-> Accessed the Cisco WLC management GUI and explored the Monitor section to understand the controller's monitoring and operational information.
-> Navigated to Monitor → Statistics → AP Join to verify the Access Point (AP) join status and review information related to AP-to-WLC connectivity.
-> Verified that the configured APs successfully joined the WLC and reviewed their join information.

<img width="1293" height="852" alt="Screenshot 2026-09-13 215417" src="https://github.com/user-attachments/assets/f4c3c7b4-00a0-4ecb-be45-f57ce385b8ac" />


Step 3 - Configure Dynamic Interfaces for the Internal & guest WLANs

-> Navigated to Controller → Interfaces and created new dynamic interfaces for the Internal and Guest wireless networks.
-> For each interface, configured the corresponding VLAN ID, IP address, subnet mask, and default gateway.
-> Configured the DHCP Server IP address for each interface so that wireless clients can obtain IP addresses from the appropriate DHCP pool configured on the Layer 3 switch.
-> Created separate interfaces for:
VLAN 100 – Internal Network
VLAN 200 – Guest Network
-> These interfaces allow the WLC to map different SSIDs to their respective VLANs and provide the appropriate network connectivity to wireless clients.

<img width="1293" height="857" alt="Screenshot 2026-09-13 221846" src="https://github.com/user-attachments/assets/b5fd35fa-5297-4f38-89ee-2329c338f1ee" />


<img width="1295" height="857" alt="Screenshot 2026-09-13 221949" src="https://github.com/user-attachments/assets/24d25fdd-9da1-431c-96d5-84cd04fa6325" />


<img width="1288" height="847" alt="Screenshot 2026-09-13 222020" src="https://github.com/user-attachments/assets/ff2f0448-7c0c-4bd2-a260-ba8a9800f9e1" />


<img width="1292" height="852" alt="Screenshot 2026-09-13 222052" src="https://github.com/user-attachments/assets/8ecb5e8d-02e0-4f19-a42a-3b2ec90d2d5b" />


Step 4 - Creating the Internal & Guest WLAN using WPA2-PSK

-> Navigated to WLANs → Create New on the WLC.
-> Created separate WLANs for the Internal and Guest wireless networks.
-> Configured a dedicated SSID for each wireless network.
-> Mapped the Internal WLAN to VLAN 100 and the Guest WLAN to VLAN 200 through the corresponding dynamic interfaces.
-> Configured the required wireless security settings for each WLAN.
-> Enabled the WLANs and verified their operational status on the WLC.

<img width="1263" height="853" alt="Screenshot 2026-09-13 223316" src="https://github.com/user-attachments/assets/0e490d87-9287-4908-889d-a73b0435f5ec" />


<img width="1265" height="855" alt="Screenshot 2026-09-13 223430" src="https://github.com/user-attachments/assets/647fab79-13d1-451c-926a-ab9ca89bee18" />


<img width="1263" height="851" alt="Screenshot 2026-09-13 223642" src="https://github.com/user-attachments/assets/cdebf23b-36fb-491e-9bab-a745a9237432" />


<img width="1263" height="855" alt="Screenshot 2026-09-13 223719" src="https://github.com/user-attachments/assets/2ec747f5-38fb-4efb-a032-7cfd2907676d" />


Step 5 -  Add a wireless client to the network and associate it with AP

-> Connected a wireless client to the configured wireless network (SSID).
-> Verified that the client successfully associated with the appropriate Access Point (AP).
-> Confirmed that the AP is managed by the WLC and is broadcasting the configured SSID.
-> Verified that the wireless client receives an IP address from the corresponding VLAN DHCP pool.
-> Tested connectivity between the wireless client and the network to confirm successful wireless access.

<img width="772" height="267" alt="Screenshot 2026-09-13 230942" src="https://github.com/user-attachments/assets/f86b8d48-f79d-4c49-8ce2-665bc67b839d" />


<img width="886" height="665" alt="Screenshot 2026-09-13 231020" src="https://github.com/user-attachments/assets/ec0caac6-7ce6-47de-9f8e-1d0e2bae68a9" />


<img width="672" height="272" alt="Screenshot 2026-09-13 231733" src="https://github.com/user-attachments/assets/4add6c31-6d90-4730-8e67-2b7aa0fbf717" />


<img width="882" height="665" alt="Screenshot 2026-09-13 231826" src="https://github.com/user-attachments/assets/4680b75a-cd9d-415e-918b-c997f8a6fa59" />





















