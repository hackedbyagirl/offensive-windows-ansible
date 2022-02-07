# offensive-windows-ansible
Ansible playbook to set up an offensive windows workstation

## Pre-Requisites
For Ansible to communicate to a Windows host and use Windows modules, the Windows host must meet these requirements:
- Ansible requires PowerShell 3.0 or newer and at least .NET 4.0 to be installed on the Windows host.
- A WinRM listener should be created and activated. More details for this can be found below.

### Upgrading PowerShell and .NET Framework
The base image of windows does not meet the requirements to run ansible, therefore, PowerShell and .NET must be upgraded. This can be done by running the following script. `Upgrade-PoweerShell.ps1` that is located in the `scripts` folder.
 
Example of how to run this script

```powershell
# Make sure you're able to run the script in powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force

# Upgrade to powershell 5.1 with automatic login and reboots
powershell.exe -ExecutionPolicy Bypass -File Upgrade-Powershell.ps1 -version 5.1 -username "Username" -password "Password"
```
Once completed, you will need to remove auto login and set the execution policy back to the default `Restricted `` for Windows clients, or ``RemoteSigned` for Windows servers). You can do this with the following PowerShell commands:

```powershell
# This isn't needed but is a good security practice to complete
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Force

$reg_winlogon_path = "HKLM:\Software\Microsoft\Windows NT\CurrentVersion\Winlogon"
Set-ItemProperty -Path $reg_winlogon_path -Name AutoAdminLogon -Value 0
Remove-ItemProperty -Path $reg_winlogon_path -Name DefaultUserName -ErrorAction SilentlyContinue
Remove-ItemProperty -Path $reg_winlogon_path -Name DefaultPassword -ErrorAction SilentlyContinue
```
The script works by checking to see what programs need to be installed (such as .NET Framework 4.5.2) and what PowerShell version is required. If a reboot is required and the username and password parameters are set, the script will automatically reboot and logon when it comes back up from the reboot. The script will continue until no more actions are required and the PowerShell version matches the target version. If the username and password parameters are not set, the script will prompt the user to manually reboot and logon when required. When the user is next logged in, the script will continue where it left off and the process continues until no more actions are required.

### WinRM Setup
Once Powershell has been upgraded to at least version 3.0, the final step is for the WinRM service to be configured so that Ansible can connect to it. There are two main components of the WinRM service that governs how Ansible can interface with the Windows host: the listener and the service configuration settings.

This script sets up both HTTP and HTTPs listeners with a self-signed cert and enables `Basic` authentication option on the service. 

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$url = "https://github.com/hackedbyagirl/offensive-windows-ansible/blob/main/scripts/ConfigureRemote.ps1"
$file = "$env:temp\ConfigureRemote.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file
```
To view the current listeners that are running on the WinRM service, run the following command:
```powershell
winrm enumerate winrm/config/Listener
```


## Tools to Add
- MSOLSpray
- Rubeus
- Microburst
- RedTeamPowerShellScripts
