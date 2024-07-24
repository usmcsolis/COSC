# Networking


## Sites:
CTFD - MASO-M-005@10.50.20.180:8000/challenges

CTFD Resources - http://10.50.20.180:8000/resources

CTFD Practice - http://networking-practice-ctfd.server.vta:8000/

CTCC Network - https://net.cybbh.io/public/networking/latest/schedule.html

xfreerdp /v:10.50.x.x /u:student /p:password /size:1920x1000 +clipboard

Subnet Chart: https://www.engineeringradio.us/blog/wp-content/uploads/2013/01/Subnet_Chart.pdf

Miro Whiteboard - https://miro.com/app/board/o9J_klSqCSY=/?share_link_id=16133753693


## VPN Setup:
```
    VPN Config File

    Installing the VPN client

        Windows
            Download Openvpn Client
            Install the client
            Save the contents of the VPN Config File as config.ovpn in the config directory for openvpn: "c:/Program Files/OpenVPN/config/config.ovpn"
            Run OpenVPN as administrator once the file is in the config directory.
            Right click on the icon and click on connect
            Enter username and password for IPA (git and vta credentials)

        Linux
            Type sudo apt-get install openvpn -y in the terminal
            Save the contents of the VPN Config File as config.ovpn in the directory location of your choosing and change directories to it
            Type sudo openvpn --config config.ovpn &
            When connecting to the VPN use the username and password you just created with the IPA server

        Mac
            Install tunnelblick
            Once installed, enter the VPN details.
            Save the contents of the VPN Config File as config.ovpn
            Drag the provided config.ovpn file into the configurations.
            When connecting to the VPN use the username and password you just created with the IPA server
            Hit connect and you should see the connection because the icon will turn green and you will see a timer start.
            Install Microsoft Remote Desktop for Mac OS
            Once MRD is installed, click the button with the + symbol and add pc.
            Put your floating IP where it says PC name, add user account from dropdown.
            Put your user name:password for system and click add
            You will be able to connect from there
```


----


# Lesson 1: Fundamentals


## Slides

Network Access: https://net.cybbh.io/-/public/-/jobs/874001/artifacts/modules/networking/slides-v4/01_data.html

Network Layer: https://net.cybbh.io/-/public/-/jobs/874001/artifacts/modules/networking/slides-v4/02_network.html

Transport to Application Layer: https://net.cybbh.io/-/public/-/jobs/874001/artifacts/modules/networking/slides-v4/03_transport.html

Traffic Capture: https://net.cybbh.io/-/public/-/jobs/874001/artifacts/modules/networking/slides-v4/06_traffic_cap.html


## OSI Model

7 Layer OSI MODEL (PDNTSPA)
![image](https://github.com/user-attachments/assets/6eb18223-a459-48a3-a01e-0fed85fb986a)

PDU Protocol Data Unit -

But Free Pizza So Delicous(x4)

Application = DATA

Presentation = DATA

Session = DATA

Transport = SEGMENTS

Network = PACKET

DataLink = FRAME

Physical = BIT


## Internet Standard Organizations

Internet Engineering Task Force (IETF) - RFCs are documents for standardization
```
Mostly known for developing and publishing "white paper" standards known as Request for Comment (RFC).

Some notable ones are:
* IPv4 (791)
* IPv6 (2460)
* TCP (793)
* UDP (768)
* HTTP 1.1 (2616)
* List of other from Wikipedia
```


Internet Assigned Numbers Authority (IANA) - Internet Numbers 
```
Controls all internet numbers such as:
* MAC OUI numbers
* Ethertypes
* IPv4 and IPv6 addresses
* IPv4 and IPv6 Multi-cast addresses
* Protocol Numbers
* Port Numbers
* 16/32-bit AS Numbers
* Domain Names (Root)
* ARP Operation Codes
```

Institute of Electrical and Electronics Engineers (IEEE) - LAN/WAN Electrical Standards
```
Most notably they developed standards for Local Area Networks (802 series) such as:

* 802.1 - LAN and WAN bridging and security
* 802.2 - LLC sub-layer
* 802.3 - Ethernet (CSMA/CD)
* 802.11 - Wireless LAN
* 802.15 - Wireless PAN
```
# Layer 1 Data
## Binary
```
Base2- Two Symbols (0 and 1)

Groups:
Bit(1 bit)
Nibble(4 bits
Byte(8 bits)
Halfword (16 bits)
Word (32 bits)

128    64    32    16    8    4    2    1
 0      0     0     0    0    0    0    0
```

![image](https://github.com/user-attachments/assets/edfb586b-f9a2-4730-a3f8-4e7a47fbed44)


## Hexadeciaml
```
Base 16 - Sixteen Symbols (0-9 and A-F)

8    4    2    1    8    4    2    1
0    1    0    1    0    0    0    1

= 51

FF =

1    1    1    1    1    1    1    1


```

![image](https://github.com/user-attachments/assets/19762878-de97-4759-a413-4f224f77fd01)

![image](https://github.com/user-attachments/assets/16d02c44-9008-4c7f-9d94-ebca2d0e4d5e)


## Base64
```
Base64 = 64 Symbols (A-Z, a-z, 0-9, +, /)
Users (=) to represent a NULL value (max of 2)
Format = MTI= MTIzNA== MTIzNDU2Nzg=

```

![image](https://github.com/user-attachments/assets/50aa4e8c-2d16-4e2d-8e3e-1a00dcaf2054)


# Lan Topologies
## Bus
![image](https://github.com/user-attachments/assets/e6915d00-fa55-4374-9ddd-0ede65939b17)

## Star
Central Node passes it to everyone else 

![image](https://github.com/user-attachments/assets/2a299de8-66b6-42d8-bc7b-dc631f301926)

## Ring
Every workstation is plugged into everyone else and it goes 1 way in a ring

![image](https://github.com/user-attachments/assets/ceded32a-f364-4af0-ad10-ddbb40173d24)

## Mesh
Everyone is connected to everyone 

![image](https://github.com/user-attachments/assets/90699989-c44d-4b21-b06f-27527b9041b7)

## Wireless
Routes via APs and no need for centeralized transmissions

![image](https://github.com/user-attachments/assets/3a9c938c-35be-4ede-88fa-4292432e439e)

## Hierarchial
Information is broken down to tiers 
```
Core

Distribution

Access Layer
```

![image](https://github.com/user-attachments/assets/89c7d021-1ddc-486f-a8fa-517c50957e73)


# Devices
## Hub
Passes information through everyone. Can have collisions where the packets are sent at the same time and clash

## Repeaters
Used to extended a signal to repeat and make it go further due to the limitations on some cabling

## Switches
Similar to hubs but can use Collision Domain and it knows what you are addressing using a MAC Addresss to reduce collisions.

## Routers
Allows you to cross networks using routing tables. Can connect different nets together. One router can connect a LAN to another LAN to create a WAN


## Ethernet Timing (BIT-TIME)
Bit Time - is the period of time is required for a bit to be placed and sensed on the media. Network speeds are measured by how many bits can be placed or sensed on the media in 1 second. Each increase in speed requires more bits to be sent during the same 1 second internal. To accomplish this the bit-times are reduced.

```
Speed       Bit-Time
10 mbps     100ns
100 mbps    10ns
1 Gbps      1ns
10 Gbps     .1ns
100 Gbps    .01ns
```

# Layer 2 Data Link
## Sublayers
MAC (Medium Access Control)

LLC (Logical Link Control)

## Message Formatting Method and Terminology

![image](https://github.com/user-attachments/assets/b2477912-db59-4914-8224-883a7ed47ac6)

HEader - Layer 2 to Layer 7

Data - Payload

Footer - FCS/CRC ( FrameCheckSequence and CyclicRedundancyCheck)

## Encapsulation and Decapsulation
When data is being trasmitted through the OSI Model header and footers are constantly being stripped and added

![image](https://github.com/user-attachments/assets/2a66375c-55bd-4ed2-97a0-200c5ddc5007)

![image](https://github.com/user-attachments/assets/5df51644-8f08-473c-bec7-14e6023b0582)

## Switches
```
Build MAC-Address (Content Addressible Memory (CAM)) Table
- Learns by reading Source MAC Address

Forwarding Frames
- Decision based on Destination MAC Address

Operational Modes
- Cut Through - (sometimes called fast forward) only examines the destination address before forwarding it to its destination segment. This is the fastest switching mode but requires the interfaces to be the same speed.

- Fragment-Free - Checks the entire packet and verifies its not split up

- Store-and-Forware - accepts and analyzes the entire frame before forwarding it to its destination
```

## EXPLOITS
```
CAM Table Overflow/ Media Acces Control (MAC) Attack
- flooding attack, is a type of security exploit that targets network switches. This attack aims to overwhelm a switch’s CAM table, which is used to store MAC address-to-port mappings, leading to a denial of service (DoS) condition or facilitating a man-in-the-middle attack.
- Similar to a buffer overflow attack, the goal is to fill the switches table with "learned" MAC addresses and see what happens. The attacker sits on one port and generates a vast number of "spoofed" MAC entries. When the CAM table is full, all additional MACs will not be learned and will default to "open". This means that traffic without a CAM entry will be flooded out on all ports of the VLAN in question. Traffic with a CAM entry won’t be affected, but neighbor switches could be.

```

## MAC Address
```
Length = 48 bit | 6 byte | 12 hex
Format =
Windows : 01-23-45-12-34-56
unix-Linux : 01:23:54:12:34:56
Cisco : 1234.5612.3456

Parts
OUI - First 24-bits assigned by IANA
Vender Assigned - Last 24-bits

```

![image](https://github.com/user-attachments/assets/76290b2b-1b54-4b9d-b330-5fad385e2a77)

```
Types:
Unicast - One to One 8th bit is OFF

MultiCast - One to MANY 8th bit is ON

BroadCast - One to ALL 8th bit is ON
```

## MAC Spoofing

```
Could not be changed at first
Used to be called:
hardware
firmware
burned-in

Now it can be changed w/ software



Spoofing is the act of disguising a communication from an unknown source as being from a known or trusted source. Spoofing is an attack vector done at several different layers of the OSI. At the Data-link layer attackers will commonly spoof the MAC-address.

Originally MAC addresses were hard coded into the firmware of the NIC and could not be easily changed. This is why MAC addresses were commonly called "Firmware", "Hardware", or "Burned-in" addresses. In order to facilitate MAC spoofing attacks it required crafting of special frames with the MAC address pre-programmed in.

Today most MAC addresses are programmed using the software. This makes modification of a device’s MAC address much simpler. In order to perform a MAC spoofing attack the malicious actor can either change their MAC address to a known or trusted address or create crafted frames with the MAC address already programmed in. MAC spoofing can be used to perform:

ARP-Cache poisoning - modify the ARP cache of devices on the same network segment.

ARP Man-in-the-middle (MitM) attacks - Specially crafted ARP messages to force 2 or more victims to send traffic thru the attacker’s system. Here the attacker can sniff or alter traffic.

```

## Ethernet Header and Frame

![image](https://github.com/user-attachments/assets/ef5da628-1f90-435b-80fc-8509589af70e)

![image](https://github.com/user-attachments/assets/c9c33467-ee6f-4aac-88a8-54c51ee84f3a)

![image](https://github.com/user-attachments/assets/4c60dcac-dc44-418d-a669-c63a8d3e1339)

```
Structure:

    Preamble (7 bytes) +Consists of alternating 1’s and 0’s to allow network synchronization with receiver clocks. Ethernet is self-clocked, the clock is extracted from the signal. The clock is used to set the bit-timing. This is so that the receiver knows what speed the bits will be arriving at. This is stripped off at the NIC and not visible by packet analyzer software.

    SFD (Start Frame Delimiter) (1 byte field) Marks the end of the preamble, and the beginning of the Ethernet frame and send an announcement that data is about to be sent to any other hosts on the same network segment. This is stripped off at the NIC and not visible by packet analyzer software.

    Destination MAC Addresses (6 bytes)

        Initial 6 bytes (48 bits) contain the Destination MAC address.

        This can be Unicast, Multicast, or Broadcst MAC address.

        This is sent first to assist in switch operation of the cut-through mode.

    Source MAC Addresses (6 bytes)

        Next 6 bytes (48 bits) contain the Source MAC Address.

        This is always a Unicast MAC address.

        It is worth noting that this is pretty much the only time that the destination address comes before the source. The source address will come first in most other headers that we deal with in this course.

    Ethertype (2 bytes) Used to indicate the next protocol encapsulated in the frame. This is provided by the LLC sub-layer.

        Common Ethertypes controlled by IANA.org:

            0x0800 - IPv4

            0x0806 - ARP

            0x86DD - IPv6

            0x8100 - VLAN Tagging 802.1q

            0x88A8 - Service VLAN tag identifier (S-Tag) (Q-in-Q tunnel)

            0x8863(4) - PPP over Ethernet (PPPoE)

            0x8847(8) - MPLS

            0x8892 - PROFINET Protocol

    Data / Payload (46-1500 bytes)

        Consists of the encapsulated upper layer headers and data payload which may be 46-1500 bytes.

        The minimum 46 bytes is based on the fact that the smallest "legal" ethernet frame size is 64 bytes; so 46 bytes of data with 18 bytes of Frame header equates to 64 bytes. Anything less than 64-bytes is assumed to be a collision fragment (or "runt"). "Padding" is used when there is less than 46-bytes of data.

        The maximum data bytes is determined by the MTU for the network segment. The MTU is the maximum size of the payload of the frame of the particular network. Ethernet II by default has a max MTU of 1500 bytes. This MTU is the amount of encapsulated data. MTU of 1500 plus the 18 byte header equates to 1518 bytes. Anything greater than this may be considered a "Jumbo" frame.

        This typically is the size of the IP packet but can be the size of other encapsulated protocols like ARP or IPv6.

        The Frame header is not calculated in to this size. So the frame size could be 1518 bytes (or more) in total when the 18 byte header is added. It’s worth noting that the 1500 bytes is of total encapsulated information and not exclusively user data. This 1500 bytes includes the 20+ byte IPv4 header and 20+ byte TCP header. If VPN or tunneling is involved then the extra headers must also fit within this 1500 bytes.

        MTU defaults:

            1500 - Ethernet

            17914 - 16 MBPS Token Ring

            4464 - 4 MBPS Token Ring

            4352 - FDDI

            2304 - IEEE 802.11 Wi-FI (WLAN)

            1280 - IPv6 path

            1492 - IEEE 802.3/802.2

            1480 - PPoE (WAN Miniport)

            576 - X.25

        If there are any other headers included, such as IPSEC, IPv4 or TCP options, then this would mean that even less user data can be encapsulated.

    FCS/CRC (Frame Check Sequence / Cyclical Redundancy Check) (4 bytes)

        Mathematical formula calculated on the entire frame. This calculation is appended in the FCS field so that the receiver can determine if the contents of the frame were corrupted in transit. This is stripped off at the NIC and not visible by packet analyzer software.

```

# VLANs (802.1Q)
## Virtual Local Area Network


![image](https://github.com/user-attachments/assets/5d0a46c8-aa5f-4b16-b9b2-6f1001c29ccf)

```
This tagging allows network administrators to logically segment a single physical network into multiple virtual networks, known as VLANs, to improve network performance, security, and manageability.
802.1Q Frame

Allows you to be able to seperate locally and logically seperated devices to be able to communicate with or without eachother via port assigning

Assign VLANS Via Interfaces

VLAN 10 = Users
VLAN 22 = Printers
VLAN 100 = SuperSecret
```
```
    Structure:

        MAC Header (12 byte field)

            Initial 6 bytes contain the Destination MAC address

            Next 6 bytes contain the Source MAC Address

        VLAN Tag (4 byte field)

            Tag Protocol ID (2 byte field)
            Initial 2 bytes contain the new effective Ethertype field of 0x8100 indicating tagging

            Tag Control Information (2 byte field)

                Priority Code Point (3 bits)
                This is used to add prioritization or QoS to VLANs

                Drop Eligible Indicator (1 bit)
                This adds drop eligibility to VLAN traffic in case of congestion

            VLAN ID (12 bit field)
            To specify the VLAN number. Can be 0x000 to 0xfff or 0* to 4095.

                1 to 1005 Normal range

                1003 to 1005 – reserved for Token Ring

                1006 to 4094 – Extended Range

        Ethertype (2 byte field)
        Used to indicate the next protocol encapsulated in the frame.

        Data / Payload (46-1500 byte field)
        Consists of the encapsulated upper layer headers and data payload which may be 46-1500 bytes

        FCS/CRC (Frame Check Sequence / Cyclical Redundancy Check) (4 byte field)
        A new calculation is conducted to accommodate the addition of the new tag information. This calculation is done by the switch or router that added the tag. This also will be stripped off by the receiving NIC and will not be viable by the network analyzer.

```

## VLAN Types
```
    Default - VLAN 1 is the default vlan. VLAN 1 will always be present on the switch and can not be deleted. All ports will be assigned to VLAN 1. When VLAN assignment is removed from a port it will automaticcally be assigned to VLAN 1.

    Data - VLANs assigned for user traffic.

        Data VLANs are used to separate user data traffic based on different groups, departments, or functions.

        Devices within the same data VLAN can communicate with each other as if they are on the same physical network.

    Voice - VLAN assigned for use for voice traffic only. Typically uses CDP messages from VOIP phones to be asigned.

        Voice VLANs are used to separate voice traffic from data traffic in networks that support Voice over IP (VoIP) systems.

        This VLAN is configured to carry voice traffic, ensuring quality of service (QoS) for voice communications.

    Management - A form of data VLAN used for switch/router remote management purposes.

        A management VLAN is a VLAN used for managing networking devices such as switches, routers, and access points.

        This VLAN is often used for remote device management, configuration, and monitoring purposes.

        It helps secure management traffic by segregating it from user data traffic.

    Native - VLAN used for switch/router generated traffic.

        These are used for control traffic such as CDP, VTP, DTP, and STP. These do not normally have "tags" applied.

        Native VLANs by default is VLAN 1 but is highly recommended to change.

        The native VLAN is used on trunk links to carry untagged frames.

        Frames from the native VLAN are not tagged when traversing trunk links, while frames from other VLANs are tagged.

```

## Without VLANs
```


Networks without VLANs operate as a single broadcast domain, where all devices connected to the same physical network segment can communicate with each other without any logical segmentation.

    Single Broadcast Domain:

        In networks without VLANs, all devices connected to the same physical network segment receive broadcast traffic intended for the entire segment.

        Broadcast traffic includes protocols such as ARP (Address Resolution Protocol) and DHCP (Dynamic Host Configuration Protocol), as well as other network-wide announcements. Each physical interface on a router is assigned to a different network. Will need one physical interface per network required. Future planning is critical as additional added networks can be difficult and costly to install.

        All hosts on the switched LAN are part of the same network and only a router can segment networks.

        In normal operation, when a switch receives a broadcast frame on one of its ports, it forwards the frame out all other ports except the port where the broadcast was received.

        On a switch with only 1 vlan configured (vlan 1 by default) all ports belong to same broadcast domain.

    Flat Network Structure:

        Networks without VLANs typically have a flat network structure, where all devices are part of the same logical network.

        Devices within the network can communicate directly with each other without the need for routing between subnets or VLANs.

    Limited Segmentation and Isolation:

        Without VLANs, there is limited segmentation and isolation of network traffic.

        Devices in different departments, groups, or security zones share the same broadcast domain and have unrestricted access to each other’s traffic, which can present security and performance challenges.

    Broadcast Storms and Traffic Congestion:

        In networks without VLANs, broadcast storms can occur if a device generates a large amount of broadcast traffic, overwhelming the network and causing performance degradation.

        Similarly, network congestion can occur as all devices share the same network bandwidth, leading to potential bottlenecks.



```

## With VLANs
```
Networks with VLANs (Virtual Local Area Networks) offer greater flexibility, security, and efficiency compared to traditional networks without VLANs. VLANs allow network administrators to logically segment a single physical network into multiple virtual networks, each with its own broadcast domain.

    Logical Segmentation:

        VLANs allow network administrators to logically segment the network into multiple broadcast domains, regardless of the physical network topology. Devices within the same VLAN can communicate with each other as if they were on the same physical network segment, while traffic between VLANs typically requires routing.

        When VLANs are implemented on a switch, the transmission of unicast, multicast, and broadcast traffic from a host in a particular VLAN are restricted to the devices that are in that VLAN only.

    Broadcast Isolation:

        Each VLAN forms a separate broadcast domain, reducing the scope of broadcast traffic. Broadcast traffic generated within a VLAN is only forwarded to devices within that VLAN, improving network efficiency and reducing unnecessary traffic on other VLANs.

    Enhanced Security:

        VLANs provide enhanced security by segregating network traffic and controlling communication between different groups of devices. Access control lists (ACLs) and firewall policies can be applied at VLAN boundaries to restrict traffic flow between VLANs based on security policies.

    Improved Performance:

        By dividing the network into smaller broadcast domains, VLANs can reduce broadcast traffic and network congestion, leading to improved performance and better overall network efficiency.

    Flexibility:

        VLANs provide flexibility in network design and management, allowing administrators to easily add, remove, or modify VLAN configurations without physical reconfiguration of network infrastructure.

        All the "tagging" processes are completely transparent to the "user" and is handled by the intermediary network devices.

        When the switch receives a frame on a port configured in access mode and assigned a VLAN, the switch will then determine what interface to send the frame out. If the outgoing interface happens to be a trunk port, the switch inserts the VLAN tag in the frame header, recalculates the Frame Check Sequence (FCS), and sends the tagged frame out of that trunk port. Inversely, when a switch receives a tagged frame from a trunk link and it determines that the outgoing interface is an access port, the switch will remove the vlan tag and the FCS is recalculated again. The Type field is also reverted back to its original value. The 4-byte tag is removed and the Type field reverts back to its original location at [12:2].

```

## VLANs 802.1AD Double Tagging

![image](https://github.com/user-attachments/assets/0a9911f1-a0ad-401f-996c-0bdea2dc199c)

```


IEEE 802.1ad is an Ethernet networking standard informally known as "Q-in-Q". The was added as an amendment to IEEE standard IEEE 802.1Q-1998. This technique was commonly used for provider bridging or tagging. A service provider could tag already tagged user frames across a service providers network and then strip it off at the other end; this is a form of tunneling.

This technique allowed the ability to insert more than one 4 byte tag into the frame. Each additional tag is inserted before the previous tag. The tags are then removed in reverse order. The first tag will be the typical 0x8100 Ethertype and include the user provided VLAN ID. Each additional tag will use 0x88A8 (standard) or 0x9100 (non-standard) Ethertype and include the provider’s VLAN ID.

    Standard VLAN Tagging (IEEE 802.1Q):

        In a standard VLAN tagging scenario, each Ethernet frame includes a 4-byte VLAN tag inserted between the source MAC address and the EtherType/Length field.

        Ethertype uses is 0x8100.

        This VLAN tag contains information such as the VLAN ID (VID) that identifies the VLAN to which the frame belongs.

        IEEE 802.1Q supports up to 4096 VLANs (VLAN IDs 1-4094), allowing network administrators to segment a network into multiple virtual LANs.

    QinQ VLAN Tagging:

        QinQ extends VLAN tagging by adding another layer of VLAN tags, effectively allowing VLAN tagging within VLAN tagging.

        In a QinQ scenario, the original Ethernet frame is encapsulated within another VLAN tag, creating a "tagged outer frame" with its own VLAN ID.

        This outer VLAN tag provides a second level of VLAN identification, allowing for hierarchical VLAN structures.

        The original VLAN tag remains intact, providing the VLAN segmentation information within the inner frame.

        Outer VLAN tag uses the Ethertype of 0x88A8.

    Usage and Benefits:

        QinQ VLAN tagging is commonly used in service provider networks, particularly in metro Ethernet deployments.

        It allows service providers to deliver multiple customer VLANs transparently over a single Ethernet link, preserving the VLAN segmentation of each customer.

        By using QinQ, service providers can avoid VLAN ID conflicts between different customers' VLANs and simplify VLAN management.

        QinQ also enables the creation of "service VLANs" or "provider VLANs" to carry traffic from multiple customer VLANs over a shared infrastructure while maintaining isolation between customers.

    Frame Format:

        In QinQ VLAN tagging, the Ethernet frame contains two 802.1Q headers:

        The outer VLAN tag (or "service tag") contains the service provider’s VLAN ID.

        The inner VLAN tag (or "customer tag") contains the customer’s VLAN ID.

        The outer VLAN tag precedes the inner VLAN tag, and the original Ethernet frame is encapsulated between them.

    IEEE 802.1ad was created for the following reasons:

        802.1Q has a 12-bit VLAN ID field, which has a theoretical maximum of 4096 tags (212). With the growth of network this has become a limitation. A double-tagged frame however has two 12 byte VLAN ID fields. This can have a theoretical max of 4096×4096 or 16,777,216 VLAN IDs.

        A tag stack creates a mechanism for some Internet Service Providers to encapsulate customer tagged 802.1Q traffic within another tag thus creating a Q-in-Q frame. The second (outer tag) is used to identify and segregate traffic from different customers; the inner tag is preserved from the original frame.

        Using Q-in-Q provides a means of constructing Layer 2 tunnels, or even applying Quality of service (QoS) policies.

        802.1ad is upward compatible with 802.1Q. Although 802.1ad is limited to two tags, there is no ceiling on the standard limiting a single frame to more than two tags, allowing for growth in the protocol. In practice Service Provider topologies often anticipate and utilize frames having more than two tags.

        It is easier for networking equipment makers to modify their existing equipment by creating multiple 802.1Q headers than to modify their equipment to implement some hypothetical new non-802.1Q extended VLAN ID field header.

```

## EXPLOIT VLAN Hopping



VLAN hopping Attack

VLAN hopping is an exploit method of attacking networked devices on separate virtual LAN (VLAN) without traversing a router or other Layer 3 device. The concept behind VLAN hopping attacks is for the attacker on one VLAN to gain access to traffic on other VLANs that would normally not be accessible. Keep in mind that VLAN hopping is typically a one-way attack. It will not be possible to get any response from the target device unless methods are setup on the target to respond with similar vlan hopping methods.

There are three primary methods of VLAN hopping:

Switch Spoofing

In this attack, an attacking host imitates a trunking switch by crafting Dynamic Trunking Protocol (DTP) frames in order to form a trunk link with the switch. With a trunk link formed the attacker can then use tagging and trunking protocols such as ISL or 802.1q. Traffic for all VLANs is then accessible to the attacking host.

```
                switch(config)# interface fastethernet 1/10
                switch(config-if)# switchport mode access
                switch(config-if)# switchport nonegotiate
                switch(config-if)# switchport access vlan 10
                switch(config)# iterface gigabit 0/1
                switch(config-if)# switchport trunk encapsulation dot1q
                switch(config-if)# switchport mode trunk
                switch(config-if)# switchport nonegotiate
```

Tagging

This attack typically requires the attacker add the target 802.1Q tag manually to an Ethernet frame even though it is an access port. This process is normally done by the switch. The switch will receive the frame and forward it out the trunk port leading to the target without it needing to be routed. This method requires that the attacker and victim are separated by a trunk and success depends on the switch firmware being vulnerable.

Double Tagging

This attack works if the attacker knows what the "native VLAN" that is used on your organization. Typically VLAN 1 is used. All VLANs will be "tagged" with its corresponding VLAN. The Native VLAN however is intended for local network communication and is not tagged. Thus anything tagged for the native VLAN will be stripped off. The attacker will insert 2 tags into their frames. The first tag will be for the Native VLAN and the second tag will be for whatever VLAN he is trying to access. Upon receipt the switch will then remove the Native VLAN tag and will leave the second VLAN tag in tact. This method also requires that the attacker and victim be separated by a trunk and a vulnerable switch.
```
                switch(config)# vlan dot1q tag native
                switch(config)# interface fastethernet 1/10
                switch(config-if)# switchport mode access
                switch(config-if)# switchport nonegotiate
                switch(config-if)# switchport access vlan 10
                switch(config)# iterface gigabit 0/1
                switch(config-if)# switchport trunk encapsulation dot1q
                switch(config-if)# switchport mode trunk
                switch(config-if)# switchport nonegotiate
                switch(config-if)# switchport trunk native vlan 999

```

# ARP 
Address Resolution Protocol: quick way to resolve MAC to IP Addresses



## Offset

![image](https://github.com/user-attachments/assets/db3f02d6-a276-4d67-8ecf-0100741a4c6f)

```


    Structure:

        Hardware type (HTYPE) This field specifies the network link protocol type.

            1 = Ethernet

            6 = Token Ring

            15 = Frame Relay

        Protocol type (PTYPE) This field specifies the internetwork protocol for which the ARP request is intended. The permitted PTYPE values share a numbering space with those for EtherType.

            0x0800 = IPv4

        Hardware length (HLEN) Length (in octets) of a hardware address.

            6 = Byte size of Ethernet MAC addresses.

        Protocol length (PLEN) Length (in octets) of addresses used in the upper layer protocol. (The upper layer protocol specified in PTYPE.)

            4 = Byte size of IPv4 addresses.

        Operation Specifies the operation that the sender is performing:

            1 = ARP request

            2 = ARP reply

            3 = RARP request

            4 = RARP reply

        Sender hardware address (SHA) Media address of the sender. In an ARP request this field is used to indicate the address of the host sending the request. In an ARP reply this field is used to indicate the address of the host that the request was looking for. (Not necessarily address of the host replying as in the case of virtual media.) Switches do not pay attention to this field, particularly in learning MAC addresses. The ARP PDU is encapsulated in Ethernet frame, and that is why Layer 2 devices examine it.

            In a ARP request, this will be the requestor’s MAC address.

            In a ARP reply, this will be the target’s MAC address.

        Sender protocol address (SPA) Internetwork address (usually IPv4 Address) of the sender.

            In a ARP request, this will be the requestor’s IP address.

            In a ARP reply, this will be the target’s IP address.

        Target hardware address (THA) Media address of the intended receiver. In an ARP request this field is ignored. In an ARP reply this field is used to indicate the address of the host that originated the ARP request.

            In a ARP request, this will be blank.

            In a ARP reply, this will be the requestor’s MAC address.

        Target protocol address (TPA) Internetwork address (usually IPv4 Address) of the intended receiver.

            In a ARP request, this will be blank.

            In a ARP reply, this will be requestor’s IP address.


```

## Types
```
ARP (OP 1 and 2)
 
RARP (OP 3 and 4)

Proxy ARP (OP 2)

Gratuitous ARP (OP 2)
```

```


ARP - A request and response in order to resolve the destination L2 (MAC) address when only the destination L3 (IPv4) address is known.

    ARP Request Operation code = 1

    ARP Reply Operation code = 2

    ARP Request:

        When a device needs to communicate with another device on the same network segment but only knows the destination’s IP address, it broadcasts an ARP request message to the entire network.

        The ARP request contains the sender’s IP address and MAC address and the IP address of the target device.

    ARP Reply:

        The device with the IP address specified in the ARP request responds with an ARP reply.

        The ARP reply contains the target device’s MAC address.

        Once the sender receives the ARP reply, it can use the MAC address to address frames destined for the target device.

RARP - A request and response in order to resolve the destination L3 (IPv4) address when only the destination L2 (MAC) is known. (This protocol has been deprecated since the widespread use of protocols like BOOTP and DHCP.)

    RARP Request Operation code = 3

    RARP Reply Operation code = 4

    When a device boots up and has no configured IP address, it broadcasts a RARP request onto the local network.

    The RARP request contains the device’s MAC address.

    RARP servers on the network receive the broadcast request and check their tables for a corresponding IP address entry associated with the MAC address.

Gratuitous ARP - An ARP reply that was not requested.

    ARP Reply Operation code = 2

    A gratuitous ARP messages is an ARP messages sent by a device to announce its own IP-to-MAC address mapping to other devices on the network.

    Gratuitous ARP messages are commonly used during network initialization or to update ARP caches in other devices.

    These are commonly used for:

        Help in detecting IP conflicts

        Assist in updating other system’s ARP cache

        To inform switches of the MAC address of the client connected to its port

        Helps pre-load other systems ARP cache when the local systems IP interface comes up

    Maliciously used to:

        Poision a victim’s ARP cache

Proxy ARP - A device (router) answers the ARP queries for IP address that is on a different network.

    The ARP proxy sees the ARP request and determines that the target Network address is not on the local network segment and is aware of how to reach the destination network.

    The proxy will offer its own MAC address in response to the request.

    Typically this device is the network gateway and is responsible to forward traffic for other networks.

    Maliciously the ARP requests can be intercepted and a Proxy ARP sent as a response to poision the victim’s ARP Cache.

ARP Cache - is a collection of Layer 2 to Layer 3 address mappings discovered utilizing the ARP request/response process. When a host needs to send a packet both the L2 and L3 addresses are needed. The host will look in this table to determine if it already knows both the L2 and L3 addresses. If the target is not in the table then a ARP request is initiated. The ARP cache can be populated statically but mostly its done dynamically. This cache can be exploited by attackers with the aim to poison the cache with incorrect information to either perform a DoS or MitM.

```


## ARP Cache
```
All resolved MAC to IP Addresses
If MAC is not in cache then ARP is used
Dynamic entries last from 2-20mins
Default gateway is present at minimum
Can be easily duped by attackers

```

## EXPLOIT MITM with ARM

```


    Address Resolution Protocol (ARP) attack using Gratuitous ARPs

When ARP was developed security was not as much of an issue. Over time it was discovered that many protocols could be used in unintended ways. Typically a host will broadcast an ARP request over the network and expects only the intended host to respond. Gratuitous ARP on the other hand is another method that a host can announce itself to the network. All other hosts believe the message and will add this entry into their ARP cache. These are the legitimate uses of ARP but malicious actors can use the open, unencrypted, and unverified nature of the protocol to their own ends.

An attacker can broadcast a gratuitous ARP, announcing itself as the networks default gateway. It will use the legitimate default gateway’s IP address but will use it’s own MAC address. All hosts on the network will assume this information to be true and update their ARP caches. This in essence will poison everyone’s ARP cache. All hosts on the network will now send all traffic to other networks to the attackers computer. The Attacker will forward all traffic to the legitimate gateway but now the attacker is included in the hosts communication.

This process creates a Layer 2 Man in the Middle.


    Proxy ARP and Security Concerns:

Typically a PC will issue an ARP request to get the unknown MAC address of a device when its IP address is known. If the device is on the same network then that device will respond with ARP Reply. If the device happens to be on a different network, the router will respond with its own MAC address. The router responds because it will see that the destination IP address is on a different network and it knows how to get there from its routing tables. The router will respond to the ARP request with its own MAC to tell the host to send all the communication to itself to get to the remote destination. The host will update its ARP cache to reflect the router (default gateway) to be used to reach remote destinations. This is called a Proxy ARP.

An attacker can intercept ARP requests for a gateway and respond with its own MAC address resulting in a Man in the Middle attack.


```


# VTP 
```
CISCO Proprietary
MODES:

Server
Client
Transparent

```
## VLAN Trunking Protocol
Simplifies an administrators job

![image](https://github.com/user-attachments/assets/aa27e9b7-0a71-4a89-a25a-ef0ec9b8771e)

```
Centrally manage everything

VLAN Trunking Protocol (VTP) is a Cisco proprietary protocol that propagates the definition of Virtual Local Area Networks (VLAN) on the whole local area network. VLAN Trunk Protocol (VTP) was developed to help reduce the administration of creating VLANs on all switches within a switched network. To do this, VTP sends VLAN information to all the switches in a VTP domain.

    Server - can create, modify or delete VLANs. Can create and forward VTP messages.

    Client - can only adopt VLAN information in VTP messages. Can forward VTP messages.

    Transparent - only forwards VTP messages but does not adopt any of the information.

VTP advertisements are sent over all trunk links. VTP messages advertise the following on its trunk ports:

    Management domain

    Configuration revision number

    Known VLANs and their specific parameters

There are three versions of VTP, version 1, version 2, version 3.

```

## VTP Issues
```
Can dumkp all VLAN information
Cause a DoS as a switch will not support conifured VLANs

VTP uses the configuration revision number to determine what is the most "up-to-date" VLAN information. Each time the server makes an update it will send a VTP message with a higher revision number. The other switches will see that the message revision number is higher than what they have recorded so they will adopt the information in the message believing it to be more current.

The concern is that if you add a new switch to the current VTP domain that has a higher VTP revision number. This could be because it was previously on another VTP domain and was not properly erased. Once connected, that switch will not accept any VTP messages from the server since its revision number is higher. But when that switch sends its own VTP message advertising what it believes the current revision number is, all the other switches will see that it has a higher revision number and will cause all switches to dump all their information and request the information from the new switch. This in effect will bring down your entire VLAN infrastructure.

Additionally, an attacker can use this same process to perform a Denial of Service on your VTP-switched network. The attacker can craft their own VTP message and send it over the network. This will cause all the switches in the VTP domain to flush all their VLAN information. This however does not change the VLANs assigned to the ports. The ports will stay assigned to the programmed VLANs. The switch however will no longer be forwarding traffic for those VLANS so the hosts will be isolated until the VLANs are re-introduced to the switch.



```


# DTP
## Dynamic Trunking Protocol
Used to dynamically create trunks when it sees trunk data

```
Modes:

Dynamic - Auto (DEFAULT)

Dynamic - Desirable

Can disable by using NO NEGOTIATE    
```

![image](https://github.com/user-attachments/assets/67423205-f7ba-423c-b478-11663a5afb4d)



# CDP, FDP, LLDP
## Cisco Discovery Protocol
```


Cisco Discovery Protocol (CDP) is a Layer 2, Cisco proprietary protocol used to share information with other directly connected Cisco devices. CDP is protocol and media independent and runs on all Cisco routers, switches, and other devices.

    CDP Shares information such as:

        Type of device

        Hostname

        Number and type of interface

        IP address

        IOS software version

    CDP can be used as a Network Discovery tool as well as assist in network design decisions and troubleshooting.



```

## Foundry Discovery Protocol
```
Foundry Discovery Protocol (FDP) is a proprietary data link layer protocol, originally developed by Foundry Networks, which was bought by Brocade. Similar to CDP, FDP enables Brocade devices to advertise to other directly connect Brocade devices on the network.
```


## Link Layer Discovery Protocol
```
Link Layer Discovery Protocol (LLDP) was designed by IEEE 802.1AB to be a vendor-neutral neighbor discovery protocol similar to CDP. LLDP also operates at layer 2 and shares similar information as does CDP with directly connected devices that support LLDP.
```

## EXPLOIT CDP Attack
```


Due to the nature of how CDP works, it can be easily used by malicious actors to map out your network infrastructure. It also shares alot of device information that an attacker can use in preparation of an attack; information like IP addresses, router models, software versions and so on can be sensitive for your organization. All information is sent in clear text and unauthenticated. Any attacker sniffing the network is able to see this information and is possible to impersonate (spoof) another device.

It is recommended to disable CDP/LLDP if not needed in your organization. It is however required for many VOIP phones to operate. Cisco VOIP send CDP messages to the switch. This is how switches know to place the phones on the "voice" vlan and not the "data" vlan.

    Disable Globally with no cdp run

    Disable on an interface with no cdp enable




```

# STP
## Spanning Tree Protocol
![image](https://github.com/user-attachments/assets/6244b64c-cf77-4a90-a8b8-34f8c536551d)

```
ROOT - Has access to the internet
Every port gets assigned a value
R - is to the Root Device
D - is for designated traffic
Without STP it would potentially get sent an undesirable path to find the router out
You can have a secondary Root
```
```


We previously mentioned that there is no TTL at Layer 2 to eventually kill a frame that never reaches its destination. This will result in frames endlessly circulating a L2 infrastructure and eventually bringing down the network. This can be caused by simply adding redundant links in your network architecture that could allow frames to potentially circulate.

Spanning Tree Protocol (STP) (802.1D) was developed to resolve this issue. STP is a Layer 2 protocol that builds a loop-free logical topology for Ethernet networks in a network that physically has loops. The basic function of STP is to prevent switching loops and the broadcast storms that can result. Spanning tree allows a network design to include physical "backup links" to provide fault tolerance if the active link fails.

STP works by creating "tree" within a network of connected layer-2 switches, and disable any links that are not part of this tree. The root of the tree determined by electing a Root Bridge and all the other switches are the branches. This essentially leaves only a single active path between any two network switches. STP is based on the algorithm invented by Radia Perlman.

STP operates by flooding Bridge Protocol Data Units (BPDUs) to all other switches in the network. BPDUs consist of:

    Switches priority value (default 32768. Lower numbers are preferred.)

    MAC address (lowest one on the switch. Lower MAC address are preferred.)


These BPDUs are used to:

    Elect the Root Bridge

    Identify the Root port on each non-root bridge

    Identify the Designated port for each segment


After the election of the Root Bridge, all BPDUs will come from the root only and each switch will forward these BPDUs out their Trunk ports. This ensures that all switches know that the root is still active.

IEEE introduced Rapid Spanning Tree Protocol (RSTP) as 802.1w in 2001. RSTP allowed ports to transition from blocking to forwarding in about 10 seconds.

In 2005, the IEEE introduced 802.1s, alternatively referred to as Multiple Spanning Tree Protocol (MSTP), extending the foundational Spanning Tree Protocol (STP) delineated by IEEE 802.1D. MSTP enriches STP by enabling the mapping of multiple VLANs to a solitary spanning tree instance, thereby aiding in the optimization of network assets and the acceleration of convergence time.

```


## STP Versions
```


    Open Standards-Based Versions:

        STP (802.1D):

            Open standard defined by the IEEE 802.1D specification.

            Basic version of the Spanning Tree Protocol, widely supported by networking equipment from various vendors.

            Defines the original spanning tree algorithm for loop prevention in Ethernet networks.

            Convergence Time: 30 to 50 seconds.

        RSTP (802.1w):

            Open standard defined by the IEEE 802.1w specification.

            Improves upon the original STP by providing faster convergence and better performance.

            Offers faster link failover times and better utilization of redundant links compared to STP.

            Widely supported across networking equipment from multiple vendors.

            Convergence Time: 6 seconds or less.

        MSTP (802.1s):

            Open standard defined by the IEEE 802.1s specification.

            Extends RSTP to support multiple spanning tree instances, each of which can encompass multiple VLANs.

            Helps reduce the number of spanning tree instances needed in large networks with multiple VLANs, improving scalability and manageability.

            Convergence Time: Similar to RSTP (6 seconds or less).

    Cisco Proprietary Versions:

        Per-VLAN Spanning Tree (PVST) and PVST+ (Per-VLAN Spanning Tree Plus):

            Proprietary spanning tree protocol developed by Cisco.

            PVST and PVST+ extend the functionality of STP by creating a separate spanning tree instance for each VLAN.

            Allows for finer control over spanning tree behavior on a per-VLAN basis, optimizing network performance and stability.

            Convergence Time: Typically similar to STP (30 to 50 seconds).

        Rapid Per-VLAN Spanning Tree (Rapid PVST):

            Cisco’s proprietary version of RSTP, tailored for use with PVST+.

            Offers faster convergence and better performance compared to traditional PVST+.

            Provides rapid failover times for individual VLANs, enhancing network resilience and uptime.

            Convergence Time: Typically similar to RSTP (6 seconds or less).

        Cisco Multiple Spanning Tree Protocol (MSTP) Implementation:

            Cisco offers its implementation of MSTP, which is compatible with the IEEE 802.1s standard.

            Allows Cisco devices to participate in MSTP environments alongside equipment from other vendors.

            Offers enhanced features and integration with other Cisco networking technologies.

            Convergence Time: Typically similar to RSTP (6 seconds or less).




```


## STP BPDUs
```


Spanning Tree Protocol (STP) uses Bridge Protocol Data Units (BPDUs) to exchange information between switches and determine the topology of the network. BPDUs contain vital information necessary for STP operation, including bridge IDs, port IDs, path costs, and other parameters.

    Contents of a BPDU:

        Bridge ID (BID):

            The BID uniquely identifies each bridge (switch) in the network and consists of two components: bridge priority and bridge MAC address.

            The bridge priority is a numerical value (default is 32768) used to determine the root bridge.

            The bridge MAC address is the MAC address of the bridge.

        Port ID:

            The Port ID uniquely identifies each port on a bridge.

            It consists of two components: port priority and port number.

            The port priority is a numerical value (default is 128) used to determine the designated port.

            The port number is the identifier of the port on the bridge.

        Path Cost:

            The path cost represents the cumulative cost of the path from the sending bridge to the root bridge.

            Each port calculates its path cost based on the speed of the link. For example, a higher speed link (e.g., Gigabit Ethernet) has a lower path cost than a lower speed link (e.g., Fast Ethernet).

        Root Bridge ID:

            The Root Bridge ID (RID) is the bridge ID of the root bridge, which is initially set to the bridge ID of the sending bridge.

            As BPDUs propagate through the network, switches update the RID in the received BPDUs to reflect the bridge ID of the root bridge.

        Message Type:

            BPDUs can be either Configuration BPDUs or Topology Change Notification (TCN) BPDUs.

            Configuration BPDUs are used for regular STP operations, such as root bridge election, topology discovery, and path selection.

            TCN BPDUs are used to notify other switches of changes in the network topology, such as link failures or port state changes.

    BPDU Exchange Process:

        Transmission:

            Each switch sends BPDUs out of all its designated ports at regular intervals (hello time), usually every 2 seconds by default.

            BPDUs are sent as multicast frames to the well-known address 01:80:C2:00:00:00.

        Reception:

            Switches receive BPDUs from neighboring switches on their designated ports.

            Upon receiving a BPDU, a switch compares the information in the BPDU with its own information to determine the best path to the root bridge.

        Processing:

            Switches process incoming BPDUs to update their internal spanning tree information, including root bridge selection, port roles (root, designated, or blocked), and path costs.

            After the root bridge election, only the root will transmit BPDUs and non-root switches will process the BPDUs sent by the root.

        Decision Making:

            Based on the information in received BPDUs, switches make decisions about the state of their ports (forwarding, blocking, or listening/learning) and adjust their forwarding tables accordingly.

            Switches use BPDUs to decide the root bridge in a STP environment. They determine the root as the one with the lowest priority. If there is a tie for priority then the lowest MAC address is used.


```

## Spanning Tree Attack

```


Spanning Tree Denial of Service attack.

Its goal is to disrupt the switch’s spanning-tree process, destabilize their CAM tables and hold the network in a repetitive state of re-electing the root bridge. This is possible because there is no authentication mechanism built into the STP and its BPDU frames.

This is done by repeatedly sending (crafted) Topology Change Notification (TCN) messages that will disrupt the system’s current understanding of the network. This will force renegotiation of the Root Bridge, resulting in a DoS attack because of the 50 second time period it takes to recalculate.


Root Bridge Election Manipulation

Another option is for the attacker to try to become the root bridge. Depending on the location of the attacker’s system, this can have a dramatic effect on the traffic flow throughout the L2 network. This can potentially cause traffic to traverse towards or thru the attacker’s device.

This attack can be done by sending specially crafted BPDUs by giving itself a more preferred BPDU. Typically specifying a lower priority value. Once this is accomplished it is possible for the attacker to see packets that are sent through them. This requires the attacker to stay connected to two switches, running bridging software, so that they can continue to send the BPDU to advertise themselves as the root bridge.


Both attacks require that the attacker be physically connected to the network.

The industry standard of 802.1D there is only 1 spanning tree instance no matter how many vlans are running on the network. So to attack STP will affect every vlan in the network. However Cisco’s proprietary STP called PVST and PVST+, there is a spanning tree instance for each vlan in the network. So to attack one will not affect the others. Each vlan spanning tree instance would need to be attacked for a full network DoS.

To mitigate STP attack you can:

    Enable portfast to have a port immediately come up to the forwarding state.

        Globally by using spanning-tree portfast default

        By interface using spanning-tree portfast

    Enable BPDU guard to prevent BPDUs from beign allowed on a switchport.

        On each access port interface use spanning-tree bpduguard enable

        Must not use this command on any trunk or switch to switch connections.


```

# Port Security
## Modes
```


The following are the possible modes:

    protect - Drops any frames with an unknown source addresses.

    restrict - Same as protect except it additionally creates a violation counter report.

    shutdown - Places the interface into an "error-disabled" state immediately and sends an SNMP trap notification. This is typically the default mode.


```

## Info
```


The purpose of configuring port security technologies is to limit, restrict, and protect network access. Configuring port security can be done on active access ports to limit the number of users or MAC addresses allowed to access onto the network. This will help to alleviate attacks such as DoS, MAC Address Flooding, and most unauthorized access.

    MAC Address Limit:

        Port security allows administrators to specify the maximum number of MAC addresses allowed on a switch port.

        When enabled, the switch monitors the MAC addresses of devices connected to the port and takes action if the number of MAC addresses exceeds the configured limit.

    MAC Address Learning:

        When a device sends traffic through a switch port, the switch learns the device’s MAC address and associates it with the port.

        The switch maintains a table, known as the MAC address table or CAM table, which maps MAC addresses to switch ports.

    Violation Actions:

        Administrators can define violation actions to be taken when port security violations occur.

        Common violation actions include shutting down the port, sending an SNMP trap, or logging a message.

        These actions help alert administrators to potential security breaches and mitigate unauthorized access attempts.

        The following are the possible modes:

            protect - Drops any frames with an unknown source addresses.

            restrict - Same as protect except it additionally creates a violation counter report.

            shutdown - Places the interface into an "error-disabled" state immediately and sends an SNMP trap notification. This is typically the default mode.


```

# Layer 2 Mitigation (Best Practices)
## Best Practices
The following are some mechanisms that can be be configured to better secure your switched network:

## Shutdown unused ports - 
Bare minimum to secure access ports is to simply shut down any and all inactive ports.
```
    interface fastethernet 0/1
    shutdown
```
## Switchport Port Security - 
Can be used to limit the number of MAC addresses that can be dynamically learned on a port or static MAC addresses can be assigned to one. Violation modes of shut down can be used to secure the port should a violation occur.
```
    switchport port-security
    switchport port-security maximum 1
    switchport port-security mac-address sticky
    switchport port-security violation shutdown
```
## IP Source Guard - 
Mitigates the effects of IP address spoofing attacks on the Ethernet LAN. With IP source guard enabled, the source IP address in the packet sent from an untrusted access interface is validated against the DHCP snooping database. If the packet cannot be validated, it is discarded.
```
    interface fastethernet 0/1
    ip verify source
    ip source binding 0100.0230.0002 vlan 11 10.10.0.40 interface fastethernet 0/1
```
## Manually assign STP Root - 
Manually assign the Spanning Tree Protocol (STP) root bridge allows for a deterministic root bridge election rather than the bridge with the lowest bridge priority. This allows the central most switch to be the root that will best allow traffic to flow in an efficent manner.
```
    spanning-tree vlan <vlan-id> priority 0
```
## BPDU Guard - 
BPDU Guard is a feature used in network switches to enhance network security by protecting against unintentional loops and rogue devices. It works by automatically shutting down a port if it receives Bridge Protocol Data Units (BPDUs), which are indicative of spanning tree protocol (STP) activity.
```
    interface fastethernet 0/1
    spanning-tree bpduguard enable
```
## DHCP Snooping - 
DHCP Snooping is a security feature commonly found in network switches that helps prevent rogue or unauthorized DHCP servers from distributing incorrect or malicious IP configuration information to network clients. It operates by monitoring and controlling DHCP messages exchanged between DHCP clients and servers. Configuration is done on ports that are connected to (or leading to) the DHCP server.
```
    ip dhcp snooping
    interface fastethernet 0/1
     ip dhcp snooping trust
     ip dhcp snooping vlan <vlan-id>
```
## 802.1x - 
The 802.1x standard defines a client-server-based access control and authentication protocol that prevents unauthorized clients from connecting to a LAN through ports until they are properly authenticated. The authentication server authenticates each client connected to a switchport before making available any services offered by the switch or the LAN.
```
    aaa new-model
    aaa authentication dot1x default group radius
    dot1x system-auth-control
    identity profile default

    interface fastethernet 0/1
    access-session port-control auto
    dot1x pae authenticator
```
## Dynamic ARP inspection (DAI) -
Prevents Address Resolution Protocol (ARP) spoofing or “man-in-the-middle” attacks. ARP requests and replies are compared against entries in the DHCP snooping database, and filtering decisions are made on the basis of the results of those comparisons.
```
    ip arp inspection vlan {vlan-id> | <vlan-range>}

    interface fastethernet 0/1
    ip arp inspection [ trust | untrust ]

    ip arp inspecion filter <arp-acl-name> vlan {vlan-id> | <vlan-range>} [static]
```
## Static CAM entries - 
Static CAM (Content Addressable Memory) entries refer to manually configured entries in the CAM table of Ethernet switches. These entries map specific MAC addresses to specific switch ports and are used to optimize network performance and facilitate specific network configurations.
```
    mac-address-table static 1234:abcd:5678 vlan 1 interface fastethernet 0/1
```
## Static ARP entries - 
Static ARP (Address Resolution Protocol) entries are manually configured mappings between IP addresses and MAC addresses in the ARP table of network devices. These entries are used to ensure stable communication between specific devices on the network.
```
    Linux:
    sudo ip neighbor add 10.10.0.50 lladdr 11:22:33:44:55:66 nud permanent dev eth0
    sudo ip neighbor delete 10.10.0.50 lladdr 11:22:33:44:55:66 nud permanent dev eth0

    Windows:
    arp -s 10.10.0.50 11:22:33:44:55:66
```
## Disable DTP negotiations - 
To disable Dynamic Trunking Protocol (DTP) negotiations on a Cisco switch interface, you need to manually configure the interface as an access port or set it to operate in a specific trunking mode, such as "trunk" or "nonegotiate."
```
    interface fastethernet 0/1
     switchport mode trunk
     switchport nonegotiate

    interface fastethernet 0/2
     switchport mode access
     switchport nonegotiate
```
## Manually assign Access/Trunk ports - 
By default, switch ports can be either a trunk or access port depending on the device connected to the port and dynamic negotiations that take place. Manually assigning ports as either trunk or access ports provides greater control and ensures that the network operates as intended.
```
    interface fastethernet 0/1
     switchport mode trunk
     switchport nonegotiate

    interface fastethernet 0/2
     switchport mode access
     switchport nonegotiate
```



 
