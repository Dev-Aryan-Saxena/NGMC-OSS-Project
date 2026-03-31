# The Open Source Audit

## A Capstone Project for OSS NGMC Course

**Student Name:** Aryan Saxena

**Registration Number:** 24BAC10040

**Chosen Software:** Linux Kernel (Operating System Core)

**License Audited:** GNU General Public License v2 (GPL v2)

**Date of Submission:** 31/03/2026

**Course:** Open Source Software — CSE0002

---

## Table of Contents

```
Introduction ............................................................................................   3

Part A — Origin and Philosophy ..........................................................   4
A1. The Spark: From Hobby to Global Infrastructure .......................   4
A2. The License — The "GPL-2.0 Only" Mandate ...........................   6
A3. The Ethics of the Kernel ..............................................................   7

Part B — Kernel Footprint ...................................................................   8

Part C — The FOSS Ecosystem ............................................................  9

Part D — Open Source vs Proprietary ................................................. 10
Comparison Table ............................................................................... 10
Deployment Verdict ............................................................................ 11

Part E — Shell Script Documentation .................................................. 12
Script 1: System Identity & Kernel Report ......................................... 12
Script 2: Kernel Module Inspector ...................................................... 15
Script 3: Boot Parameter & Permission Auditor ................................. 19
Script 4: Kernel Log Analyzer ………................................................ 23
Script 5: Open Source Manifesto Generator ....................................... 26

Conclusion ............................................................................................... 29

References ................................................................................................ 29
```

---

## Introduction

The Open Source Audit is a comprehensive exploration of how free and open-source software (FOSS) functions in the real world, both technically and philosophically. While many projects focus on user-facing applications, this audit targets the very foundation of modern computing: the Linux Kernel. The purpose of this project is to move beyond the abstract definition of "open source" and instead perform a deep-dive into the software that powers everything from Android smartphones and SpaceX rockets to the world's fastest supercomputers.

I chose the Linux Kernel as the subject of this audit because it is the ultimate testament to the scalability of the open-source model. It is perhaps the most complex collaborative project in human history, involving thousands of developers from competing corporations (Intel, AMD, Google, Red Hat) working together on a single shared resource. By auditing the kernel, I aim to understand how the GPL v2 license acts as a "peace treaty" that allows these rivals to collaborate, and how the technical architecture of a monolithic kernel manages to remain modular and secure.

This report is structured to mirror the dual nature of open source. We begin with the historical and philosophical origins of Linux (Part A), examining Linus Torvalds’ 1991 announcement and the critical choice of the GPL v2 license. We then move into the technical reality of how the kernel lives on a machine (Part B), specifically focusing on the /proc and /sys interfaces. Part C explores the massive ecosystem of distributions and the GNU/Linux relationship, followed by a critical comparison against proprietary kernels like Windows NT (Part D). Finally, Part E documents a suite of five custom shell scripts designed to audit kernel modules, boot parameters, and security logs.

On a personal level, this project is a milestone in my journey as a computer science student. Understanding the kernel is not just a technical requirement; it is an initiation into the "social contract" of software. Every tool I use sits atop the kernel's syscalls. By auditing Linux, I am learning that the most powerful software on Earth is not owned by a billionaire or a corporation, but is a common heritage that I have the right to study, modify, and improve.

---

## Part A — Origin and Philosophy

### A1 — The Spark: From Hobby to Global Infrastructure

In August 1991, a 21-year-old student at the University of Helsinki named Linus Torvalds posted a message to the Comp.os.minix newsgroup. He famously stated he was working on a free operating system, "just a hobby, won't be big and professional like gnu." At the time, the world was dominated by expensive, proprietary Unix systems or the limited, academic Minix. Torvalds wanted something that ran on his new 80386 PC.

The early 90s were a time of "Unix Wars"; fragmented, expensive versions of Unix like Solaris and HP-UX were fighting for dominance. Meanwhile, the Free Software Foundation’s own kernel, the GNU Hurd, was suffering from "second-system effect," struggling with an overly complex microkernel architecture. Into this vacuum stepped Linux. Torvalds chose a monolithic architecture, a design where all OS services run in the same address space as the core kernel. While technically "old-fashioned" according to computer science professors like Andrew Tanenbaum, it was practical, fast, and it worked.

The true genius of the Linux Kernel's origin wasn't just the code; it was the decision to use the internet for collaborative development. Torvalds didn't wait for a "1.0" release to show the world. He released early and often, inviting strangers to find bugs and suggest features. This shattered the "Cathedral" model of software development (where a small group works in secret) and birthed the "Bazaar" model, where a sprawling community co-creates the product.

What I find most remarkable is the resilience shown during the 1992 "Tanenbaum–Torvalds debate." Tanenbaum argued that Linux was obsolete because it wasn't a microkernel. Torvalds defended his pragmatic approach, arguing that performance and hardware accessibility mattered more than academic purity. History has vindicated Torvalds; the monolithic-but-modular design of Linux allowed it to adapt to every hardware architecture imaginable, from tiny embedded sensors to the massive IBM Z-series mainframes.

The evolution from a "hobby" to the backbone of the internet happened because Linux became a "commons." When the internet boom of the late 90s hit, companies like IBM realized it was cheaper to contribute to a shared kernel than to maintain their own proprietary Unix versions. This "co-opetition" is the engine of Linux. Today, over 80% of kernel contributions come from developers paid by corporations, yet the kernel remains free from corporate capture because of the legal "moat" created by its license.

---

### A2 — The License: The "GPL-2.0 Only" Mandate

The Linux Kernel is released under the GNU General Public License version 2 (GPL v2). Linus Torvalds has frequently called the choice of the GPL v2 the "best thing I ever did." To understand why, we must look at how it differs from other licenses.

GPL v2 is a "copyleft" license. It is built on four fundamental freedoms:

* Freedom 0: The freedom to run the kernel for any purpose.
* Freedom 1: The freedom to study how the kernel works (source code access).
* Freedom 2: The freedom to redistribute copies.
* Freedom 3: The freedom to distribute modified versions.

The "catch" of the GPL v2 and its greatest strength is the requirement that if you distribute a modified version of the kernel, you must also provide the source code under the same GPL v2 license. This prevents "tivoization" (in version 3) and proprietary forking. You cannot take the Linux Kernel, add a secret feature, and sell it as a closed-source product.

Crucially, Linux is licensed as "GPL-2.0 only," not "GPL-2.0 or later." This was a deliberate choice by the kernel community to avoid the more restrictive terms of the GPL v3. The GPL v2 is focused on the code itself; it ensures that the improvements made by a company like Intel flow back into the main tree so that everyone, including Intel’s competitors, can benefit from them.

In my audit, I researched the "Binary Blob" controversy. While the kernel source is GPL v2, many hardware drivers require "firmware blobs" compiled code that isn't open. The kernel community allows these to be loaded into the kernel to ensure hardware compatibility, though purists (like the FSF) maintain a "Linux-libre" version that strips these out. This highlights the pragmatic philosophy of Linux: it prioritizes the user's ability to actually use their hardware over absolute ideological purity.

---

### A3 — The Ethics of the Kernel

The ethics of the Linux Kernel revolve around the concept of "Digital Sovereignty." In a world where Microsoft or Apple can remotely disable features or change the terms of service of an OS, Linux provides an exit. Because the kernel is open, no single entity can "kill" it. If the current maintainers disappeared, the community could simply fork it and continue.

Is it ethical for multi-billion dollar companies to profit from a kernel maintained by thousands? The answer lies in the "Reciprocity Principle." When Google uses Linux for Android, they are not just "taking." They contribute massive amounts of code back to the memory management and networking subsystems. This creates a "Virtuous Cycle": the more a company uses Linux, the more incentive they have to make it better, which in turn makes it better for everyone else.

However, the "Many Eyes" theory (the idea that open source is inherently more secure because anyone can audit it) has been challenged by incidents like the Heartbleed bug (though that was in OpenSSL, not the kernel). It taught us that "many eyes" only work if people are actually looking. This led to the creation of the Core Infrastructure Initiative, where companies now fund full-time security audits for the kernel. The ethics of Linux have evolved from "it's free" to "it's our collective responsibility to keep it secure."

---

## Part B — Kernel Footprint

Linux on a Linux System: The Anatomy of a Booted Kernel

When I audit the kernel on my Ubuntu system, I am not looking for a single file, but a living process. The kernel itself lives as a compressed file in the /boot directory, usually named something like vmlinuz-6.5.0-generic. This is the file the bootloader (GRUB) loads into RAM at startup.

However, the "footprint" of the kernel is best seen through its interfaces:

* `/proc Filesystem`: This is a "virtual" filesystem. It doesn't exist on disk; it's a window into the kernel's brain. For example, `cat /proc/meminfo` doesn't read a file; it asks the kernel for a real-time report on RAM.
* `/sys (sysfs)`: This provides information about the hardware devices recognized by the kernel.
* `/lib/modules`: This directory contains the Kernel Modules (.ko files). Modern kernels use a modular architecture, meaning they can load and unload drivers (like for a USB webcam) on the fly without rebooting.

During my audit, I used `lsmod` to see which modules were currently active. I found that even a simple laptop has over 100 modules loaded, handling everything from the touchpad to encrypted file systems. This modularity is what makes Linux so versatile a single kernel image can boot on a desktop, but only load the modules needed for a server if deployed there.

The security of the kernel footprint is managed by the "Ring 0" privilege level. The kernel has total control over the CPU and memory, while user applications (like Chrome or VS Code) run in "Ring 3." The only way an application can talk to the hardware is through "Syscalls" (System Calls). My audit identified that there are roughly 350-400 syscalls in a modern kernel, acting as the strictly guarded gates to the hardware.

---

## Part C — The FOSS Ecosystem

The Core of the Universe

The Linux Kernel is the heart of the "GNU/Linux" ecosystem. It's important to clarify that "Linux" is just the kernel it needs the GNU C Library (glibc), the GNU Compiler Collection (GCC), and a set of "Coreutils" (like ls, cp, and mv) to be a functional operating system.

The ecosystem is organized into "Distributions" (Distros):

* Debian/Ubuntu: Focus on stability and ease of use.
* RHEL/Fedora: Focus on enterprise-grade security and "bleeding edge" features.
* Arch Linux: Focus on "The Arch Way" simplicity and total user control.
* Android: A specialized Linux distribution that replaced the GNU tools with a custom Java-based environment (Dalvik/ART).

The governance of the kernel is headed by the "Benevolent Dictator for Life" (BDFL), Linus Torvalds, though he took a break in 2018 to improve his "empathy and conduct." Day-to-day work is handled by "Subsystem Maintainers" trusted experts who manage specific parts like the Network stack or the USB subsystem. This hierarchy ensures that despite the chaos of thousands of contributors, the code remains high-quality.

---

## Part D — Open Source vs Proprietary

### Linux vs. Windows NT (Proprietary)

| Dimension    | Linux Kernel (Open Source)                | Windows NT Kernel (Proprietary)                |
| ------------ | ----------------------------------------- | ---------------------------------------------- |
| Cost         | Free (GPL v2).                            | Licensed as part of Windows OS.                |
| Transparency | Full source code available for audit.     | "Black box" source code is a trade secret.     |
| Modification | Anyone can patch and recompile.           | Only Microsoft can modify it.                  |
| Architecture | Monolithic (Modular).                     | Hybrid Microkernel.                            |
| Security     | Transparent CVE tracking/community fixes. | "Security through obscurity" / Vendor updates. |
| Verdict      | Best for transparency, servers, and IoT.  | Dominant in consumer desktop due to legacy.    |

---

### Verdict: Would I Recommend Linux?

Yes. For any infrastructure where security and long-term viability are priorities, Linux is the only choice. Proprietary kernels suffer from "Planned Obsolescence" once a vendor stops supporting an OS version, the kernel becomes a security liability. With Linux, as long as there is one person interested in the code, it can be patched. Also , it gives the user absolute freedom over the OS where as windows and mac restricts it , we can even delete the OS and linux kernel won’t mind it - in one way or another - it can be said that - “It’s your OS, you can do whatever you want with it , we don’t care, play with it , break it, modify it, contribute and if we like it we will introduce it as a new feature.”

---

## Part E — Shell Script Documentation

### Script 1 — System Identity

**Purpose:** Displays kernel version, architecture, and current student metadata.

```bash
#!/bin/bash
# =============================================================
# Script 1  : System Identity Report
# Author    : Aryan Saxena (24BAC1040)
# Course    : Open Source Software — CSE0002
# Software  : Linux Kernel (chosen for OSS Audit)
# Purpose   : Displays a system identity report as a formatted
#             welcome screen using dynamic environment data.
# Date      : 31 March 2026
# =============================================================

# --- VARIABLES ---
# Project metadata
STUDENT_NAME="Aryan Saxena"
REG_NUMBER="24BAC10040"
AUDIT_TOPIC="Linux Kernel"

# --- COMMAND SUBSTITUTION ---
# We use standard commands so the script adapts to any machine it runs on.
KERNEL_VER=$(uname -r)
CURRENT_USER=$(whoami)
USER_HOME=$HOME
# 'uptime -p' shows duration without revealing boot timestamps or load averages
SYS_UPTIME=$(uptime -p)
CURRENT_DT=$(date '+%A, %d %B %Y, %T')

# Safely identifying the Distribution without exposing unique system IDs
if [ -f /etc/os-release ]; then
    DISTRO=$(grep '^PRETTY_NAME' /etc/os-release | cut -d '=' -f2 | tr -d '"')
else
    DISTRO="Linux System"
fi

# --- DISPLAY OUTPUT ---
echo "================================================================"
echo "           OPEN SOURCE AUDIT: SYSTEM IDENTITY REPORT            "
echo "================================================================"
echo ""
echo "  [STUDENT INFORMATION]"
echo "  Name          : $STUDENT_NAME"
echo "  Registration  : $REG_NUMBER"
echo "  Software Audit: $AUDIT_TOPIC"
echo ""
echo "  [SYSTEM ENVIRONMENT]"
echo "  Distribution  : $DISTRO"
echo "  Kernel Version: $KERNEL_VER"
echo "  Logged User   : $CURRENT_USER"
echo "  Home Path     : $USER_HOME"
echo "  System Uptime : $SYS_UPTIME"
echo "  Date & Time   : $CURRENT_DT"
echo ""
echo "  [FOSS COMPLIANCE NOTICE]"
echo "  This system is powered by the Linux Kernel, which is"
echo "  distributed under the GNU General Public License v2 (GPLv2)."
echo "  This license ensures that the source code remains open,"
echo "  auditable, and free for all users to modify and redistribute."
echo ""
echo "================================================================"
echo "                END OF SYSTEM IDENTITY REPORT                   "
echo "================================================================"
```

---

### Script 2 — Kernel Module Inspector

**Purpose:** Audits loaded modules and identifies specific drivers.

```bash
#!/bin/bash
# =============================================================
# Script 2  : FOSS Package & Component Inspector
# Author    : Aryan Saxena (24BAC10040)
# Course    : Open Source Software — CSE0002
# Software  : Linux Kernel (chosen for OSS Audit)
# Purpose   : Checks for kernel-related packages, retrieves 
#             versions, and uses a case statement for descriptions.
# Concepts  : Case Statements, Package Management, If-Else
# Date      : 31 March 2026
# =============================================================

# --- VARIABLES ---
# The primary "package" for a kernel audit is the running image and headers
PRIMARY_PKG="linux-image-$(uname -r)"
SUPPORT_PKGS=("libc6" "gcc" "kmod" "bash")

# --- HEADER ---
echo "================================================================"
echo "           FOSS COMPONENT & PACKAGE INSPECTOR                   "
echo "================================================================"
echo ""

# --- UNIT 2 CONCEPT: PACKAGE CHECKING ---
# We check if the kernel image package is registered in the OS database
echo "  [PRIMARY COMPONENT CHECK]"
if dpkg -s "$PRIMARY_PKG" > /dev/null 2>&1; then
    # If installed, extract the version string
    VERSION=$(dpkg-query -W -f='${Version}' "$PRIMARY_PKG")
    echo "  Component : $PRIMARY_PKG"
    echo "  Status    : INSTALLED"
    echo "  Version   : $VERSION"
else
    # Fallback for non-Debian systems or manual builds
    echo "  Component : $PRIMARY_PKG"
    echo "  Status    : ACTIVE (Detected via System Runtime)"
    echo "  Version   : $(uname -v | awk '{print $1}')"
fi
echo ""

# --- UNIT 2 CONCEPT: CASE STATEMENT ---
# Using a case statement to provide descriptions based on the component name
echo "  [ECHO SYSTEM COMPONENT DESCRIPTIONS]"
echo "  --------------------------------------------------------------"

# Adding the primary package to the list for the description loop
for PKG in "$PRIMARY_PKG" "${SUPPORT_PKGS[@]}"; do
    
    # The Case statement matches the package name to its FOSS purpose
    case "$PKG" in
        linux-image*)
            DESC="The core binary of the Linux Kernel; handles CPU and RAM."
            ;;
        libc6)
            DESC="The GNU C Library; the essential interface between kernel and apps."
            ;;
        gcc)
            DESC="The GNU Compiler Collection; used to build the kernel from source."
            ;;
        kmod)
            DESC="Tools for loading and unloading modular kernel drivers."
            ;;
        bash)
            DESC="The Bourne Again SHell; the standard FOSS command interpreter."
            ;;
        *)
            DESC="An essential open-source component of the Linux ecosystem."
            ;;
    esac

    # Display the result in a clean format
    printf "  %-20s | %s\n" "$PKG" "$DESC"
done

# --- PHILOSOPHICAL NOTE ---
echo ""
echo "  [AUDITOR'S OBSERVATION]"
echo "  Unlike proprietary systems, where the 'kernel' is a hidden"
echo "  monolith, Linux allows us to inspect each supporting"
echo "  package (like GCC or LibC) that was used to bring the"
echo "  system to life. This transparency is the core of FOSS."
echo ""
echo "================================================================"
echo "                END OF COMPONENT INSPECTOR                      "
echo "================================================================"
```

---

### Script 3 — Boot Parameter & Permission Auditor

**Purpose:** Checks /proc/cmdline for boot flags and verifies permissions of the kernel image.

```bash
#!/bin/bash
# =============================================================
# Script 3  : Disk and Permission Auditor
# Author    : Aryan Saxena (24BAC10040)
# Course    : Open Source Software — CSE0002
# Software  : Linux Kernel (chosen for OSS Audit)
# Purpose   : Audits disk usage, ownership, and permissions of 
#             critical kernel and system directories.
# Concepts  : For Loops, File Test Operators, Text Formatting
# Date      : 31 March 2026
# =============================================================

# --- VARIABLES ---
# List of critical directories related to the Kernel and OS hierarchy
# We use an array for the loop to iterate through
CHECK_DIRS=("/boot" "/etc" "/bin" "/lib/modules" "/var/log" "/tmp")

# Setting column widths for a clean table output
COL_PATH=18
COL_PERM=12
COL_OWNER=10
COL_SIZE=10

# --- HEADER ---
echo "================================================================"
echo "           DISK AND PERMISSION AUDITOR (KERNEL FOOTPRINT)       "
echo "================================================================"
echo ""

# Print Table Header
printf "%-${COL_PATH}s | %-${COL_PERM}s | %-${COL_OWNER}s | %s\n" \
       "Directory" "Permissions" "Owner" "Disk Usage"
echo "----------------------------------------------------------------"

# --- UNIT 2 CONCEPT: FOR LOOP ---
# Iterating through the list of system directories
for DIR in "${CHECK_DIRS[@]}"; do

    # Check if the directory exists using the -d test operator
    if [ -d "$DIR" ]; then
        
        # 1. Extract Permissions (e.g., drwxr-xr-x)
        # Using 'ls -ld' and 'awk' to pull the first field
        PERMS=$(ls -ld "$DIR" | awk '{print $1}')

        # 2. Extract Owner
        # Using 'awk' to pull the third field (username)
        OWNER=$(ls -ld "$DIR" | awk '{print $3}')

        # 3. Calculate Disk Usage
        # 'du -sh' gives human-readable size. 
        # 2>/dev/null hides 'Permission Denied' errors to keep output clean/secure.
        SIZE=$(du -sh "$DIR" 2>/dev/null | awk '{print $1}')
        
        # If SIZE is empty (due to high security), set a fallback
        SIZE=${SIZE:-"Locked"}

        # Print the formatted row
        printf "%-${COL_PATH}s | %-${COL_PERM}s | %-${COL_OWNER}s | %s\n" \
               "$DIR" "$PERMS" "$OWNER" "$SIZE"
    else
        # If the directory doesn't exist on this specific flavor of Linux
        printf "%-${COL_PATH}s | %s\n" "$DIR" "Directory Not Found"
    fi
done

# --- SECURITY NOTE ---
echo ""
echo "  [AUDITOR'S SECURITY SUMMARY]"
echo "  The /boot directory contains the compressed kernel image."
echo "  The /lib/modules directory contains the kernel drivers."
echo "  The /var/log directory tracks kernel events via 'dmesg'."
echo ""
echo "  Auditing permissions ensures that critical system files"
echo "  remain 'root' owned to prevent unauthorized modification."
echo "================================================================"
echo "                END OF DISK AND PERMISSION AUDIT                "
echo "================================================================"
```

---

### Script 4 — Kernel Log (dmesg) Analyzer

**Purpose:** Scans the kernel ring buffer for hardware warnings or errors.

```bash
#!/bin/bash
# =============================================================
# Script 4  : Kernel Log (dmesg) Analyzer
# Author    : Aryan Saxena (24BAC10040)
# Course    : Open Source Software — CSE0002
# Software  : Linux Kernel (chosen for OSS Audit)
# Purpose   : Analyzes the kernel ring buffer for specific 
#             keywords (ERROR/WARN) to audit system stability.
# Concepts  : While-Read Loops, If-Then, Counters, Redirection
# Date      : 31 March 2026
# =============================================================

# --- VARIABLES ---
# To keep this secure and portable, we create a temporary local log file
# of the current kernel messages instead of accessing sensitive root logs.
TEMP_LOG="kernel_audit_temp.log"
dmesg | tail -n 100 > "$TEMP_LOG"

# Keyword to search for (Unit 5 Concept: Search/Grep logic)
KEYWORD="EXT4-fs"  # Common kernel flag; you can change this to "ERROR" or "WARN"
COUNT=0

# --- HEADER ---
echo "================================================================"
echo "           KERNEL LOG FILE ANALYZER (DMESG AUDIT)               "
echo "================================================================"
echo ""
echo "  Target Keyword : $KEYWORD"
echo "  Analyzing the last 100 kernel messages..."
echo "  --------------------------------------------------------------"

# --- UNIT 2 & 5 CONCEPT: WHILE-READ LOOP ---
# Reading the file line-by-line while preserving formatting
while IFS= read -r LINE; do

    # --- UNIT 2 CONCEPT: IF-THEN ---
    # Check if the line contains the keyword (case-insensitive)
    if echo "$LINE" | grep -iq "$KEYWORD"; then
        # If match is found, increment the counter (Arithmetic Expansion)
        COUNT=$((COUNT + 1))
        
        # Print the matching line for the audit report (truncated for brevity)
        echo "  [MATCH FOUND]: ${LINE:0:70}..."
    fi

done < "$TEMP_LOG"  # Input redirection (Unit 5)

# --- SUMMARY REPORT ---
echo "  --------------------------------------------------------------"
echo "  [AUDIT SUMMARY]"
echo "  Total occurrences of '$KEYWORD' : $COUNT"
echo ""

# Logic to interpret results for the report
if [ "$COUNT" -eq 0 ]; then
    echo "  Status: STABLE. No critical $KEYWORD flags found in the kernel."
else
    echo "  Status: INVESTIGATE. Found $COUNT instances of $KEYWORD flags."
fi

# Clean up the temporary file (Security Best Practice)
rm -f "$TEMP_LOG"

echo "================================================================"
echo "                END OF KERNEL LOG ANALYSIS                      "
echo "================================================================"

```

---

### Script 5 — Open Source Manifesto Generator

**Purpose:** Interactive script to capture the student's philosophy on Kernel development.

```bash
#!/bin/bash
# =============================================================
# Script 5  : Open Source Manifesto Generator
# Author    : Aryan Saxena (24BAC10040)
# Course    : Open Source Software — CSE0002
# Software  : Linux Kernel (chosen for OSS Audit)
# Purpose   : Interactively collects user values to generate a
#             personalized FOSS philosophy statement (.txt file).
# Concepts  : Interactive Input (read), Strings, File Redirection
# Date      : 31 March 2026
# =============================================================

# --- HEADER ---
echo "================================================================"
echo "           THE OPEN SOURCE MANIFESTO GENERATOR                  "
echo "================================================================"
echo ""
echo "  Welcome. Please answer three questions to generate your"
echo "  personalized Linux Kernel Audit Manifesto."
echo "  --------------------------------------------------------------"

# --- UNIT 5 CONCEPT: INTERACTIVE INPUT ---
# Asking the user for their personal values regarding FOSS
read -p "  1. What is the most important feature of Linux? (e.g. Security): " ATTR
read -p "  2. Why should the Kernel remain Open Source? (e.g. Trust): " REASON
read -p "  3. One word to describe the FOSS community? (e.g. Global): " COMM

# --- STRING CONCATENATION ---
# Composing a short paragraph using the gathered variables
LINE1="As an auditor of the Linux Kernel, I believe its strength lies in its $ATTR."
LINE2="In a world of proprietary walls, the Kernel must stay Open Source to ensure $REASON."
LINE3="Driven by a $COMM community, we ensure that the foundation of computing remains free."

MANIFESTO_TEXT="$LINE1 $LINE2 $LINE3"

# --- FILE PERSISTENCE ---
# Generating a secure filename using the current system user's name
# This ensures no personal name is leaked into the script code itself.
OUT_FILE="manifesto_$(whoami).txt"

# Saving the paragraph to a file (Unit 5: Output Redirection)
echo "----------------------------------------" > "$OUT_FILE"
echo "       MY OPEN SOURCE MANIFESTO        " >> "$OUT_FILE"
echo "----------------------------------------" >> "$OUT_FILE"
echo "$MANIFESTO_TEXT" >> "$OUT_FILE"
echo "" >> "$OUT_FILE"
echo "Generated on: $(date)" >> "$OUT_FILE"
echo "----------------------------------------" >> "$OUT_FILE"

# --- FINAL DISPLAY ---
echo ""
echo "  [SUCCESS]"
echo "  Your manifesto has been composed and saved to: $OUT_FILE"
echo ""
echo "  --- PREVIEW ---"
cat "$OUT_FILE"
echo "  ----------------"
echo ""
echo "================================================================"
echo "                END OF MANIFESTO GENERATOR                      "
echo "================================================================"
```

---

## Conclusion

Auditing the Linux Kernel has been a transformative experience. I started this project seeing the kernel as a piece of "plumbing" something that just stays in the background. I ended it seeing the kernel as a masterpiece of social and technical engineering. The fact that thousands of people who have never met can build something more stable than the world's largest corporations is proof that the FOSS model is not just an alternative; it is the future.

The "GPL v2" is not just a license; it is the engine of this success. By forcing reciprocity, it ensures that no one can "steal" the community's work, which in turn encourages everyone to contribute. As I enter the professional world, I take with me the lesson of the kernel: transparency and collaboration will always outpace secrecy and isolation.

---

## References

1. Torvalds, L. (1991). The "Just a hobby" email. Comp.os.minix.

2. Love, R. (2010). Linux Kernel Development (3rd ed.). Addison-Wesley.

3. Corbet, J., Kroah-Hartman, G., & McPherson, A. (2024). How the Linux Kernel Development Process Works. Linux Foundation.

4. GNU Project. (1991). GNU General Public License v2.0.

5. Tanenbaum, A. S. (1992). "LINUX is obsolete" Debate.

6. The Linux Documentation Project. (2025). The /proc Filesystem Guide.

---
