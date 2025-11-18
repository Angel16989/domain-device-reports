# ??? Domain Device Reports 
 
![PowerShell](https://img.shields.io/badge/PowerShell-5.1+-blue.svg) ![License](https://img.shields.io/badge/license-MIT-green.svg) ![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg) 
 
> **PowerShell automation scripts for generating Active Directory domain device reports and logging Windows Update status.** 
 
## ?? Overview 
 
This repository contains PowerShell scripts that automate the collection and reporting of: 
 
- Domain-joined computer inventory 
- Windows Update compliance status 
- System information and last logon timestamps 
- Automated CSV report generation with timestamps 
 
Perfect for IT administrators who need regular reports for compliance, auditing, or infrastructure monitoring. 
 
## ? Features 
 
- ? **Automated Domain Device Inventory** - Query all computers in your Active Directory 
- ? **Windows Update Status Tracking** - Monitor update compliance across devices 
- ? **CSV Export** - Reports saved as CSV for easy analysis in Excel/Power BI 
- ? **Timestamped Logging** - Automatic date/time stamping for version control 
- ? **Lightweight** - Pure PowerShell, no additional dependencies 
- ? **Schedulable** - Run via Task Scheduler for automated reporting
 
## ?? Reports Generated 
 
### Domain Devices Report 
 
Captures: Name, DNSHostName, OperatingSystem, OS Version, Last Logon Date 
 
**Example:** `DomainDevices_20251117_184215.csv` 
 
### Windows Update Status Report 
 
Tracks Windows Update compliance and status across your infrastructure. 
 
**Example:** `WindowsUpdateStatus_20251117_191726.csv` 
 
## ?? Prerequisites 
 
- PowerShell 5.1 or higher 
- Active Directory PowerShell Module 
- Domain admin or equivalent permissions 
- Network access to domain controllers 
 
## ?? Usage 
 
1. Clone the repo or download scripts 
2. Run scripts as Administrator 
3. Reports auto-save to `/reports/` directory 
 
### Schedule with Task Scheduler 
 
```powershell 
$action = New-ScheduledTaskAction -Execute 'PowerShell.exe' -Argument '-File "C:\path\to\script.ps1"' 
$trigger = New-ScheduledTaskTrigger -Daily -At 6:00AM 
Register-ScheduledTask -TaskName "Daily Domain Report" -Action $action -Trigger $trigger 
```
 
## ?? Repository Structure 
 
``` 
domain-device-reports/ 
ÃÄÄ reports/              # Auto-generated CSV reports 
³   ÃÄÄ DomainDevices_*.csv 
³   ÀÄÄ WindowsUpdateStatus_*.csv 
ÀÄÄ README.md 
``` 
 
## ?? Author 
 
**Angel16989** 
 
- GitHub: [@Angel16989](https://github.com/Angel16989) 
 
## ?? License 
 
MIT License - Free to use and modify. 
 
---
 
Made for IT Professionals managing Windows Active Directory environments.
