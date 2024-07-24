# Networking
----
## Sites:
CTFD - MASO-M-005@10.50.20.180:8000/challenges

CTFD Resources - http://10.50.20.180:8000/resources

CTFD Practice - http://networking-practice-ctfd.server.vta:8000/

CTCC Network - https://net.cybbh.io/public/networking/latest/schedule.html

xfreerdp /v:10.50.x.x /u:student /p:password /size:1920x1000 +clipboard

Subnet Chart: https://www.engineeringradio.us/blog/wp-content/uploads/2013/01/Subnet_Chart.pdf

Miro Whiteboard - https://miro.com/app/board/o9J_klSqCSY=/?share_link_id=16133753693

---

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

## OSI Model

























































































































































































































































----





























