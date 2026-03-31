**OSS Audit — Linux Kernel** 

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Student: Aryan Saxena
Roll Number: 24BAC10040
Course: Open Source Software — CSE0002
Chosen Software: Linux Kernel (Operating System Core)
License: GNU General Public License v2 (GPL v2)
Repository: https://github.com/Dev-Aryan-Saxena/NGMC-OSS-Project.git

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

📖 About This Project
This repository contains the capstone audit of the Linux Kernel, the most significant collaborative project in software history. Conducted as part of the Open Source Software (OSS NGMC) course, this audit examines the kernel's transition from a 1991 hobby project to global infrastructure.
The project includes a deep-dive analysis into the GPL v2 "Copyleft" licensing model and its technical footprint on modern Linux systems. To complement the written report, I have developed five original shell scripts that demonstrate practical Linux auditing, subsystem inspection, and shell scripting proficiency.



🐧 **Chosen Software : The Linux Kernel**
The Linux Kernel was created by Linus Torvalds in 1991. Unlike proprietary kernels (Windows NT), Linux is a monolithic but modular system. Its success is rooted in its license; by choosing the GPL v2, Torvalds ensured that every improvement made by global corporations must be shared back with the community. This audit explores how this "social contract" powers the modern world.


🛠️ **Setup & Configuration**

**1. Environment Setup**
The project is designed for Linux environments (Ubuntu, Debian, CentOS, RHEL, Fedora). The scripts are designed to be "Hardware Agnostic," meaning they audit the kernel logic rather than specific hardware serials, ensuring user privacy.

**2. Dependency Check**

Ensure your system has standard coreutils and kernel tools installed.
- Ubuntu / Debian: sudo apt update && sudo apt install kmod coreutils -y
- RHEL / Fedora: sudo dnf install kmod coreutils -y


**3. Execution Instructions**

# Clone the repository
git clone https://github.com/Dev-Aryan-Saxena/NGMC-OSS-Project.git
cd Shell-Scripts

# Make all scripts executable
chmod +x *.sh

# Run the scripts
./[script_name].sh



📁 **Repository Structure**

NGMC-OSS-Project/
├── README.md                                         ← Project documentation 
├── OSS-Report.md                                     ← Project report 
├──Shell-Scripts-Screenshots/                         ←O/P Screenshots
     ├──DiskAndPermissionAuditor.jpg
     ├──FossPackageInspector.jpg
     ├──LogFileAnalyser.jpg
     ├──SystemIdentityReport.jpg
     ├──TheOpenSourceManifestoGenerator.jpg
└── Shell-Scripts/
    ├── diskAndPermmisssionAuditor.sh                ← Disk and Permission Auditor
    ├── fossPackageInspector.sh                      ← FOSS Package Inspector
    ├── logFileAnalyser.sh                           ← Log File Analyzer
    ├── systemIdentityReport.sh                      ← System Identity Report
    └── theOpenSourceManifestoGenerator.sh           ← Open Source Manifesto Generator



📜 **Script Descriptions**

**Script 1: System Identity Report**
**File**: systemIdentityReport.sh
**Description**: Displays a formatted welcome screen with distribution details, kernel version, and the GPL v2 license notice.
**Concepts**: Variables, Command Substitution $(), and echo.


**Script 2: Kernel Component Inspector**
**File**: fossPackageInspector.sh
**Description**: Audits the presence of the linux-image package and supporting FOSS tools (GCC, LibC). Uses a case statement to describe the purpose of each subsystem.
**Concepts**: if-else, case statements, and dpkg/rpm queries.

**Script 3: Disk & Permission Auditor**
**File**: diskAndPermissionAuditor.sh
**Description**: Loops through critical kernel directories (/boot, /lib/modules) to report permissions, ownership, and disk usage.
**Concepts**: for loops, du, ls -ld, and awk.

**Script 4: Kernel Log Analyzer**
**File**: logFileAnalyzer.sh
**Description**: Interrogates the kernel ring buffer (dmesg) for specific technical flags or errors and provides a frequency count.
**Concepts**: while read loops, input redirection, and arithmetic expansion.

**Script 5: Open Source Manifesto Generator**
**File**: theOpenSourceManifestoGenerator.sh
**Description**: An interactive tool that collects user input on FOSS values and generates a persistent .txt manifesto file.
**Concepts**: read -p, string concatenation, and file writing with > and >>.

🛡️ **Security & Privacy Note**
- No Hardcoded Data: These scripts use environment variables like $USER and $HOME to ensure no personal paths are leaked.
- Non-Invasive: Script 4 uses a local temporary file for log analysis to avoid requiring sudo or accessing sensitive system logs.
- Portable: Designed to run safely on any standard Linux distribution without exposing hardware UUIDs or MAC addresses.

⚖️ **License**
This project is submitted as coursework for the OSS NGMC course. The shell scripts and report are original works for academic evaluation.
