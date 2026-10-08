---
id: oz6d389qjhcr8l0smp18f9s
title: Linux Commands Part1
desc: ''
updated: 1791389426517
created: 1791130871462
---
## Linux User Management

### Add User

```bash
sudo useradd sample
sudo passwd sample
```

### Show User

```bash
id sample
```

Or:

```bash
getent passwd sample
```

### `/etc/passwd`

```bash
cat /etc/passwd
```

Example:

```text
sample:x:1001:1001::/home/sample:/bin/sh
```

Format:

```text
username:password:UID:GID:GECOS:home:shell
```

### `/etc/shadow`

```bash
sudo cat /etc/shadow
```

Example:

```text
sample:!:20730:0:99999:7:::
```

Contains password hash and password-aging/security information.

### Quick Summary

```text
/etc/passwd → User/account information
/etc/shadow → Password/security information
id          → User ID and group information
getent      → User information from local files or LDAP/SSSD
```
## DNF Package Management

### List Installed Packages

```bash
sudo dnf list installed
```

At the same time, we can also get the packages which are not installed and are available for installation from remote repositories.

### List Available Packages

```bash
sudo dnf list available
```

In case we want both the packages which are installed and available for installation, we can use the `all` option.

### List All Packages

```bash
sudo dnf list all
```

The above command can produce thousands of lines of output. We can pipe the output to `grep` to filter the content.

```bash
sudo dnf list all | grep nginx
```

### Install a Package

```bash
sudo dnf install nginx
```

The above command will prompt for confirmation before proceeding with the installation. To avoid the prompt, use the `-y` option.

```bash
sudo dnf install nginx -y
```

### Remove / Erase a Package

```bash
sudo dnf remove nginx -y
```

### Update a Package

```bash
sudo dnf update nginx -y
```

### Update the Complete System

```bash
sudo dnf update -y
```

## DNF Repositories

If you wonder how DNF manages package installation, you will see that it downloads the package and then installs it.

But where does it download the package from?

The `dnf` command refers to the repository configuration files available under:

```text
/etc/yum.repos.d/*.repo
```

These `.repo` files contain the repository destinations from which DNF downloads packages.

## Example: Jenkins Repository

Let's understand this with an example.

First, try to search for Jenkins:

```bash
sudo dnf list | grep jenkins
```

The command will not find Jenkins if the Jenkins repository has not been configured.

### Check List of Repositories

```bash
ls /etc/yum.repos.d
```

### Download Jenkins Repository

```bash
sudo curl https://pkg.jenkins.io/redhat-stable/jenkins.repo -o /etc/yum.repos.d/jenkins.repo
```

### Check List of Repositories Again

```bash
ls /etc/yum.repos.d
```

Now the Jenkins repository file should be available.

After adding the repository, you can search for Jenkins:

```bash
sudo dnf list | grep jenkins
```

You can then install Jenkins using DNF.

## Install a Package Directly Using URL

We can also install an RPM package directly using its URL:

```bash
sudo dnf install https://pkg.jenkins.io/redhat-stable/jenkins-2.190.2-1.1.noarch.rpm -y
```

## Quick Summary

```text
dnf list installed       → List installed packages
dnf list available       → List available packages
dnf list all             → List installed + available packages
dnf install <package>    → Install a package
dnf remove <package>     → Remove a package
dnf update <package>     → Update a package
dnf update               → Update the complete system
```

## Repository Location

```text
/etc/yum.repos.d/*.repo
        ↓
Repository configuration
        ↓
Remote package repository
        ↓
DNF downloads package
        ↓
Package gets installed
```

## Understanding `ls -l` Output

```text
-rw-r--r-- 1 root root 0 Oct 4 16:37 sample.txt
│         │ │    │    │     │
│         │ │    │    │     └── File name
│         │ │    │    └──────── Date/time
│         │ │    └───────────── Size: 0 bytes
│         │ └────────────────── Group: root
│         └──────────────────── Owner: root
└────────────────────────────── Permissions
```

### Permissions: `-rw-r--r--`

```text
-    → Regular file
rw-  → Owner: read + write
r--  → Group: read only
r--  → Others: read only
```

### Summary

- **Owner:** `root`
- **Group:** `root`
- **Size:** `0 bytes`
- **Permissions:** Owner can read/write; others can only read
- **File:** `sample.txt`

## `chown` Command

`chown` is used to **change the owner and/or group** of a file or directory.

### Syntax

```bash
chown [owner]:[group] <file>
```

### Change Owner

```bash
sudo chown sample sample.txt
```

Changes the owner of `sample.txt` to `sample`.

### Change Owner and Group

```bash
sudo chown sample:developers sample.txt
```

Changes:

```text
Owner → sample
Group → developers
```

### Change Group Only

```bash
sudo chown :developers sample.txt
```

### Change Ownership Recursively

Use `-R` for directories and their contents:

```bash
sudo chown -R sample:developers /home/sample
```

### Check Ownership

```bash
ls -l sample.txt
```

Example:

```text
-rw-r--r-- 1 sample developers 0 Oct 4 16:37 sample.txt
```

### Quick Summary

```text
chown user file              → Change owner
chown user:group file        → Change owner and group
chown :group file            → Change group
chown -R user:group dir      → Recursively change ownership
```
# Linux `ls` Commands

These are common Linux/macOS `ls` commands:

- `ls` — Lists files and directories in the current directory.
- `ls -l` — Lists files in **long format**, showing permissions, owner, group, size, and modification time.
- `ls -A` — Lists **almost all** files, including hidden files, but excludes `.` and `..`.
- `ls -lA` — Combines `-l` and `-A`: long-format listing including hidden files.
- `ls -ltr` — Lists files in long format, sorted by **modification time**, with the **oldest files first**.

## Options Explained

| Option | Meaning |
|---|---|
| `ls` | List files and directories |
| `-l` | Long listing format |
| `-A` | Show hidden files except `.` and `..` |
| `-t` | Sort by modification time |
| `-r` | Reverse the sorting order |

# Linux `rm` Commands

These commands are used to **remove (delete) files and directories** in Linux/macOS.

## Commands

- `rm filename` — Removes a file. Usually asks for confirmation only when required by permissions or aliases.
- `rm -f filename` — Forcefully removes a file without prompting.
- `rm -rf directoryname` — Recursively and forcefully removes a directory and **everything inside it**.

## Options Explained

| Option | Meaning |
|---|---|
| `rm` | Remove/delete |
| `-f` | Force removal; do not prompt |
| `-r` | Recursively remove directories and their contents |

# Linux `cp` and `mv` Commands

Both `cp` and `mv` are used to work with files and directories.

- `cp` → Copy files/directories
- `mv` → Move or rename files/directories

---

# 1. `cp` Command

The `cp` command is used to copy files or directories.

## Syntax

    cp source destination

## Example: Copy a File

    cp file1.txt file2.txt

This creates a copy of `file1.txt` named `file2.txt`.

The original file remains.

    Before:
    file1.txt

    After:
    file1.txt
    file2.txt

---

## Copy a File to a Directory

    cp file.txt /home/user/documents/

This copies `file.txt` into the `documents` directory.

---

## Copy Multiple Files

    cp file1.txt file2.txt /home/user/documents/

Both files are copied into the `documents` directory.

---

## Copy a Directory

To copy a directory and its contents, use `-r` (recursive):

    cp -r directory1 directory2

Example:

    cp -r project backup

This creates a copy of the `project` directory called `backup`.

---

## Useful `cp` Options

| Option | Meaning |
|---|---|
| `-r` | Copy directories recursively |
| `-i` | Ask before overwriting |
| `-f` | Force copying/overwriting |
| `-v` | Show what is being copied |
| `-p` | Preserve file attributes |

Example:

    cp -rv project backup

This recursively copies `project` to `backup` and displays what is being copied.

---

# 2. `mv` Command

The `mv` command is used to move or rename files and directories.

## Syntax

    mv source destination

---

## Move a File

    mv file.txt /home/user/documents/

The file is moved from the current directory to `documents`.

    Before:

    current/
    └── file.txt

    documents/

    After:

    current/

    documents/
    └── file.txt

The original location no longer contains `file.txt`.

---

# 3. Rename a File

`mv` is also used to rename files.

    mv oldname.txt newname.txt

Example:

    mv report.txt final_report.txt

This changes:

    report.txt

to:

    final_report.txt

No separate "rename" command is required.

---

# 4. Move a Directory

    mv project /home/user/documents/

This moves the entire `project` directory to `documents`.

---

# 5. Rename a Directory

    mv old_directory new_directory

Example:

    mv project project_backup

The directory is renamed from:

    project

to:

    project_backup

---

# Useful `mv` Options

| Option | Meaning |
|---|---|
| `-i` | Ask before overwriting |
| `-f` | Force move/overwrite |
| `-v` | Show what is being moved |

Example:

    mv -iv file.txt backup/

- `-i` → Ask before overwriting
- `-v` → Show the operation

---

# `cp` vs `mv`

| Feature | `cp` | `mv` |
|---|---|---|
| Purpose | Copy | Move / Rename |
| Original remains? | Yes | No |
| Can copy files? | Yes | Yes |
| Can move files? | No | Yes |
| Can work with directories? | Yes, with `-r` | Yes |
| Used for renaming? | No | Yes |
| Creates a duplicate? | Yes | No |

---

# Example: `cp`

    cp file.txt backup.txt

Result:

    file.txt
    backup.txt

Both files exist.

The original `file.txt` is still present.

---

# Example: `mv`

    mv file.txt backup.txt

Result:

    backup.txt

`file.txt` no longer exists under its old name.

---

# Main Difference

    cp → Make a copy

    mv → Move to another location

    mv → Rename a file or directory

Think of it like this:

    cp:

    Original ────────────────┐
                             ├──> Copy
                             └──> Original remains


    mv:

    Original ────────────────> New location/name
                               Original location is empty

---

# Quick Memory Trick

    cp = COPY
    mv = MOVE
    mv = RENAME

---

# Common Commands

    # Copy a file
    cp file.txt backup.txt

    # Copy a directory
    cp -r project project_backup

    # Copy a file into a directory
    cp file.txt documents/

    # Copy multiple files
    cp file1.txt file2.txt documents/

    # Move a file
    mv file.txt documents/

    # Move a directory
    mv project documents/

    # Rename a file
    mv old.txt new.txt

    # Rename a directory
    mv old_folder new_folder

---

# Important: `-i` for Safety

Both `cp` and `mv` can overwrite an existing destination.

Use `-i` to ask for confirmation before overwriting:

    cp -i file.txt backup/

    mv -i file.txt backup/

You may see:

    overwrite 'backup/file.txt'?

You can then answer:

    y

or:

    n

---

# Summary

| Command | Purpose |
|---|---|
| `cp file1 file2` | Copy file1 to file2 |
| `cp -r dir1 dir2` | Copy directory recursively |
| `mv file dir/` | Move file into directory |
| `mv old new` | Rename file/directory |
| `cp -i` | Ask before overwriting |
| `mv -i` | Ask before overwriting |
| `cp -v` | Show copy operation |
| `mv -v` | Show move operation |

## One-Line Difference

    cp → Original stays + a copy is created.

    mv → Original is moved/renamed; no duplicate is created.

# `awk` Command — Brief Explanation

`awk` is a Linux command used to **search, filter, and extract data from text files**, especially when the data is arranged in columns.

## Basic Syntax

    awk 'pattern {action}' file

Example:

    awk '{print $1}' file.txt

This prints the **first column** of every line.

---

## Important Concepts

Suppose the file contains:

    John 25 Developer
    Alice 30 Manager
    Bob 28 Tester

`awk` treats the data as fields:

    $1 → John
    $2 → 25
    $3 → Developer

### Common Variables

| Syntax | Meaning |
|---|---|
| `$0` | Entire line |
| `$1` | First field |
| `$2` | Second field |
| `$NF` | Last field |
| `NF` | Number of fields |
| `NR` | Current line number |

---

## Field Separator `-F`

By default, `awk` uses spaces/tabs as separators.

For `/etc/passwd`, fields are separated by `:`.

awk -F ':' '{print $1}' /etc/passwd


Meaning:

-F ':' → Use : as the separator $1 → First field print $1 → Print the first field


Output:

    root
    daemon
    bin
    sys
    ...

---

## Conditions

You can filter data using conditions:

awk '$2 > 25 {print $1}' employees.txt


Meaning:

If column 2 is greater than 25 ↓ Print column 1
```
