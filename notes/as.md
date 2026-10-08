---
id: p2yue7ayz2o0mih7i8jmsa6
title: As
desc: ''
updated: 1790958072220
created: 1790958063617
---
UNIX, GNU/Linux & Linux Distributions
1. UNIX

UNIX is a family of operating systems that originated at Bell Labs in the 1970s.

Examples

IBM AIX

HP-UX

Oracle Solaris

UNIX introduced many concepts that are still widely used today:

Processes

Files and directories

Users and permissions

Shells

Pipes

Networking

2. GNU

GNU is a free and open-source software project started by Richard Stallman in 1983.

GNU stands for:

GNU's Not Unix

The GNU project created many important Unix-like tools.

Examples of GNU software
Bash       → Shell
Coreutils  → ls, cp, mv, rm, cat, etc.
GCC        → C/C++ compiler
GDB        → Debugger
grep       → Text searching
sed        → Text processing
awk        → Text processing
make       → Build automation

3. Linux

Linux is a kernel, originally created by Linus Torvalds in 1991.

The kernel manages:

CPU

Memory

Processes

Devices

Networking

Hardware interaction

Linux itself is not a complete operating system.

4. GNU/Linux

A typical GNU/Linux system combines:

Applications
     ↓
GNU tools + other software
     ↓
Linux Kernel
     ↓
Hardware


Therefore:

GNU software + Linux kernel + other components = GNU/Linux system

In everyday usage, people commonly call this simply Linux.

5. Linux Distribution

A Linux distribution (distro) is a complete operating system built around the Linux kernel.

It typically includes:

Linux Kernel
+ GNU utilities
+ Package manager
+ System libraries
+ System services
+ Applications

Popular distributions
Family	Distributions	Package Manager
Debian	Debian, Ubuntu, Linux Mint	apt
Red Hat	RHEL, Fedora, Rocky, AlmaLinux	dnf
Arch	Arch Linux, Manjaro	pacman
SUSE	SLES, openSUSE	zypper
Alpine	Alpine Linux	apk
Gentoo	Gentoo	Portage
6. Important Relationship
                    UNIX
                      │
                Unix philosophy
                      │
              ┌───────┴───────┐
              │               │
          UNIX systems     GNU/Linux
                              │
                         Linux Kernel
                              +
                         GNU tools
                              +
                       Other software
                              │
                 ┌────────────┴────────────┐
                 │                         │
              Debian                    Red Hat
                 │                         │
              Ubuntu                    RHEL
              Mint                     Fedora
                                      Rocky
                                      AlmaLinux


Linux is Unix-like, but Linux is not the original UNIX.

7. UNIX vs GNU/Linux
Feature	UNIX	GNU/Linux
Origin	Bell Labs	Linux: Linus Torvalds; GNU: GNU Project
Kernel	Unix/Unix-derived	Linux kernel
Source	Often proprietary historically	Primarily open source
Examples	AIX, HP-UX, Solaris	Ubuntu, Debian, RHEL
Common use	Enterprise/legacy systems	Servers, cloud, DevOps, desktops
8. For DevOps

You don't need to learn every Linux distribution.

Focus on:

First: Ubuntu/Debian
apt update
apt install nginx

Then: RHEL family
dnf install nginx


Learn these Linux fundamentals:

1. Files & directories
2. Users & groups
3. Permissions
4. Processes
5. Services/systemd
6. SSH
7. Networking
8. Disk & storage
9. Logs
10. Package management
11. Bash scripting


Then progress toward:

Linux
  ↓
Git
  ↓
Networking
  ↓
Bash
  ↓
Docker
  ↓
CI/CD
  ↓
Cloud
  ↓
Terraform / Ansible
  ↓
Kubernetes
  ↓
Monitoring

Quick Summary

UNIX → Operating-system family and historical standard

GNU → Collection of free Unix-like software and tools

Linux → Kernel

GNU/Linux → Linux kernel + GNU tools + other software

Distribution → Complete GNU/Linux system, such as Ubuntu, Debian, or RHEL

DevOps → Learn Linux fundamentals, especially Ubuntu/Debian and RHEL-based systems.