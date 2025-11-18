# ??? Domain Device Reports 
 
![PowerShell](https://img.shields.io/badge/PowerShell-5.1+-5391FE?style=for-the-badge&logo=powershell&logoColor=white) ![Windows](https://img.shields.io/badge/Windows-Server-0078D6?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge) ![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge) 
 
<p align="center"> 
  <img src="https://img.icons8.com/fluency/96/000000/server.png" alt="Server Icon" width="100"/> 
</p> 
 
<h3 align="center">Automated Active Directory Domain Monitoring & Reporting</h3> 
 
<p align="center"> 
  Remotely monitor, inventory, and audit all domain-joined devices from your VM or domain controller.<br /> 
  Generate comprehensive CSV reports for compliance, security audits, and infrastructure management. 
</p> 
 
<p align="center"> 
  <a href="#-features">Features</a>  
  <a href="#-quick-start">Quick Start</a>  
  <a href="#-reports">Reports</a>  
  <a href="#-usage">Usage</a>  
  <a href="#-troubleshooting">Troubleshooting</a> 
</p> 
 
---
 
## ?? Table of Contents 
 
- [Overview](#-overview) 
- [Features](#-features) 
- [What's Inside](#-whats-inside) 
- [Quick Start](#-quick-start) 
- [Reports Generated](#-reports-generated) 
- [Installation](#-installation) 
- [Usage](#-usage) 
- [Configuration](#-configuration) 
- [Automation](#-automation) 
- [Advanced Examples](#-advanced-examples) 
- [Troubleshooting](#-troubleshooting) 
- [Security Considerations](#-security-considerations) 
- [Contributing](#-contributing) 
- [License](#-license) 
- [Support](#-support) 
 
---
 
## ?? Overview 
 
**Domain Device Reports** is a lightweight PowerShell automation toolkit designed for IT administrators managing Windows Active Directory environments. Run these scripts from any domain-joined VM or domain controller to remotely gather comprehensive information about all devices on your network-without touching a single workstation. 
 
Perfect for: 
- ?? **Enterprise IT Teams** - Monitor hundreds of domain devices from a central location 
- ?? **Security Auditors** - Track OS versions, patch levels, and compliance 
- ?? **Infrastructure Managers** - Generate reports for stakeholders 
- ? **Automation Engineers** - Schedule daily/weekly reports via Task Scheduler 
- ?? **IT Students & Labs** - Learn AD querying and PowerShell automation
 
---
 
## ? Features 
 
| Feature | Description | 
|------|-------------| 
| ?? **Remote Discovery** | Query Active Directory for all domain-joined computers from your VM | 
| ?? **Device Inventory** | Collect OS versions, hostnames, DNS names, and last logon timestamps | 
| ?? **Windows Update Tracking** | Monitor update compliance and pending updates across all devices | 
| ?? **CSV Export** | Auto-generate timestamped CSV files ready for Excel, Power BI, or SIEM tools | 
| ? **Automated Scheduling** | Set up with Windows Task Scheduler for hands-free daily/weekly reports | 
| ?? **Zero Installation** | Pure PowerShell - no external dependencies or databases required | 
| ??? **Read-Only Operations** | Safe queries that don't modify AD or devices - perfect for auditing | 
| ?? **Scalable** | Efficiently handles domains with 10 to 10,000+ devices | 
| ?? **Secure** | Uses your existing AD credentials and permissions | 
 
---
 
## ?? What's Inside 
 
```plaintext 
domain-device-reports/ 
ÃÄÄ ?? Get-DomainDevices.ps1          # Main inventory script 
ÃÄÄ ?? Get-WindowsUpdateStatus.ps1    # Update compliance checker 
ÃÄÄ ?? reports/                        # Auto-generated CSV reports 
³   ÃÄÄ DomainDevices_YYYYMMDD_HHMMSS.csv 
³   ÀÄÄ WindowsUpdateStatus_YYYYMMDD_HHMMSS.csv 
ÃÄÄ ?? README.md                       # This file 
ÀÄÄ ?? .gitignore                      # Keeps reports folder clean 
``` 
 
---
 
## ?? Quick Start 
 
### Prerequisites 
 
Before running these scripts, ensure you have: 
 
- ? **Windows Server 2016+** or **Windows 10/11** (domain-joined) 
- ? **PowerShell 5.1+** (pre-installed on modern Windows) 
- ? **Active Directory PowerShell Module** (RSAT-AD-PowerShell) 
- ? **Domain Admin or delegated AD read permissions** 
- ? **Network connectivity** to domain controllers
 
### Installation 
 
**1. Install Active Directory Module (if not already installed):** 
 
```powershell 
# On Windows Server 
Install-WindowsFeature RSAT-AD-PowerShell 
 
# On Windows 10/11 
Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0 
``` 
 
**2. Clone or Download This Repository:** 
 
```bash 
git clone https://github.com/Angel16989/domain-device-reports.git 
cd domain-device-reports 
``` 
 
**3. Run Your First Report:** 
 
```powershell 
# Open PowerShell as Administrator 
.\Get-DomainDevices.ps1 
``` 
 
?? **That's it!** Check the `reports/` folder for your generated CSV file. 
 
---
 
## ?? Reports Generated 
 
### 1?? Domain Devices Inventory 
 
**File:** `DomainDevices_YYYYMMDD_HHMMSS.csv` 
 
Comprehensive inventory of all domain-joined computers: 
 
| Column | Description | Example | 
|-----|-----|-----| 
| **Name** | Computer NetBIOS name | `SRV-DC01` | 
| **DNSHostName** | Fully qualified domain name | `SRV-DC01.Homelab.local` | 
| **OperatingSystem** | OS name & edition | `Windows Server 2022 Standard` | 
| **OperatingSystemVersion** | Build number | `10.0 (20348)` | 
| **lastLogonDate** | Last domain authentication | `17/11/2025 6:11:36 PM` | 
| **Enabled** | Account status | `True` / `False` | 
| **DistinguishedName** | Full AD path | `CN=SRV-DC01,OU=Servers,DC=Homelab,DC=local` | 
 
**Use Cases:** 
- ?? Asset inventory for compliance audits 
- ?? Identify inactive or stale computer accounts 
- ?? Track OS distribution across your network 
- ?? Find devices that haven't logged on recently
 
### 2?? Windows Update Status 
 
**File:** `WindowsUpdateStatus_YYYYMMDD_HHMMSS.csv` 
 
Tracks Windows Update compliance and patch status: 
 
| Column | Description | 
|-----|-----| 
| **ComputerName** | Device hostname | 
| **UpdatesAvailable** | Number of pending updates | 
| **CriticalUpdates** | Security patches waiting | 
| **LastUpdateCheck** | When device checked WSUS/Windows Update | 
| **RebootPending** | Whether restart is required | 
| **AutoUpdateEnabled** | Update configuration status | 
 
**Use Cases:** 
- ?? Security compliance reporting 
- ?? Identify vulnerable systems missing patches 
- ?? Plan maintenance windows 
- ?? Track patch deployment success rates 
 
---
 
## ?? Usage 
 
### Basic Usage 
 
**Generate Domain Devices Report:** 
```powershell 
.\Get-DomainDevices.ps1 
``` 
 
**Check Windows Update Status:** 
```powershell 
.\Get-WindowsUpdateStatus.ps1 
``` 
 
**Specify Custom Output Path:** 
```powershell 
.\Get-DomainDevices.ps1 -OutputPath "C:\Reports\domain-report.csv" 
``` 
 
### Advanced Examples 
 
**Filter by Specific OU:** 
```powershell 
Get-ADComputer -Filter * -SearchBase "OU=Workstations,DC=YourDomain,DC=local" | 
    Select-Object Name, OperatingSystem, LastLogonDate | 
    Export-Csv "workstations-only.csv" -NoTypeInformation 
``` 
 
**Find Stale Computer Accounts (no logon in 90+ days):** 
```powershell 
$StaleDate = (Get-Date).AddDays(-90) 
Get-ADComputer -Filter * -Properties LastLogonDate | 
    Where-Object { $_.LastLogonDate -lt $StaleDate } | 
    Export-Csv "stale-computers.csv" -NoTypeInformation 
```
 
**Get Computers by Operating System:** 
```powershell 
Get-ADComputer -Filter {OperatingSystem -like "*Server 2022*"} -Properties OperatingSystem | 
    Select-Object Name, OperatingSystem | 
    Export-Csv "windows-server-2022.csv" -NoTypeInformation 
``` 
 
---
 
## ?? Automation 
 
### Schedule with Task Scheduler 
 
Set up automated daily/weekly reports: 
 
```powershell 
# Create scheduled task for daily domain device report at 6 AM 
$Action = New-ScheduledTaskAction -Execute "powershell.exe" ` 
    -Argument "-NoProfile -ExecutionPolicy Bypass -File `"C:\domain-device-reports\Get-DomainDevices.ps1`"" 
 
$Trigger = New-ScheduledTaskTrigger -Daily -At 6:00AM 
 
$Principal = New-ScheduledTaskPrincipal -UserId "DOMAIN\AdminUser" -RunLevel Highest 
 
Register-ScheduledTask -TaskName "Daily Domain Device Report" ` 
    -Action $Action -Trigger $Trigger -Principal $Principal ` 
    -Description "Generates daily AD computer inventory report" 
```
 
### Weekly Cleanup Script 
 
Automatically archive old reports: 
 
```powershell 
# Keep only last 30 days of reports 
Get-ChildItem -Path "C:\domain-device-reports\reports" -Filter *.csv | 
    Where-Object {$_.LastWriteTime -lt (Get-Date).AddDays(-30)} | 
    Remove-Item -Force 
``` 
 
---
 
## ??? Troubleshooting 
 
<details> 
<summary>? **Error: Module 'ActiveDirectory' not found**</summary> 
 
**Solution:** Install RSAT Active Directory tools: 
 
```powershell 
# Windows Server 
Install-WindowsFeature RSAT-AD-PowerShell 
 
# Windows 10/11 
Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0 
``` 
</details> 
 
<details> 
<summary>? **Error: Access Denied**</summary> 
 
**Solutions:** 
1. Run PowerShell as Administrator 
2. Ensure your account has domain read permissions 
3. Verify you're logged in with domain credentials 
</details>
 
<details> 
<summary>? **Error: Cannot connect to remote devices for Windows Update status**</summary> 
 
**Solution:** Enable WinRM on target devices: 
 
```powershell 
# On each remote device (or via Group Policy): 
Enable-PSRemoting -Force 
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "*" -Force 
``` 
</details> 
 
<details> 
<summary>?? **Slow performance with large domains**</summary> 
 
**Optimization tips:** 
1. Query only specific OUs instead of entire domain 
2. Limit properties retrieved with `-Properties` parameter 
3. Run during off-peak hours 
4. Filter results at query time instead of after retrieval 
</details> 
 
---
 
## ?? Security Considerations 
 
- ? **Read-Only:** Scripts only query AD; they don't modify anything 
- ? **Credential Safety:** Uses your existing Windows authentication 
- ? **Audit Trail:** All queries are logged in domain controller security logs 
- ?? **Permissions:** Requires domain read access-follow principle of least privilege 
- ?? **Report Storage:** CSV files may contain sensitive info-store securely 
- ?? **Best Practice:** Run from secure, domain-joined VM, not personal workstation
 
---
 
## ?? Contributing 
 
Contributions are welcome! Whether it's: 
 
- ?? Bug reports 
- ?? Feature requests 
- ?? Documentation improvements 
- ?? Code contributions 
 
**To contribute:** 
 
1. Fork the repository 
2. Create a feature branch: `git checkout -b feature/AmazingFeature` 
3. Commit your changes: `git commit -m 'Add AmazingFeature'` 
4. Push to the branch: `git push origin feature/AmazingFeature` 
5. Open a Pull Request 
 
---
 
## ?? License 
 
This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details. 
 
```text 
MIT License - Free to use, modify, and distribute. 
No warranty provided. Use at your own risk. 
``` 
 
---
 
## ?? Support 
 
Need help? Have questions? 
 
- ?? **Documentation:** You're reading it! 
- ?? **Issues:** [GitHub Issues](https://github.com/Angel16989/domain-device-reports/issues) 
- ?? **Discussions:** [GitHub Discussions](https://github.com/Angel16989/domain-device-reports/discussions) 
- ?? **Contact:** Open an issue or reach out via GitHub 
 
---
 
## ?? Author 
 
**Angel16989** 
 
- ?? GitHub: [@Angel16989](https://github.com/Angel16989) 
- ?? Focus: IT Automation, Active Directory, PowerShell Scripting 
 
---
 
## ?? Acknowledgments 
 
- Built with ?? for IT professionals managing Active Directory environments 
- Inspired by real-world needs in enterprise infrastructure management 
- Special thanks to the PowerShell and sysadmin communities 
 
---
 
<p align="center"> 
  <strong>? If this project helped you, consider giving it a star!</strong> 
</p> 
 
<p align="center">Made with ?? for IT Professionals</p>
