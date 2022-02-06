# Hosts
- 1 Windows Domain Controller
  - Windows Server 2019
    - dc01
- 4 Windows Servers
  - Windows Server 2019
    - win2019-1
  - Windows Server 2019 with Active Directory Certificate Services + Web Enrollment + Web Service for Petit Potam
    - win2019-adcs
  - Windows Server 2022
    - win2022-1
  - Windows Server 2008 - Metasploitable3
    - metasploitable-win2k8
- 4 Windows Workstations
  - Win10 (`StefanScherer/windows_10` Vagrant box, used because it supports both virtualbox & vmware_desktop)
    - win10-1
    - win10-2
    - win10-dev
      - Win10 Development Environment (Customized via Chocolatey)
  - Win7
    - win7-1
- 1 Kali Box (Customized)
  - kali
- 1 Ubuntu Server
  - Ubuntu Server 14.04 - Metasploitable3
    - metasploitable-ub1404

## Alternative Vagrant boxes
* Windows 10
  * Enterprise SAC
    * [gusztavvargadr/windows-10](https://app.vagrantup.com/gusztavvargadr/boxes/windows-10) 
    * Has extra stuff
      * [gusztavvargadr/windows-10-enterprise](https://app.vagrantup.com/gusztavvargadr/boxes/windows-10-enterprise)
  * With Visual Studio + Docker
    * [gusztavvargadr/visual-studio](https://app.vagrantup.com/gusztavvargadr/boxes/visual-studio)
* Windows Server 2019
  * Standard LTSC
    * [gusztavvargadr/windows-server-standard](https://app.vagrantup.com/gusztavvargadr/boxes/windows-server)
  * SQL Server
    * [gusztavvargadr/sql-server](https://app.vagrantup.com/gusztavvargadr/boxes/sql-server)
  * IIS
    * [gusztavvargadr/iis](https://app.vagrantup.com/gusztavvargadr/boxes/iis)
