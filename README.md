Simple Network Topology

A star topology built in Cisco Packet Tracer: a router connecting two subnets, each with a switch, two PCs, and a networked printer.

Topology diagram
<img width="923" height="545" alt="image" src="https://github.com/user-attachments/assets/1d97ec09-52bc-469c-b8f3-5a14a27a55f3" />

Design
Device	Role
Router0 (2911)	Connects the two subnets
ACCOUNTS switch (2960-24TT)	Subnet 1: PC0, PC1, Printer0
DELIVERY switch (2960-24TT)	Subnet 2: PC2, PC3, Printer1
Addressing
Network address `192.168.40.0`, split into two `/25` subnets, sized for up to 126 hosts per department with room to grow.
Subnet 1 (Accounts)
Subnet mask: `255.255.255.128`
Network ID: `192.168.40.0`
Valid host range: `192.168.40.1 - 192.168.40.126`
Broadcast: `192.168.40.127`
Subnet 2 (Delivery)
Subnet mask: `255.255.255.128`
Network ID: `192.168.40.128`
Valid host range: `192.168.40.129 - 192.168.40.254`
Broadcast: `192.168.40.255`

Each PC is configured with a static IP in its subnet, with Router0's subinterface as the default gateway.
Verification

PC2's static configuration:
![PC2 IP configuration]
<img width="425" height="302" alt="image" src="https://github.com/user-attachments/assets/3037fb03-c374-4dca-92f8-3269dcb8df82" />

What I'd do differently
This is flat subnetting with a router doing inter-subnet routing; it doesn't use VLANs or a router-on-a-stick / Layer 3 switch setup, which is how a real two-department network would more likely be segmented.
No DHCP — every host is statically addressed, which doesn't scale past a handful of devices.
No access control between the two subnets; anything on Accounts can reach anything on Delivery.

What I learned

Working through this helped me understand subnetting in practice rather than just on paper — picking a mask that fits the host count, calculating valid ranges and broadcast addresses by hand, and seeing how a router's interfaces become the gateway for each side. It also showed me how a ping failure during testing usually traces back to a gateway or mask typo rather than the router itself.
