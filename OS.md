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
