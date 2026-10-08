---
id: 40pi01jiz1svgvbs4om6jme
title: Unix&Linux
desc: ''
updated: 1790959478539
created: 1790958479718
---
# UNIX, Linux, GNU & Linux Flavours

## 1. What is UNIX?

**UNIX** is a family of operating systems that originated at **Bell Labs in the 1970s**.

It introduced many concepts still used today:
- Files and directories
- Processes
- Users and permissions
- Shells
- Pipes
- Networking

Examples:
- IBM AIX
- HP-UX
- Oracle Solaris

---

## 2. What is Linux?

**Linux is a kernel**, created by **Linus Torvalds in 1991**.

The kernel is responsible for managing:
- CPU
- Memory
- Processes
- Hardware
- Networking
- Devices

Linux is **Unix-like**, meaning it follows many of the concepts and design principles of UNIX.

---

## 3. UNIX vs Linux

| Feature | UNIX | Linux |
|---|---|---|
| Origin | Bell Labs, 1970s | Linus Torvalds, 1991 |
| Type | Operating-system family | Kernel |
| Source | Historically mostly proprietary | Open source |
| Examples | AIX, HP-UX, Solaris | Ubuntu, Debian, RHEL |
| Common usage | Enterprise/legacy systems | Servers, Cloud, DevOps, Desktop |
| Cost | Often commercial | Usually free/open source |

### Simple difference

> **UNIX is an operating-system family, while Linux is an open-source Unix-like kernel used to build Linux distributions.**

---

## 4. What is GNU?

**GNU** is a free and open-source software project started by **Richard Stallman in 1983**.

GNU stands for:

> **GNU's Not Unix**

GNU provides many tools used on Linux systems:

- Bash → Shell
- Coreutils → `ls`, `cp`, `mv`, `rm`, etc.
- GCC → Compiler
- grep → Text searching
- sed → Text processing
- awk → Text processing
- make → Build automation

### GNU + Linux

```text
Applications
     ↓
GNU tools + other software
     ↓
Linux Kernel
     ↓
Hardware


