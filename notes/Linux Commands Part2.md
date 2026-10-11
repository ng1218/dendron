---
id: fq5tkofnzfnh9c4xohix1fe
title: Linux Commands Part2
desc: ''
updated: 1791735086894
created: 1791733850110
---
# chmod 755 script.sh Explained

`chmod 755 script.sh` changes the permissions of `script.sh` so that:

- Owner: Read, Write, Execute
- Group: Read, Execute
- Others: Read, Execute

## 1. Understand 755

The three digits represent three categories of users:

| Digit | User Category | Permissions |
|---|---|---|
| 7 | Owner | Read, Write, Execute |
| 5 | Group | Read, Execute |
| 5 | Others | Read, Execute |

Therefore:

755 = rwxr-xr-x

## 2. Permission Values

Linux permissions have the following numeric values:

| Permission | Symbol | Value |
|---|---|---|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |
| No permission | - | 0 |

Add these values to calculate each digit.

- 7 = 4 + 2 + 1 = rwx
- 5 = 4 + 0 + 1 = r-x
- 0 = 0 + 0 + 0 = ---

## 3. Example

Run:

    chmod 755 script.sh

Check the permissions:

    ls -l script.sh

Example output:

    -rwxr-xr-x 1 user user 120 Oct 11 script.sh

Explanation:

    - rwx r-x r-x
      |   |   |
      |   |   +-- Others
      |   +------ Group
      +---------- Owner

The first `-` indicates that this is a regular file.

## 4. Why Is chmod 755 Used in DevOps?

Suppose you have a deployment script named `deploy.sh`:

    #!/bin/bash
    echo "Deploying application..."

You can make it executable:

    chmod 755 deploy.sh

Then execute it:

    ./deploy.sh

Output:

    Deploying application...

The owner can read, modify, and execute the script. Group members and other users can read and execute it, but cannot modify it through normal file permissions.

## 5. Common chmod Permissions

| Command | Meaning |
|---|---|
| `chmod 777 file` | Everyone can read, write, and execute |
| `chmod 755 file` | Owner has full permissions; others can read and execute |
| `chmod 750 file` | Owner has full permissions; group can read and execute; others have no permissions |
| `chmod 644 file` | Owner can read and write; group and others can only read |
| `chmod 600 file` | Only the owner can read and write |

## 6. DevOps Interview Tip

Avoid using `chmod 777` unnecessarily because it allows everyone to modify the file.

Use the principle of least privilege: grant only the permissions that users and applications actually need.

## Memory Trick

Remember:

- 4 = Read
- 2 = Write
- 1 = Execute

Add the values to calculate each permission digit.

Example:

    chmod 755 script.sh

    7 = 4 + 2 + 1 = rwx
    5 = 4 + 0 + 1 = r-x
    5 = 4 + 0 + 1 = r-x

Final permissions:

    rwxr-xr-x

# Display Disk space
-------------
## Command
du -ah /var/log | sort -h

### Explanation
- `du` → Displays disk usage.
- `-a` → Includes files and directories.
- `-h` → Shows sizes in human-readable format (K, M, G).
- `/var/log` → Directory containing system and application logs.
- `|` → Passes output to the next command.
- `sort -h` → Sorts sizes from smallest to largest.

### DevOps Use Case
Identify large log files consuming disk space.

### Find the 10 Largest Entries
du -ah /var/log | sort -rh | head -n 10

- `sort -rh` → Sorts largest to smallest.
- `head -n 10` → Displays the top 10 entries.




