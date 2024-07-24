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


# Ethernet Timing (BIT-TIME)
Bit Time - is the period of time is required for a bit to be placed and sensed on the media. Network speeds are measured by how many bits can be placed or sensed on the media in 1 second. Each increase in speed requires more bits to be sent during the same 1 second internal. To accomplish this the bit-times are reduced.

```
Speed       Bit-Time
10 mbps     100ns
100 mbps    10ns
1 Gbps      1ns
10 Gbps     .1ns
100 Gbps    .01ns
```

#













 
