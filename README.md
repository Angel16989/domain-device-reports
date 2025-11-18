# 🖥️ Domain Device Reports

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
  <a href="#-features">Features</a> •
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-reports">Reports</a> •
  <a href="#-usage">Usage</a> •
  <a href="#-troubleshooting">Troubleshooting</a>
</p>

---

## 📋 Table of Contents

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

## 🎯 Overview

**Domain Device Reports** is a lightweight PowerShell automation toolkit designed for IT administrators managing Windows Active Directory environments. Run these scripts from any domain-joined VM or domain controller to remotely gather comprehensive information about all devices on your network—without touching a single workstation.

Perfect for:
- 🏢 **Enterprise IT Teams** - Monitor hundreds of domain devices from a central location
- 🔒 **Security Auditors** - Track OS versions, patch levels, and compliance
- 📊 **Infrastructure Managers** - Generate reports for stakeholders
- ⚡ **Automation Engineers** - Schedule daily/weekly reports via Task Scheduler
- 🎓 **IT Students & Labs** - Learn AD querying and PowerShell automation

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔍 **Remote Discovery** | Query Active Directory for all domain-joined computers from your VM |
| 📊 **Device Inventory** | Collect OS versions, hostnames, DNS names, and last logon timestamps |
| 🔄 **Windows Update Tracking** | Monitor update compliance and pending updates across all devices |
| 📁 **CSV Export** | Auto-generate timestamped CSV files ready for Excel, Power BI, or SIEM tools |
| ⏰ **Automated Scheduling** | Set up with Windows Task Scheduler for hands-free daily/weekly reports |
| 🚀 **Zero Installation** | Pure PowerShell - no external dependencies or databases required |
| 🛡️ **Read-Only Operations** | Safe queries that don't modify AD or devices - perfect for auditing |
| 📈 **Scalable** | Efficiently handles domains with 10 to 10,000+ devices |
| 🔐 **Secure** | Uses your existing AD credentials and permissions |

---

## 📦 What's Inside

```plaintext
domain-device-reports/
├── 📄 Get-DomainDevices.ps1          # Main inventory script
├── 📄 Get-WindowsUpdateStatus.ps1    # Update compliance checker
├── 📁 reports/                        # Auto-generated CSV reports
│   ├── DomainDevices_YYYYMMDD_HHMMSS.csv
│   └── WindowsUpdateStatus_YYYYMMDD_HHMMSS.csv
├── 📄 [README.md](http://_vscodecontentref_/1)                       # This file
└── 📄 .gitignore                      # Keeps reports folder clean

🚀 Quick Start
Prerequisites
Before running these scripts, ensure you have:

✅ Windows Server 2016+ or Windows 10/11 (domain-joined)
✅ PowerShell 5.1+ (pre-installed on modern Windows)
✅ Active Directory PowerShell Module (RSAT-AD-PowerShell)
✅ Domain Admin or delegated AD read permissions
✅ Network connectivity to domain controllers
Installation
1. Install Active Directory Module (if not already installed):

2. Clone or Download This Repository:

3. Run Your First Report:

🎉 That's it! Check the reports/ folder for your generated CSV file.

📊 Reports Generated
1️⃣ Domain Devices Inventory
File: DomainDevices_YYYYMMDD_HHMMSS.csv

Comprehensive inventory of all domain-joined computers:

Column	Description	Example
Name	Computer NetBIOS name	SRV-DC01
DNSHostName	Fully qualified domain name	SRV-DC01.Homelab.local
OperatingSystem	OS name & edition	Windows Server 2022 Standard
OperatingSystemVersion	Build number	10.0 (20348)
lastLogonDate	Last domain authentication	17/11/2025 6:11:36 PM
Enabled	Account status	True / False
DistinguishedName	Full AD path	CN=SRV-DC01,OU=Servers,DC=Homelab,DC=local
Use Cases:

📋 Asset inventory for compliance audits
🔍 Identify inactive or stale computer accounts
📊 Track OS distribution across your network
🕐 Find devices that haven't logged on recently
2️⃣ Windows Update Status
File: WindowsUpdateStatus_YYYYMMDD_HHMMSS.csv

Tracks Windows Update compliance and patch status:

Column	Description
ComputerName	Device hostname
UpdatesAvailable	Number of pending updates
CriticalUpdates	Security patches waiting
LastUpdateCheck	When device checked WSUS/Windows Update
RebootPending	Whether restart is required
AutoUpdateEnabled	Update configuration status
Use Cases:

🔒 Security compliance reporting
⚠️ Identify vulnerable systems missing patches
📅 Plan maintenance windows
🎯 Track patch deployment success rates
💻 Usage
Basic Usage
Generate Domain Devices Report:

Check Windows Update Status:

Specify Custom Output Path:

Advanced Examples
Filter by Specific OU:

Find Stale Computer Accounts (no logon in 90+ days):

Get Computers by Operating System:

⚙️ Automation
Schedule with Task Scheduler
Set up automated daily/weekly reports:

Weekly Cleanup Script
Automatically archive old reports:

🛠️ Troubleshooting
Solution: Install RSAT Active Directory tools:

Solutions:

Run PowerShell as Administrator
Ensure your account has domain read permissions
Verify you're logged in with domain credentials</details>
Solution: Enable WinRM on target devices:

Optimization tips:

Query only specific OUs instead of entire domain
Limit properties retrieved with -Properties parameter
Run during off-peak hours
Filter results at query time instead of after retrieval</details>
🔒 Security Considerations
✅ Read-Only: Scripts only query AD; they don't modify anything
✅ Credential Safety: Uses your existing Windows authentication
✅ Audit Trail: All queries are logged in domain controller security logs
⚠️ Permissions: Requires domain read access—follow principle of least privilege
⚠️ Report Storage: CSV files may contain sensitive info—store securely
🔐 Best Practice: Run from secure, domain-joined VM, not personal workstation
🤝 Contributing
Contributions are welcome! Whether it's:

🐛 Bug reports
💡 Feature requests
📝 Documentation improvements
🔧 Code contributions
To contribute:

Fork the repository
Create a feature branch: git checkout -b feature/AmazingFeature
Commit your changes: git commit -m 'Add AmazingFeature'
Push to the branch: git push origin feature/AmazingFeature
Open a Pull Request
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

💬 Support
Need help? Have questions?

📖 Documentation: You're reading it!
🐛 Issues: GitHub Issues
💡 Discussions: GitHub Discussions
📧 Contact: Open an issue or reach out via GitHub
👤 Author
Angel16989

🐙 GitHub: @Angel16989
💼 Focus: IT Automation, Active Directory, PowerShell Scripting
🌟 Acknowledgments
Built with ❤️ for IT professionals managing Active Directory environments
Inspired by real-world needs in enterprise infrastructure management
Special thanks to the PowerShell and sysadmin communities


