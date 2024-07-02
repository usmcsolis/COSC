# Important 

https://os.cybbh.io/public/os/latest/index.html


http://10.50.22.197:8000/http://10.50.22.197:8000/

## Stack 8
```
Stack 8 : 10.50.35.48
```

## Remote Connection Instructions

```
xfreerdp /u:student /v:10.50.35.48 /dynamic-resolution +glyph-cache +clipboard


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


