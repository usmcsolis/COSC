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
ssh -X student@10.8.0.6
garviel : luna

Workstation2 (Windows)
ssh -X student@10.8.0.4
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



# Alternate Data Streams (Day 2 Continued)
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




