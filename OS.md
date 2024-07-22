# Important 

https://os.cybbh.io/public/os/latest/index.html


http://10.50.22.197:8000

/http://10.50.22.197:8000/

## Stack 8
```
Stack 8 : 10.50.35.48

File Server:
10.8.0.3
student
password

```

 
## TEST Stack 8
```
windows
ssh -X 10.50.39.235


Linux
ssh -X 10.50.31.156
```

## Remote Connection Instructions

```
Admin_station
xfreerdp /u:student /v:10.50.35.48 /dynamic-resolution +glyph-cache +clipboard
student : password

File Server (windows)
ssh -X student@10.8.0.3
student : password

Terra (linux)
ssh -X garviel@10.8.0.6
garviel : luna

Workstation2 (Windows)
ssh -X andy@10.8.0.4
andy.dwyer : BurtMacklinFBI

Minas_Tirith
ssh -X bombadil@10.8.0.7
bombadil : jolly

Workstation 2
ssh -X andy.dwyer@10.8.0.4
andy.dwyer : BurtMacklinFBI
```
```
USER=
IP_ADDRESS=
xfreerdp /u:$USER /v:$IP_ADDRESS> /dynamic-resolution +glyph-cache +clipboard

USER=
IP_ADDRESS=
ssh -X ${USER}@${IP_ADDRESS}

```
```
student
password
```

## Mission Command Console
```
http://10.50.22.197:8000/
```

```
Username: MASO-M-005
Password: 1558758836Abc__1558758836Abc_
```

Join Class:
```
M24005
password
```

# Powershell (Day 1)

verb-noun

do-this


## Get-HOST
```
PS C:\> get-host | select-object Version

Version
-------
5.1.19041.1682
```

## Get-HELP

```
Get-Help                                                          # Displays help about command syntax
Get-Help <about_command_syntax>
```

## Get-Alias

```
Get-Alias <alias>                                                 # Displays aliases for a given command name
Get-Alias dir                                                     # Returns Get-ChildItem
```
 
## Get Object

```
Get-Process | Get-Member                       # Gives the methods and properties of the object/cmdlet
cmdlet).property                               # Command Structure
(Get-Process).Name                             # Returns the single property of 'name' of every process
```

## (Start|Stop)-Process

```
Start-Process Notepad.exe                            # This cmdlet uses the Process.Start Method of the System.Diagnostics.Process class to open notepad.exe
Stop-Process -name notepad                           # This cmdlet uses the Process.Kill Method of the System.Diagnostics.Process class to stop notepad.exe
Get-Process | Select-Object Name, ID, path           # Displays the Get-Process Properties of 'Name, ID, Path' for every process

```

## Where-Object

```
Get-Process | Get-Member | Where-Object {$_.Membertype -match "Method"}       # Displays all objects with Method in their name from the results from Get-Member of the Get-Process cmdlet
```

## .kill()

```
Start-Process calc                              # Open an instance of calculator
(Get-Process calculator*).kill()                # Stops a named process using the kill() method directly
Stop-Process -name calculator*                  # Uses a cmdlet to call the Process.Kill method

```

## CIM

Returns System Information

API CALLS

WMI and CIM classes are almost the same thing

CIM is newer


```
Get-Cimclass *                                                                  # Lists all CIM Classes
Get-CimInstance –Namespace root\securitycenter2 –ClassName antispywareproduct   # Lists the antispywareproduct class from the root/security instance
Get-CimInstance -ClassName Win32_LogicalDisk -Filter “DriveType=3” | gm         # Shows properties and methods for this Instance
Get-WmiObject -Class Win32_LogicalDisk -Filter “DriveType=3”                    # Using the Windows Management Instrumentation method

```

## Do-While
do {<statement list>} while (<condition>)
```
do { Write-Host "----------";
Write-Host "Count = $count";
Write-Host "a = $a";
Write-Host "x=",$x[$a];
$count++; $a++; } while ($x[$a] -ne 0)


Count = 0
a = 0
x= 1
----------
Count = 1
a = 1
x= 2
----------
Count = 2
a = 2
x= 78
```


## Do-Until
do {<statement list>} until (<condition>)
```
do { Write-Host "----------";
Write-Host "Count = $count";
Write-Host "a = $a";
Write-Host "x =",$x[$a];
$count++; $a++; } until ($x[$a] -eq 0)


Count = 0
a = 0
x = 1
----------
Count = 1
a = 1
x = 2
----------
Count = 2
a = 2
x = 78
```

## For Loop
```
for (<Init>; <Condition>; <Repeat>)
{
    <Statement list>
}
```

```
$array = ("item1", "item2", "item3")
for($i = 0; $i -lt $array.length; $i++){ $array[$i] }
item1
item2
item3

```

## For Each
```
$letterArray = "a","b","c","d"
foreach ($letter in $letterArray)
{
  Write-Host $letter
}
```
```
foreach ($file in Get-ChildItem)
{
  Write-Host $file
}
```

## While Loop

```


while (<condition>){<statement list>}



```


```

while($val -ne 3)
{
    $val++
    Write-Host $val
}
#or
while($val -ne 3){$val++; Write-Host $val}
```


## Error Messaging

```
Remove-Item does_not_exist.txt                                         # Displays errors in red
Remove-Item does_not_exist.txt -ErrorAction SilentlyContinue           # Hides any errors
New-Item -Type File it_exists.txt                                      # Creates a new file called 'it_exists.txt'
Remove-Item it_exists.txt -Verbose                                     # Returns a message notifying that it was deleted
```

## Execution Policy
Is what is allowed to run on the powershell


```
Get-ExecutionPolicy -list                                             # Lists all of the Scopes and ExecutionPolicies on the system
Get-ExecutionPolicy                                                   # Gets the current user's ExecutionPolicy
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser  # Sets the ExecutionPolicy for the CurrentUser to Unrestricted

```

## Comparison 

 Equality
	Matching
	Replacement
	Containment
	Type

```
-lt
-le
-gt
-ge
-eq
-ne
-like
-match

```

## Comments

```

Get-Process # comment                                           # Creates a comment beside cmdlet
<# comment                                                      # Begins a multiline comment
|
|
comment #>                                                      # Ends the multiline comment
```


## Profiles

Profile that will load anytime PS is loaded including settings and environemt

```
All User, All Hosts
All User, Current Host
Current User, All Hosts
Current Users, Current Host

$PsHome\Profile.ps1
$PsHome\Microsoft.PowerShell_profile.ps1
$Home\[My]Documents\Profile.ps1
$Home\[My ]Documents\WindowsPowerShell\Profile.ps1
```
Testing the Profiles
```
Test-Path -Path $profile.currentUsercurrentHost
Test-Path -Path $profile.currentUserAllHosts
Test-Path -Path $profile.AllUsersAllHosts
Test-Path -Path $profile.AllUserscurrentHost


```

## Building Powershell Profile

```
function Color-Console {
  $Host.ui.rawui.backgroundcolor = "black"
  $Host.ui.rawui.foregroundcolor = "green"
  $hosttime = (Get-ChildItem -Path $PSHOME\PowerShell.exe).CreationTime
  $hostversion="$($Host.Version.Major)`.$($Host.Version.Minor)"
  $Host.UI.RawUI.WindowTitle = "PowerShell $hostversion ($hosttime)"
  Clear-Host
}
Color-Console
```


## Transcript
History of everything that was entered

```
start-transcript
start-transcript | out-null                       # Pipe to out-null so users don't see that commands are being recorded

Start-Transcript C:\MyWork.txt                    # Starts to log commands into the c:\mywork.txt file
Get-Service                                       # Run get-service command and inputs that and the results into the transcript.
Stop-Transcript                                   # End the transcript
notepad c:\MyWork.txt                             # View the contents of the created transcript

```

Allows you to track everything youve done so if something changes you can say you didnt do it


## Download File (PS)

```
$url = "http://downloads.volatilityfoundation.org/releases/2.6/volatility_2.6_win64_standalone.zip"
$output = "$PSScriptRoot\volatility_2.6_win64_standalone.zip"
$start_time = Get-Date

$wc = New-Object System.Net.WebClient 
$wc.DownloadFile($url, $output) 


(New-Object System.Net.WebClient).DownloadFile($url, $output)

```

# Linux Essentials (Day 2)

## PWD 
```
student:~$ pwd 
/home/student 
```

## Situational Awareness
```
hostname or uname -a displays the name of the host you are currently on.

whoami shows the user you are currently logged in as (useful after gaining access through service exploitation).

w or who shows who else is logged in.

ip addr or ifconfig displays network interfaces and configured IP addresses.

ip neigh or arp displays MAC addresses of devices observed on the network.

ip route or route shows where packets will be routed for a particular destination address.

ss or netstat will show network connections, with the appropriate flags will show listening ports

nft list tables or iptables -L to view firewall rules. (FIREWALL RULES)

sudo -l displays commands the user may run with elevated permissions.

```


## Help

```
help

--help

man

```


## Variables

Assigning 
```

a = 100
echo $a

```

$ is used to call your variable

## Command Substitution

```
student:~$ directories=$(ls /) 
student:~$ echo $directories 
bin   dev  home        initrd.img.old  lib64       media  opt   root  sbin  srv  tmp  var      vmlinuz.old
boot  etc  initrd.img  lib             lost+found  mnt    proc  run   snap  sys  usr  vmlinuz

```


## Redirection

standard input 0 ←--- the default for a command arguments

standard output 1 ←--- the default for successful command output

standard error 2 ←--- the default for failed commands or errors


```

student:~$ ls bacon 
ls: cannot access 'bacon': No such file or directory

workstation21:$ ls bacon 2> errorfile 
workstation21:$ cat errorfile 
ls: cannot access 'bacon': No such file or directory

```


## For Loop

```
student:~$ for item in $objects; do echo $item; done 
/etc/NetworkManager
/etc/PackageKit
/etc/UPower
/etc/X11
/etc/acpi
/etc/adduser.conf
/etc/alternatives
/etc/anacrontab
/etc/apg.conf
/etc/apm
_truncated_

```

## If


```
student:~$ for object in $objects; \ 
do if [ -d $object ]; then echo "$object is a directory"; \ 
else echo "$object is file" ; \ 
fi ; \ 
done 

/etc/X11 is a directory
/etc/acpi is a directory
/etc/adduser.conf is a file
/etc/alternatives is a directory
/etc/anacrontab is a file
/etc/apg.conf is a file
/etc/apm is a directory
/etc/apparmor is a directory

student:~$ for object in $objects; do if [ -d $object ]; then echo "$object is a directory"; else echo "$object is a file" ; fi ; done 
```

## While

```
curtime=$(date +"%s") 
echo $curtime

exittime=$(expr $curtime + 3) 
echo $exittime

while [ $exittime -ge $curtime ]; do echo "To Infinity and Beyond?" ; curtime=$(date +"%s") ; done 
To Infinity and Beyond?
To Infinity and Beyond?
To Infinity and Beyond?
To Infinity and Beyond?
_Truncated_ #It goes for three seconds

```


## File

Can allow you to see what type of file your file are.
elf binary


## /etc/passwd

```

student@linux-opstation-kspt:/bin$ cat /etc/passwd | grep student 
student:x:1001:1001::/home/student:/bin/bash 
 (1)   (2) (3) (4) (5)   (6)          (7)


cmd line: Execute cat /etc/passwd and pipe it to grep to filter on student.
cmd output: Student entry in the /etc/passwd file.



Sections of output lines
Username
Password. An x character indicates that an encrypted password is stored in /etc/shadow file.
UID Value
GUID Value
User ID Info (GECOS). The comment field
Homeome Directory.
Command/Shell /bin/bash

```

## Permissions

Read
Read contents (File)
List contents of dir (Dir)

Write
Write contents (File)
Create/Delete in the dir (Dir)

Exe 
Run file as an executable (File)
Move into the dir (Dir)

```
chmod 755
student@linux-opstation-kspt:/bin$ ls -lisa /bin/dd 
student@linux-opstation-kspt:/bin$ 130341 76 -rwx r-x r-x 1 root root 76000 Jan 18  2018 /bin/dd
                                             (2)  (3) (4)   (5)   (6)

Showing permissions.
2 The Owner has Read, Write, and Execute permissions.
3 The Group has Read and Execute permissions.
4 Anyone who is not the User/Owner or belonging to the Group has Read and Execute permissions.
5 The file’s Owner.
6 The files' Group.
```

## Sticky Bit

Only the owner of the sticky bit can delete the file
If a user has write access to a directory, they can delete any file from it. That may cause problems though in some directories like /var/tmp. To address this Linux has what is known as the sticky bit. The sticky bit removes the ability to delete files unless the user attempting is the owner of the file.



## Special Permisions

```
SUID or GUID Bit

SUID and SGID Demo
student@linux-opstation-kspt:~$ ls -l /bin/ping 
-rwsr-xr-x 1 root root 64424 Jun 28  2019 /bin/ping 

Execute ls -l on /bin/ping.
Notice the s in the users field? What permissions does this executable effectively have?


```

## Grep

```
student@linux-opstation-kspt:~$ ls -Rlisa /etc | grep password 
 1137 4 -rw-r--r--   1 root root 1440 Jan 31  2020 common-password
 1156 4 -rw-r--r--   1 root root 1160 Oct  9  2018 gdm-password
ls: cannot open directory '/etc/polkit-1/localauthority': Permission denied 
ls: cannot open directory '/etc/ssl/private': Permission denied
ls: cannot open directory '/etc/sudoers.d': Permission denied


```

## Awk

```
student@linux-opstation-kspt:~$ ls -l /etc 
drwxr-xr-x  7 root root       4096 Feb  4  2020 NetworkManager
drwxr-xr-x  2 root root       4096 Feb  4  2020 PackageKit
drwxr-xr-x  2 root root       4096 Feb  4  2020 UPower
_truncated_

student@linux-opstation-kspt:~$ ls -l /etc | awk -F " " '{print$3","$4","$9}' > files.csv 
student@linux-opstation-kspt:~$ cat files.csv
root,root,NetworkManager
root,root,PackageKit
root,root,UPower
_truncated_

```


## Sed 
edits

```
student@linux-opstation-kspt:~$ cat /etc/passwd | grep root 
root:x:0:0:root:/root:/bin/bash

student@linux-opstation-kspt:~$ cat /etc/passwd | grep root | sed s/root/bacon/g 
bacon:x:0:0:bacon:/bacon:/bin/bash



```


## Regex

-P Perl regex

```
student@linux-opstation-kspt:~$ grep -P '\b\d{3}-\d{2}-\d{4}\b' results.txt
629-75-1985
386-67-7872
478-71-4964

```


6cebf155e9c8f49d76ae1268214ff0b5

# Windows Registry Keys (Day 3)

## Structure

Hive
Key
Subkeys
Values

## Registry Hive or ROOT Keys

LM
HKEY_LOCAL_MACHINE
U
HKEY_USERS
CU
HKEY_CURRENT_USERS
CC
HKEY_CURRENT_CONFIG
CR
HKEY_CLASSES_ROOT

## KHLM_Local_Machine (HKLM)

HARDWARE - contains a database of installed devices along with their drivers

SAM - Security Account Manager stores user and group accounts along with NTLM hashes of passwords

Security - Local Security policy accessed by lsass.exe used to determine rights and permissions for users on the machine

System - Contains keys pertaining to system startup such as programs started on boot or driver load order.

## HKLM_USERS (HKU)

User Environment settings for the desktop

Shortcuts

File associations


## HKLM_CURRENT_USER (HKCU)

HKEY_CURRENT_USER is the copy of the logged in user’s registry key based on thier SID from HKEY_USERS.


## HKLM_Current_Config (HKCC)

HKEY_CURRENT_CONFIG is a symbolic link (pointer or shortcut or alias) to the following registry key:

```
HKEY_Local_Machine (HIVE)
              └──SYSTEM (Key)
                      └──CurrentControlSet (Subkey)
                                    └── Hardware Profiles (Subkey)
                                                └── Current (Subkey)
```

## HKLM_Classes_Root (HKCR)

HKEY_CLASSES_ROOT is a symbolic link (pointer or shortcut or alias) to the following registry key:
```
HKEY_Local_Machine (HIVE)
              └──Software (Key)
                      └──Classes (Subkey)

```


## Extension Types

No extension = Actual Hive File

.alt extension = Backup copy of hive, used in Windows 2000

.log extension = Transaction log of changes to a hive

.sav extension = Backup copy of hive created at the end of text-mode (console)


## Registry Manipulation (Regedit)

via GUI - regedit.exe

```
Using Regedit.exe to query the Registry
Click on the search bar and type in regedit.exe
If prompted by UAC, click yes
Click on the drop down for HKEY_CURRENT_USER
Click the drop down for Software
Click the drop down for Microsoft
Click the drop down for Windows
Click the drop down for CurrentVersion
Click the drop down for Run
We have successfully queried a key using regedit.exe

```

rex.exe

```
reg.exe

CLI

Located at C:\Windows\System32\reg.exe

Can connect to a remote registry, using the PC’s NetBios Name or IP address

Does not have to be in workgroup/domain. Only need username/password

Needs the RemoteRegistry Service (svchost.exe / regsvc.dll) to be running to work

Can load hives files from disk to the active registry

Available in XP and beyond

Can only export text .reg files

Can only query HKLM and HKU remotely
```

```
reg /?                    #Displays help for all of the reg.exe commands
reg query /?              #Displays help for the `reg query`
reg add /?                #Displays help for `reg add`
reg delete /?             #Displays help for `reg delete`

/v stands for Value; In this case the name of this Key Value.
/t stands for Type; Types can be any of the Data Types that we went over earlier.
/d stands for Data; Is what is the actual Data or in this case a command to open a file every time the system is ran.

reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v testme /t REG_SZ /d C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
reg delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v testme


```

## Registry Manipulation (Powershell)

```
Query

Get-ChildItem cmdlet gets the items in one or more specified locations.

Get-ItemProperty cmdlet gets the items in one or more specified locations.

Get-Item cmdlet gets the item at the specified location. It doesn’t get the contents of the item at the location unless you use a wildcard character (*) to request all the contents of the item.


Modify

Set-ItemProperty cmdlet changes the value of the property of the specified item. example, changing setting to :true or :false.

Remove-ItemProperty cmdlet to delete registry values and the data that they store.


Create

New-Item cmdlet creates a new item and sets its value. In the registry, New-Item creates registry keys and entries.

New-Itemproperty cmdlet creates a new property for a specified item and sets its value. Typically, this cmdlet is used to create new registry values, because registry values are properties of a registry key item.


```


```
Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run 
Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\ 
Get-item HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run



New-Item "HKLM:\Software\Microsoft\Office\14.0\Security\Trusted Documents\TrustRecords" -Force
New-ItemProperty "HKLM:\Software\Microsoft\Office\14.0\Security\Trusted Documents\TrustRecords" -Name "%USERPROFILE%Downloads/test-document.doc" -PropertyType Binary -Value ([byte[]](0x30,0x31,0xFF)) 
New-ItemProperty HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run -Name Test -PropertyType String -Value C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe


Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run -Name SecurityHealth -NewName Test
Remove-ItemProperty -Path "HKLM:\Software\Microsoft\Office\14.0\Security\Trusted Documents\TrustRecords" -Name "%USERPROFILE%Downloads/test-document.doc"
Set-ItemProperty HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run -Name Test -Value Bacon.exe
```



## Powershell PSDrives

```
Get-PSDrive

New-PSDrive -Name HKU -PSProvider Registry -Root HKEY_USERS
```


To create a new Windows PowerShell drive, you must supply three parameters:

A Name for the drive (you can use any valid Windows PowerShell name)

The PSProvider (use "FileSystem" for file system locations, "Registry" for registry locations, and it could also be a shared folder on a remote server.)

The Root, that is, the path to the root of the new drive.




## Foresically Relevant Keys

https://drive.google.com/file/d/1XzThO4pyhlm86Qxzu--6_5XlYpfldeZu/view

Windows Registry Cheat Sheet
Microsoft Edge Internet URL history and Browser Artifacts and Forensics

HKEY_CLASSES_ROOT\Local Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Storage\microsoft.microsoftedge_8wekyb3d8bbwe\Children\001\Internet Explorer\DOMStorage


```
USB history / USB Forensics

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB

This registry key contains information about all USB devices that have been connected to the system at some point, regardless of whether they are currently connected or not. It includes information about the USB controllers, hubs, and individual devices. Each device is typically identified by a unique identifier (like a device instance path or hardware ID).

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR

This registry key specifically deals with USB storage devices, such as USB flash drives, external hard drives, etc. It contains information about connected USB storage devices, including details like device instance paths, hardware IDs, and other configuration information.
```

```
Recent MRU history / MRU in forensics
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU

MRU is the abbreviation for most-recently-used.

This key maintains a list of recently opened or saved files via typical Windows Explorer-style common dialog boxes (i.e. Open dialog box and Save dialog box).

For instance, files (e.g. .txt, .pdf, htm, .jpg) that are recently opened or saved files from within a web browser (including IE and Firefox) are maintained.
```

```
Recent Files with LNK files
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
```

```
Windows User Profiles User Account Forensics

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
```

```
Saved Network Profiles and How to decode Network history
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles
```

```
Windows Virtual Memory and why it is important
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management

This key maintains Windows virtual memory (paging file) configuration.

The paging file (usually C:\pagefile.sys) may contain evidence/important information that could be removed once the suspect computer is shutdown.
```

```
Recent search terms using Windows default search and Cortana
HKEY_CURRENT_USER\Software\Microsoft\Windows Search\ProcessedSearchRoots

Index of Search results by SID

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Search

Recent files searched
```



## Keys for Persistence

HKLM\Software\Microsoft\Windows\CurrentVersion\Run

HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\Run

HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKLM\SYSTEM\CurrentControlSet\services

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders

HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon



# Alternate Data Streams (Day 3 Continued)
ADS Does not change the MD5 hash so you can hide data

## Regular Data Stream on a File (CLI)
```
C:\windows\system32>echo Always try your best > reminder.txt 

C:\windows\system32>dir reminder.txt 
 Directory of C:\windows\system32
 02/27/2021 07:13 PM                 25 reminder.txt
                1 File(s)            25 bytes
                0 Dir(s) 20,060,768,688 bytes free

C:\windows\system32>type reminder.txt 
Always try your best
```




## Creating ADS on a FILE (CLI)
```
C:\windows\system32>echo social security numbers > reminder.txt:secret.info 

C:\windows\system32>dir reminder.txt 
 Directory of C:\windows\system32
 02/27/2021 07:13 PM                  23 reminder.txt
                 1 File(s)            23 bytes
                 0 Dir(s) 20,060,712,960 bytes free

C:\windows\system32>type reminder.txt 
Always try your best
```

## Viewing ADS  (CLI)

```
C:\windows\system32>more < reminder.txt:secret.info 
social security numbers

C:\windows\system32>notepad reminder.txt:secret.info 

C:\windows\system32>dir /R reminder.txt 
 Directory of C:\windows\system32
 02/27/2021 07:13 PM                   23 reminder.txt
                                       26 reminder.txt:secret.info:$DATA
                1 File(s)              23 bytes
                0 Dir(s)   20,060,557,312 bytes free

C:\windows\system32>type reminder.txt:secret.info 
The filename, directory name, or volume label syntax is incorrect.

```




## Regular Data Stream on a File (Powershell)
```
PS C:\windows\system32>echo "Always do your best" > reminder.txt 

PS C:\windows\system32>Get-ChildItem .\reminder.txt 
    Directory: C:\windows\system32
Mode                LastWriteTime        Length  name
----                -------------        ------  ----
-a----           2/28/2021  2:40 AM          44   reminder.txt

PS C:\windows\system32>Get-Content reminder.txt 
Always do your best
```




## Creating ADS on a FILE (Powershell)
```
PS C:\windows\system32>Set-Content .\reminder.txt -Value "social security numbers" -Stream secret.info 

PS C:\windows\system32>Get-Childitem reminder.txt 
    Directory: C:\windows\system32
Mode                LastWriteTime        Length  name
----                -------------        ------  ----
-a----           2/28/2021  2:41 AM          44   reminder.txt

PS C:\windows\system32>Get-Content reminder.txt 
Always do your best
```

## Viewing ADS  (Powershell)

```
PS C:\windows\system32>Get-Item reminder.txt -Stream * 
PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32\reminder.txt::$DATA
PSParentPath : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32
PSChildName : reminder.txt::$DATA
PSDrive       : C
PSProvider    : Microsoft.PowerShell.Core\FileSystem
PSIsContainer : False
FileName      : C:\windows\system32\reminder.txt 
Stream        : :$DATA 
Length        : 44PS C:\windows\system32>Get-Item reminder.txt -Stream * 
PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32\reminder.txt::$DATA
PSParentPath : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32
PSChildName : reminder.txt::$DATA
PSDrive       : C
PSProvider    : Microsoft.PowerShell.Core\FileSystem
PSIsContainer : False
FileName      : C:\windows\system32\reminder.txt 
Stream        : :$DATA 
Length        : 44

PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32\reminder.txt:secret.info
PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32
PSChildName  : reminder.txt:secret.info
PSDrive       : C
PSProvider    : Microsoft.PowerShell.Core\FileSystem
PSIsContainer : False
FileName      : C:\windows\system32\reminder.txt
Stream        : secret.info 
Length        : 25

PS C:\windows\system32>Get-Content reminder.txt -Stream secret.info 
social security numbers

PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32\reminder.txt:secret.info
PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\windows\system32
PSChildName  : reminder.txt:secret.info
PSDrive       : C
PSProvider    : Microsoft.PowerShell.Core\FileSystem
PSIsContainer : False
FileName      : C:\windows\system32\reminder.txt
Stream        : secret.info 
Length        : 25

PS C:\windows\system32>Get-Content reminder.txt -Stream secret.info 
social security numbers
```



# Windows Boot Process (Day 4)

http://1.bp.blogspot.com/-MaRtDTHH1Vo/UysJF8KXNbI/AAAAAAAAALo/D6Kt2f8Gpmo/s1600/Walkthrough_Diagram.jpg



## Why Do we care about the Boot process?
```
Rootkits are a type of malware that hide themselves and other applications. They typically run in kernel mode, so they have the same privileges as the operating system and can sometimes start before it. Because traditionally, anti-malware software doesn’t load until after the kernel and boot drivers do, rootkits often exploit weaknesses in the startup process:

Firmware Rootkits overwrite the PC’s BIOS or other hardware firmware so the rootkit can start before the OS even loads

Bootkits replace the OS bootloader to load the bootkit before the OS

Kernel rootkits replace a portion of the OS kernel so the rootkit can start when the OS loads

Driver rootkits pretend to be a boot driver that the OS uses to communicate with PC

Avenues of Attack An exposed operating system can be easily used to further Offensive goals such as pivots or compromised to steal data
```


## BIOS and UEFI
BIOS and UEFI are firmware that ensure critical hardware like SATA devices (Hard Drives), Display Adapters, and SDRAM(Synchronous dynamic random-access memory) are functional then, locates the MBR(Master Boot Record) or GPT(GUID Partition Tables).
```
ROM (Read only memory)

EPROM (Electronically Programmable Read only memory)

EEPROM (Electronically Erasable Programmable read only memory)

Flash memory

BIOS and UEFI do the same thing, but minor differences make UEFI more popular than BIOS in the current day. Without getting into low level specifics some of the benefits of UEFI:

UEFI Boots much faster than BIOS systems, especially for Windows machines.

UEFI Firmware is usually loaded into flash memory or EEPROM, making it easier to update and patch.

UEFI offers SECURED BOOT mode which only allows verified drivers to load.

UEFI offers drive support of up to 9 zettabytes, while BIOS only works with 2 terabytes.
```


## BIOS Master Boot Record
Once the BIOS checks hardware, it finds the MBR (Master Boot Record). The MBR contains Disk Partitions like /dev/sda1 or DISK 1 C:\
The partition contains code that starts the first stage of loading an Operating System, called a Boot Loader
```
Boot Loaders

Windows 2003 and older used NTLDR or New Technology Loader

Windows 7 Service Pack 1 and newer uses bootmgr or New Technology Loader

From this point the Boot Loader takes over and starts the Operating System
```


## UEFI Boot Manager
UEFI does the same hardware checks as BIOS, but instead of using the MBR it reads an EFI Partition. The EFI Partition contains UEFI Boot Managers Windows bootmgfw.efi or Windows Boot Manager
From this point onwards, the UEFI Boot Manager takes over and starts the Operating System. How can I tell if my machine is running BIOS or UEFI?
```
findstr /C:"Detected boot environment" "C:\Windows\Panther\Setupact.log"
Get-Content C:\Windows\Panther\Setupact.log | Select-String "Detected boot environment"
```
winload.exe = BIOS, winload.efi = UEFI
```
bcdedit | findstr /i winload
```



## Windows System Intialization
This is a simplified version of the Windows Boot Process from the kernel (ntoskrnl.exe) to the execution of LogonUi.exe (the process that prompts for user interaction). It is broken into five steps.
```
Loading the Operating System Kernel

Initializing the Kernel

Starting Subsystems

Starting Session 0

Starting Session 1
```




## Loading the Operating System Kernel
```
On UEFI Systems

bootmgfw.efi reads a BCD (Boot Configuration Data) located in the EFI system partition to load the file winload.efi



On BIOS Systems

bootmgr or NTLDR reads the file \Boot\BCD to locate winload.exe

The purpose of both winload programs is to load basic drivers and start the next part of the Windows Boot Process - loading the Kernel.



Winload.exe loads the Windows kernel:

Loads essential drivers required to read data from disk

Loads the windows kernel (ntoskernel.exe) and dependencies

Winresume.exe reads previously saved data from hiberfil.sys (hibernation mode) to restore a previous Windows instance.

On UEFI systems, winresume.exe is named winresume.efi, and is located at \windows\system32\boot.
```


## Intializing the Kernel


```
The kernel, as previously discussed, is the heart of the Operating System. Without it, the system cannot function.

In Windows, the kernel is named Ntoskrnl.exe and is a critical system file. It does the following tasks during the boot process:

Loads the Windows Registry

Loads device drivers

Starts the system pagefile located at C:\pagefile.sys

Loads hal.dll

hal.dll provides abstraction between hardware interfaces and Ntoskrnl.exe

Once the kernel is done loading it spawns System which hosts threads that only run in kernel mode responsible things like drivers. System then spawns the session management processes smss.exe and csrss.exe
```


## Starting Subsystems
```
smss.exe (Session Manager Subsystem) does the following tasks:

Loads environmental variables like %APPDATA% and %COMPUTERNAME%

Populates the pagefile located in C:\pagefile.sys

Starts the kernel and user mode sub systems.

Starts a csrss.exe to manage processes and threads for each User Subsystem.
```


## Kernel Subsystems
```
The kernel subsystem creates and manages every resource available to Windows by interacting with drivers on the system. It controls things like:

System power state

Process creation and threads

Graphical rendering

Access Control Lists via the Security Reference Monitor

It is important to understand - users cannot interact directly with any kernel-mode process or even see them
```
## User Subsystems
The user subsystem manages all user applications like process creation, internet connectivity, and object access through API calls to hal.dll
User Subsystems run in Session 0 and Session 1
![image](https://github.com/Acosta-Xavier/Notes/assets/172090154/f28a7a90-d9fd-4f44-bf37-a159f8818150)


## User Subsystem Session 0
```
Session 0 is for security and high privilege processes such as services. They are run in a separate session to isolate them from individual user’s processes.

smss.exe installs the Win32 subsystem kernel and user mode components (win32k.sys - kernel; winsrv.dll - user; and csrss.exe - user.)

csrss.exe - The Client/Server Runtime Subsystem supports process / thread creation and management.

wininit.exe marks itself as critical, initializes the Windows temp directory, loads the rest of the registry, and starts user mode scheduling. It also installs programs that require a reboot to finish the install process. It also starts:

lsm.exe - the Local Session Manager (LSM) handles all sessions of a system (both remote desktop sessions and local system sessions.)

lsass.exe - the Local Security Authority Subsystem (LSASS) provides user authentication services, manages the local security policy, and generates access tokens.

services.exe the Services Control Manager (SCM) loads AutoStart services, using LSASS to authenticate if they run as something other than System.

wininit.exe then waits for system shutdown to undo everything it started.
```

## Viewing Services
Showing the Spooler Service using SC
```
sc query spooler

SERVICE_NAME: Spooler
DISPLAY_NAME: Print Spooler
        TYPE               : 110  WIN32_OWN_PROCESS  (interactive)
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

Showing the Service Control Manager registry key
```
reg query HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services | findstr Spooler

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Spooler
```

Showing the contents of the Spooler Service Registry Key

```
reg query HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Spooler

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Spooler
    DisplayName    REG_SZ    @%systemroot%\system32\spoolsv.exe,-1
    Group    REG_SZ    SpoolerGroup
    ImagePath    REG_EXPAND_SZ    %SystemRoot%\System32\spoolsv.exe 
    Description    REG_SZ    @%systemroot%\system32\spoolsv.exe,-2
    ObjectName    REG_SZ    LocalSystem 
```
Showing services

```
C:\Windows> tasklist /svc

Image Name                     PID Session Name        Session#
========================= ======== ================ ===========
svchost.exe                   1040 EventSystem, fdPHost, FontCache, netprofm,
                                   nsi, WdiServiceHost
svchost.exe                   1076 AeLookupSvc, Appinfo, AppMgmt, BITS,
                                   CertPropSvc, EapHost, gpsvc, iphlpsvc,
                                   ProfSvc, Schedule, SCPolicySvc, SENS,
                                   ShellHWDetection, Themes, Winmgmt, wuauserv
CTAudSvc.exe                  1216 CTAudSvcService
igfxCUIService.exe            1328 igfxCUIService2.0.0.0
svchost.exe                   1388 CryptSvc, Dnscache, LanmanWorkstation,
                                   NlaSvc, WinRM
spoolsv.exe                   1568 Spooler
svchost.exe                   1604 FDResPub, QWAVE, SCardSvr, SSDPSRV
svchost.exe                   1644 BFE, DPS, MpsSvc
armsvc.exe                    1768 AdobeARMservice
```

## User Subsystem Session 1
Session 1 is for the first interactive user (note: each session gets its own copy of csrss.exe.) Session 1 and up are standard user sessions. This includes everyone from the default Administrator to custom accounts created. It is the entire desktop experience on Windows.
```
Spawn a Session 1 ( or higher) csrss.exe

Spawn Winlogon.exe which by default prompts for credentials with logonui.exe

Spawn userinit.exe which creates an account token and creates a custom environment

Spawn explorer.exe as the customized graphical environment.
```

## Windows BCEdit Demo
`https://os.cybbh.io/public/os/latest/006_windows_boot_process/winboot_fg.html'




Q: What can I do if the Windows boot settings became corrupted?

A: Fix it with the bcdedit command
BCDEdit command help
```
c:\demo>bcdedit /?
```





## What does a normal bcdedit output look like?

```
c:\demo>bcdedit

Windows Boot Manager
--------------------
identifier              {bootmgr}
device                  partition=C:
description             Windows Boot Manager
locale                  en-US
inherit                 {globalsettings}
default                 {current}
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
displayorder            {current}
toolsdisplayorder       {memdiag}
timeout                 29

Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \windows\system32\winload.exe
description             Windows 7 - Tiger Paw
locale                  en-US
inherit                 {bootloadersettings}
recoverysequence        {91061b50-0fa8-11e9-aa6e-00155d49334a}
displaymessageoverride  Recovery
recoveryenabled         Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \windows
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
nx                      OptIn
bootmenupolicy          Standard
```

## Backup and Restore

```
c:\demo>bcdedit /export C:\Lion_BCD
c:\demo>bcdedit /import C:\Lion_BCD

```

## Modify Decription

```
c:\demo>bcdedit /set {<identifier>} description "Windows 7 - Lion Den" (1)

```

## Create new partition
```
c:\demo>bcdedit /create {ntldr} /d "Windows XP Pro SP2 - Tiger Paw"


-Specify the Partition

c:\demo>bcdedit /set {ntldr} device partition=C:


-Specify the Path to ntldr

c:\demo>bcdedit /set {ntldr} path \ntldr


-Specify the Display Order

c:\demo>bcdedit /displayorder {ntldr} /addfirst
```

## Show added Partition

```
c:\demo>bcdedit

Windows Boot Manager
--------------------
identifier              {bootmgr}
device                  partition=C:
description             Windows Boot Manager
locale                  en-US
inherit                 {globalsettings}
default                 {current}
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
displayorder            {ntldr}
                        {current}
toolsdisplayorder       {memdiag}
timeout                 29

Windows Legacy OS Loader
------------------------
identifier              {ntldr}
device                  partition=C:
path                    \ntldr
description             Windows XP Pro SP2 - Tiger Paw

Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \windows\system32\winload.exe
description             Windows 7 - Lion Den
locale                  en-US
inherit                 {bootloadersettings}
recoverysequence        {91061b50-0fa8-11e9-aa6e-00155d49334a}
displaymessageoverride  Recovery
recoveryenabled         Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \windows
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
nx                      OptIn
bootmenupolicy          Standard

```

## Add, Remove, Change Values Options

```
_Output_Truncated_
Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \windows\system32\winload.exe
description             Windows 7 - Tiger Paw
locale                  en-US
inherit                 {bootloadersettings}
recoverysequence        {91061b50-0fa8-11e9-aa6e-00155d49334a}
displaymessageoverride  Recovery
recoveryenabled         Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \windows
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
nx                      OptIn
safeboot                Minimal
bootmenupolicy          Standard


bcdedit /deletevalue {current} safeboot (1)
bcdedit /set {bootmgr} timeout 29 (2)
bcdedit /delete {ntldr} -f
```


# Linux Boot Process (Day 5)

```
	 Computer Turns ON

BIOS		or		UEFI

MBR 		or 		GPT

grub		or 		grub.efi

	   Linux Kernel

	       Init

 Sysv Init 	or 		Systemd Init
 /sbin/init			/lib/systemd/systemd
executes runlevels 		executes *.units

	Brings the system to login state
 
```

## MBR Layout


```
The first 512 bytes of a hard drive contains the Master Boot Record. It contains the following information:

    Bootstrap Code		446

    Partition entry 1		16

    Partition entry 2		16

    Partition entry 3		16

    Partition entry 4		16

    Boot signature		2
----------------------------------------------------
				512 Total Bytes

```

Each Partition is 16 bytes and you can have 4 partitions per MBR

## Locate the Harddrive and Partition

```
student@linux-opstation-kspt:~$ lsblk 

NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0    7:0    0 31.1M  1 loop /snap/snapd/10707
loop1    7:1    0 55.4M  1 loop /snap/core18/1944
loop2    7:2    0 44.7M  1 loop /snap/openstackclients/38
loop3    7:3    0 55.5M  1 loop /snap/core18/1988
loop4    7:4    0 31.1M  1 loop /snap/snapd/11036
sr0     11:0    1  514K  0 rom  /media/student/config-2
vda    252:0    0  128G  0 disk 
└─vda1 252:1    0  128G  0 part / 
```

A block device is a special file that refers to a device





## Examining MBR Contents


```

student@linux-opstation-kspt:~$ sudo xxd -l 512 -g 1 /dev/vda

00000000: eb 63 90 00 00 00 00 00 00 00 00 00 00 00 00 00  .c.............. 
00000010: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
_truncated_
000001b0: cd 10 ac 3c 00 75 f4 c3 fa b7 12 e6 00 00 80 00  ...<.u.......... 
000001c0: 21 02 83 0f 2e 40 00 08 00 00 df f7 ff 0f 00 00  !....@.......... 
000001d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000001e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000001f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 aa  ..............U.

	Execute xxd to hexdump 512 bytes in separated by 1 byte from /dev/vda to the screen
	The start of the hard drive shown by the code eb 63. File signature for an MBR.
	The first partition of the hard drive in 0x01be shown as 80
	The second partition entry is blank!

```

## Make MRB Copy Byte for Byte

```

student@linux-opstation-kspt:~$ dd if=/dev/vda of=MBRcopy bs=512 count=1 
dd: failed to open '/dev/vda': Permission denied 

student@linux-opstation-kspt:~$ sudo !! 
1+0 records in
1+0 records out
512 bytes copied, 0.00026952 s, 1.9 MB/s
student@linux-opstation-kspt:~$ file MBRcopy 
MBRcopy: DOS/MBR boot sector

Execute dd which copies 512 bytes once from /dev/vda to a file in my current directory called MBR
Notice, dd failed to run
!! represents the previous command. Run it with sudo permissions.
Execute file to read the file signature from the MBR file

```

## GUID Partition Table (GPT)

GPT is a newer version of MBR

```
    GPT Only works with UEFI Firmware

    GPT has many boot sectors stored around the disk as redundancy so an issue in one will not deadline the entire machine

    GPT supports 128(and more depending on Operating System) separate physical partitions, while MBR supports only 4

    GPT Supports partitions up to 9 zettabytes. Which is ridiculous.
```


## Second Stage Bootloader (GRUB)

The MBR in Grub Stage 1 loads the 2nd stage bootloader, named Grub Stage 2 or GRUB. GRUB Stage 2 rests inside the selected active partition mounted in /boot or in a completely separate partition.


## Grand Unified Bootloader (GRUB)

GRUB(Grand Unified Bootloader) has one purpose - to load the Linux Kernel a user choses from a location in the hard drive. The GRUB has two stages which load it from two separate locations.


## BIOS --> MBR --> GRUB
```
    Stage 1 : boot.img located in the first 440 bytes of the MBR loads…​

    Stage 1.5 : core.img located in the MBR between the bootstrap and first partition. It loads…​

    Stage 2 : /boot/grub/i386-pc/normal.mod which loads the grub menu and then reads

        /boot/grub/grub.cfg Which displays a list of Linux kernels available to load on the system

```


## UEFI --> GPT --> GRUB
```


    Stage 1 : grubx64.efi Located on an EFI partition or in /boot loads…​

    Stage 2 : /boot/grub/x86_64-efi/normal.mod

        /boot/grub/grub.cfg Which displays a list of Linux kernels available to load on the system


```

## Looking at GRUB to find Kernel

```
student@linux-opstation-kspt:/$ cat /boot/grub/grub.cfg 
_truncated_
set linux_gfx_mode=auto
export linux_gfx_mode
menuentry 'Ubuntu' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-LABEL=cloudimg-rootfs' {
        recordfail
        load_video
        gfxmode $linux_gfx_mode
        insmod gzio
        if [ x$grub_platform = xxen ]; then insmod xzio; insmod lzopio; fi
        insmod part_msdos
        insmod ext2
        if [ x$feature_platform_search_hint = xy ]; then
          search --no-floppy --fs-uuid --set=root  6c0fba3b-b236-4b3a-b999-db7359c5d220
        else
          search --no-floppy --fs-uuid --set=root 6c0fba3b-b236-4b3a-b999-db7359c5d220
        fi
        linux   /boot/vmlinuz-4.15.0-76-generic root=LABEL=cloudimg-rootfs ro  console=tty1 console=ttyS0 
        initrd  /boot/initrd.img-4.15.0-76-generic
_truncated_


 	Concatenate the contents of /boot/grub/grub.cfg to the screen.
	The kernel is loaded with the command linux. The file /boot/vmlinuz-4.15.0-76-generic contains the Linux Kernel.
```


## Linux Kernel
The Kernel is the heart of a Operating System. It has complete control on everything within it such as memory management, device management, Input/output Device request control, and managing process scheduling with the Central processing unit.




The Linux Kernel originated from the Unix kernel and is unique from Windows in that it is :
1. A Monolithic Kernel

    System calls all functionality to the user such as CPU scheduling, memory management, and file management. A systemcall is a way in which a program requests services from the kernel. Everything that occurs on the system occurs through a systemcall

2. Modular

    Modules are extensions to base functionality of the Linux Operating System. This modularity allows for modifications baseline system functionality without rebuilding the kernel and failures will not stop the machine from starting.


## System Calls in Linux

```
student@linux-opstation-kspt:/$ ltrace -S cat /etc/passwd 
_truncated_
open("/etc/passwd", 0, 037777402000 <unfinished ...>  
SYS_openat(0xffffff9c, 0x7ffcbb66d68c, 0, 0)       = 3
<... open resumed> )                               = 3
__fxstat(1, 3, 0x7ffcbb66be40 <unfinished ...>
SYS_fstat(3, 0x7ffcbb66be40)                       = 0
<... __fxstat resumed> )                           = 0
posix_fadvise(3, 0, 0, 2 <unfinished ...>
SYS_fadvise64(3, 0, 0, 2)                          = 0
<... posix_fadvise resumed> )                      = 0
malloc(135167 <unfinished ...>
SYS_mmap(0, 0x22000, 3, 34)                        = 0x7f0b09df0000
<... malloc resumed> )                             = 0x7f0b09df0010
read(3 <unfinished ...>
SYS_read(3, "root:x:0:0:root:/root:/bin/bash\n"..., 131072) = 1875
<... read resumed> , "root:x:0:0:root:/root:/bin/bash\n"..., 131072) = 1875 
write(1, "root:x:0:0:root:/root:/bin/bash\n"..., 1875 <unfinished ...> 



	Execute ltrace to track the systemcalls occurring when running cat /etc/passwd.
	open systemcall on /etc/passwd returns a file descriptor of 3.
	read systemcall on file descriptor of 3 returns the amount of bytes in the file.
	write systemcall to write all the 1875 bytes from /etc/passwd to stdout.
```


## Modules in Linux

```
student@linux-opstation-kspt:/$ ltrace -S lsmod  

Module                  Size  Used by
aesni_intel           188416  0
aes_x86_64             20480  1 aesni_intel 
crypto_simd            16384  1 aesni_intel
glue_helper            16384  1 aesni_intel
cryptd                 24576  3 crypto_simd,ghash_clmulni_intel,aesni_intel
psmouse               151552  0
ip_tables              28672  0
virtio_blk             20480  2 
virtio_net             49152  0
virtio_rng             16384  0
virtio_gpu             53248  3

 	Execute lsmod to list modules in Linux
	Module required to use AES Encryption
	Modules for Virtual Input / Output Devices used in Openstack instances.

```

## INIT
The kernel, once loaded, is hard coded to reach out and execute /sbin/init. This starts the process of bringing the system to a desired level of functionality using Initialization Daemons. There are two main initialization daemons now : Systemd and SysV.

Systemd and SysV are two main INIT Daemons

A term used in Init is a Run Level. A Run Level defines the state of a machine after it has completed booting and is prompting for a user login. Run levels numbered from zero(0) to six(6) have special meaning, but they are not rigid in definition.

## Run Levels
Run Levels in SysV are a series of scripts that start or kill background processes on Linux at specific run levels. The scripts have a specific naming scheme that determine how the init process interacts with them.


The first letter K or S means Kill or Start the process that that script handles

The two digit number that follows K or S dictates the order the scripts execute

```
student@linux-opstation-kspt:/etc/rc3.d$ ls -l /etc/rc3.d/ 

lrwxrwxrwx 1 root root 15 Jan 31  2020 S01acpid -> ../init.d/acpid 
lrwxrwxrwx 1 root root 17 Feb  4  2020 S01anacron -> ../init.d/anacron
lrwxrwxrwx 1 root root 16 Jan 31  2020 S01apport -> ../init.d/apport
lrwxrwxrwx 1 root root 13 Jan 31  2020 S01atd -> ../init.d/atd
lrwxrwxrwx 1 root root 26 Jan 31  2020 S01console-setup.sh -> ../init.d/console-setup.sh
lrwxrwxrwx 1 root root 14 Jan 31  2020 S01cron -> ../init.d/cron
lrwxrwxrwx 1 root root 14 Jan 31  2020 S01dbus -> ../init.d/dbus
lrwxrwxrwx 1 root root 14 Feb  4  2020 S01gdm3 -> ../init.d/gdm3


student@linux-opstation-kspt:/etc/rc3.d$ ls -l /etc/rc1.d/ 

lrwxrwxrwx 1 root root 20 Feb  4  2020 K01alsa-utils -> ../init.d/alsa-utils
lrwxrwxrwx 1 root root 13 Jan 31  2020 K01atd -> ../init.d/atd
lrwxrwxrwx 1 root root 20 Jan 31  2020 K01cryptdisks -> ../init.d/cryptdisks
lrwxrwxrwx 1 root root 26 Jan 31  2020 K01cryptdisks-early -> ../init.d/cryptdisks-early
lrwxrwxrwx 1 root root 18 Jan 31  2020 K01ebtables -> ../init.d/ebtables
lrwxrwxrwx 1 root root 14 Feb  4  2020 K01gdm3 -> ../init.d/gdm3 
```

Run-Levels 
```
0		HALT
	
1		Single User

2		Multi-user Mode

3		Multi-user with Networking

4		Not Used/ User-defined

5		Multi-user Mode with Networking and GUI Desktop

6		Reboot
	

```

## SysV 
SysV initialization is a legacy system initialization method, but it is still used today in many older systems Linux systems or Unix machines like Oracle’s Solaris. It starts with the kernel executing the first process on the machine, or the Initialization daemon. In SysV machines it is the /etc/init program. Then, init reads /etc/inittab to start creating processes in groups called Run Levels. The processes that each Run Level starts are defined in /etc/rc*.d

```
cat /etc/inittab

is:5:initdefault: 


l0:0:wait:/etc/rc0.d
l1:1:wait:/etc/rc1.d
l2:2:wait:/etc/rc2.d
l3:3:wait:/etc/rc3.d
l4:4:wait:/etc/rc4.d 
l5:5:wait:/etc/rc5.d
l6:6:wait:/etc/rc6.d

```

## Systemd
Systemd is the modern initialization method. It starts with the kernel spawning /sbin/init which is symbolically linked to /lib/systemd/system. systemd interacts with flat configuration files called units. There are many types, but the target and service units determine system initialization.

The kernel spawns /usr/lib/systemd/system as the first process on the system. It then executes configurations starting at mounting the local file system to bringing the system to a desired state specified in the default target unit. Targets in systemd are like runlevels in SysV. The name of the default target is default.target and located in /lib/systemd/system.


Systemd uses TARGETS instead of Run Levels

Showing Default Target Unit

```
student@linux-opstation-kspt:/$ ls -lisa /lib/systemd/system/default.target

lrwxrwxrwx 1 root root 16 May  3 11:30 default.target -> graphical.target 


Symbolically linked default.target to graphical.target unit.
The system will, by default, try to run the system to the specifics set by graphical.target.
```


Target Units 
Systemd target units are a set of value=data pairs to create processes in a set order on the system. But, they are simple to understand at a functional level by understanding the value=data fields within each.


Default target is GRAPHICAL TARGET
```
student@linux-opstation-kspt:/$ ls -lisa /lib/systemd/system/default.target

lrwxrwxrwx 1 root root 16 May  3 11:30 default.target -> graphical.target
```

Run-levels vs Targets

```
0		HALT							poweroff.target
	
1		Single User						rescue.target

2		Multi-user Mode						multi-user.target

3		Multi-user with Networking				multi-user.target

4		Not Used/ User-defined					multi-user.target

5		Multi-user Mode with Networking and GUI Desktop		graphical.target

6		Reboot							reboot.target

```
Examining Contents of graphical.target
```
cat /lib/systemd/system/default.target | tail -n 8

Description=Graphical Interface
Documentation=man:systemd.special(7)
Requires=multi-user.target
Wants=display-manager.service 
Conflicts=rescue.service rescue.target
After=multi-user.target rescue.service rescue.target display-manager.service 
AllowIsolate=yes

wants=display-manager.service attempts to start other units. If they fail to start, the calling target unit will still execute.
requires=multi-server.target attempts to start other units. If they fail to start, the calling target unit will fail to execute.


```

Target.unit want and requires dependencies search locations

    /etc/systemd/system/*

    /lib/systemd/system/*

    /run/systemd/generator/*

    More found in System Unit Man Page


Showing more wants and requires to graphical.target

```
student@linux-opstation-kspt:/$ ls -l /etc/systemd/system/ | grep graphical
drwxr-xr-x 2 root root 4096 Feb  4  2020 graphical.target.wants 

student@linux-opstation-kspt:/$ ls -l /etc/systemd/system/graphical.target.wants/
total 0
lrwxrwxrwx 1 root root 43 Jan 31  2020 accounts-daemon.service -> /lib/systemd/system/accounts-daemon.service  
lrwxrwxrwx 1 root root 35 Feb  4  2020 udisks2.service -> /lib/systemd/system/udisks2.service 

student@linux-opstation-kspt:/$ ls -l /lib/systemd/system | grep graphical
lrwxrwxrwx 1 root root   16 Nov 15  2019 default.target -> graphical.target
-rw-r--r-- 1 root root  598 Jan 28  2018 graphical.target
drwxr-xr-x 2 root root 4096 Jan 31  2020 graphical.target.wants 
lrwxrwxrwx 1 root root   16 Nov 15  2019 runlevel5.target -> graphical.target

student@linux-opstation-kspt:/$ ls -l /lib/systemd/system/graphical.target.wants/
total 0
lrwxrwxrwx 1 root root 39 Nov 15  2019 systemd-update-utmp-runlevel.service -> ../systemd-update-utmp-runlevel.service 


A graphical.target wants directory in /etc/systemd/system/
graphical.target also target wants udisks2.service and accounts-daemon.service
Yet another graphical.target wants directory in /lib/systemd/system/
graphical.target also wants systemd-update-utmp-runlevel.service
```

## Systemd Dependencies

```
systemctl list-dependencies graphical.target

graphical.target
● ├─accounts-daemon.service
● ├─apport.service
● ├─gdm.service 
● ├─grub-common.service
● ├─qemu-guest-agent.service
● ├─systemd-update-utmp-runlevel.service
● ├─udisks2.service 
● ├─ureadahead.service
● └─multi-user.target 
●   ├─anacron.service

```

## /etc/environment
The /etc/environment file sets Global Variables. Global Variables are accessible by every user or process on the system. It is read once when the machine completes Init. Any changes to the file require a system restart for them to apply.

```
cat /etc/environment

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games" 
```

## /etc/profile
/etc/profile is a script that executes whenever a user logs into an interactive shell on Linux. its functionality depends entirely on the version of Linux being used. Ubuntu Linux uses it to set the BASH shell prompt by executing /etc/bash.bashrc and execute any script named *.sh in /etc/profile.d.

```

student@linux-opstation-kspt:~$ cat /etc/profile

# /etc/profile: system-wide .profile file for the Bourne shell (sh(1))
# and Bourne compatible shells (bash(1), ksh(1), ash(1), ...).

if [ "${PS1-}" ]; then
  if [ "${BASH-}" ] && [ "$BASH" != "/bin/sh" ]; then 
    # The file bash.bashrc already sets the default PS1.
    # PS1='\h:\w\$ '
    if [ -f /etc/bash.bashrc ]; then 
      . /etc/bash.bashrc  
    fi
_truncated_
if [ -d /etc/profile.d ]; then
  for i in /etc/profile.d/*.sh; do
    if [ -r $i ]; then
      . $i 
    fi
  done
  unset i
fi


If the variable $BASH is set and does not equal /bin/sh then execute
if the /etc/bash.bashrc exists, execute it.
/etc/bash.bashrc creates the bash prompt student@linux-opstation-kspt:~$
If the directory /etc/profile.d exists, execute any script named *.sh in that directory.
```

## .bash_profile / .bashrc
They execute on a per user basis for interactive logins only. Both files are located every user’s /home directory. They are user specific configurations and freely editable by the owning user or root.
If a shell is created it executes the file


Example of Login and Non-Login Shell
```
student@linux-opstation-kspt:~$ echo "echo 'Im in `~/.profile`'" >> .profile 
student@linux-opstation-kspt:~$ echo "echo 'Im in ~/.bashrc'" >> .bashrc 

student@linux-opstation-kspt:~$ bash
student@linux-opstation-kspt:~$ Im in ~/.bashrc
student@linux-opstation-kspt:~$ exit 
student@linux-opstation-kspt:~$ exit 

#Log back into same Linux machine
Last login: Fri Feb 26 12:55:13 2021 from 10.250.0.20
Im in ~/.bashrc
Im in /etc/profile 
student@linux-opstation-kspt:~$




Echo a phrase into .profile and .bashrc
Create a Non-Login interactive shell by spawning a new bash session
Exit the new session AND logout of the machine
Logins create an interactive login shell; therefore,
```





# Windows Process Validity (Day 6)

What is process validity?


    Being able to distinguish a Process as a known good from a possible bad from its attributes and characteristics.

    Today’s Malware typically use their stealth and obfuscation abilities in order to hide in various artifacts such as:

        processes

        files

        registry keys

        drivers

        etc.

    They try to leave as little evidence of their presence as possible by mimicking or by hooking onto legitimate processes or services.

Why is it important




    OCO - Offensive Operations

        We need to protect our toolset (malware we’ve created).

        Find any other types of malware on the box that could compromise our tools.

    DCO - Defensive Operations

        Find malware and defend our networks

        Make sure we are not compromised or have sensitive information stolen from us.

            Could be the difference between life and death for soldiers on mission.



## Processes, DLLs, and Services




What is a process?

        A program running on your computer, whether executed by the user or running in the background.

        Examples include:

            Background tasks like spell checker

            Executables like Google Chrome and Notepad


What is a DLL?

    Dynamic Link Library

        A non-standalone program that can be run by (linked to) multiple programs at the same time.

        Cannot be directly executed. Dependent on an exe to use as an entry point, such as RUNDLL.EXE (a process that calls on the functionality of the DLL)

        Allows developers to make minor changes without affecting other parts of the program.

    Some Examples Include:

        Comdlg32 - Performs common dialog box related functions.

        Device drivers

        ActiveX Controls


What is a Service?

    Long-running executables that run in their own Windows sessions (i.e. in the background)

        Can be set to auto start when the computer boots or a user logs on.

        Can be paused and restarted.

        Do not interact with/show any user interface.



## Processes in PS

```
Powershell: Get-Process
CMD: tasklist


```


Get-Process
```
PS C:\Users\student> Get-Process

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    278      18     9420      18984       3.61   6304   1 ApplicationFrameHost
    342      19     4516       3988              4624   0 armsvc
    958      57   127900     202620      51.38    632   1 atom
    572      82   182356     266836     117.64   3148   1 atom
    321      33    92760     164644       0.56   7864   1 atom
    222      15     6884      28916       0.03   8024   1 atom
    733      27   143268     172480      38.33  13980   1 atom
     68       5     2040       4128       0.02   7504   1 cmd



Get-Process | Sort -Property Id | more
PS C:\Users\student> Get-Process | Sort -Property Id | more

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
      0       0       60          8                 0   0 Idle
   4240       0      192         96                 4   0 System
      0       0      184      22332                72   0 Secure System
      0      17     6552      28656               132   0 Registry
    168      11     1432       3484               452   0 wininit
     53       3     1056        940               504   0 smss

-- More --


Get-Process | Select Name, Id, Description | Sort -Property Id | more
PS C:\Users\student> Get-Process | Select Name, Id, Description | Sort -Property Id | more

Name                       Id Description
----                       -- -----------
Idle                        0
System                      4
Secure System              72
Registry                  132
wininit                   452
smss                      504
LsaIso                    572
csrss                     576
svchost                   624
atom                      632 Atom
svchost                   852
rundll32                 1616 Windows host process (Rundll32)
CompPkgSrv               1788 Component Package Support Server
Slack                    1816 Slack

-- More --

PS C:\Users\student> Get-Process SMSS,CSRSS,LSASS | Sort -Property Id

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
     53       3     1056        940               504   0 smss
    717      33     3684       3688               576   1 csrss
    784      24     1928       2788               876   0 csrss
   1612      39    10352      18076              1028   0 lsass


PS C:\Users\student> Get-Process chrome | foreach {$_.modules} | more

   Size(K) ModuleName                                         FileName
   ------- ----------                                         --------
      2244 chrome.exe                                         C:\Program Files (x86)\Google\Chrome\Application\chrome.exe
      2008 ntdll.dll                                          C:\WINDOWS\SYSTEM32\ntdll.dll
       756 KERNEL32.DLL                                       C:\WINDOWS\System32\KERNEL32.DLL
      2852 KERNELBASE.dll                                     C:\WINDOWS\System32\KERNELBASE.dll
      1016 chrome_elf.dll                                     C:\Program Files (x86)\Google\Chrome\Application\88.0.4324...
        40 VERSION.dll                                        C:\WINDOWS\SYSTEM32\VERSION.dll

-- More --


PS C:\Users\student> Get-Process chrome | foreach {$_.modules} | Where-Object ModuleName -like '\*chrome*' | more

   Size(K) ModuleName                                         FileName
   ------- ----------                                         --------
      2244 chrome.exe                                         C:\Program Files (x86)\Google\Chrome\Application\chrome.exe
      1016 chrome_elf.dll                                     C:\Program Files (x86)\Google\Chrome\Application\88.0.4324...
      2244 chrome.exe                                         C:\Program Files (x86)\Google\Chrome\Application\chrome.exe
      1016 chrome_elf.dll                                     C:\Program Files (x86)\Google\Chrome\Application\88.0.4324...
    152776 chrome.dll                                         C:\Program Files (x86)\Google\Chrome\Application\88.0.4324...

-- More --


PS C:\WINDOWS\system32>  Get-CimInstance Win32_Process

ProcessId Name                        HandleCount WorkingSetSize VirtualSize
--------- ----                        ----------- -------------- -----------
0         System Idle Process         0           8192           4096
4         System                      4114        36864          3997696
108       Registry                    0           34344960       93061120
372       smss.exe                    59          425984         2203359731712
476       csrss.exe                   583         2076672        2203413258240
552       wininit.exe                 165         1449984        2203387731968
560       csrss.exe                   360         1101824        2203404800000
/---OUTPUT TRUNCATED---/




    2) View the additional Properties with Get-Member

PS C:\WINDOWS\system32>  Get-CimInstance Win32_Process | Get-Member
   TypeName:
Microsoft.Management.Infrastructure.CimInstance#root/cimv2/Win32_Process

Name                       MemberType     Definition
----                       ----------     ----------
/---OUTPUT TRUNCATED---/
ParentProcessId            Property       uint32 ParentProcessId {get;}
/---OUTPUT TRUNCATED---/





    3) View the processes with PID and PPID sorted by PID

PS C:\WINDOWS\system32>  Get-CimInstance Win32_Process | select name,ProcessId,ParentProcessId | sort processid

name                        ProcessId ParentProcessId
----                        --------- ---------------
System Idle Process                 0               0
System                              4               0
msedge.exe                         32            9744
Registry                          108               4
smss.exe                          372               4
svchost.exe                       396             696
dwm.exe                           408             612
csrss.exe                         476             468
notepad.exe                       488            7524
/---OUTPUT TRUNCATED---/



    View an instance of all Win32 (system) services.

        Get-Ciminstance Win32_service | Select Name, Processid, Pathname | more

            Pipe in ft -wrap to see full file name/path

PS C:\Users\student> Get-Ciminstance Win32_service | Select Name, Processid, Pathname | ft -wrap | more

Name                                                   Processid Pathname
----                                                   --------- --------
AdobeARMservice                                             4624 "C:\Program Files (x86)\Common Files\Adobe\ARM\1.0\armsvc.exe"
AJRouter                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestricted -p
ALG                                                            0 C:\WINDOWS\System32\alg.exe
AppIDSvc                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestricted -p
Appinfo                                                     7752 C:\WINDOWS\system32\svchost.exe -k netsvcs -p
AppReadiness                                                   0 C:\WINDOWS\System32\svchost.exe -k AppReadiness -p
AppXSvc                                                    13292 C:\WINDOWS\system32\svchost.exe -k wsappx -p
AudioEndpointBuilder                                        3168 C:\WINDOWS\System32\svchost.exe -k LocalSystemNetworkRestricted -p
Audiosrv                                                    3920 C:\WINDOWS\System32\svchost.exe -k LocalServiceNetworkRestricted -p
autotimesvc                                                    0 C:\WINDOWS\system32\svchost.exe -k autoTimeSvc
AxInstSV                                                       0 C:\WINDOWS\system32\svchost.exe -k AxInstSVGroup
BDESVC                                                      1628 C:\WINDOWS\System32\svchost.exe -k netsvcs -p
BFE                                                         3908 C:\WINDOWS\system32\svchost.exe -k LocalServiceNoNetworkFirewall -p
BITS                                                           0 C:\WINDOWS\System32\svchost.exe -k netsvcs -p
BrokerInfrastructure                                        1172 C:\WINDOWS\system32\svchost.exe -k DcomLaunch -p

-- More --


```



## Processes in CMD


```


    View all processes

        tasklist

C:\Users\student> tasklist | more

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0         96 K
Secure System                   72 Services                   0     22,332 K
Registry                       132 Services                   0     28,948 K
smss.exe                       504 Services                   0        940 K
csrss.exe                      876 Services                   0      2,800 K
wininit.exe                    452 Services                   0      3,484 K
csrss.exe                      576 Console                    1      3,648 K
winlogon.exe                   916 Console                    1      6,204 K
services.exe                   976 Services                   0      6,996 K

-- More --





    Display verbose task information in the output

        tasklist /v

C:\Users\student> tasklist /v | more
svchost.exe                   3012 Services                   0      5,364 K Unknown         N/A
Image Name                     PID Session Name        Session#    Mem Usage Status          User Name                      CPU Time Window Title
========================= ======== ================ =========== ============ =============== ========================   ===============================
System Idle Process              0 Services                   0          8 K Unknown         NT AUTHORITY\SYSTEM              1628:26:24 N/A
System                           4 Services                   0         96 K Unknown         N/A                              0:44:21 N/A
Secure System                   72 Services                   0     22,332 K Unknown         N/A                              0:00:00 N/A
Registry                       132 Services                   0     37,948 K Unknown         N/A                              0:00:12 N/A
smss.exe                       504 Services                   0        940 K Unknown         N/A                              0:00:00 N/A
csrss.exe                      876 Services                   0      2,908 K Unknown         N/A                              0:00:06 N/A
wininit.exe                    452 Services                   0      3,488 K Unknown         N/A                              0:00:00 N/A

-- More --


    isplay service information for each process without truncation

        tasklist /svc

C:\Users\student> tasklist /svc

Image Name                     PID Services
========================= ======== ============================================
System Idle Process              0 N/A
System                           4 N/A
Secure System                   72 N/A
Registry                       132 N/A
smss.exe                       504 N/A
csrss.exe                      876 N/A
wininit.exe                    452 N/A
csrss.exe                      576 N/A
winlogon.exe                   916 N/A
services.exe                   976 N/A
LsaIso.exe                     572 N/A
lsass.exe                     1028 EFS, KeyIso, SamSs, VaultSvc
svchost.exe                   1172 BrokerInfrastructure, DcomLaunch, PlugPlay,
                                   Power, SystemEventsBroker

-- More --



    Display modules/dlls associated to all processes.

        tasklist /m | more

C:\Users\student> tasklist /m | more

Image Name                     PID Modules
========================= ======== ============================================
System Idle Process              0 N/A
System                           4 N/A
Secure System                   72 N/A
Registry                       132 N/A
smss.exe                       504 N/A
csrss.exe                      876 N/A
wininit.exe                    452 N/A
csrss.exe                      576 N/A
winlogon.exe                   916 N/A
services.exe                   976 N/A
LsaIso.exe                     572 N/A
lsass.exe                     1028 N/A
svchost.exe                   1160 N/A
sihost.exe                    4720 ntdll.dll, KERNEL32.DLL, KERNELBASE.dll,
                                   msvcp_win.dll, ucrtbase.dll, combase.dll,
                                   RPCRT4.dll, sechost.dll, advapi32.dll,
                                   msvcrt.dll, CoreMessaging.dll, WS2_32.dll,
                                   ntmarta.dll, kernel.appcore.dll,
-- More --



    Display modules/dlls associated to a specific process.

        tasklist /m /fi "IMAGENAME eq chrome.exe"

C:\Users\student> tasklist /m /fi "IMAGENAME eq chrome.exe" | more

Image Name                     PID Modules
========================= ======== ============================================
chrome.exe                    8260 ntdll.dll, KERNEL32.DLL, KERNELBASE.dll,
                                   chrome_elf.dll, VERSION.dll, msvcrt.dll,
                                   ADVAPI32.dll, sechost.dll, RPCRT4.dll,
                                   CRYPTBASE.DLL, bcryptPrimitives.dll,
                                   ntmarta.dll, ucrtbase.dll, user32.dll,
                                   win32u.dll, GDI32.dll, gdi32full.dll,
                                   msvcp_win.dll, IMM32.DLL, SHELL32.dll,
                                   windows.storage.dll, combase.dll, Wldp.dll,
                                   SHCORE.dll, shlwapi.dll, chrome.dll,

-- More  --



    Formating options

        tasklist /fo:{table|list|csv}`

C:\Users\student> tasklist /fo:table | more

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0         96 K
Secure System                   72 Services                   0     22,332 K
Registry                       132 Services                   0     37,876 K
smss.exe                       504 Services                   0        964 K
csrss.exe                      876 Services                   0      2,940 K
wininit.exe                    452 Services                   0      3,712 K

-- More --

C:\Users\student> tasklist /fo:list | more

Image Name:   System Idle Process
PID:          0
Session Name: Services
Session#:     0
Mem Usage:    8 K

Image Name:   System
PID:          4
Session Name: Services
Session#:     0
Mem Usage:    96 K

Image Name:   Secure System
PID:          72
Session Name: Services
Session#:     0
Mem Usage:    22,332 K

-- More --

C:\Users\student> tasklist /fo:csv | more

"Image Name","PID","Session Name","Session#","Mem Usage"
"System Idle Process","0","Services","0","8 K"
"System","4","Services","0","96 K"
"Secure System","72","Services","0","22,332 K"
"Registry","132","Services","0","37,876 K"
"smss.exe","504","Services","0","964 K"
"csrss.exe","876","Services","0","2,940 K"
"wininit.exe","452","Services","0","3,712 K"
"csrss.exe","576","Console","1","4,948 K"
"winlogon.exe","916","Console","1","6,600 K"
"services.exe","976","Services","0","7,636 K"

-- More --





    Filtering for specific string/process

        tasklist /fi "IMAGENAME eq lsass.exe"

C:\Users\student>tasklist /fi "IMAGENAME eq lsass.exe

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
lsass.exe                     1028 Services                   0     17,984 K


```

## Processes in GUI



Task Manager

    Microsoft Default

Procexp.exe

    We’ll go over it in Sysinternal Tools Lesson


## Services in PS


```


    View only system services and display Name, PID, and the path they are initiated from.

        Get-Ciminstance Win32_service | Select Name, Processid, Pathname | more

            Pipe in a ft -wrap to see full pathname.

PS C:\Users\student> Get-Ciminstance Win32_service | Select Name, Processid, Pathname | more

Name                                                   Processid Pathname
----                                                   --------- --------
AdobeARMservice                                             4624 "C:\Program Files (x86)\Common Files\Adobe\ARM\1.0\armsvc.exe"
AJRouter                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestri...
ALG                                                            0 C:\WINDOWS\System32\alg.exe
AppIDSvc                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestri...
Appinfo                                                     7752 C:\WINDOWS\system32\svchost.exe -k netsvcs -p
AppReadiness                                                   0 C:\WINDOWS\System32\svchost.exe -k AppReadiness -p
AppXSvc                                                        0 C:\WINDOWS\system32\svchost.exe -k wsappx -p
AudioEndpointBuilder                                        3168 C:\WINDOWS\System32\svchost.exe -k LocalSystemNetworkRestric...
Audiosrv                                                    3920 C:\WINDOWS\System32\svchost.exe -k LocalServiceNetworkRestri...

-- More --


    View all services.

        Get-service

PS C:\Users\student> get-service | more

Status   Name               DisplayName
------   ----               -----------
Stopped  AarSvc_5d854       Agent Activation Runtime_5d854
Running  AdobeARMservice    Adobe Acrobat Update Service
Stopped  AJRouter           AllJoyn Router Service
Stopped  ALG                Application Layer Gateway Service
Stopped  AppIDSvc           Application Identity

-- More  --


    View a defined service, showing all properties in list format.

        get-service ALG | format-list *

PS C:\Users\student> get-service ALG | format-list *


Name                : ALG
RequiredServices    : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
DisplayName         : Application Layer Gateway Service
DependentServices   : {}
MachineName         : .
ServiceName         : ALG
ServicesDependedOn  : {}
ServiceHandle       :
Status              : Stopped
ServiceType         : Win32OwnProcess
StartType           : Manual
Site                :
Container           :


    View only currently running services.

        Get-Service | Where-Object {$_.Status -eq "Running"}

PS C:\Users\student> Get-Service | Where-Object {$_.Status -eq "Running"} | more

Status   Name               DisplayName
------   ----               -----------
Running  AdobeARMservice    Adobe Acrobat Update Service
Running  Appinfo            Application Information
Running  AppXSvc            AppX Deployment Service (AppXSVC)
Running  AudioEndpointBu... Windows Audio Endpoint Builder
Running  Audiosrv           Windows Audio
Running  BDESVC             BitLocker Drive Encryption Service
Running  BFE                Base Filtering Engine

-- More  --



```


## Services in CMD

```
    iew Services

        sc query

C:\Users\student>sc query | more

SERVICE_NAME: AdobeARMservice
DISPLAY_NAME: Adobe Acrobat Update Service
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

SERVICE_NAME: Appinfo
DISPLAY_NAME: Application Information

-- More --

    View extended information for all services.

        sc queryex type=service

C:\Users\student>sc queryex type=service | more

SERVICE_NAME: AdobeARMservice
DISPLAY_NAME: Adobe Acrobat Update Service
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
        PID                : 4624
        FLAGS              :

SERVICE_NAME: Appinfo
DISPLAY_NAME: Application Information

-- More  --


    View extended information for all inactive services.

        sc queryex type=service state=inactive

C:\Users\student>sc queryex type=service state=inactive | more

SERVICE_NAME: AJRouter
DISPLAY_NAME: AllJoyn Router Service
        TYPE               : 20  WIN32_SHARE_PROCESS
        STATE              : 1  STOPPED
        WIN32_EXIT_CODE    : 1077  (0x435)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
        PID                : 0
        FLAGS              :

SERVICE_NAME: ALG
DISPLAY_NAME: Application Layer Gateway Service
        TYPE               : 10  WIN32_OWN_PROCESS

-- More  --


    Additional examples of the SC command

C:\sc /?                           # Basic service enumeration
C:\sc qc                           # Configuration information for a service
C:\sc queryex eventlog             # Information for the eventlog service including pid
C:\sc qdescription eventlog        # Query eventlog service description
C:\sc qc eventlog                  # Show the binary command that loads the service
C:\sc showsid eventlog             # Displays the service SID and status
c:\sc enmudepend                   # Lists the services that cannot run unless the specified service is running


    View all currently running services.

        net start

C:\Users\student>net start | more
These Windows services are started:

   Adobe Acrobat Update Service
   Application Information
   AppX Deployment Service (AppXSVC)
   AVCTP service
   Background Tasks Infrastructure Service
   Base Filtering Engine

-- More  --



```


## Services in GUI

```


services.msc

    Pull it up in the Windows search bar and show them around if you’d like.

PsService

    Sysinternal Tool

```


## Scheduled Task in PS


```


    View all properties of the first scheduled task.

        Get-ScheduledTask | Select * | select -First 1

PS C:\Users\student> Get-ScheduledTask | Select * | select -First 1


State                 : Ready
Actions               : {MSFT_TaskExecAction}
Author                : Adobe Systems Incorporated
Date                  :
Description           : This task keeps your Adobe Reader and Acrobat applications up to date with the latest enhancements and security fixes
Documentation         :
Principal             : MSFT_TaskPrincipal2
SecurityDescriptor    :
Settings              : MSFT_TaskSettings3
Source                :
TaskName              : Adobe Acrobat Update Task
TaskPath              : \
Triggers              : {MSFT_TaskLogonTrigger, MSFT_TaskDailyTrigger}
URI                   : \Adobe Acrobat Update Task
Version               :
PSComputerName        :
CimClass              : Root/Microsoft/Windows/TaskScheduler:MSFT_ScheduledTask
CimInstanceProperties : {Actions, Author, Date, Description...}
CimSystemProperties   : Microsoft.Management.Infrastructure.CimSystemProperties




```


## Scheduled Task IN CMD

```
schtasks /query /tn "IchBinBosh" /v /fo list

Folder: \
HostName:                             ADMIN-STATION
TaskName:                             \IchBinBosh
Next Run Time:                        6/1/2021 5:02:00 PM
Status:                               Ready
Logon Mode:                           Interactive only
Last Run Time:                        6/1/2021 4:47:00 PM
Last Result:                          0
Author:                               ADMIN-STATION\andy.dwyer
Task To Run:                          powershell.exe -win hidden -encode JABMAD0ATgBlAHcALQBPAGIAagBlAGMAdAAgAFMAeQBzAHQAZQBtAC4ATgBlAHQALgBTAG8AYwBrAGUAdABzAC4AVABjAHAATABpAHMAdABlAG4AZQByACgANgA2ADYANgApADsAJABMAC4AUwB0AGEAcgB0ACgAKQA7AFMAdABhAHIAdAAtAFMAbABlAGUAcAAgAC0AcwAgADYAMAA=
Start In:                             N/A
Comment:                              N/A
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          andy.dwyer
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        One Time Only, Minute
Start Time:                           4:02:00 PM
Start Date:                           6/1/2021
End Date:                             N/A
Days:                                 N/A
Months:                               N/A
Repeat: Every:                        0 Hour(s), 15 Minute(s)
Repeat: Until: Time:                  None
Repeat: Until: Duration:              Disabled
Repeat: Stop If Still Running:        Disabled


```


## Scheduled Task in GUI



```



Windows Default

    Task Scheduler

Sysinternal tool

    Autoruns.

        We’ll go over this more in Sysinternal Tools.


```


## Auto Run Registry 

What are some Registry keys that can be used for autoruns?

    Registry Keys Locations, Locations connected with Services.

        HKLM\Software\Microsoft\Windows\CurrentVersion\Run - Local Machine

        HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

        HKLM\System\CurrentControlSet\Services

    Remember that the Users have individual Hives with autoruns as well as the Current User.

        HKCU\Software\Microsoft\Windows\CurrentVersion\Run - Current User

        HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce

        HKU\<sid>\Software\Microsoft\Windows\CurrentVersion\Run - Specific User

        HKU\<sid>\Software\Microsoft\Windows\CurrentVersion\RunOnce

    The order in which services are loaded can be adjusted.

        HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\ServiceGroupOrder

        HKEY_LOCAL_MACHINE\CurrentControlSet\Control\GroupOrderList



    A: High PID duplicate, unfamiliar process name, and misspelling.

        Two smss.exe, one with a high PID of 8972

        bad.exe

        reqedit.exe
## NetConnections in PS

```

PS C:\Users\andy.dwyer> Get-NetTCPConnection -State Established

LocalAddress        LocalPort RemoteAddress      RemotePort State       AppliedSetting OwningProcess
------------        --------- -------------      ---------- -----       -------------- -------------
10.23.0.2           49701     52.177.165.30      443        Established Internet       2988
10.23.0.2           22        10.250.0.15        59038      Established Internet       2944
```

## NetConnections in CMD

```


    Show netstat help and point out the following:

        netstat /?

-a   Displays all connections and listening ports
-n   Displays addresses and port numbers in numerical form
-o   Displays the owning process ID (PID) associated with each connection
-b   Displays the executable involved in creating each connection (must have admin rights)


    Displays all TCP/UDP connections with ports in numerical form with PID and executable associated to the connections

        netstat -anob | more

andy.dwyer@ADMIN-STATION C:\Users\andy.dwyer>

netstat -anob | more

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:22             0.0.0.0:0              LISTENING       2944
 [sshd.exe]
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       832
  RpcSs
 [svchost.exe]
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
 Can not obtain ownership information
  TCP    0.0.0.0:3389           0.0.0.0:0              LISTENING       304
  TermService
 [svchost.exe]
  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING       4456
  CDPSvc

-- More --



```

## NetConnections in GUI

```
TCPView

    We will go over this in Sysinternal tools



```

## ID Abnormalities and Suspicious Activity

```


    Q: What are some Abnormal things we could see in a process list?

        Misspelling of process names and descriptions.

            Ex. scvhost instead of svchost

        Directory the process is running out of.
        Q: Which directory are windows executables typically run out of?

            System Processes run from C:\Windows\System32

            Third party processes will run elsewhere.

            Ex. Chrome runs from C:\Program Files

        Processes that have non-standard listening ports open or ports with SYN/SENT.

            Like HTTP being used on any port other than 80. (ex. HTTP over port 808 or 880)

        Multiple processes with the same name that should be unique such as LSASS, SMSS
 submitted the JST 
            System process with a high PID.

        Handles or DLLs a process is using.

            Dig Deeper into DLLs:

                Microsoft Compromised DLLs

                DLL Hijacking




    A: High PID duplicate, unfamiliar process name, and misspelling.

        Two smss.exe, one with a high PID of 8972

        bad.exe

        reqedit.exe



```





# User Access Control (Day 6 Continued)

## Color Codes


Multiple color-coded consent prompts

    Red - Application or publisher blocked by group policy

    Blue & gold - Administrative application

    Blue - Trusted and Authenticode signed application

    Yellow - Unsigned or signed but not trusted application



## How does UAC know how to act



When an application is run, UAC checks that file’s manifest for instructions

What is a file Manifest?

    A manifest file on Windows holds Metadata and tells Windows how the file should be executed.

There are three types of execution levels in a file’s manifest.

    asInvoker - The application will run with the same permissions as the process that started it. The application can be elevated to a higher permission level by selecting Run as Administrator.

        Ex: C:\Windows\System32\cmd.exe

    requireAdministrator - The application will run with administrator permissions. The user who starts the application must be a member of the Administrators group. If the opening process is not running with administrative permissions, the system will prompt for credentials.

    highestAvailable - The application will run with the highest permission level that it can. If the user who starts the application is a member of the Administrators group, this option is the same as requireAdministrator. If the highest available permission level is higher than the level of the opening process, the system will prompt for credentials.

        Ex: C:\Windows\regedit.exe

1.3.1 Autoelevate setting

    Some Windows executables can "auto elevate" without a prompt.

    Files that have "auto elevate" in their permissions will not prompt UAC



## Viewing Manifest Settings

```



The Sysinternals Tool sigcheck will allow the viewing of these settings.
Map the Sysinternals Command in Powershell

PS C:\Users\student> net use * http://live.sysinternals.com
PS C:\Users\student> z:

View the autoelevate setting of slui

PS Z:\> ./sigcheck -m C:\Windows\System32\slui.exe

View the highest available setting of regedit

PS Z:\> ./sigcheck -m C:\windows\regedit.exe

How to locate Windows executables that have autoelevate in the manifest

PS Z:\> ./strings –s c:\windows\system32\*.exe | findstr /i autoelevate



```

## Demo (Fodhelper.exe)

```
What is fodhelper?

Fodhelper - Introduced in Windows 10 to manage optional features like region-specific keyboard settings. Fodhelper.exe is located in the C:\Windows\System32 folder

Explain how the UAC Bypass fodhelper exploit was found.

    Researcher used Procmon to find the registry keys being called that do not exist.

    Show the registry hives on screen and ask the students which hive can be edited as a non-admin user and ask why this is important to us? (Non-admin users can edit the HKCU keys and manipulate the behavior of the system)

        HKCU:\Software\Classes\ms-settings\shell\open\command

Demo using Procmon to find registry keys called by autoelevate applications

    Open Procmon

    Run fodhelper.exe

    Stop Capture

    Create Filter ProcessName is fodhelper.exe

    Create Filter Operation is RegOpenKey Action Include

    Look for Registry Keys HKCU\software\classes

    Look fro Registry Keys HKCU\ms-settings\shell\open\command

	Explain the Registry Key HKCU is writable by the user and that ms-settings\shell\open\command doesn’t exist so we can exploit this key to perform what behavior we want

What does this key allow us to do?

PS C:\Users\Student> HKCU:\Software\Classes\ms-settings\shell\open\command

    Enables us to provide to the program additional instructions on what to do when the program opens.

What does the DelegateExecute string value do?

    Tells the program to execute what is in the default value of the registry key.

Demo via GUI so students can do Activity via PowerShell and demonstrate command-line knowledge.
Look at autoElevate & requestedExecutionLevel

PS C:\Users\Student> ./sigcheck -m C:\windows\system32\fodhelper.exe

Open the registry editor

PS C:\Users\Student> regedit.exe

Create the key

Right click on HKCU:\Software\Classes and select New > Key

Name it ms-settings

Then add New > Key shell

Then add New > Key open

Then add New > Key command
Create the String Value

Right click in the whitespace on the right side of pane Create New > String Value DelegateExecute
Right Click on (Default) String value

Add C:\windows\system32\cmd.exe
From command-line execute

C:\windows\system32\fodhelper.exe

NOTE:A new window will pop up with Administrator privileges

Activity: UAC Bypass
```



# Sysinternals Tool (Day 6 Continued)

## Sysinternals Download


    Windows Sysinternals is a collection of advanced system utilities that were established to help users manage,troubleshhot and diagnose Windows systems and applications. The sysinternals tools are housed on the website https://live.sysinternals.com/ to be readily available to run directly from the site. We will have the tools downloaded on our box(es) for ease of use.

    These are a few commands/instructions to have the tools on your local Windows box.

PS C:\windows\system32> net use * http://live.sysinternals.com 
Drive Z: is now connected to http://live.sysinternals.com.

The command completed successfully.

	The 'net use' command can be used to create a connection to the Live Sysinternals website. (can be persistent with parameter set)


PS C:\windows\system32> New-PSDrive -Name "SysInt" -PSProvider FileSystem -Root "\\live.sysinternals.com\Tools" 

Name           Used (GB)     Free (GB) Provider      Root                                                    CurrentLocation
----           ---------     --------- --------      ----                                                    ---------------
SysInt                                 FileSystem    \\live.sysinternals.com\Tools

	'New-PSDrive' is a PowerShell command used to create a temporary or persistent connection to the Live Sysinternals website.

PS C:\Users\andy.dwyer\Desktop> $wc = new-object System.Net.WebClient 

PS C:\Users\andy.dwyer\Desktop> $wc.DownloadFile("https://download.sysinternals.com/files/SysinternalsSuite.zip",
"$pwd\SysinternalsSuite.zip") 

PS C:\Users\andy.dwyer\Desktop> Expand-Archive SysinternalsSuite.zip 

	Location may be different on your box The webclient provides common methods for sending and receiving data to/from a URI (Uniform Resource Identifier)
	Download the .zip file from the website
	Unzip the file, creates a folder on the desktop


## Procmon Process Monitor




Using PROCMON to monitor the Windows Boot Process


Q: What is Process Monitor?

    Process Monitor is an advanced monitoring tool for Windows that shows real-time File System, Registry and Process/Thread activity. It combines the features of two legacy Sysinternals utilities, Filemon and Regmon.

    It also has an option to Log at boot and we are going to go over a demo and analyze the Windows Boot Process.


Q: What does Procmon capture?

    Registry - Anything from creating, reading, deleting, or querying keys

    File System - File creation, writing, deleting, etc and this includes both local and network drives

    Network - This only shows source and destination TCP/UDP traffic

    Process - These events are for processes and threads where a process starts, a thread starts or exits, etc. Probably better in ProcExp

    Profiling - Checks the amount of processor time and memory use of each process


    Tabs

        File - Has the save feature which allows exporting to CSV and CML as well as the native PML format, backup up files in virtual memory or in previous PMLs, import and export your Procmon configurations, and turn on and off Capture Events.

        Edit - Has features for ease of access: Copy, Find, Find highlight, Find Bookmark, an Auto-scroll, and Clear Display.

        Event - Options for the currently selected event as if you right clicked. You can view Properties, Stack, Toggle Bookmark, Jump To, Search Online, Filter Include/Exclude, and Highlight options.

        Filter - For advanced search options it has Enabled Advanced Output, Filter, Reset Filter, Load (saved) Filters, Save Filters, Organize (saved) Filters, Drop Filtered Events (will not capture events that you are filtering) and highlight filters (or things that you have highlighted).

        Tools - Summary outputs and information cheat sheets. System Details, Process Tree, Process Activity Summary, File Summary, Registry Summary, Stack Summary, Network Summary, Cross Reference Summary (paths that are written and read between differing processes)

        Options - Configuration of the GUI, Has Always on Top, Font, Highlight Colors, Configure Symbols (for the stack tab), Select Columns, History Depth (how many events it will hold), Profiling Events (if you want it changed to milliseconds), Enable Boot Logging, Show Resolved Network Addresses, Hex Offsets and Length, Hex Process and Thread IDs.

        Help - Help Manual, Command Line Options, About


    Default Columns

        Time - Shows the exact time the event occurred

        Process Name - The name of the process that generated the event. It doesn’t show the full path by default, but if you hover over it then the full path is displayed.

        PID - Process ID

        Operation - Name of the operation being logged, with corresponding icon (registry, file, network, process)

        Path - The path of the event that was being touched (the affected) and not the event of the process (the instigator)

        Result - This shows the result of the operation in codes like SUCCESS or ACCESS DENIED

        Detail - additional information for troubleshooting



## Autoruns



Q: What is AUTORUNS?

    Autoruns shows applications automatically started on during system boot or login as well as the Registry and file system locations for auto-start configurations. Examples: AppInit, Winlogon, Scheduled Tasks, Services, Logon, etc.


    The External Interface

        Highlighted items that are colors notate special meanings

            Pink - Means no publisher information was found or the digital signature doesn’t exist or match.

            Green - Used when comparing previous set of Autorun data to indicate an item wasn’t there last time.

            Yellow - The startup entry is there, but the file or job it points to doesn’t exist anymore.

        Highlight a task - Right-Clicking or Entry Tab - Allows you to Jump to where the entry resides in the File System, Search Online, Open in Process Explorer, Go to it’s Registry Key or Task Scheduler.

        User Tab - Allows you to analyze different user accounts autoruns (must be administrator to view other accounts).

        Options Tab- Allows you to hide certain entries and also allows font changes and scan options. The Scan Option allows you to choose to scan Per-User Locations, Verify code signatures, and Check Virustotal.com.

        File Tab - Allows you to Analyze Offline systems and compare files from other systems or yours, Very handy.


Q: Where are some of the places that AUTORUNS look?

    The Internal Tabs

        Everything - Shows all of the outputs from the other tabs together on this one tab. One stop Shop, Not as messy as you might think.

        Explorer - This tab list add-on components that load themselves into Windows Explorer. Mostly context menu add-ons and the sort.

        Logon - Checks the normal locations for things to be automatically loaded, including registry keys Run and RunOnce keys, the Start Menu, up to 43 locations.

        Internet Explorer - This tab list all of the browser extensions, toolbars, browser helper objects that are used by malware to either spy or show you ads.

        Scheduled Tasks - This tab shows Tasks that are scheduled. Malware uses it to install, reinstall, and do all types of nefarious things with this.

        Services - This tab list auto-start services. Malware sometimes hides itself as a service by creating it’s own service that helps make sure that other malware processes are running.

        Drivers - .Sys files. Used to call a bunch of system and svchost executables. Malware can hide in here, look at the path.

        Codecs - Libraries of code that handle media playback for videos and audio. Used by malware to automatically start on systems.

        Boot Execute - Things that can’t happen when windows is loaded like a hard drive check.

        Image Hijacks - Will let you know if a program has been replaced with another, ex: when you run notepad.exe it runs calc.exe instead.

        AppInit - Settings where RequireSignedAppInit_DLLs key is set to 0 and any DLLs that were loaded with that setting will be showed.

        KnownDLLs - Listed to make sure you can verify and that they are all verified and published DLLs.

        Winlogon - Shows DLLs that register for Winlogon notification of logon events.

        Winsock Providers - Networking, shows registered winsock providers. Malware often installs itself as these because there are few tools that can remove them.

        Print Monitors - Third party printer applications, Drivers and Dlls that load into the print spooling service. Malware uses this support to autostart itself.

        LSA Providers - Shows registered LSA authentication notification and security packages.

        Network Providers - Third party network providers.

        WMI - Views WMI related persistence (Ex: If a powershell script was using a get-wmiobject, it would show up).

        Office - Shows Office related material. If excel scripts or power points were infected and opening at start they would show here.


## Autorun Demo

```


    Have students log into their Admin-Station as Army/andy.dwyer.


    Have students go to C:\SysinternalsSuite <Location may be different> and open up Autoruns.exe go to the Options tab and make sure that Hide Windows Entries is unchecked.


    The entry created from the PROCMON demo "RunME Notepad (Verified) c:\windows\notepad.exe" under the HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run section in the Everything tab and the Logon tab should be visible.

        Side note: Unchecking the Hide Windows Entries can create a lot of unneeded clutter. Go to the Options tab and check Hide Windows Entries.

        Notate that anything (Verified) Microsoft Windows as a Publisher is removed to the class.


    Discuss what we are looking at and what we are looking for using our notepad.exe as an example such things as registry keys, path, names, digital signatures, etc.


    Click on the Logon tab, it gives a chunk of information that the Everything tab gave us but gives us only where autoruns checks for "normal" autorun locations. Discuss the locations that malware might hide. (ex: Run, RunOnce, etc)


    Click on the Scheduled tasks tab. Discuss what ways malware might use schedule tasks and what ways we could mitigate it. (ex: create schedule task to install itself, to set a callback at a certain time/ group policy)


    Click on the Services tab. Discuss ways that malware can take advantage of services and ways to mitigate it. (ex: create a service that auto starts at boot that runs a malware process, group policy)


    Discuss the advantages and disadvantages if any and what use do they believe if any they can get out of the tool.


    Clarify any Questions or gaps in learning. END DEMO

    ANY QUESTIONS




```

## Procexp



Analyze Windows running processes using PROCEXP


Q: What is Process Explorer

    Process Explorer is a task manager and system monitor which collects information on running processes with such features as Hierarchical view of processes, live CPU activity, ability to kill and suspend processes, display DLLs loaded, create process dumps, display handles and much more.

    There will be a lot of similarities in the options and results that both Task Manager and Process Explorer give.

    Process Explorer should be run as administrator to get it’s full usage.

    Process Explorer has a powerful search capability that can show processes and their respective DLLs and handles.


    Default Interface Columns

        Process - Processes are listed according to their parent child relationship. Processes listed as a sub row are child processes of the upper process.

        CPU - Shows general CPU usage percentage of this process.

        Private Bytes - Shows the size of memory only used by this process and not shared with other processes and DLL’s.

        PID - Shows the process identifier given by the operating system and used to easily identify the process.

        Description - Shows process information (what it is).

        Company Name - Shows the application publisher company.


    Interface Tabs

        File - Allows you to run applications as if from the "Run window" and if you are administrator you can run as a limited user (lower credentials), save functions, and the ability to shutdown, restart, lock, etc the system.

        Options - Allows you to the option to run Process Explorer at logon, the ability the verify Image (digital) signatures, check virus total, to replace task manager with process explorer, and configure graphical options such as colors/fonts/thread symbols/tray icons/highlight duration.

        View - Shows system information (resource monitor in task manager), manipulate how you view the processes such as speed/refresh rate, allows column manipulation such as adding and removing columns.

        Process - Is for individual clicked on processes. It shows windows which allows selected processes to be brought to front or maximized or minimized, set affinity which allocated CPU usage, sets priority for it’s placement in the pool, can kill/kill tree/restart/suspend, create a process dump, search the selected process on virustotal, the select the process’s properties and search it online.

        Find - Used for finding Handles and DLLs.

        Handle - If split window is selected this will appear. Select a handle on the lower panel and you are able to close the handle or select it’s properties. It is interchangeable with a DLL tab depending on what you select to look at in the lower panel. The DLL tab shows properties, search online, and check virus total.

        Users - Used for controlling users on host if you are admin. Can connect, disconnect, logoff, remote control, send messages, and view some brief properties about the user’s status.

        Help - Help manual and an about


    Colors (Selected by default)

        Green - New Objects - Briefly flashes "Green" before changing into one of the 9 other colors.

        Red - Deleted Objects - Dead.

        Lavender - Own Processes - Processes owned by the current logged in user.

        Salmon - Services

        Gray - Suspended Processes

        Purple - Packed Images -Processes might contain compressed code hidden inside them. Malware uses it because it obfuscates the contents of the file.

        Cyan - Immersive Process - Windows Store App related, Uses Windows 8+ new APIs



## Procexp Demo

```


    Have students open up their Admin-Station and log in as Army\andy.dwyer.


    Once logged on they will need to go to C:\SysinternalsSuite <Location may be different> and Right-Click on Procexp.exe and select Run as Administrator and Maximize it.

        Press "spacebar" to pause ProcExp from refreshing any further so it will be easier to continue (hitting spacebar again will un-pause it).


    Find notepad.exe (If the process tree is not already in Tree form then go to the View tab and click on Process Tree) and discuss the lay out and columns reinforcing the FG.

        Once notepad.exe is found, double-click it. The data returned is PATH, CMDLINE, AUTOSTART, TCP/IP, STRINGS, and much more. Discuss why this is important.


    Close the window. Go to the Options tab, click on VirusTotal.com and click on Check VirusTotal.com and discuss VirusTotal and it’s effects. Agree to the Terms of service to continue.

        A new column populates on the far right called VirusTotal and everything now has a score (or almost everything).


    Click on the Options" tab again and click Verify Image Signatures to check that everything has verified publisher digital signatures (discuss why this is important).

        The Verified Signer column and Company name are now listed (what are we looking for?).


    Click on View and click on Select Columns, Select Auto Start Location and retouch on autoruns briefly in the Process Image tab and Receives and Sends from the Process Network tab.

        Explain what we are looking for from these Three tabs are autorun locations and network traffic.


    Between the View and Process tabs there is a Show Lower Pane button, click that button and it will bring up a list of Handles or DLLs, we want Handles (Handles in Windows refer to an integer value that is used to uniquely identify a resource in memory like a window, an open file, a process, etc).

        To change between the two, you would click on the View tab and click on Lower Pane View and there are two options DLLs and Handles.

        We can see any Files, Processes, Registry keys associated with our selected process and discuss some of the things we might be looking for.


    Switch to DLLs by repeating the previous step. Discuss what we are looking for and why we are looking at DLLs. Unsigned, not in C:\Windows\System32, No description, weird names, anything that looks abnormal.


    Double click on notepad.exe, click on the Image tab and to click the Explore option for Path information.

        The first thing to look for is if there are any DLLs in the folder that are not listed in Process Explorer. Discuss rogue DLLs and files.

        Malware sometimes has associated DLLs that come packaged with it or is itself a DLL that plugs into legitimate processes or other DLLs, Discuss ways Malware injects.

        Look at time stamps at the files in the folder and at the files themselves, but at this point we would start to move onto other tools and methods.


    Discuss the advantages and disadvantages if any and what use do they believe if any they can get out of the tool.

    ANY QUESTIONS?



```

## TCP View


Analyze Windows network connections using TCPVIEW

Q: What is TCPVIEW?

    TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections.[1]

    It’s a more informative Graphical (GUI) representation of the NETSTAT command

    Shows network connections

Open TCPView

    If you see any Red Rows

        That indicates when a network connection terminates

    If you see any Green Rows

        That indicates when a connection is made

    If the colors are disappearing to quickly, you can modify the Update Speed

        View → Update Speed → 5 seconds

        Keeps colors longer to see what is stopping or starting

    Column Sorting

        Allows you to see lines grouped by State or Process

Q: What are some known malicious ports?

    1337 Leet Port = 1337 means "elite" in hacker/cracker spelling (1=L, 3=E, 7=T, "LEET"="ELITE"). Because of the reference, it may be used by some backdoors.

    31337 Eleet port

    4444 Metasploit default listener port

        To kill Processes

    Right click → End Process



## PSExec



Analyze Windows privileges' using PsExec

Q: What is PsExec?

    light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software.

    Switches

        -s Run as System account

        -i interacts with the desktop

        -c Copy the specified program to the remote system for execution.

    Demo regedit.exe

        Open as regular user

        Go to HKLM\SAM\SAM

        Can’t go deeper

From an admin cmd shell

psexec -i -s regedit.exe

    Can view down to HKLM\SAM\SAM\Domains\Accounts\Users

This function will not work in our current environment but talk about the ability of running the tool across a network. Also, demo a cmd shell back from another system as System

PsExec -s \\file-server cmd.exe
whoami
nt authority\system




## PSLoggedon



Analyze Windows logons using PsLoggedon

Q: What is PsLoggedon used for?

    It can list users that are logged on currently to a system

Q: How can I view the options for PsLoggedon?

    psloggedon.exe /? -accepteula

Q: What does the -accepteula do?

    Prevents a pop up to accept the End User License Agreement

Show output from running PsLoggedon

PS C:\SysinternalsSuite> .\PsLoggedon.exe

PsLoggedon v1.35 - See who's logged on
Copyright (C) 2000-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

Users logged on locally:
     <unknown time>             ADMIN-STATION\cloudbase-init
     5/10/2021 2:02:19 PM       ADMIN-STATION\student
     5/10/2021 2:07:48 PM       ADMIN-STATION\andy.dwyer

No one is logged on via resource shares.

The following function will not work in our current environment but talk about the ability of pulling logon information from remote boxes. Set up a Server List for this demo

Write-Output File-Server > "$env:HOMEPATH\Desktop\ServerList.txt"
Write-Output Domain-Controll >> "$env:HOMEPATH\Desktop\ServerList.txt"
Write-Output $env:Computername >> "$env:HOMEPATH\Desktop\ServerList.txt"

Run PsLoggedon on all the systems in the list

Foreach ($system in (gc "$env:HOMEPATH\Desktop\ServerList.txt") ) {.\PsLoggedon.exe \\$system -nobanner}


Q: How could this tool be used in Cyber?

    Gather a list of every user currently logged on a system

    Possibly find for a malicious actor in the network

    Look for logged on users who are logging in outside of normal hours




## LogonSessions



Analyze Windows session using LogonSessions

While Psloggedon shows who is logged on and what time he/she logged on, loggonsessions shows how that user logged on.

2
Interactive
A user logged on to this computer.

3
Network
A user or computer logged on to this computer from the network.

4
Batch
Batch logon type is used by batch servers, where processes may be executing on behalf of a user without their direct intervention.

5
Service
A service was started by the Service Control Manager.

7
Unlock
This workstation was unlocked.

8
NetworkCleartext
A user logged on to this computer from the network. The user’s password was passed to the authentication package in its un-hashed form. The built-in authentication packages all hash credentials before sending them across the network. The credentials do not traverse the network in plaintext (also called cleartext).

9
NewCredentials
A caller cloned its current token and specified new credentials for outbound connections. The new logon session has the same local identity, but uses different credentials for other network connections.

10
RemoteInteractive
A user logged on to this computer remotely using Terminal Services or Remote Desktop.

11
CachedInteractive
A user logged on to this computer with network credentials that were stored locally on the computer. The domain controller was not contacted to verify the credentials.[2]


## PsList

```


Analyze Windows processes using PsList on local or remote systems

Q: What is PsList used for?

    Another command line tool for gathering process information

    Allows you to refresh the tool for a specified period of time

Q: How do you get the help file for PsList?

pslist /?

Q: How can I get a process list that updates every 10 seconds for 100 seconds?

pslist -s 100 -r 10

    -s [n] run for this many seconds

    -r n refresh every n seconds

Q: Why is this important to Cyber?

    To see if a new admin logs in. Can’t refresh this by default with tasklist or get-process

    To see when a new process starts that could jeopardize your mission

Q: How can this be run on a remote system?

pslist \\file-server 

	Will not work in current environment

Show the output from running the tool

PS C:\SysinternalsSuite> pslist

PsList v1.4 - Process information lister
Copyright (C) 2000-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

Process information for ADMIN-STATION:

Name                Pid Pri Thd  Hnd   Priv        CPU Time    Elapsed Time
Idle                  0   0   4    0     52   115:19:16.046    28:59:33.270
System                4   8 101 4115    188     0:01:21.687    28:59:33.270
Registry            104   8   4    0    360     0:00:03.484    28:59:40.221
smss                324  11   2   59    500     0:00:00.171    28:59:33.264
csrss               432  13  12  539   1772     0:00:00.921    28:59:09.665
wininit             508  13   1  168   1356     0:00:00.078    28:59:09.146
csrss               516  13  10  388   1640     0:00:00.656    28:59:09.139
winlogon            604  13   3  281   2420     0:00:00.125    28:59:09.097
services            652   9   5  669   4872     0:00:14.375    28:59:09.056
lsass               664   9   7 1700   8080     0:00:09.531    28:59:08.760
_Output_Truncated_


```



## PsInfo

```


Analyze Windows system information using PsInfo

    Gathers key system information from both local and remote systems.

The following function will not work in our current environment but talk about the ability of pulling PsInfo information from remote boxes. Set up a Server List for this demo

Write-Output File-Server > "$env:HOMEPATH\Desktop\ServerList.txt"
Write-Output Domain-Controll >> "$env:HOMEPATH\Desktop\ServerList.txt"
Write-Output $env:Computername >> "$env:HOMEPATH\Desktop\ServerList.txt"

Run PsInfo on all the systems in the list

Foreach ($system in (gc "$env:HOMEPATH\Desktop\ServerList.txt") ) {.\Psinfo.exe -hs -nobanner \\$system | out-file $env:homepath\Desktop\psinfo.txt -append}


Show the output from running the tool

    Talk about the importance of identifying the following system information and how it can be used to associate possible exploits by either the network owner or an adversary.

PS C:\SysinternalsSuite> psinfo

PsInfo v1.78 - Local and remote system information viewer
Copyright (C) 2001-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

System information for \\ADMIN-STATION:
Uptime:                    1 day 5 hours 9 minutes 14 seconds
Kernel version:            Windows 10 Enterprise, Multiprocessor Free
Product type:              Professional
Product version:           6.3
Service pack:              0
Kernel build number:       17763
Registered organization:
Registered owner:
IE version:                9.0000
System root:               C:\windows
Processors:                4
Processor speed:           2.2 GHz
Processor type:            AMD EPYC-Rome Processor
Physical memory:           2 MB
Video driver:              Microsoft Basic Display Adapter



```


## Strings

```


Analyze Windows files using Strings

    Switches

        -a ASCII

Must provide literal file path

strings -a C:\users\andy.dwyer\Desktop\<doc>.txt



```



## Handle


```


Analyze Windows handles process using Handle

Q: What is a handle?

    Handles are data structures that represent open instances of basic operating system objects applications interact with, such as files, registry keys, synchronization primitives, and shared memory.

    Applications can’t access objects directly, must obtain a handle

    Handles for each process are tracked in an internal table known as the Object Manager

    Handles allow a common interface to objects, regardless of underlying changes to the object

    Handles allow Windows to track ACLs for objects during handle creation time

DEMO: Killing a handle using Sysinternal handle.exe

Step one: Open Powershell.exe and start-transcript

PS C:\windows\system32> Start-Transcript 
Transcript started, output file is C:\Users\andy.dwyer\Documents\PowerShell_transcript.ADMIN-STATION.x9xkJMAJ.20210510184103.txt

	Note the file name and location

Step two: Locate the PID number of powershell.exe, we will run tasklist and scroll down until you find powershell

tasklist

Step three: In a different cmd prompt, use the following command to show the handles in use with powershell.exe

C:\windows\system32>handle.exe -p <pid of powershell> -accepteula

Nthandle v4.22 - Handle viewer
Copyright (C) 1997-2019 Mark Russinovich
Sysinternals - www.sysinternals.com

   40: File  (RW-)   C:\Windows\System32
   C4: File  (R-D)   C:\Windows\System32\WindowsPowerShell\v1.0\en-US\powershell.exe.mui
  174: Section       \BaseNamedObjects\__ComCatalogCache__
  1C4: Section       \BaseNamedObjects\windows_shell_global_counters
  1F4: Section       \...\Cor_SxSPublic_IPCBlock
  1F8: Section       \BaseNamedObjects\Cor_Private_IPCBlock_v4_10188
  208: Section       \Sessions\2\BaseNamedObjects\windows_shell_global_counters
  _Output_Truncated_

Step four: Show that the start-transcript log file cannot be altered. Open in notepad and type anything then try to save it

Step five: Run the following command

C:\windows\system32>handle.exe -p 10188 -c c:\Users\andy.dwyer\Documents\PowerShell_transcript.ADMIN-STATION.x9xkJMAJ.20210510184103.txt

Nthandle v4.22 - Handle viewer
Copyright (C) 1997-2019 Mark Russinovich
Sysinternals - www.sysinternals.com

    C: WaitCompletionPacket
Close handle C in powershell.exe (PID 10188)? (y/n)

After the handle is closed reopen the log file back in notepad and show the file can now be edited.

Q: Why are handles important to Cyber?

    Looking at handles to DLLs will help understand what malware could be doing as well as killing handles to logs could prevent behavior on systems from being recorded.



```

## -accepteula





SC showsid legit





# Linux Process Validity (Day 7)


A process is one of the most important fundamental concepts of the Linux Operating System. A process refers to a program in execution; it is a running instance of a program. It is made up of the program instruction, data read from files and other programs or input from a system user.

Each Linux system has numerous processes running. You may be familiar, or will become familiar, with most of these processes if you regularly use commands like "ps" or "top" to display them.




## Listing Processes



The ps command is a native Unix/Linux utility for viewing information concerning a selection of running processes on a system: it reads this information from the virtual files in /proc filesystem
Output of ps command

student@linux-opstation-grkv:~$ ps 
  PID TTY          TIME CMD
 7198 pts/1    00:00:00 bash 
 7213 pts/1    00:00:00 ps

	ps (report a snapshot of the current processes) command
	the output provides information about the currently running processes, including their process identification numbers (PID).



The top command is used to show the Linux processes. It provides a dynamic real-time view of the running system. Usually, this command shows the summary information of the system and the list of processes or threads which are currently managed by the Linux Kernel. Additional columns, like ppid, can be added by pressing f in the main window. A hierarchical view of the process tree can be displayed by pressing shift + v.
Output of top command

student@linux-opstation-grkv:~$ top 

top - 15:30:43 up 2 days, 13:04,  3 users,  load average: 0.00, 0.00, 0.00
Tasks: 205 total,   1 running, 167 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.3 us,  0.7 sy,  0.0 ni, 99.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  4039312 total,  2133660 free,  1070632 used,   835020 buff/cache
KiB Swap:        0 total,        0 free,        0 used.  2642820 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND 
 1572 gdm       20   0  802524  50388  37608 S  0.3  1.2   0:53.50 gsd-color
 7239 student   20   0   44540   4028   3392 R  0.3  0.1   0:00.16 top
    1 root      20   0  159928   9144   6728 S  0.0  0.2   0:08.14 systemd
-- Truncated




Similar to top, htop is a utility used to display various information about Linux processes dynamically, but in a more human friendly way. Also like top it can be configured to show an operator exactly the set of information needed for the task at hand. At the bottom of the htop window there is a bar with some available actions, namely F5 to present the process listing in a hierarchicall tree view, and F2 to add or remove columns such as ppid.




## Startup Processes



The startup process follows the boot process and brings the Linux computer to an operational state in which it is usable for productive work. It is highly important that a demarcation is established in virtual memory to prevent programs running in user space to directly interact with the kernel.

Executing the ps command with the -elf argument will do a full format listing of all running processes on the system in long format
*Output of ps -elf command

student@linux-opstation-grkv:~$ ps -elf | head 
F S UID        PID  PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD         
4 S root         1     0  0  80   0 - 39982 -      Feb25 ?        00:00:08 /sbin/init  
1 S root         2     0  0  80   0 -     0 -      Feb25 ?        00:00:00 [kthreadd]  

--Truncated



F:      Field Table
S:      Current status of the process
UID:    The effective user ID of the process's owner
PID:    Process ID
PPID:   The parent process's ID
C:      The processor utilization for scheduling. This field is not displayed when the -c option is used
PRI:    The kernel thread's scheduling priority. Higher numbers mean higher priority
NI:     The process's nice number, which contributes to its scheduling priority. Making a process "nicer" means lowering its priority
ADDR:   The address of the proc structure
SZ:     The virtual address size of the process
WCHAN:  The address of an event or lock for which the process is sleeping
STIME:  The starting time of the process (in hours, minutes, and seconds)
TTY:    The terminal from which the process (or its parent) was started. A question mark indicates there is no controlling terminal
TIME:   The total amount of CPU time used by the process since it began
CMD:    The command that generated the process

	init (/sbin/init) has a process ID of 1; and its parent, the Kernel has a PID of 0. The kernel starts /sbin/init which is the parent/grandparent of all user mode processes.
	Modern Linux kernels/distros also have [kthreadd] which is a kernel thread daemon which is second after init so it will have a PID of 2 and will also have no parent.



 ## Kernel Space

 

Kernel space is that area of virtual memory where kernel processes will run. This division is required for memory access protections. Code running in kernel mode has unrestricted access to the processor and main memory. This is a powerful but dangerous privilege that allows a kernel process to easily crash the entire system. The kernel is the core of the operating system. It normally has full access to all memory and machine hardware (and everything else on the machine). To keep the machine as stable as possible, you normally want only the most trusted, well-tested code to run in kernel mode/kernel space.

Executing code in kernel space will give it unrestricted access to any of the memory address space and to any underlying hardware. Kernel space is reserved for the highest of trusted functions within a system. Kernel mode is generally reserved for the lowest-level (ring 0), most trusted functions of the operating system. Due to the amount of access the kernel have, any instability within the kernel’s executing code can result in complete system failure.

Kernel space can be accessed by user processes only through the use of system calls.



## User Space



    User mode, in comparison, restricts access to a (usually quite small) subset of memory and safe CPU operations. User space refers to the parts of main memory that the user processes can access. If a process makes a mistake and crashes, the consequences are limited and can be cleaned up by the kernel. This means that if your web browser crashes, it won’t take down the whole system. Think of it as a form of sand-boxing — it restricts user programs so they can’t mess with memory (and other resources) owned by other programs or by the OS kernel. This limits (but usually doesn’t entirely eliminate) their ability to do bad things like crashing the machine. Because of the restricted access, malfunctions within user mode are limited only to the system space they are operating within.



## API 

An API (Application Programming Interface - set of protocols, routines, and, functions that allow the exchange of data among various applications and devices) and/or System calls (method that allows a program to request services from the kernel) are made by user mode processes to the kernel to request memory and physical hardware access. 


## OS Protection

In Computer Science, the ordered protection domains are referred to as Protection Rings. These mechanisms help in improving fault tolerance and provide Computer Security. Operating Systems provide different levels to access resources. Rings are hierarchically arranged from most privileged to least privileged.



Use of Protection Rings provides logical space for the levels of permissions and execution. Two important uses of Protection Rings are:

    Improving Fault Tolerance

    Provide Computer Security

There are basically 4 levels ranging from 0 which is the most privileged to 3 which is least privileged. Most Operating Systems use level 0 as the kernel or executive and use level 3 for application programs.

    Rings 1-2 cannot run privileged instructions but this is the only real limit; otherwise they are as privileged as ring 0. The intent by Intel in having rings 1 and 2 is for the OS to put device drivers at that level, so they are privileged, but somewhat separated from the rest of the kernel code.

Operational Value

    The goal in most, if not all, exploitative exercises is to be able to manipulate kernel mode processes and memory.

    In doing so, an adversary can gain complete control over the OS and obfuscate their methodology.



## Process Ownership, EUID, RUID, UID

Process Ownership

A Linux process is nothing but running instance of a program. For example, when you start Firefox to browse Internet, you can create a new process. In Linux, each process is given a unique number called as a process identification (PID). Linux kernel makes sure that each process gets a unique PID. /sbin/init or /lib/systemd/systemd on modern Linux distros always has a PID of 1 because it is eternally the first process on the Linux based system.

    A user is an entity that can run processes and own files. Users exist primarily to support permissions and boundaries. Every user-space process has a user owner, and processes are said to run as the owner. A user may terminate or modify the behavior of its own processes (within certain limits), but it cannot interfere with other users’ processes. In addition, users may own files and choose whether they share them with other users.

    Users of the system may be:

        Human Users = people who log into the system; or

        System Users = used to start non-interactive background services such as databases

    From the perspective of the operating system, there is no distinction between human users and system users and all the information is stored in the same file. However, there is a range of user IDs reserved for human users and another range for system users. To view this range, execute the following command and point out that the system UID’s range from 100 - 999 and the user range is 1000 - 60000.

Show range of User IDs for system and human users

  student@linux-opstation-grkv:~$ grep UID /etc/login.defs                  

	UID_MIN:                1000        
	UID_MAX:                60000       
	#SYS_UID_MIN:           100         
	#SYS_UID_MAX:           999         

	grep for UID from the shadow password suite configuration file login.defs
	minimum userid assigned to a regular user
	maximum userid assigned to a regular user
	minimum userid assigned to a system user
	maximum userid assigned to a system user


4.2 Effective User ID (EUID)

Effective user ID (EUID) defines the access rights for a process. In layman’s term it describes the user whose file access permissions are used by the process.


4.3 Real User ID (RUID)

The real user ID is who you really are (the one who owns the process). It also defines the user that can interact with the running process—most significantly, which user can kill and send signals to a process.

    Users can only modify / interact with files /processes that they own or that have been shared with them.

	The distinction between a real and an effective user id is made because you may have the need to temporarily take another user’s identity (most of the time, that would be root, but it could be any user).
	EUID and RUID are mostly always the same. They can be different when special permissions (like SUID bits) are set on files.
Viewing special permissions on passwd executables

student@linux-opstation-grkv:~$ ls -l /usr/bin/passwd         
-rwsr-xr-x 1 root root 59640 Mar 22  2019 /usr/bin/passwd
   ^          ^
  <2>        

	command list permissions of the passwd executables
	depicts that the SUID bit is set on the executable
	shows that the SUID bit is set by the user root
	In the example above; the SUID bit is set on the passwd executable so that when a normal user (non-root user) attempts to change their password, the executable is run with effective permissions of root. In this instance the real user is the non-root user and effective user is root.

Operational Value

    The "context" that a program runs in is something that is very important to keep track of. For Example:

        The /usr/bin/passwd command runs with an EUID of root no matter who runs it.

            ls -l /usr/bin/passwd

        This is done, because when a user updates their password, the /etc/shadow file is overwritten, which can only be done by root.

        However, the passwd command tracks the RUID ensuring that a normal user can’t change another user’s password


 ## System Calls

original process
original process asking the kernel to create another process must perform a fork() system call
original process after fork() system call
identical copy of original process after fork() system call
identical copy of original process performs exec(ls) system call
kernel replaces identical copy of original process with that of the new process


## Fork() and Exec()



    fork - creates a new process by duplicating the calling process. The new process is referred to as the child process. The calling process is referred to as the parent process.

        The fork “processes” can be explained as the recreation of a process from system space and duplicated into user space in an attempt restrict user access to system processes/space.

    exec - When a process calls exec, the kernel starts program, replacing the current process.





## Signals



Signals are software interrupts sent to a program to indicate that an important event has occurred. The events can vary from user requests to illegal memory access errors. Some signals, such as the interrupt signal, indicate that a user has asked the program to do something that is not in the usual flow of control.

Every signal has a default action associated with it. The default action for a signal is the action that a script or program performs when it receives a signal.

Some of the possible default actions are −

Terminate the process.
Ignore the signal.
Dump core. This creates a file called core containing the memory image of the process when it received the signal.
Stop the process.
Continue a stopped process


SIGHUP
1	
Hangup (POSIX)

SIGINT	
2
Terminal interrupt (ANSI)

SIGQUIT
3	
Terminal quit (POSIX)

SIGILL
4
Illegal instruction (ANSI)

SIGTRAP	
5
Trace trap (POSIX)

SIGIOT
6
IOT Trap (4.2 BSD)

SIGBUS
7
BUS error (4.2 BSD)

SIGFPE
8
Floating point exception (ANSI)

SIGKILL
9
Kill(can’t be caught or ignored) (POSIX)

SIGUSR1
10
User defined signal 1 (POSIX)

SIGSEGV
11
Invalid memory segment access (ANSI)

SIGUSR2
12
User defined signal 2 (POSIX)

SIGPIPE
13
Write on a pipe with no reader, Broken pipe (POSIX)

SIGALRM
14
Alarm clock (POSIX)

SIGTERM
15
Termination (ANSI)

SIGSTKFLT
16
Stack fault

SIGCHLD	
17
Child process has stopped or exited, changed (POSIX)

SIGCONTv
18
Continue executing, if stopped (POSIX)

SIGSTOP
19
Stop executing(can’t be caught or ignored) (POSIX)

SIGTSTP	
20	
Terminal stop signal (POSIX)

SIGTTIN	
21
Background process trying to read, from TTY (POSIX)

SIGTTOU
22
Background process trying to write, to TTY (POSIX)

SIGURG
23
Urgent condition on socket (4.2 BSD)

SIGXCPU
24
CPU limit exceeded (4.2 BSD)

SIGXFSZ
25
File size limit exceeded (4.2 BSD)

SIGVTALRM
26
Virtual alarm clock (4.2 BSD)

SIGPROF
27
Profiling alarm clock (4.2 BSD)

SIGWINCH
28
Window size change (4.3 BSD, Sun)

SIGIO
29
I/O now possible (4.2 BSD)

SIGPWR
30
Power failure restart (System V)


## DEMO PRocess Enumeration


Steps to follow when running scripts
	create a file for Each script with the following command nano <name>.sh
	copy and paste the contents of the script, close and save
	run the script with the following command: `source <name>.sh
using less with the ps -elf command to page through the long output

student@linux-opstation-grkv:~$ ps -elf | less 
F S UID        PID  PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD
4 S root         1     0  0  80   0 - 40015 -      Feb25 ?        00:00:08 /sbin/init        
1 S root         2     0  0  80   0 -     0 -      Feb25 ?        00:00:00 [kthreadd]
1 I root         4     2  0  60 -20 -     0 -      Feb25 ?        00:00:00 [kworker/0:0H]

--Truncated

	shows the command prior to execution
	shows the output one page view at a time. Can exit out of it by hitting the q key on your keyboard


display top five lines of the process table

student@linux-opstation-grkv:~$ ps -elf | head -n5   
F S UID        PID  PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD
4 S root         1     0  0  80   0 - 56461 ep_pol 18:23 ?        00:00:07 /sbin/init splash     
1 S root         2     0  0  80   0 -     0 kthrea 18:23 ?        00:00:00 [kthreadd]
1 I root         3     2  0  60 -20 -     0 rescue 18:23 ?        00:00:00 [rcu_gp]
1 I root         4     2  0  60 -20 -     0 rescue 18:23 ?        00:00:00 [rcu_par_gp]

	head command will display the top ten listings. When used with -n# will display the number of required listings
	note the top two PID’s and PPID’s


Show only kthreadd processes

student@linux-opstation-grkv:~$ ps --ppid 2 -lf | head              
F S UID        PID  PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD
1 I root         3     2  0  60 -20 -     0 rescue 18:23 ?        00:00:00 [rcu_gp]         
1 I root         4     2  0  60 -20 -     0 rescue 18:23 ?        00:00:00 [rcu_par_gp]
1 I root         6     2  0  60 -20 -     0 worker 18:23 ?        00:00:00 [kworker/0:0H]
1 I root         8     2  0  60 -20 -     0 rescue 18:23 ?        00:00:00 [mm_percpu_wq]
1 S root         9     2  0  80   0 -     0 smpboo 18:23 ?        00:00:00 [ksoftirqd/0]

--Truncated

	--ppid # will show only the parent process with the stated id
	note that [kthreaded] processes have a PPID of 2 and with enclosed with brackets []


Show all processes except kthreadd processes

student@linux-opstation-grkv:~$ ps --ppid 2 -Nlf | head                 
F S UID        PID  PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD          
4 S root         1     0  0  80   0 - 56461 ep_pol 18:23 ?        00:00:07 /sbin/init splash
1 S root         2     0  0  80   0 -     0 kthrea 18:23 ?        00:00:00 [kthreadd]
4 S root       310     1  0  79  -1 - 25836 ep_pol 18:23 ?        00:00:00 /lib/systemd/systemd-journald
4 S root       336     1  0  80   0 -  8503 ep_pol 18:23 ?        00:00:00 /lib/systemd/systemd-udevd
4 S systemd+   576     1  0  80   0 - 17750 ep_pol 18:23 ?        00:00:00 /lib/systemd/systemd-resolved
4 S systemd+   578     1  0  80   0 - 36527 ep_pol 18:23 ?        00:00:00 /lib/systemd/systemd-timesyncd

--Truncated

	-N is used in connection with --ppid to negate the required ppid
	output will not contain ppid of 2 i.e {kthreaded] processes


display process output in Ascii art process tree

student@linux-opstation-grkv:~$ ps -elf --forest | tail             
0 S student   3185  3178  0  80   0 - 219853 poll_s Feb25 tty2    00:00:00  \_ /usr/lib/evolution/evolution-addressbook-factory-subprocess --factory all --bus-name org.gnome.evolution.dataserver.Subprocess.Backend.AddressBookx3178x2 --own-path /org/gnome/evolution/dataserver/Subprocess/Backend/AddressBook/3178/2
0 S student   3243     1  0  80   0 - 175142 poll_s Feb25 tty2    00:00:00 /usr/lib/gnome-terminal/gnome-terminal-server                                                   
0 S student   3251  3243  0  80   0 -  5774 wait   Feb25 pts/2    00:00:00  \_ bash
4 S root      3310  3251  0  80   0 - 15870 -      Feb25 pts/2    00:00:00      \_ su root
4 S root      3311  3310  0  80   0 -  5510 -      Feb25 pts/2    00:00:00          \_ bash
0 S student   4357     1  0  80   0 -  1159 wait   Feb25 tty2     00:00:00 /bin/sh -c /usr/lib/ubuntu-release-upgrader/check-new-release-gtk
0 S student   4358  4357  0  80   0 - 127623 poll_s Feb25 tty2    00:00:00  \_ /usr/bin/python3 /usr/lib/ubuntu-release-upgrader/check-new-release-gtk

--Truncated

	--forest will display the output in Ascii tree format. Tail command will output the last ten lines
	output shows a diagrammatic view of the process table


Key Points

    Shows some simple commands and switch options to view Linux processes

    ps -elf #Displays processes

        -e #Displays every process on the system

        -l #Lists processes in a long format

        -f #Does a full-format listing

    ps --ppid 2 -lf #Displays only kthreadd processes (so, only kernel-space processes)

        Processes spawned from kthreadd will always have a PPID of 2

    ps --ppid 2 -Nlf #Displays anything except kthreadd processes (so, only user-space processes)

        -N #Negates the selection

    ps -elf --forest #Displays processes in an ASCII tree

        --forest #ASCII art process tree

Operational Value

    Excellent command for process enumeration.




## Foreground and Background


Processes that require a user to start them or to interact with them are called foreground processes.

Processes that are run independently of a user are referred to as background processes.

Programs and commands run as foreground processes by default.




## Orphan Process


An orphan process is a running process whose parent process has finished or terminated and is adopted by sbin/init and will have a PPID of 1.

    Key Points

        disown -a && exit #Close a shell/terminal and force all children to be adopted


6.1.1 Demonstration - Orphan

Copy code below and paste into any editor of choice. Give a name to the script. In this instance the script will be called orphan.sh, make file an executable and run twice in succession.
Code for orphan demonstration

#!/bin/bash

#Print PID of current shell
echo $$

#Pause  for  NUMBER seconds
sleep 5 &

#List process table and output PID associated with "sleep"
ps -elf | grep -v  grep | grep sleep

#!/bin/bash on the first line, meaning that the script should always be run with bash


Simple demonstration to show how orphans are created

student@linux-opstation-grkv:~$ chmod +x orphan.sh          

student@linux-opstation-grkv:~$ ./orphan.sh                 
13409                                                       
0 S student  13410 13409  0  80   0 -  1983 hrtime 23:16 pts/1    00:00:00 sleep 5      

student@linux-opstation-grkv:~$ ./orphan.sh             
13415                                                               
0 S student  13410     1  0  80   0 -  1983 hrtime 23:16 pts/1    00:00:00 sleep 5      
0 S student  13416 13415  0  80   0 -  1983 hrtime 23:16 pts/1    00:00:00 sleep 5

	make orphan.sh an executable
	first run of orphan.sh
	13409 is the PID of the shell containing the executable
	PID 13410 is the PID of the sub process created when the file was executed. Its parent PID is 13409
	second run of orphan.sh
	new PID of shell containing the code is now 13415
	running the code a second time terminates the original process with PID 13409 containing the code. Sub process with PID of 13410 will now become an orphan and will be reclaimed by /sbin/init. Its PPID will now be 1


6.1.2 Resources

    Orphan Exploit Exercise

    More about Orphan Processes




## Zombie (DEFUNCT) Process


A zombie process (or defunct process) is a process that has completed execution but hasn’t been reaped by its parent process. As result it holds a process entry in the form of a PID in the process table. Zombies cannot be killed as they are already dead and do not use resources. However, they do take up PIDs in the process table which is a finite resource. Zombie entries can be removed from the process table by killing its parent process.


6.2.1 Demonstration - zombies

Copy code below and paste into any editor of choice. Give a name to the script. In this instance the script will be called zombie.sh, make file an executable and run once
Code for zombie demonstration

#!/bin/bash

#Print PID of current shell
echo $$

#Pause  for  NUMBER seconds
sleep 2 &

#Pause signal
kill -19 $(echo $$)

#!/bin/bash on the first line, meaning that the script should always be run with bash


Simple demonstration to show how zombies are created

student@linux-opstation-grkv:~$ chmod +x zombie.sh          

student@linux-opstation-grkv:~$ ps -elf | grep -v grep | grep sleep     

student@linux-opstation-grkv:~$ ./zombie.sh         
13981                                   

[1]+  Stopped                 ./zombie.sh

student@linux-opstation-grkv:~$ ps -elf| grep -v grep | grep sleep          
0 Z student  13982 13981  0  80   0 -     0 -      00:17 pts/1    00:00:00 [sleep] <defunct>        

student@linux-opstation-grkv:~$ kill -18 13981                  
[1]+  Done                    ./zombie.sh

student@linux-opstation-grkv:~$ ps -elf| grep -v grep | grep sleep          

	make zombie.sh an executable
	List continents of process table and confirm that there is no zombie on process list
	execute file zombie.sh
	PID 13981 is the PID of the shell containing the executable
	After two seconds list contents of the process table containing sleep in the command section
	After the sleep command completes, the process associated with the executable will not be around to reap its return code as it was paused due to the kill -19 command in the code. The process associated with sleep, with PID of 13982 will now become a zombie as its parent with PID 13981 is paused. Note the z and <defunct> in the process list
	kill -18 will send the continue\restart signal to PID 13981 which will clear the zombie entry from the process list
	this command will return no output as the zombie entry has been cleared from the process list


6.2.2 Resources

    Example - ZombieLoad Attack

    Zombie Security Risks





## Daemons 


A daemon process is an intentionally orphaned process in order to have a background process.

Key Points

    What is a daemon and how are they created?

        Program that runs as a background process (Ex. syslogd, sshd, cron)

        All daemons are Orphans, but all orphans are not Daemons

        A daemons purpose is to manage/monitor a service: {status, start, restart}

        man cron - to see an example of a daemon that starts during the boot process


Operational Value

    Persistence - Daemons are services that should run for duration of system operation, since init is parent, would require shutdown for parent to die.

    Malicious processes are sometimes orphaned and named to make it look like a daemon process ps --ppid 1 -lf


6.3.1 Interacting With Linux Services


A service is a program that runs in the background outside the interactive control of system users as they lack an interface. This in order to provide even more security, because some of these services are crucial for the operation of the operating system.

On the other hand, in systems like Unix or Linux, the services are also known as daemons. Sometimes the name of these services or daemons ends with the letter d. For example, sshd is the name of the service that handles SSH.

The commands used to interact with services on a Unix/Linux system differs based on distribution [sysV or systemD]


6.3.1.1 Interacting With Services on a SYSV System


A system that uses the SysV scheme usually comes with the service program used to manage the services while the system is running. You can check on the status of a service, or all services, and start or stop a service, respectively, using the service utility:


Check status/start/stop/restart a service on sysV

student@linux-opstation-grkv:~$ service <servicename> status/start/stop/restart


6.3.1.2 Interacting With Services on a SYSTEMD System

In recent years, Linux distributions have increasingly transitioned from other init systems to systemd. The systemd suite of tools provides a fast and flexible init model for managing an entire machine from boot onwards

The basic object that systemd manages and acts upon is a “unit”. Units can be of many types, but the most common type is a “service” (indicated by a unit file ending in .service). To manage services on a systemd enabled server, our main tool is the systemctl command.


List all unit files that systemd has listed as active

student@linux-opstation-grkv:~$ systemctl list-units
UNIT                                                                                LOAD   ACTIVE SUB       DESCRIPTION
proc-sys-fs-binfmt_misc.automount                                                   loaded active waiting   Arbitrary Executable File Formats F
sys-devices-pci0000:00-0000:00:01.1-ata1-host0-target0:0:0-0:0:0:0-block-sr0.device loaded active plugged   QEMU_DVD-ROM config-2
sys-devices-pci0000:00-0000:00:03.0-virtio1-net-ens3.device                         loaded active plugged   Virtio network device

--Truncated


List all units that systemd has loaded or attempted to load into memory, including those that are not currently active, add the --all switch:

student@linux-opstation-grkv:~$ systemctl list-units --all
  UNIT                                                                                LOAD      ACTIVE   SUB       DESCRIPTION
  proc-sys-fs-binfmt_misc.automount                                                   loaded    active   waiting   Arbitrary Executable File Fo
  dev-cdrom.device                                                                    loaded    active   plugged   QEMU_DVD-ROM config-2
  dev-disk-by\x2did-ata\x2dQEMU_DVD\x2dROM_QM00001.device                             loaded    active   plugged   QEMU_DVD-ROM config-2

--Truncated


Check status of a service

student@linux-opstation-grkv:~$ systemctl status <servicename.service>

student@linux-opstation-grkv:~$ systemctl status <PID of service>


Start/stop/restart a service

student@linux-opstation-grkv:~$ systemctl start/stop/restart <servicename.service>



## JOB Control


ob control is the ability to stop/suspend the execution of processes (command) and continue/resume their execution as per your requirements.

The jobs command displays the status of jobs started in the current terminal window. Jobs are numbered starting from 1 for each session. The job ID numbers are used by some programs instead of PIDs (for example, by fg and bg commands).


6.4.1 Demonstration - Job Control


Jobs

student@linux-opstation-grkv:~$ ping 8.8.8.8 &          
[1] 14130                   
student@linux-opstation-grkv:~$ PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=112 time=8.51 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=112 time=8.40 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=112 time=8.31 ms
fg                              
ping 8.8.8.8
64 bytes from 8.8.8.8: icmp_seq=4 ttl=112 time=8.72 ms
^Z                              
[1]+  Stopped                 ping 8.8.8.8

student@linux-opstation-grkv:~$ jobs            
[1]+  Stopped                 ping 8.8.8.8      

student@linux-opstation-grkv:~$ kill -9 %1      

[1]+  Stopped                 ping 8.8.8.8

	the command is executed as a background process indicated by & at the end
	value in [] denotes job id and 14130 denotes PID
	fg command is entered on the keyboard to bring job to the foreground
	ctrl+z is used to stop the job
	jobs command will list all jobs and their status
	list that job id 1 is stopped
	job id 1 is abruptly terminated with the kill -9 command. Use the % when terminating jobs by their respective ids

	the bg command can be use to background a job and ctrl+c command can be use to kill an active process


6.5 Cron Jobs


The Unix cron service runs programs repeatedly on a fixed schedule. Most experienced administrators consider cron to be vital to the system because it can perform automatic system maintenance.

The cron daemon checks the directories /var/spool/cron, /etc/cron.d and the file /etc/crontab, once a minute and executes any commands specified that match the time.

    Two types of cron jobs

        System cron jobs

            run as root and rigidly scheduled

            perform system-wide maintenance tasks (Cleaning out /tmp or rotating logs)

            controlled by /etc/crontab

        User cron jobs

            Use 'crontab’ command to create user cron jobs

            stored in /var/spool/cron/crontabs/

One can run any program with cron at whatever time they want the job to execute. The program running through cron is called a cron job.

On Unix-like systems, the crontab command opens the cron table for editing. The cron table is the list of tasks scheduled to run at regular time intervals on the system.

Syntax

    crontab -u [user] file This command will load the crontab data from the specified file

    crontab -l -u [user] This command will display/list user’s crontab contents

    crontab -r -u [user] This Command will remove user’s crontab contents

    crontab -e -u [user] This command will edit user’s crontab contents

	Crontab jobs will run with the permissions of the owner of the crontab file

Contents placement of the crontab file

  ┌───────────── minute (0 - 59)
  │ ┌───────────── hour (0 - 23)
  │ │ ┌───────────── day of the month (1 - 31)
  │ │ │ ┌───────────── month (1 - 12)
  │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
  │ │ │ │ │                           7 is also Sunday on some systems)
  │ │ │ │ │
  │ │ │ │ │
  * * * * * <Time/Day to execute    "Command to Execute"

(Mnemonic: Minnie Has Daily Money Worries)
* The syntax of each line expects a cron expression made of five fields, followed
by a shell command to execute.


Cron Examples

* Run backup everyday at 0412
** `12 4 * * *`    /usr/bin/backup

* Send a message to all logged in users, 0000 hours on 1 Jan
** `0 0 1 1 *`     wall "Happy New Year"

Other advanced usage....

* Send a message at minute 15 of each hour to logged in users on Sunday
** `15 * * * 0`    wall "Shouldn't you be in church?"

* Run backup on Wed, and Sat at 0515
** `15 5 * * 3,6`   /usr/bin/backup

* Save open tcp port listing hourly from 9PM to 5AM every day
** `0 0-5,21-23 * * *`    echo $(ss -nltp) >> /home/andy.dwyer/tcplist.context

6.5.1 Resources

    Cron Schedule Expression Editor



## Process and Proc Dir



    The /proc/ directory — also called the proc file system — contains a hierarchy of special files which represent the current state of the kernel, allowing applications and users to peer into the kernel’s view of the system.

    Every process accesses files in order to complete its work. These processes keep track of open files using File Descriptors.

7.1 File Descriptors

    In Unix and Unix-like computer operating systems, a file descriptor ("FD" or less frequently known as "fildes") is a unique identifier (aka handle) for a file or other input/output resource, such as a pipe or network socket.

    When you open a file, the operating system creates an entry to represent that file and store the information about that opened file.

        So if there are 100 files opened in your OS then there will be 100 entries in the OS (somewhere in kernel).

        These entries are represented by integers like (…​100, 101, 102…​.).

            This entry number is the file descriptor. So it is just an integer number that uniquely represents an opened file in the operating system. If your process opens 10 files then your Process table will have 10 entries for file descriptors.

7.1.1 Viewing File Descriptors

    View File Descriptors using the LSOF command.

    List all open files being used by every process.

        sudo lsof | tail -30

        --- Trimmed ---
                     <2>                         <1>                                                    
        COMMAND     PID   TID             USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
        gdbus     18768 18772          student   12u     unix 0x0000000000000000      0t0    2409093 type=STREAM
        gdbus     18768 18772          student   14r      REG              252,1  1327119      18343 /var/lib/dpkg/status (deleted)
        gdbus     18768 18772          student   15r      CHR                1,9      0t0         11 /dev/urandom
        gdbus     18768 18772          student   16r      CHR                1,8      0t0         10 /dev/random
        --- Trimmed ---

	File Descriptors and their permissions
	PID and PPID
	Open file being accessed


    List all open files for a specific process.

        sudo lsof -c sshd

        sshd    14139 student    2u   CHR                1,3      0t0       6 /dev/null
        sshd    14139 student    3u  IPv4            2761262      0t0     TCP linux-opstation-mikh:ssh->192.168.249.87:43044 (ESTABLISHED)
        sshd    14139 student    4u  unix 0xffff917eb0205000      0t0 2761302 type=DGRAM
        sshd    14139 student    5u  unix 0xffff917ec7a51000      0t0 2761519 type=STREAM
        sshd    14139 student    6r  FIFO               0,12      0t0 2761523 pipe
        sshd    14139 student    7w  FIFO               0,24      0t0     289 /run/systemd/sessions/6101.ref
        sshd    14139 student    8w  FIFO               0,12      0t0 2761523 pipe
        sshd    14139 student    9u   CHR                5,2      0t0      87 /dev/ptmx
        sshd    14139 student   11u   CHR                5,2      0t0      87 /dev/ptmx
        sshd    14139 student   12u   CHR                5,2      0t0      87 /dev/ptmx

7.1.2 Interpretting File Descriptors

This information and more available in the lsof man page.

 - The number in front of flag(s) is the file descriptor number used by the process associated with the file
u - File open with Read and Write permission
r - File open with Read permission
w - File open with Write permission
W - File open with Write permission and with Write Lock on entire file
mem - Memory mapped file, usually for share library

7.2 - Navigating Proc Directory

    List all the proc directories.

        ls -l /proc/

        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 1
        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 10
        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 100
        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 1018
        dr-xr-xr-x  9 xrdp             xrdp                           0 Feb  9  2021 1081
        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 1085
        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 11
        dr-xr-xr-x  9 root             root                           0 Feb  9  2021 1104

    Grab the PID of a process.

        ps -elf | grep sshd

        4 S root      1107     1  0  80   0 - 18077 -      Feb09 ?        00:00:00 /usr/sbin/sshd -D
        4 S root     14035  1107  0  80   0 - 26424 -      14:21 ?        00:00:00 sshd: student [priv]
        5 S student  14139 14035  0  80   0 - 27031 -      14:22 ?        00:00:00 sshd: student@pts/0

    List contents for that PID directory.

        sudo ls -l /proc/14139

        total 0
        dr-xr-xr-x 2 student student 0 Aug 27 17:14 attr
        -rw-r--r-- 1 root    root    0 Aug 27 17:14 autogroup
        -r-------- 1 root    root    0 Aug 27 17:14 auxv
        -r--r--r-- 1 root    root    0 Aug 27 17:14 cgroup
        --w------- 1 root    root    0 Aug 27 17:14 clear_refs
        -r--r--r-- 1 root    root    0 Aug 27 17:12 cmdline
        -rw-r--r-- 1 root    root    0 Aug 27 17:14 comm
        -rw-r--r-- 1 root    root    0 Aug 27 17:14 coredump_filter
        -r--r--r-- 1 root    root    0 Aug 27 17:14 cpuset
        lrwxrwxrwx 1 root    root    0 Aug 27 14:22 cwd -> /
        -r-------- 1 root    root    0 Aug 27 17:14 environ
        lrwxrwxrwx 1 root    root    0 Aug 27 14:22 exe -> /usr/sbin/sshd    

	The exe link to actual binary file being executed.







# Windows Auditing and Logging (Day 8)

## Artifacts

Are objects wiuthin a computer system that contain important information relevant to the activities performed on the system by the user

```
    UserAssist

    Windows Background Activity Moderator (BAM)

    Recycle Bin

    Prefetch

    Jump Lists

    Recent Files

    Browser Artifacts
```

## Security Identifer (SID)


```
PS C:\> Get-LocalUser | select Name,SID 
Name               SID
----               ---
Admin              S-1-5-21-1584283910-3275287195-1754958050-1000
Administrator      S-1-5-21-1584283910-3275287195-1754958050-500
cloudbase-init     S-1-5-21-1584283910-3275287195-1754958050-1002
DefaultAccount     S-1-5-21-1584283910-3275287195-1754958050-503
Guest              S-1-5-21-1584283910-3275287195-1754958050-501
andy.dwyer         S-1-5-21-1584283910-3275287195-1754958050-1005
sshd               S-1-5-21-1584283910-3275287195-1754958050-1003
student            S-1-5-21-1584283910-3275287195-1754958050-1004
WDAGUtilityAccount S-1-5-21-1584283910-3275287195-1754958050-504
```
WMI 32
```
PS C:\> Get-WmiObject win32_useraccount | select name,sid 
name               sid
----               ---
Admin              S-1-5-21-1584283910-3275287195-1754958050-1000
Administrator      S-1-5-21-1584283910-3275287195-1754958050-500
cloudbase-init     S-1-5-21-1584283910-3275287195-1754958050-1002
DefaultAccount     S-1-5-21-1584283910-3275287195-1754958050-503
Guest              S-1-5-21-1584283910-3275287195-1754958050-501
andy.dwyer         S-1-5-21-1584283910-3275287195-1754958050-1005
sshd               S-1-5-21-1584283910-3275287195-1754958050-1003
student            S-1-5-21-1584283910-3275287195-1754958050-1004
WDAGUtilityAccount S-1-5-21-1584283910-3275287195-1754958050-504
_Output_Truncated_
```
Get-LocalUser will show local Users and SID on a system
Get-WmiObject will show local and domain Users and SID

{empty} +


Command Line SID
```
C:\windows\system32>wmic UserAccount get name,sid 
Name                SID
Admin               S-1-5-21-1584283910-3275287195-1754958050-1000
Administrator       S-1-5-21-1584283910-3275287195-1754958050-500
cloudbase-init      S-1-5-21-1584283910-3275287195-1754958050-1002
DefaultAccount      S-1-5-21-1584283910-3275287195-1754958050-503
Guest               S-1-5-21-1584283910-3275287195-1754958050-501
andy.dwyer          S-1-5-21-1584283910-3275287195-1754958050-1005
sshd                S-1-5-21-1584283910-3275287195-1754958050-1003
student             S-1-5-21-1584283910-3275287195-1754958050-1004
WDAGUtilityAccount  S-1-5-21-1584283910-3275287195-1754958050-504
```
wmic useraccount get name,sid will show local Users and SID


## UserAssist

Tracks GUI based programming that were ran by a particular user


They are located in 
```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count\ *
```
they are encoded in ROT13 NEEDS TO BE DECODED

The GUID represents a particular file extension.

CEBFF5CD-ACE2-4F4F-9178-9926F41749EA 
A list of applications, files, links, and other objects that have been accessed


F4E57C4B-2036-45F0-A9AB-443BCFE33D9F 
Lists the Shortcut Links used to start programs
```
PS C:\> Get-ItemProperty "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist
```

## Windows Background ACtivity Moderator (BAM)


BAM Provides the following:

full path of an executable

last execution date/time


```
Show in Reg Edit:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings #On 1809 and Newer

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\UserSettings #On 1803 and below
```


CMD command to get Windows OS Version - Ran in Admin-Station

    systeminfo
```
C:\WINDOWS\system32>systeminfo

Host Name:                 ADMIN-STATION
OS Name:                   Microsoft Windows 10 Enterprise
OS Version:                10.0.19045 N/A Build 19045 
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
/----Output Truncated----/
```
	see table below - 19045 (Windows 10 (22H2)) is the last Windows 10 Version


Powershell cmdlet to get Windows OS Version - Ran in Admin-Station

    Get-Computerinfo
```
Get-ComputerInfo | select osname,osversion,OsHardwareAbstractionLayer

OsName                           OsVersion   OsHardwareAbstractionLayer
------                           ---------   --------------------------
Microsoft Windows 10 Enterprise  10.0.19045  10.0.19041.2251
```


## Recycle Bin

When a user deletes a file in Windows it goes to the recylce bin

```
    SID - determines which user deleted it

    Timestamp - When it was deleted

    $RXXXXXX - content of deleted files

    $IXXXXXX - original PATH and name
```
Location

```
C:\$Recycle.bin
```

DEMO

```
PS C:\> Get-Childitem 'C:\$RECYCLE.BIN' -Recurse -Verbose -Force | select FullName 
FullName
--------
C:\$RECYCLE.BIN\S-1-5-18
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1004
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005
C:\$RECYCLE.BIN\S-1-5-21-950816436-4199619115-1663388479-500
C:\$RECYCLE.BIN\S-1-5-18\desktop.ini
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1004\desktop.ini
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005\$I8QZ1U8.txt
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005\$IBBLWX1.txt
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005\$IGJUCO3.txt
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005\$R8QZ1U8.txt
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005\$RBBLWX1.txt
C:\$RECYCLE.BIN\S-1-5-21-1584283910-3275287195-1754958050-1005\$RGJUCO3.txt
_Output_Truncated_
```
Output shows all of the contents of the Recycle Bin. -Recurse will look at all user’s/SID’s contents

Look at the different directories (SIDs) discuss how you would determine what users they belong to.

Q: Since this gives us all the users on the machine, how would you find the specific user this information belogs to?
Match SID to USER:


```
 PS C:\> wmic useraccount where 'sid="S-1-5-21-1584283910-3275287195-1754958050-1005"' get name 
Name
andy.dwyer
```

To find Recycle Bin artifacts for a specific user, match the SID, then append it to the previous command:
```
PS C:\> Get-Content 'C:\$Recycle.Bin\S-1-5-21-1584283910-3275287195-1754958050-1005\$R8QZ1U8.txt' 
This is the file for Auditing
```
Reads the contents of a particular file within the Recycle BIN



 ## Prefetch

Files that are created by the OS when an application is ran for the first time

 back hitting the driver in the lip with a few bullet fragments. The suspects fled on foot and were apprehended the following day by SWAT. The Trooper was treated for his injuries and later released. Both suspects were out on bond at the time of the shooting.

Q: What is the windows prefetch used for?

These files are named in a predetermined format and the prefetch name consists of the name of the application, hash noting the location from which the application was run, and a “.PF” file extension.

Q: What is the purpose of analysing the prefetch?

Q: If you found a program in prefetch that you know you did not run, what would that be an indicator of?

For example, the prefetch file for calc.exe would appear as CALC.EXE-0FE8F3A9.pf, where 0FE8F3A9 is a hash of the path from where the file was executed.

The prefetch files are stored in “\Root\Windows\Prefetch” folder.
* Analysis of prefetch files reveals the evidence of the intial program execution for a user and from a specific location at a specific time.

Prefetch entries may remain even after the program has been deleted or uninstalled.

This information together with timeline analysis helps in determining what programs have been executed in the system.

Evidence of program execution can be a valuable resource for forensic investigators. They can prove that a suspect ran a program like CCleaner to cover up any potential wrongdoing.

Limited to 128 files on Win7

Limited to 1024 files on Win8-10

Win8-10 Prefetch files store the last eight execution times. The file creation time of the prefetch file will indicate the original time of execution within 10 seconds leaving the investigator with a total of nine execution times.

Prefetch entries record the location of the associated executable and files referenced by that executable. Look for any files executed or referenced from a temp directory as this is typically an outlier.

By default, Windows Server does not have Prefetch enabled.

Use Eric Zimmerman’s PECmd.exe utility to analyze Prefetch data

General Format of a prefetch file: (exename)-(hash-of-path).pf



Location
```
c:\Windows\Prefetch
```

Demo
```
PS C:\> Get-Childitem -Path 'C:\Windows\Prefetch' -ErrorAction Continue | select -First 8 
    Directory: C:\Windows\Prefetch
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        2/11/2021   3:53 PM                ReadyBoot
-a----        2/11/2021   3:39 PM         334168 AgAppLaunch.db
-a----        2/16/2021   2:13 PM        1450197 AgCx_S1_S-1-5-21-1584283910-3275287195-1754958050-1004.snp.db
-a----        2/23/2021   7:29 PM        1690240 AgCx_S2_S-1-5-21-1584283910-3275287195-1754958050-1005.snp.db
-a----        3/11/2021   7:21 PM          83229 AgGlFaultHistory.db
-a----        3/11/2021   7:21 PM         420736 AgGlFgAppHistory.db
-a----        3/11/2021   7:21 PM        1629990 AgGlGlobalHistory.db
-a----        2/22/2021   5:19 PM         125687 AgGlUAD_P_S-1-5-21-1584283910-3275287195-1754958050-1004.db
Output shows the programs that were run and when they were executed that are stored in the Prefetch location.

```

## Jump List

Things you access alot


The Windows 7-10 taskbar (Jump List) is engineered to allow users to “jump” or access items they have frequently or recently used quickly and easily.

The data stored in the Automatic Destinations folder will each have a unique file prepended with the AppID of the associated application.

First time of execution of application.

Creation Time = First time item added to the AppID file.

Last time of execution of application w/file open.

Modification Time = Last time item added to the AppID file.

Jumplists allow us to get visibility about the intent or knowledge an attacker had when opening a particular file, launching a particular application or browsing a specific directory during the course of an interactive session.

Jumplist entries

 back hitting the driver in the lip with a few bullet fragments. The suspects fled on foot and were apprehended the following day by SWAT. The Trooper was treated for his injuries and later released. Both suspects were out on bond at the time of the shooting.
```
Win7/8/10

C:\%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations (C:\Users\king\AppData\Roaming\Microsoft\Windows\Recent)

Show in Explorer:
C:\%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations (C:\Users\king\AppData\Roaming\Microsoft\Windows\Recent)
```


Demo

```


PS C:\> Get-Childitem -Recurse C:\Users\*\AppData\Roaming\Microsoft\Windows\Recent -ErrorAction Continue | select FullName, LastAccessTime 
FullName                                                                                                                                     LastAccessTime
--------                                                                                                                                     --------------
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations                                                        3/11/2021 8:21:30 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\1bc392b8e104a00e.automaticDestinations-ms              3/11/2021 6:24:55 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\5f7b5f1e01b83767.automaticDestinations-ms              3/11/2021 8:16:30 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\9b9cdc69c1c24e2b.automaticDestinations-ms              3/11/2021 6:24:55 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\9d1f905ce5044aee.automaticDestinations-ms              3/11/2021 6:24:55 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\cf02284227526d80.automaticDestinations-ms              3/11/2021 7:02:30 PM

or

PS C:\> Get-Childitem -Recurse $env:USERPROFILE\AppData\Roaming\Microsoft\Windows\Recent -ErrorAction SilentlyContinue | select FullName,LastAccessTime 
FullName                                                                                                                                     LastAccessTime
--------                                                                                                                                     --------------
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations                                                        3/11/2021 8:21:30 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations                                                           3/11/2021 8:21:30 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\14287.lnk                                                                    3/9/2021 6:15:30 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\Active_Directory.lnk                                                         3/8/2021 7:07:26 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\Artifacts (2).lnk                                                            3/3/2021 8:30:33 PM
C:\Users\andy.dwyer\AppData\Roaming\Microsoft\Windows\Recent\Artifacts.lnk                                                                3/3/2021 7:12:42 PM

or

- Make sure sysinternals is mounted or unzipped
- Gci C:\users\student\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations | % {z:\strings.exe -accepteula $_} >> c:\recentdocs.txt

Output shows all users Jump Lists artifacts
Output shows the Jump Lists Artifacts for the currently logged user
Output redirected through strings.exe and into a file provides more readable output.

```


## Recent Files



Registry Key that will track the last files and folders opened and is used to populate data in “Recent” menus of the Start menu.
Tracks last 150 files or folders opened.
Entry and modification time of this key will be the time and location the last file of a specific extension was opened.

Location
```
HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs

HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt
```


```
PS C:\> Get-Item 'Registry::\HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.*' 
    Hive: \HKEY_USERS\S-1-5-21-1584283910-3275287195-1754958050-1005\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
Name                           Property
----                           --------
.html                          MRUListEx : {0, 0, 0, 0...}
                               0         : {114, 0, 101, 0...}
.pdf                           0         : {49, 0, 52, 0...}
                               MRUListEx : {0, 0, 0, 0...}
.ps1                           0         : {65, 0, 114, 0...}
                               MRUListEx : {2, 0, 0, 0...}
                               1         : {65, 0, 99, 0...}
                               2         : {82, 0, 83, 0...}
.sh                            0         : {116, 0, 101, 0...}
                               MRUListEx : {0, 0, 0, 0...}
.txt                           0         : {114, 0, 101, 0...}
                               MRUListEx : {4, 0, 0, 0...}
                               1         : {114, 0, 101, 0...}
                               2         : {114, 0, 101, 0...}
                               3         : {97, 0, 117, 0...}
                               4         : {97, 0, 117, 0...}
.vcex                          MRUListEx : {0, 0, 0, 0...}
                               0         : {67, 0, 111, 0...}
```
	With the * we can see the types of files/ information that was recently viewed.



```
PS C:\> Get-Item 'Registry::\HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt' 
    Hive: \HKEY_USERS\S-1-5-21-1584283910-3275287195-1754958050-1005\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
Name                           Property
----                           --------
.txt                           0         : {114, 0, 101, 0...}
                               MRUListEx : {4, 0, 0, 0...}
                               1         : {114, 0, 101, 0...}
                               2         : {114, 0, 101, 0...}
                               3         : {97, 0, 117, 0...}
```
	With .txt we can see the text files/ information that was recently viewed. Queries the Hex Value Stored in the Key

This command will allow you to read some of the data stored within the keys:

```
Converting a Single Value from Hex to Unicode

[System.Text.Encoding]::Unicode.GetString((gp "REGISTRY::HKEY_USERS\*\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt")."0") 
recent1.txt b2     敲散瑮⸱湬kH	뻯    .              recent1.lnk

	Shows the text file represented by 0, you can change number to veiw the rest of the files
Convert all of a users values from HEX to Unicode

[System.Text.Encoding]::Unicode.GetString((gp "REGISTRY::HKEY_USERS\*\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt")."0")
recent1.txt b2     敲散瑮⸱湬kH	뻯    .              recent1.lnk 
```

```
PS C:\> Get-Item "REGISTRY::HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt" | select -Expand property | ForEach-Object {
    [System.Text.Encoding]::Default.GetString((Get-ItemProperty -Path "REGISTRY::HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt" -Name $_).$_)
}   
r e c e n t 1 . t x t   b 2           recent1.lnk H 	  ï¾        .                             r e c e n t 1 . l n k   
                ÿÿÿÿ
r e c e n t 2 . t x t   b 2           recent2.lnk H 	  ï¾        .                             r e c e n t 2 . l n k   
r e c e n t 3 . t x t   b 2           recent3.lnk H 	  ï¾        .                             r e c e n t 3 . l n k   
a u d i t i n g . t x t   f 2           auditing.lnk  J 	  ï¾        .                             a u d i t i n g . l n k   
a u d i t . t x t   \ 2           audit.lnk D 	  ï¾        .                             a u d i t . l n k
(Change/manipulate the extensions -.txt- to different extensions to view different sets of information)
```
Shows and converts all of the text files located in the Recent Files Registry location

## Browser Artifacts

Stores details for each user account. Records number of times a site is visited (frequency). History will record the access to the file on the website that was accessed via a link. Many sites in history will list the files that were opened from remote sites and downloaded to the local system.
```
%USERPROFILE%\AppData\Local\Google\Chrome\User Data\Default\history
C:\Users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\

```


Areas of Interest
1. URLS
The urls table contains the basic browsing history for Chrome. This will include a single instance for all the URLs visited, a timestamp for the last time visited, and a counter for the number of times visited.

2. Current Session/Tabs
If you are examining a system that still has an active session available, Chrome will store the browsing activity here under current session and if there are multiple tabs open it will store it under current tabs.

3. Top Sites
Chrome shows the user their most frequently visited sites in panels on a homepage, which allows the user to quickly click on a frequently visited site. We recover the data around any URL that is listed as a “Top Site” in Chrome.


Searching
```
# Frequency
PS C:\> Z:\strings.exe 'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\History' -accepteula 
_Output_Truncated_
https://git.cybbh.space/users/sign_in
https://git.cybbh.space/users/auth/ldapmain/callback
https://git.cybbh.space/os/public/-/jobs/artifacts/master/file/os/modules/015_windows_sysinternals/pages/15_SysInternals_winSlides.html?job=generate_adoc-slides
https://git.cybbh.space/os/public/-/jobs/artifacts/master/file/os/modules/014_windows_ad/pages/12_BloodHound_Slides.html?job=generate_adoc-slides
https://git.cybbh.space/os/public/-/jobs/artifacts/master/file/os/modules/011_win_logging/pages/8_Win_Auditing_Logging.html?job=generate_adoc-slides+
_Output_Truncated_

# Most Visited
PS C:\> Z:\strings.exe 'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\Top Sites' 
_Output_Truncated_
Fox News - Breaking News Updates | Latest News Headlines | Photos & News Videos
http://10.50.24.186:8000/themes/core/static/cyberchef.htm
https://github.com/volatilityfoundation/volatility/wiki/Command-Reference
http://172.20.25.182:8000/
http://cyberchef.com/
https://www.target.com/
http://vta.cybbh.space/
http://www.yahoo.com/
_Output_Truncated_

# User Names
PS C:\> Z:\strings.exe  'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\Login Data' 
_Output_Truncated_
http://172.20.25.182:8000/ctfadmin
https://git.cybbh.space/<USERNAME>
d9Q
https://vta.cybbh.space/<USERNAME>
https://login.yahoo.com/<USERNAME>
http://172.20.25.182:8000/ctfadmin
https://git.cybbh.space/<USERNAME>
https://vta.cybbh.space/
_Output_Truncated_
```
```
Find FQDNs in Sqlite Text files

$History = (Get-Content 'C:\users\student\AppData\Local\Google\Chrome\User Data\Default\History') -replace "[^a-zA-Z0-9\.\:\/]","" 

PS C:\> $History| Select-String -Pattern "(https|http):\/\/[a-zA-Z_0-9]+\.\w+[\.]?\w+" -AllMatches|foreach {$_.Matches.Groups[0].Value}| ft 
http://172.20.25
https://login.yahoo.com
https://os.cybbh.io
https://git.cybbh.space
http://172.20.25
_Output_Truncated_
```



## Auditing 
The Auditing Windows portion of this FG covers the concept of Windows Auditing using native tools along with the analysis of generated artifacts using cmd, powershell, or the GUI based program Eventviewer.


Enable auditing on a text file
```
    Create a text file on the Desktop

PS C:\Users\andy.dwyer\Desktop\Audit> new-item C:\Users\andy.dwyer\Desktop\Auditing.txt
    Directory: C:\Users\andy.dwyer\Desktop
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         6/7/2021   2:45 PM              0 Auditing.txt

    Add content to the file then show the contents
```
```
PS C:\Users\andy.dwyer\Desktop\Audit> set-content C:\Users\andy.dwyer\Desktop\Auditing.txt "This is the file for Auditing"

PS C:\Users\andy.dwyer\Desktop\Audit> get-content C:\Users\andy.dwyer\Desktop\Auditing.txt
This is the file for Auditing

    Set audit policy to Full Control for the "User Name" object
```
```
Rt click <file> on the desktop > Properties > Security > Advanced > Auditing > Continue > Add > Select a Principle > Type <username> (andy.dwyer) > Check Names > Ok >  Full Control > Ok > Apply > Ok

    Double click the file in Explorer, view that no auditing happened

    In Event Viewer, observe no log was created ( eventvwr )

eventvwr 
> Windows Logs > Security

(1) Opens Event Viewer GUI
```
```
    Enable the Audit Object Access

PS C:\Users\andy.dwyer> auditpol /get /category:* 
System audit policy
Category/Subcategory                      Setting
System
  Security System Extension               No Auditing
  System Integrity                        Success and Failure
  IPsec Driver                            No Auditing
  Other System Events                     Success and Failure
  Security State Change                   Success
Logon/Logoff
  Logon                                   Success and Failure
  Logoff                                  Success
  Account Lockout                         Success
_output_truncated_

(1) Shows all of the Audit Policy settings
```
```
PS C:\Users\andy.dwyer> auditpol /get /category:"Object Access" 
System audit policy
Category/Subcategory                      Setting
Object Access
  File System                             No Auditing
  Registry                                No Auditing
  Kernel Object                           No Auditing
  SAM                                     No Auditing
  Certification Services                  No Auditing
_output_truncated_

(1) Shows all of the Object Access Subcategory settings
```
```
PS C:\Users\andy.dwyer> auditpol /get /subcategory:"File System" 
System audit policy
Category/Subcategory                      Setting
Object Access
  File System                             No Auditing

(1) Shows the Fiel System subcategory setting
```
```
PS C:\Users\andy.dwyer> auditpol /set /subcategory:"File System" 
The command was successfully executed.
PS C:\Users\andy.dwyer> auditpol /get /subcategory:"File System" 
System audit policy
Category/Subcategory                      Setting
Object Access
  File System                             Success

(1) Sets the File System subcategory (2) Show that the File System setting changed
```
```
    Open the .txt file again, and open Event Viewer to show that there is an entry in the Security log


Change the settings back to default

PS C:\Users\andy.dwyer> auditpol /set /subcategory:"File System" /success:disable
The command was successfully executed.
PS C:\Users\andy.dwyer>
```

## Event Logs
```
10.1 Locations

*.evtx files accessed by:

    Windows Event View Application

    Get-Eventlog or Get-WinEvent in Powershell

    wevtutil in Command Prompt

```

```
C:\windows\system32>auditpol /get /category:"Object Access" 
System audit policy
Category/Subcategory                      Setting
Object Access
  File System                             No Auditing
  Registry                                No Auditing
  Kernel Object                           No Auditing
  SAM                                     No Auditing
  Certification Services                  No Auditing
  Application Generated                   No Auditing

C:\windows\system32>auditpol /set /subcategory:"File System" 
The command was successfully executed.

C:\windows\system32>auditpol /get /category:"Object Access"
System audit policy
Category/Subcategory                      Setting
Object Access
  File System                             Success
  Registry                                No Auditing
  Kernel Object                           No Auditing

C:\windows\system32>auditpol /set /subcategory:"File System" /success:disable 
The command was successfully executed.

 auditpol /get /category:* 
```


Command Prompt Logging

```
C:\windows\system32>wevtutil el 

C:\windows\system32>wevtutil el | find /c /v "" 
1149

C:\windows\system32>wevtutil gli security 
creationTime: 2019-01-03T22:39:36.602Z
lastAccessTime: 2021-03-15T15:47:53.735Z
lastWriteTime: 2021-03-15T15:47:53.735Z
fileSize: 15798272
attributes: 32
numberOfLogRecords: 17595
oldestRecordNumber: 1

C:\windows\system32>wevtutil qe security /c:3 /f:text 
Event[0]:
  Log Name: Security
  Source: Microsoft-Windows-Eventlog
  Date: 2019-01-03T20:22:38.227
  Event ID: 1102

_Output_Truncated_
```


```
Powershell
PS C:\> Get-EventLog -LogName System -Newest 10 
   Index Time          EntryType   Source                 InstanceID Message
   ----- ----          ---------   ------                 ---------- -------
    1102 Mar 15 12:00  Information EventLog               2147489661 The system uptime is 2750871 seconds.
    1101 Mar 14 12:00  Information EventLog               2147489661 The system uptime is 2664471 seconds.
    1100 Mar 13 23:52  Information Microsoft-Windows...   16 The description for Event ID '16' in Source 'Microsoft-Windows-Kernel-Gen...
    1099 Mar 13 23:52  Information Microsoft-Windows...   16 The description for Event ID '16' in Source 'Microsoft-Windows-Kernel-Gen...
    1098 Mar 13 12:00  Information EventLog               2147489661 The system uptime is 2578071 seconds.
    1097 Mar 12 21:52  Information Microsoft-Windows...   16 The description for Event ID '16' in Source 'Microsoft-Windows-Kernel-Gen...
    1096 Mar 12 21:52  Information Microsoft-Windows...   16 The description for Event ID '16' in Source 'Microsoft-Windows-Kernel-Gen...
    1095 Mar 12 12:00  Information EventLog               2147489661 The system uptime is 2491671 seconds.
    1094 Mar 11 20:58  Error       DCOM                   10016 The description for Event ID '10016' in Source 'DCOM' cannot be found.  T...
    1093 Mar 11 18:27  Information Microsoft-Windows...   16 The description for Event ID '16' in Source 'Microsoft-Windows-Kernel-Gen...

PS C:\> Get-EventLog -LogName System -Newest 3 | Format-Table -Wrap 
   Index Time          EntryType   Source                 InstanceID Message
   ----- ----          ---------   ------                 ---------- -------
    1102 Mar 15 12:00  Information EventLog               2147489661 The system uptime is 2750871 seconds.
    1101 Mar 14 12:00  Information EventLog               2147489661 The system uptime is 2664471 seconds.
    1100 Mar 13 23:52  Information Microsoft-Windows-Ke   16 The description for Event ID '16' in Source
                                   rnel-General           'Microsoft-Windows-Kernel-General' cannot be found.  The local computer may not have the necessary registry information or message DLL files to display the message, or you may not have permission to access them. The following  information is part of the event:'119', '\??\C:\windows\ServiceProfiles\NetworkService\AppData\Local\Microsoft\Windows\DeliveryOptimization\State\dosvcState.dat', '4', '1'
```


```
PS C:\> Get-WinEvent -Listlog * 
LogMode   MaximumSizeInBytes RecordCount LogName
-------   ------------------ ----------- -------
Circular            20971520         993 Application
Circular            20971520           0 HardwareEvents
Circular             1052672           0 Internet Explorer
Circular            20971520           0 Key Management Service
Circular            20971520       17711 Security
Circular            20971520         576 System
Circular            15728640         176 Windows PowerShell
Circular            20971520             ForwardedEvents
Circular            10485760           0 Microsoft-AppV-Client/Admin
_Output_Trucncated_

PS C:\> (Get-WinEvent -Listlog *).count 
426

PS C:\> Get-WinEvent -Listlog * | findstr /i "Security" 
Circular            20971520       18179 Security
Circular             1052672           0 Microsoft-Windows-Security-Adminless/Operational
Circular             1052672           0 Microsoft-Windows-Security-Audit-Configuration-Client/Operational
Circular             1052672           0 Microsoft-Windows-Security-EnterpriseData-FileRevocationManager/Operational
Circular             1052672             Microsoft-Windows-Security-ExchangeActiveSyncProvisioning/Operational
Circular             1052672             Microsoft-Windows-Security-IdentityListener/Operational
_Output_Truncated_

```


```
PS C:\> Get-Winevent -FilterHashtable @{logname='Security';id='4624'} | ft -Wrap 
   ProviderName: Microsoft-Windows-Security-Auditing
TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------                                    3/15/2021 7:42:19 PM          4624 Information      An account was successfully logged on.                                                        Subject:
                                                    	Security ID:		S-1-5-18
                                                    	Account Name:		ADMIN-STATION$
                                                    	Account Domain:		WORKGROUP
                                                    	Logon ID:		0x3E7
                                                    Logon Information:
                                                    	Logon Type:		5
                                                    	Restricted Admin Mode:	-
                                                    	Virtual Account:	No
                                                    	Elevated Token:		Yes
                                                    Impersonation Level:	Impersonation
                                                    New Logon:
                                                    	Security ID:		S-1-5-18
                                                    	Account Name:		SYSTEM
                                                    	Account Domain:		NT AUTHORITY
                                                    	Logon ID:		0x3E7
                                                    	Linked Logon ID:	0x0
                                                    	Network Account Name:	-
                                                    	Network Account Domain:	-
                                                    	Logon GUID:             {00000000-0000-0000-0000-000000000000}
_Output_Truncated_

PS C:\> Get-Winevent -FilterHashtable @{logname='Security';id='4624'} | ft -Wrap | findstr /i "generated" 

```


```
Powershell Operational logs

PS C:\> Get-WinEvent Microsoft-Windows-PowerShell/Operational | Where-Object {$_.Message -ilike "*RunspacePool*"} | Format-List 
TimeCreated  : 3/8/2021 7:28:43 PM
ProviderName : Microsoft-Windows-PowerShell
Id           : 8195
Message      : Opening RunspacePool

TimeCreated  : 3/8/2021 7:28:43 PM
ProviderName : Microsoft-Windows-PowerShell
Id           : 8194
Message      : Creating RunspacePool object
                	 InstanceId 18bed982-3d17-47b0-8f7a-0836900efea6
                	 MinRunspaces 1
                	 MaxRunspaces 1
_Output_Truncated_

Get-WinEvent Microsoft-Windows-PowerShell/Operational | Where-Object {$_.Message -ilike "*Pipeline ID = ##"} | Format-List

```

## Powershell Artifacts
PowerShell Transcript is a feature that creates a record of all or part of a PowerShell session to a text file.


```
PS C:\> Start-Transcript 
Transcript started, output file is C:\Users\andy.dwyer\Documents\PowerShell_transcript.ADMIN-STATION.OGp3Fa
x7.20210316141734.txt
```

Powershell History

```


PS C:\> Get-History 
  Id CommandLine
  -- -----------
   1 Get-PSDrive
   2 get-process | select name,id,Description | sort -Property id
   3 regedit
   4 cls
_Output_Truncated_
C:\Users\username\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt


PS C:\> Get-Content "C:\users\$env:username\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt" 
Get-CimInstance Namespace root\securitycenter2 ClassName antispywareproduct
Get-CimInstance -Namespace root\securitycenter2 -ClassName antispywareproduct
hostname
whoami
exit
get-process
_Output_Truncated_
```


## Powershell Script Blocking



Script block logging records blocks of code as they are executed by the PowerShell engine, thereby capturing the full contents of code executed by an attacker, including scripts and commands. Due to the nature of script block logging, it also records de-obfuscated code as it is executed.

What logs are generated by PowerShell?

By default no logs are generated by PowerShell. This is dangerous since this basically means any actions in PowerShell have no trail to follow. By default a few of the more powerful features of Windows and PowerShell are turned off, but let’s discuss what each one means and how to use them to our advantage in defense of our machines.

    "A PowerShell “script block” is the base level of executable code in PowerShell. It might represent a command typed interactively in the PowerShell console, supplied through the command line, or wrapped in a function, script, workflow, etc."

    Script block logging doesn’t just look at the code that was supplied via the console or scripts that have been ran, but what the PowerShell engine actually runs.

    This feature will show any obfuscated commands (i.e. Base64, Rot 13 or CaSe InSenSiTive StRingS, etc) as well as the decoded input that the PowerShell engine runs.

    While not available in PowerShell 4.0, PowerShell 5.0 will automatically log code blocks if the block’s contents match on a list of suspicious commands or scripting techniques, even if script block logging is not enabled.

Q: How do I enable Script Block logging?

```
reg add HKLM\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging\ /v EnableScriptBlockLogging /t REG_DWORD /d 1 /f
```

    4103 is Verbose powershell command execution enabled via Script Block Logging.

    4104 show the actual scripts ran, the encoded and decodes versions. If it was a file it will show the files name run then another even will have the script within that file

    4105 is the time a script started aka the PowerShell engine was started

    4106 is the time a script ended aka the PowerShell engine was stopped



# Memory Analysis (Day 9)

Volatile Memory
	

    Non-persistent - requires power to maintain stored information; immediate loss of data after power loss.

    Examples: RAM

Non-Volatile Memory
	

    Persistent - Does not require a continuous power supply to retain the dta stored in a computing device

    Examples: HDD, USB

## Order of Volatility



Order of Volatility From Most to Least

    CPU registers, cache

    Routing table, ARP cache, process table, kernel stats, memory

    Temporary file systems

    Disk

    Remote logging and monitoring data

    Physical configuration, network topology

    Archival media - backups
https://datatracker.ietf.org/doc/html/rfc3227#section-2.1

## Volatility Versions


Python
	

    Updated Frequently

    All profiles available

	

    Lengthy Install

    Can’t run without Python installed

Standlone
	

    No install necessary

    Quick and easy to download/run

    Can run without python

	

    Not all profiles included

    Not updated frequently



## Using Volatility


```
PS C:\windows\system32> invoke-webrequest -uri "https://github.com/notepad-plus-plus/notepad-plus-plus/releases/download/v7.8.8/npp.7.8.8.Installer.x64.exe" -outfile "C:\npp.7.8.8.Installer.x64.exe" 

PS C:\windows\system32> cd C:\ 

PS C:\> start-process npp.7.8.8.Installer.x64.exe -ArgumentList '/S' 

	invoke-webrequest downloads Notepad++ 7.8.8 installer to C:\
	cd to C:\
	start-process to launch Notepad++ 7.8.8 installer and accept defaults (/s)
```


```


PS C:\Users\andy.dwyer\Desktop\Memory_Analysis> .\volatility_2.6_win64_standalone.exe -h 

	-h or --help will list options and supported plugin commands for Volatility

```


```


PS C:\Users\andy.dwyer\Desktop\Memory_Analysis> .\volatility_2.6_win64_standalone.exe -f <FILENAME> --profile=<PROFILE> <PLUGIN> 

	At a minimum, the Volatility executable followed by a filename (-f), profile(--profile=), and plugin should be used when working with a memory image/dump.



PS C:\Users\andy.dwyer\Desktop\Memory_Analysis> .\volatility_2.6_win64_standalone.exe -f ".\cridex.vmem" imageinfo 
          Suggested Profile(s) : WinXPSP2x86, WinXPSP3x86 (Instantiated with WinXPSP2x86) 
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (C:\Users\andy.dwyer\Desktop\Memory_Analysis\cridex.vmem)
                      PAE type : PAE
                           DTB : 0x2fe000L
                          KDBG : 0x80545ae0L
          Number of Processors : 1
     Image Type (Service Pack) : 3
                KPCR for CPU 0 : 0xffdff000L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2012-07-22 02:45:08 UTC+0000
     Image local date and time : 2012-07-21 22:45:08 -0400
```
```norse god freya
Volatility syntax to list available plugins for a given profile
PS C:\Users\andy.dwyer\Desktop\Memory_Analysis> .\volatility_2.6_win64_standalone.exe -f ".\cridex.vmem" --profile=WinXPSP2x86 -h 

	help (-h) syntax to list plugins available for the profile WinXPSP2x86 (--profile=WinXPSP2x86)
```

## Volatility Methodoloy

```



The SANS Institute recommends the following commands when using Volatility.

    Identify Rogue Processes: pslist vs. psscan; output results to a dot file to have a nice visual representation of parent/child process relationships

        Process validity - look for things that are off (misspellings, high PIDs, multiples that shouldn’t be, etc.)

    DLLs and Handles: dlllist, dlldump

    Network Artifacts: connections

    Hunt for Code Injection: malfind

    Check for rootkit: psscan, devicetree

    Dump suspicious processes and drivers: dlldump, procdump, memdump, filescan, svcscan, driverirp



```



## Registry Analysis

```


It is possible to read the registry from the box but a bit more involved. The list below shows plugins and options one may use within Volatility to achieve this.

    hivelist - Shows addresses of hives and filesystem locations

    printkey

        use -o with the virtual offset to show subkeys

        use -K with the location of the registry key you want on the filesystem (note double quotes with this method) "path\to\key"

    hivedump - use -o with virtual offset to recursively list all subkeys

    hashdump - may or may not work, depending

    dumpregistry - Go nuclear. Dumps the whole registry to disk (requires --dump-dir)

Try other plugins to investigate other artifacts mentioned in earlier lectures. Run help in Volatility to see what plugins you have available for use.

```


# Active Directory (Day 9)



1.) Domains

    Active Directory objects (users or devices) that all use the same database or are typically in the same location.

2.) Trees

    Several Domains grouped together. Typically, has a primary domain controller for the entire tree.

3.) Forests

    Forests are groups of trees connected together via trust relationships.



## Initial Recon

1. Get a list of AD Commands Available

PS> Get-Command -Module activedirectory

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Add-ADCentralAccessPolicyMember                    1.0.1.0    ActiveDirectory
Cmdlet          Add-ADComputerServiceAccount                       1.0.1.0    ActiveDirectory
Cmdlet          Add-ADDomainControllerPasswordReplicationPolicy    1.0.1.0    ActiveDirectory
Cmdlet          Add-ADFineGrainedPasswordPolicySubject             1.0.1.0    ActiveDirectory

__________CUT____________



2. Get the Default Domain Password Policy

    AD supports one set of password and account lockout policies for a domain. Beginning in Windows Server 2008, you can override the default password and account lockout policies in a domain using Fine-Grained Password Policies (FGPP

PS> Get-ADDefaultDomainPasswordPolicy

ComplexityEnabled           : True
DistinguishedName           : DC=army,DC=warriors
LockoutDuration             : 00:30:00
LockoutObservationWindow    : 00:30:00
LockoutThreshold            : 0
MaxPasswordAge              : 42.00:00:00
__________CUT____________


3. Check for any Fine-Grained Password Policies

PS> Get-ADFineGrainedPasswordPolicy -Filter {name -like "*"}

   -No returns means it is not set-


4. Get Forest details

PS> Get-ADForest

ApplicationPartitions : {DC=DomainDnsZones,DC=army,DC=warriors, DC=ForestDnsZones,DC=army,DC=warriors}
CrossForestReferences : {}
DomainNamingMaster    : domain-controll.army.warriors
Domains               : {army.warriors}
__________CUT____________


5. Get Domain details:

PS> Get-ADDomain

AllowedDNSSuffixes                 : {}
ChildDomains                       : {}
ComputersContainer                 : CN=Computers,DC=army,DC=warriors
DeletedObjectsContainer            : CN=Deleted Objects,DC=army,DC=warriors
DistinguishedName                  : DC=army,DC=warriors
__________CUT____________


6. Get AD Groups

Get-ADGroup -Filter *

DistinguishedName : CN=System Admins,CN=Users,DC=army,DC=warriors
GroupCategory     : Security
GroupScope        : Global
Name              : System Admins
__________CUT____________


7. Get a groups details

PS> Get-ADGroup -Identity 'IA Analysts Team'

DistinguishedName : CN=IA Analysts Team,CN=Users,DC=army,DC=warriors
GroupCategory     : Security
GroupScope        : Global
Name              : IA Analysts Team
__________CUT____________


8. Get a list of a groups members

PS> Get-ADGroupMember -Identity 'IA Analysts Team' -Recursive
   -No return means there are no assigned members-


9. Get AD users

PS> Get-ADUser -Filter 'Name -like "*"'

DistinguishedName : CN=Willie.Liu,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors
Enabled           : True
GivenName         : Willie
Name              : Willie.Liu
ObjectClass       : user
__________CUT____________


10. To see additional properties, not just the default set

PS> Get-ADUser -Identity 'Nina.Webster' -Properties Description

Description       : 3rd PLT Soldier
DistinguishedName : CN=Nina.Webster,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors
Enabled           : True
GivenName         : Nina
Name              : Nina.Webster
ObjectClass       : user
ObjectGUID        : b35ba844-5b40-4eb4-96fd-ffafef36269a
Office            :
SamAccountName    : Nina.Webster
SID               : S-1-5-21-1181003830-945744892-2632747169-1820
Surname           : Webster
UserPrincipalName :


## Enumerate Users


Find Disabled users

PS> get-aduser -filter {Enabled -eq "FALSE"} -properties name, enabled

DistinguishedName : CN=Guest,CN=Users,DC=army,DC=warriors
Enabled           : False
GivenName         :
Name              : Guest
ObjectClass       : user
__________CUT____________


Enable that user

PS> Enable-ADAccount -Identity guest
   -Nothing returned if successful execution-


Change the password

PS> Set-AdAccountPassword -Identity guest -NewPassword (ConvertTo-SecureString -AsPlaintext -String "PassWord12345!!" -Force)
   -Nothing returned if successful execution-


Add the user to an Admin Group

Add-ADGroupMember -Identity "Domain Admins" -Members guest
-Nothing returned if successful execution-



## Scenario 2


Get Distinguished Name to match AD format

PS> Get-ADuser -filter * | select distinguishedname, name

CN=Amelie.Benjamin,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors     Amelie.Benjamin
CN=Ramon.Gibbs,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors         Ramon.Gibbs
CN=Willie.Liu,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors          Willie.Liu
CN=Yair.Roth,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors           Yair.Roth
CN=Elisha.Coleman,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors      Elisha.Coleman
__________CUT____________


Create a new user

New-ADUser -Name "Bad.Guy" -AccountPassword (ConvertTo-SecureString -AsPlaintext -String "PassWord12345!!" -Force) -path "OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors"
   -Nothing returned if successful execution-


Enable the user

Enable-ADAccount -Identity "Bad.Guy"
   -Nothing returned if successful execution-


Add the user to an Admin Group

Add-ADGroupMember -Identity "Domain Admins" -Members "Bad.Guy"
   -Nothing returned if successful execution-


Remove User

PS> Remove-ADUser -Identity "Bad.Guy"

Confirm
Are you sure you want to perform this action?
Performing the operation "Remove" on target "CN=Bad.Guy,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y


Remove From Group

PS> Remove-ADGroupMember -Identity "Domain Admins" -Members guest

Confirm
Are you sure you want to perform this action?
Performing the operation "Remove" on target "CN=Bad.Guy,OU=3RD PLT,OU=CCO,OU=3RDBN,OU=WARRIORS,DC=army,DC=warriors".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y


Disable Guest account

PS> Disable-AdAccount -Identity Guest
   -Nothing returned if successful execution-



## Enumerate User DCO POV


Get All Domain Admin Accounts

PS> Get-AdGroupMember -identity "Domain Admins" -Recursive | %{Get-ADUser -identity $_.DistinguishedName}
7ThZ6YymPWum8GV
PS> Get-AdGroupMember -identity "Domain Admins" -Recursive | %{Get-ADUser -identity $_.DistinguishedName} | select name, Enabled

name            Enabled
----            -------
Administrator      True
andy.dwyer         True
Giada.Barrett      True
Garrett.Lowery     True
Trevon.Wolfe       True
Angelo.Berry       True
__________CUT____________


Get ALL Enterprise Admin accounts

Get-AdGroupMember -identity "Enterprise Admins" -Recursive | %{Get-ADUser -identity $_.DistinguishedName} | select name, Enabled

name          Enabled
----          -------
Administrator    True
__________CUT____________



## Display RSoP Info


1. Display Help

C:> gpresult /?

GPRESULT [/S system [/U username [/P [password]]]] [/SCOPE scope]
           [/USER targetusername] [/R | /V | /Z] [(/X | /H) <filename> [/F]]

Description:
    This command line tool displays the Resultant Set of Policy (RSoP)
    information for a target user and computer.
__________CUT____________



2. Output the computer and user node settings of a user

C:> gpresult /user Webster /v

C:> gpresult /user Administrator /v

RSOP data for ARMY\Administrator on DOMAIN-CONTROLL : Logging Mode


OS Configuration:            Primary Domain Controller
OS Version:                  10.0.17763
Site Name:                   Default-First-Site-Name
Roaming Profile:             N/A
Local Profile:               C:\Users\Administrator
__________CUT____________


3. Displays data about the machine and logged on user

C:> gpresult /r

COMPUTER SETTINGS

    CN=DOMAIN-CONTROLL,OU=Domain Controllers,DC=army,DC=warriors
    Last time Group Policy was applied: 2/25/2021 at 6:21:44 PM
    Group Policy was applied from:      domain-controll.army.warriors
    Group Policy slow link threshold:   500 kbps
    Domain Name:                        ARMY
    Domain Type:                        Windows 2008 or later
__________CUT____________


4. Force any group policy setting to take affect immediately versus rebooting the computer

C:> gpupdate /force

Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.



## Admin Best Practices

1. Get Name Property from the Active Directory Group named "Domain Admins"

PS> (Get-AdGroupMember -Identity 'domain admins').Name
Administrator
System Admins LV1

PS> Get-AdGroupMember -Identity 'domain admins' | select name

name
--------
Administrator
System Admins LV1


2. Get Active Directory Group 'System' Admin Names 'LvL 1'

PS> (Get-AdGroupMember -Identity "System Admins LV1").Name
System Admins


3. Get Active Directory Group 'System Admin' Names

PS> (Get-AdGroupMember -Identity "System Admins").Name
andy.dwyer
System Admins
Print Server Group
System Admins LV2
Giada.Barrett
Garrett.Lowery
Trevon.Wolfe
Angelo.Berry

4. Get Active Directory Group 'System' Admin Names 'LVL 2'

PS> (Get-AdGroupMember -Identity "System Admins LV2").Name
Silas.Salas
Shania.Reilly
Santino.Glass
Xavier.Ibarra
London.Cantrell7ThZ6YymPWum8GV
Raegan.Lee






Vrc0vw7ZUaLBpQp

norse god freya

Get-ADuser -Filter {name -like "*tiff.*"} -properties *





grep -f /filename /filename 




# Review

## Powershell Profiles

Persistence 

Profiles 
$HOME/Profile
$Profiles

All Users, All Hosts
$PsHome\Profile.ps1

All Users, Current Host
$PsHome\Microsoft.PowerShell_profile.ps1

Current User, All Hosts
$Home\[My]Documents\Profile.ps1

Current User, Current Host
$Home\[My ]Documents\WindowsPowerShell\Profile.ps1


$profile | Get-Member -Type NoteProperty                        # Displays the profile values of Names, MemberType, and Paths.
$Profile | get-member -type noteproperty | ft -wrap             # Displays the same results but completed in case it was cut off '...'
$PROFILE | Get-Member -MemberType noteproperty | select name    # Narrowed results to display only Names

## Windows Reg


regedit
reg query
get-childitem / get-item 

Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run 

Get-ChildItem HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\ 

Get-item HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run


net use * http://live.sysinternals.com



HKLM\Software\Microsoft\Windows\CurrentVersion\Run

HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\Run

HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\RunOnce

HKLM\SYSTEM\CurrentControlSet\services

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders

HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon



Microsoft Edge Internet URL history and Browser Artifacts and Forensics
HKEY_CLASSES_ROOT\Local Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Storage\microsoft.microsoftedge_8wekyb3d8bbwe\Children\001\Internet Explorer\DOMStorage


USB history / USB Forensics
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB

        This registry key contains information about all USB devices that have been connected to the system at some point, regardless of whether they are currently connected or not. It includes information about the USB controllers, hubs, and individual devices. Each device is typically identified by a unique identifier (like a device instance path or hardware ID).

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR
This registry key specifically deals with USB storage devices, such as USB flash drives, external hard drives, etc. It contains information about connected USB storage devices, including details like device instance paths, hardware IDs, and other configuration information.


Recent MRU history / MRU in forensics

    HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU

        MRU is the abbreviation for most-recently-used.

        This key maintains a list of recently opened or saved files via typical Windows Explorer-style common dialog boxes (i.e. Open dialog box and Save dialog box).

        For instance, files (e.g. .txt, .pdf, htm, .jpg) that are recently opened or saved files from within a web browser (including IE and Firefox) are maintained.


Recent Files with LNK files
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs


Windows User Profiles User Account Forensics
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList


Saved Network Profiles and How to decode Network history
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles


Windows Virtual Memory and why it is important=
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management


## ADS

Get-Item reminder.txt -Stream * 



## Linux Essentials
ls --help 


read
r
4
Read the contents of the file
List the contents of the directory

write
w
2
Write content into a file
Create/delete in the directory

exe
x
1
Run the file as an executable
Move into the directory



## Windows Boot Process
findstr /C:"Detected boot environment" "C:\Windows\Panther\Setupact.log"
Get-Content C:\Windows\Panther\Setupact.log | Select-String "Detected boot environment"




c:\demo>bcdedit

Windows Boot Manager
--------------------
identifier              {bootmgr}
device                  partition=C:
description             Windows Boot Manager
locale                  en-US
inherit                 {globalsettings}
default                 {current}
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
displayorder            {current}
toolsdisplayorder       {memdiag}
timeout                 29

Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \windows\system32\winload.exe
description             Windows 7 - Tiger Paw
locale                  en-US
inherit                 {bootloadersettings}
recoverysequence        {91061b50-0fa8-11e9-aa6e-00155d49334a}
displaymessageoverride  Recovery
recoveryenabled         Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \windows
resumeobject            {2bd08882-0f8f-11e9-94b6-0002c9550dce}
nx                      OptIn
bootmenupolicy          Standard



##  Linux Boot Process
/sbin/init
/etc/init
etc/inittab



cat /etc/inittab

is:5:initdefault: 


l0:0:wait:/etc/rc0.d
l1:1:wait:/etc/rc1.d
l2:2:wait:/etc/rc2.d
l3:3:wait:/etc/rc3.d
l4:4:wait:/etc/rc4.d 
l5:5:wait:/etc/rc5.d
l6:6:wait:/etc/rc6.d


student@linux-opstation-kspt:/etc/rc3.d$ ls -l /etc/rc3.d/ 

lrwxrwxrwx 1 root root 15 Jan 31  2020 S01acpid -> ../init.d/acpid 
lrwxrwxrwx 1 root root 17 Feb  4  2020 S01anacron -> ../init.d/anacron
lrwxrwxrwx 1 root root 16 Jan 31  2020 S01apport -> ../init.d/apport
lrwxrwxrwx 1 root root 13 Jan 31  2020 S01atd -> ../init.d/atd
lrwxrwxrwx 1 root root 26 Jan 31  2020 S01console-setup.sh -> ../init.d/console-setup.sh
lrwxrwxrwx 1 root root 14 Jan 31  2020 S01cron -> ../init.d/cron
lrwxrwxrwx 1 root root 14 Jan 31  2020 S01dbus -> ../init.d/dbus
lrwxrwxrwx 1 root root 14 Feb  4  2020 S01gdm3 -> ../init.d/gdm3


student@linux-opstation-kspt:/etc/rc3.d$ ls -l /etc/rc1.d/ 

lrwxrwxrwx 1 root root 20 Feb  4  2020 K01alsa-utils -> ../init.d/alsa-utils
lrwxrwxrwx 1 root root 13 Jan 31  2020 K01atd -> ../init.d/atd
lrwxrwxrwx 1 root root 20 Jan 31  2020 K01cryptdisks -> ../init.d/cryptdisks
lrwxrwxrwx 1 root root 26 Jan 31  2020 K01cryptdisks-early -> ../init.d/cryptdisks-early
lrwxrwxrwx 1 root root 18 Jan 31  2020 K01ebtables -> ../init.d/ebtables
lrwxrwxrwx 1 root root 14 Feb  4  2020 K01gdm3 -> ../init.d/gdm3 



cat /lib/systemd/system/default.target | tail -n 8

Description=Graphical Interface
Documentation=man:systemd.special(7)
Requires=multi-user.target
Wants=display-manager.service 
Conflicts=rescue.service rescue.target
After=multi-user.target rescue.service rescue.target display-manager.service 
AllowIsolate=yes



student@linux-opstation-kspt:/$ ls -l /etc/systemd/system/ | grep graphical
drwxr-xr-x 2 root root 4096 Feb  4  2020 graphical.target.wants 

student@linux-opstation-kspt:/$ ls -l /etc/systemd/system/graphical.target.wants/
total 0
lrwxrwxrwx 1 root root 43 Jan 31  2020 accounts-daemon.service -> /lib/systemd/system/accounts-daemon.service  
lrwxrwxrwx 1 root root 35 Feb  4  2020 udisks2.service -> /lib/systemd/system/udisks2.service 

student@linux-opstation-kspt:/$ ls -l /lib/systemd/system | grep graphical
lrwxrwxrwx 1 root root   16 Nov 15  2019 default.target -> graphical.target
-rw-r--r-- 1 root root  598 Jan 28  2018 graphical.target
drwxr-xr-x 2 root root 4096 Jan 31  2020 graphical.target.wants 
lrwxrwxrwx 1 root root   16 Nov 15  2019 runlevel5.target -> graphical.target

student@linux-opstation-kspt:/$ ls -l /lib/systemd/system/graphical.target.wants/
total 0
lrwxrwxrwx 1 root root 39 Nov 15  2019 systemd-update-utmp-runlevel.service -> ../systemd-update-utmp-runlevel.service 





    This means that the default.target is actually graphical.target

    The graphical.target unit wants to start:

        display-manager.service

        udisks2.service

        accounts-daemon.service

        systemd-update-utmp-runlevel.service

    But, the graphical.target requires the multi-user.target to execute.



## Process Validity 

PS C:\Users\student> Get-Process

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    278      18     9420      18984       3.61   6304   1 ApplicationFrameHost
    342      19     4516       3988              4624   0 armsvc
    958      57   127900     202620      51.38    632   1 atom
    572      82   182356     266836     117.64   3148   1 atom
    321      33    92760     164644       0.56   7864   1 atom
    222      15     6884      28916       0.03   8024   1 atom
    733      27   143268     172480      38.33  13980   1 atom
     68       5     2040       4128       0.02   7504   1 cmd


     PS C:\Users\student> Get-Ciminstance Win32_service | Select Name, Processid, Pathname | ft -wrap | more

Name                                                   Processid Pathname
----                                                   --------- --------
AdobeARMservice                                             4624 "C:\Program Files (x86)\Common Files\Adobe\ARM\1.0\armsvc.exe"
AJRouter                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestricted -p
ALG                                                            0 C:\WINDOWS\System32\alg.exe
AppIDSvc                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestricted -p
Appinfo                                                     7752 C:\WINDOWS\system32\svchost.exe -k netsvcs -p
AppReadiness                                                   0 C:\WINDOWS\System32\svchost.exe -k AppReadiness -p
AppXSvc                                                    13292 C:\WINDOWS\system32\svchost.exe -k wsappx -p
AudioEndpointBuilder                                        3168 C:\WINDOWS\System32\svchost.exe -k LocalSystemNetworkRestricted -p
Audiosrv                                                    3920 C:\WINDOWS\System32\svchost.exe -k LocalServiceNetworkRestricted -p
autotimesvc                                                    0 C:\WINDOWS\system32\svchost.exe -k autoTimeSvc
AxInstSV                                                       0 C:\WINDOWS\system32\svchost.exe -k AxInstSVGroup
BDESVC                                                      1628 C:\WINDOWS\System32\svchost.exe -k netsvcs -p
BFE                                                         3908 C:\WINDOWS\system32\svchost.exe -k LocalServiceNoNetworkFirewall -p
BITS                                                           0 C:\WINDOWS\System32\svchost.exe -k netsvcs -p
BrokerInfrastructure                                        1172 C:\WINDOWS\system32\svchost.exe -k DcomLaunch -p


PS C:\Users\student> Get-Ciminstance Win32_service | Select Name, Processid, Pathname | more

Name                                                   Processid Pathname
----                                                   --------- --------
AdobeARMservice                                             4624 "C:\Program Files (x86)\Common Files\Adobe\ARM\1.0\armsvc.exe"
AJRouter                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestri...
ALG                                                            0 C:\WINDOWS\System32\alg.exe
AppIDSvc                                                       0 C:\WINDOWS\system32\svchost.exe -k LocalServiceNetworkRestri...
Appinfo                                                     7752 C:\WINDOWS\system32\svchost.exe -k netsvcs -p
AppReadiness                                                   0 C:\WINDOWS\System32\svchost.exe -k AppReadiness -p
AppXSvc                                                        0 C:\WINDOWS\system32\svchost.exe -k wsappx -p
AudioEndpointBuilder                                        3168 C:\WINDOWS\System32\svchost.exe -k LocalSystemNetworkRestric...
Audiosrv                                                    3920 C:\WINDOWS\System32\svchost.exe -k LocalServiceNetworkRestri...

-- More --



PS C:\Users\student> get-service ALG | format-list *


Name                : ALG
RequiredServices    : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
DisplayName         : Application Layer Gateway Service
DependentServices   : {}
MachineName         : .
ServiceName         : ALG
ServicesDependedOn  : {}
ServiceHandle       :
Status              : Stopped
ServiceType         : Win32OwnProcess
StartType           : Manual
Site                :
Container           :




schtasks /query /tn "IchBinBosh" /v /fo list

Folder: \
HostName:                             ADMIN-STATION
TaskName:                             \IchBinBosh
Next Run Time:                        6/1/2021 5:02:00 PM
Status:                               Ready
Logon Mode:                           Interactive only
Last Run Time:                        6/1/2021 4:47:00 PM
Last Result:                          0
Author:                               ADMIN-STATION\andy.dwyer
Task To Run:                          powershell.exe -win hidden -encode JABMAD0ATgBlAHcALQBPAGIAagBlAGMAdAAgAFMAeQBzAHQAZQBtAC4ATgBlAHQALgBTAG8AYwBrAGUAdABzAC4AVABjAHAATABpAHMAdABlAG4AZQByACgANgA2ADYANgApADsAJABMAC4AUwB0AGEAcgB0ACgAKQA7AFMAdABhAHIAdAAtAFMAbABlAGUAcAAgAC0AcwAgADYAMAA=
Start In:                             N/A
Comment:                              N/A
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          andy.dwyer
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        One Time Only, Minute
Start Time:                           4:02:00 PM
Start Date:                           6/1/2021
End Date:                             N/A
Days:                                 N/A
Months:                               N/A
Repeat: Every:                        0 Hour(s), 15 Minute(s)
Repeat: Until: Time:                  None
Repeat: Until: Duration:              Disabled
Repeat: Stop If Still Running:        Disabled



Autorun Registry Locations
https://os.cybbh.io/public/os/latest/011_windows_auditing_&_logging/artifacts_fg.html#_10_1_locations

    Q: What are some Registry keys that can be used for autoruns?

        Registry Keys Locations, Locations connected with Services.

            HKLM\Software\Microsoft\Windows\CurrentVersion\Run - Local Machine

            HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

            HKLM\System\CurrentControlSet\Services

        Remember that the Users have individual Hives with autoruns as well as the Current User.

            HKCU\Software\Microsoft\Windows\CurrentVersion\Run - Current User

            HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce

            HKU\<sid>\Software\Microsoft\Windows\CurrentVersion\Run - Specific User

            HKU\<sid>\Software\Microsoft\Windows\CurrentVersion\RunOnce

        The order in which services are loaded can be adjusted.

            HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\ServiceGroupOrder

            HKEY_LOCAL_MACHINE\CurrentControlSet\Control\GroupOrderList




andy.dwyer@ADMIN-STATION C:\Users\andy.dwyer>netstat -anob | more

Active Connections

net star

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:22             0.0.0.0:0              LISTENING       2944
 [sshd.exe]
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       832
  RpcSs
 [svchost.exe]
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
 Can not obtain ownership information
  TCP    0.0.0.0:3389           0.0.0.0:0              LISTENING       304
  TermService
 [svchost.exe]
  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING       4456
  CDPSvc

-- More --

TCP View

## Process Validity in Linux


The cron daemon checks the directories /var/spool/cron, /etc/cron.d and the file /etc/crontab, once a minute and executes any commands specified that match the time.



    crontab -u [user] file This command will load the crontab data from the specified file

    crontab -l -u [user] This command will display/list user’s crontab contents

    crontab -r -u [user] This Command will remove user’s crontab contents

    crontab -e -u [user] This command will edit user’s crontab contents


## Auditing and Logging
https://os.cybbh.io/public/os/latest/011_windows_auditing_&_logging/artifacts_fg.html#_10_1_locations



