---
id: sesmyz7g8guk4p1u67jgqqv
title: Linux Commands
desc: ''
updated: 1791130131247
created: 1790959820758
---
# The `ps -ef` Command Guide

The **`ps -ef`** command is a standard utility used in Unix and Linux operating systems to display a detailed, full-format snapshot of all currently running processes on the system. 

---

## Breakdown of the Command

* **`ps`**: Stands for **Process Status**. It gives you information about active processes.
* **`-e`**: Selects **every** process running on the system (equivalent to `-A`).
* **`-f`**: Produces a **full-format** listing, which includes more detailed columns like the parent process ID, start time, and full command arguments.

---

## Understanding the Output Columns

When you run `ps -ef`, the output typically displays several columns. Here is what each one means:

* **`UID`**: The user ID or username of the person who owns and started the process.
* **`PID`**: The unique **Process ID** assigned to that running program.
* **`PPID`**: The **Parent Process ID** (the PID of the process that launched this one).
* **`C`**: Processor utilization (CPU usage) during the lifetime of the process.
* **`STIME`**: The start time or date the process began running.
* **`TTY`**: The controlling terminal associated with the process (`?` means it's not attached to a terminal, like a background daemon).
* **`TIME`**: The cumulative CPU time the process has used.
* **`CMD`**: The actual command line (including arguments) used to launch the process.

---

## Practical Examples

### 1. Basic Usage
Simply type the command in your terminal:
```bash
ps -ef

## Enterprise RHEL Identity & Sudo

### Architecture

```text
Company Identity Provider
   │
   ├── Active Directory / LDAP
   │       │
   │       ▼
   │      SSSD
   │       │
   │       ▼
   │    RHEL Server
   │       │
   │       ▼
   │     sudo
   │       │
   │       ▼
   │   Root privileges
```

### Components

| Component | Purpose |
|---|---|
| **AD / LDAP** | Stores corporate users and groups |
| **SSSD** | Connects RHEL to AD/LDAP and provides identity/authentication information |
| **Kerberos** | Often used with AD for authentication and SSO |
| **SSO** | Allows users to authenticate once and access multiple services |
| **sudo** | Controls which users/groups can perform privileged operations |
| **sudoers** | Defines sudo permissions |
| **Azure / RHEL VM** | Provides VM infrastructure; company must configure identity integration |

### Important Distinction

- **AD / LDAP** = Identity
- **SSSD** = Linux integration
- **Kerberos** = Authentication / SSO
- **sudo** = Privilege control
- **sudoers** = Defines sudo permissions

### Example Login Flow

```text
Alice
  │
  ▼
Active Directory
  │
  ▼
SSSD
  │
  ▼
RHEL VM
  │
  ▼
sudoers
  │
  ▼
Root access
```

### How They Work Together

A newly created RHEL VM in Azure does **not automatically know about the company's AD/LDAP users**.

The company must configure the RHEL server to integrate with its identity provider.

Once configured:

```text
AD / LDAP
    ↓
   SSSD
    ↓
 RHEL Server
    ↓
   sudo
    ↓
Privileged Access
```

### Authentication vs Authorization

**Authentication** answers:

> Who are you?

For example:

```text
Alice
  ↓
SSSD
  ↓
AD / LDAP / Kerberos
  ↓
Authenticated
```

**Authorization** answers:

> What are you allowed to do?

For example:

```text
Alice
  ↓
Member of linux-admins
  ↓
sudoers
  ↓
Allowed to run commands as root
```

### Example sudoers Configuration

If the company has an LDAP/AD group called `linux-admins`:

```text
%linux-admins ALL=(ALL) ALL
```

The `%` means that `linux-admins` is a group.

Members of that group can use:

```bash
sudo <command>
```

For example:

```bash
sudo systemctl restart nginx
```

### Typical Enterprise Flow

```text
Employee
   │
   ▼
Active Directory / LDAP
   │
   │ Identity + Group Membership
   ▼
SSSD
   │
   ▼
RHEL Server
   │
   ├── SSH
   ├── PAM
   ├── NSS
   └── sudo
          │
          ▼
       sudoers
          │
          ▼
    Privileged Access
```

### Key Point

> **AD / LDAP = Identity**
>
> **SSSD = Linux integration**
>
> **Kerberos = Authentication / SSO**
>
> **sudo = Privilege control**
>
> **sudoers = Defines sudo permissions**

Azure provides the VM infrastructure, but the company normally needs to configure the RHEL VM to integrate with its chosen identity provider.
