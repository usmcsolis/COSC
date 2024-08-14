# Security
## Information
```
CTFD:
http://10.50.20.30:8000/
http://10.50.20.30:8000/challenges

Cybbh:
https://sec.cybbh.io/public/security/latest/index.html

Stack:
16

Username:
MASO-005-M

Password:
W5KhuRv7dByR2Lk

Jumpbox:
10.50.39.67

windows_opstation_em90
192.168.65.10
10.50.21.242

lunix_opstation_em90 (password = password)
192.168.65.20
10.50.37.42

ssh student@10.50.37.42 -X

STACK Website:
vta.cybbh.space
ipa
```

## Control Sockets (Demo)

```
## Set up control socket
ssh -MS /tmp/jump student@10.50.39.67


## Ping Sweep
for i in {97..137}; do (ping -c 1 192.168.28.$i | grep "bytes from" &); done


## Dynamic Port Forward
ssh -S /tmp/jump jump -O forward -D 9050


## NMAP to find IP ports
proxychains nmap 192.168.28.100


## Port Interrigation
proxychains nc 192.168.28.129
proxychains nc 192.168.28.129 2222
proxychains wget -r http://192.168.28.129


## Creating Port Forwarding to host Alt Ports
ssh -S /tmp/jump jump -O forward -L 4567:192.168.28.100:80 -L 1234:192.168.28.100:2222


## Cancel Port Forwards
ssh -S /tmp/jump jump -O cancel -L 4567:192.168.28.100:80
ssh -S /tmp/jump jump -O -D 9050
ssh -S /tmp/jump jump -O cancel -L 4567:192.168.28.100:80 -L 1234:192.168.28.100:2222



## Using FIREFOX to see website hosted on .100:80
http://127.0.0.1:4567


## Creating a MS socket to the next hop found on port 2222
ssh -MS /tmp/t1 student@127.0.0.1 -p 1234 
```

# Penetration Testing

https://sec.cybbh.io/-/public/-/jobs/872115/artifacts/slides/01-pentesting-overview.html



## Phase 1: Mission Definition

    Define mission goals and targets.

    Determine scope of mission.

    What networks are valid targets?

    What machines are valid targets?

    What attacks or exploits are authorized/appropriate?

    Define RoE.

## Phase 2: Recon

    Information gathering about the target through public sources.

    Websites, job postings, search engines, etc.

    Done without touching the target.

## Phase 3: Footprinting

    Accumulate data through scanning and/or interation with the target/target resources.

    Use a variety of scanning and fingerprinting to determine information about target networks and devices.

## Phase 4: Exploitation/Initial Access

    Gain intial foothold into target network

    There is a more in-depth discussion that is done in exploitation research lesson

## Phase 5: Post-exploitation

    Establish persistence

    escalate priveleges

    obfuscate

    cover your tracks

    exfiltrate target data

## Phase 6: Document Mission

    Document and report mission details.















































































































































































































