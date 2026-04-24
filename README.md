# OS Optimisation & Security Hardening – BlackBeard Ltd (Case Study)

## 🛡️ Project Overview

A full Windows 11 Pro virtualisation, optimisation, and security hardening project built inside Oracle VirtualBox. The goal was to simulate a production-ready enterprise endpoint, applying real-world sysadmin and cybersecurity practices from installation through to hardening and benchmarking.

A companion research report was produced comparing DOS, Windows, and Linux across security architecture, memory management, CPU scheduling, and vulnerability exposure — culminating in a strategic OS recommendation.

---

## 🖥️ Environment

| Component | Detail |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Guest OS | Windows 11 Pro (64-bit) |
| vRAM | 128MB – VBoxSVGA |
| RAM Allocated | 9GB |
| CPU Cores | 10 |
| Virtual Storage | 80GB VDI (dynamic) – C:\ |
| Secondary Disk | 30GB NTFS – E:\BackupDrive |

---

## ⚙️ What Was Built

### Installation & VM Configuration
- Clean Windows 11 Pro install via ISO — no upgrade path, no legacy residue
- UK English locale enforced for regional compliance consistency
- Intel NIC driver resolved post-install via VirtualBox shared folder bridge
- Guest Additions installed: full-screen resolution, clipboard sync, drag-and-drop, shared folder support

### User & Access Control
- Two standard user accounts created: `Analyst` and `Auditor`
- Principle of Least Privilege (PoLP) enforced — no admin rights on standard accounts
- Group Policy applied via MMC per-user:
  - Command Prompt disabled
  - Registry Editor disabled
  - Screen inactivity timeout configured

### System Optimisation
- Startup apps disabled: Xbox, Copilot, Teams, OneDrive
- Paging file increased: 2GB → 16GB
- Power mode set to Best Performance
- Visual effects disabled to reduce VM overhead
- Xbox Game Bar removed via PowerShell
- Remote Registry service disabled to cut lateral movement risk
- Disk Cleanup run: temp files, error reports, DirectX cache cleared

### Security Hardening
- Windows Defender fully configured:
  - Real-time protection enabled
  - Cloud-delivered protection enabled
  - Automatic sample submission enabled
  - Tamper protection enabled
  - Controlled Folder Access enabled (ransomware protection)
- System Restore Point created on C:\
- Event log sizes expanded: Application/System 2MB → 32MB, Security 20MB → 32MB (overwrite oldest)
- OpenSSH Server installed and set to auto-start for encrypted remote administration
- Weekly full antivirus scan automated via Task Scheduler (Sundays 4AM)
- Weekly backup configured via Control Panel (Sundays 5PM) — full user data + C:\ system image → E:\BackupDrive
- File History enabled: backup every 6 hours, retention 2 years

### Benchmarking
- WinSAT disk benchmark run pre and post optimisation via PowerShell
- Full WinSAT formal benchmark blocked mid-run by Controlled Folder Access — confirmed correct behaviour; unapproved tools correctly denied hardware metric access

---

## 📊 OS Comparative Research

| Area | DOS | Windows | Linux |
|---|---|---|---|
| Memory | 640KB limit, no virtual memory | Virtual memory, ASLR, paging | Demand-paging, overcommit |
| CPU Scheduling | Cooperative | Preemptive (Round Robin, SJF) | CFS (Completely Fair Scheduler) |
| File System | FAT only | NTFS, FAT32 | EXT4, XFS, Btrfs |
| Security | None | Defender, ASLR, AD, BitLocker | SELinux, AppArmor, iptables |
| Verdict | Decommission/isolate | Recommended for enterprise | Viable with trained staff |

---

## 🔧 Tools & Technologies

`Oracle VirtualBox` `Windows 11 Pro` `PowerShell` `Windows Defender` `Task Scheduler`
`Group Policy (MMC)` `OpenSSH` `WinSAT` `Event Viewer` `File History` `Disk Management`
