---
id: e5t49sosfqdmlwlxc7abt1r
title: Top 60 Commands
desc: ''
updated: 1791735079312
created: 1791734926944
---
# Top 60 Linux Commands for DevOps Engineers

Linux commands are essential for DevOps engineers to manage servers, troubleshoot applications, monitor system resources, analyze logs, configure networking, and automate deployments.

## 1. Files and Directories

| # | Command | Description |
|---:|---|---|
| 1 | `pwd` | Display the current working directory. |
| 2 | `ls -lah` | List all files, including hidden files, with readable sizes. |
| 3 | `cd /path` | Change the current directory. |
| 4 | `mkdir -p app/logs` | Create directories recursively. |
| 5 | `touch file.txt` | Create an empty file or update its timestamp. |
| 6 | `cp source dest` | Copy files or directories. |
| 7 | `mv old new` | Move or rename files. |
| 8 | `rm -r directory` | Remove a directory and its contents. |
| 9 | `find /var/log -name "*.log"` | Find files by name. |
| 10 | `du -sh /var/log` | Display total disk usage of a directory. |

### Example: Find the 10 Largest Entries

```bash
du -ah /var/log | sort -rh | head -n 10
```

**Explanation:**
- `du` → Display disk usage.
- `-a` → Include files and directories.
- `-h` → Show human-readable sizes.
- `sort -rh` → Sort sizes from largest to smallest.
- `head -n 10` → Display the first 10 results.

**DevOps use case:** Identify large files consuming disk space.

---

## 2. Read and Process Files

| # | Command | Description |
|---:|---|---|
| 11 | `cat file.txt` | Display file contents. |
| 12 | `less file.txt` | Browse large files page by page. |
| 13 | `head -n 20 file.txt` | Display the first 20 lines. |
| 14 | `tail -n 50 file.txt` | Display the last 50 lines. |
| 15 | `tail -f app.log` | Follow new log entries in real time. |
| 16 | `grep -in "error" app.log` | Search text, ignoring case and showing line numbers. |
| 17 | `awk '{print $1}' file.txt` | Extract the first field from each line. |
| 18 | `sed 's/old/new/g' file.txt` | Replace text in output. |
| 19 | `sort file.txt` | Sort lines alphabetically. |
| 20 | `uniq -c` | Count adjacent duplicate lines. |

### Example: Find Frequent Error Messages

```bash
grep -i "error" app.log | sort | uniq -c | sort -nr | head
```

**Explanation:**
- `grep` → Find matching lines.
- `sort` → Group identical lines together.
- `uniq -c` → Count adjacent identical lines.
- `sort -nr` → Sort counts numerically in descending order.
- `head` → Display the top results.

**Memory trick:**
- `grep` = Search.
- `awk` = Extract and analyze fields.
- `sed` = Substitute and edit text.
- `sort` = Order lines.
- `uniq` = Count adjacent duplicates.

---

## 3. Processes and System Monitoring

| # | Command | Description |
|---:|---|---|
| 21 | `ps aux` | List running processes. |
| 22 | `top` | Monitor CPU and memory usage in real time. |
| 23 | `htop` | Interactively monitor processes; may require installation. |
| 24 | `pgrep nginx` | Find process IDs by process name. |
| 25 | `kill -15 PID` | Request graceful process termination. |
| 26 | `free -h` | Display memory usage. |
| 27 | `uptime` | Show uptime and system load averages. |
| 28 | `nproc` | Display the number of available processing units. |
| 29 | `vmstat 1` | Display system performance statistics every second. |
| 30 | `dmesg -T` | Display kernel messages with readable timestamps. |

### Example: Troubleshoot a Slow Server

```bash
uptime
free -h
top
ps aux
dmesg -T | tail -n 30
```

**DevOps use case:** Investigate high system load, memory pressure, resource-intensive processes, and kernel-level issues.

**Important:** A high load average does not necessarily mean the CPU is overloaded. Check CPU usage, I/O wait, and system resources together.

---

## 4. Disk, Storage, and Permissions

| # | Command | Description |
|---:|---|---|
| 31 | `df -h` | Display filesystem disk usage. |
| 32 | `lsblk` | List disks and block devices. |
| 33 | `du -ah /var/log \| sort -h` | Sort file and directory sizes from smallest to largest. |
| 34 | `chmod 755 script.sh` | Set file permissions using numeric notation. |
| 35 | `chown user:group file.txt` | Change file ownership and group. |
| 36 | `stat file.txt` | Display file metadata and permissions. |
| 37 | `id` | Display the current user's UID and group IDs. |
| 38 | `whoami` | Display the current username. |
| 39 | `sudo command` | Run a command with elevated privileges. |
| 40 | `mount` | Display mounted filesystems. |

### Example: Understand `chmod 755`

```bash
chmod 755 script.sh
ls -l script.sh
```

Permission values:

| Permission | Value |
|---|---:|
| Read (`r`) | 4 |
| Write (`w`) | 2 |
| Execute (`x`) | 1 |

Therefore:

- `7 = 4 + 2 + 1 = rwx`
- `5 = 4 + 0 + 1 = r-x`
- `5 = 4 + 0 + 1 = r-x`

Result:

```text
-rwxr-xr-x
```

**In one sentence:** `chmod 755 script.sh` gives the owner full permissions and allows everyone else to read and execute the script.

### Example: Find the 10 Largest Entries in `/var/log`

```bash
du -ah /var/log | sort -rh | head -n 10
```

**Explanation:**
- `du` → Displays disk usage.
- `-a` → Includes files and directories.
- `-h` → Displays human-readable sizes.
- `/var/log` → Directory containing system and application logs.
- `|` → Passes output to the next command.
- `sort -rh` → Sorts sizes from largest to smallest.
- `head -n 10` → Displays the top 10 entries.

**DevOps use case:** Investigate log growth and disk-space alerts.

---

## 5. Networking and Connectivity

| # | Command | Description |
|---:|---|---|
| 41 | `ip addr` | Display network interfaces and IP addresses. |
| 42 | `ip route` | Display the routing table. |
| 43 | `ping -c 4 example.com` | Test basic network reachability. |
| 44 | `curl -I https://example.com` | Display HTTP response headers. |
| 45 | `wget https://example.com/file.zip` | Download a file. |
| 46 | `ss -lntp` | Inspect listening TCP ports and processes. |
| 47 | `dig example.com` | Query DNS records. |
| 48 | `traceroute example.com` | Trace the network path; may require installation. |
| 49 | `nc -vz host 443` | Test TCP connectivity to a host and port. |
| 50 | `tcpdump -i any port 443` | Capture packets matching a port filter. |

### Example: Troubleshoot an Application on Port 8080

```bash
ss -lntp
curl -v http://localhost:8080
nc -vz server.example.com 8080
```

**Explanation:**
- `ss -lntp` → Check which TCP ports are listening.
- `curl -v` → Inspect the HTTP connection and response.
- `nc -vz` → Test TCP connectivity to a remote host and port.

**DevOps use case:** Troubleshoot unreachable applications, service ports, and connectivity problems.

**Note:** Use `sudo` when elevated privileges are required. A failed `ping` does not always indicate a network failure because ICMP traffic may be blocked.

---

## 6. Services, Logs, and Automation

| # | Command | Description |
|---:|---|---|
| 51 | `systemctl status nginx` | Check the status of a service. |
| 52 | `systemctl restart nginx` | Restart a service. |
| 53 | `systemctl enable nginx` | Enable a service at boot. |
| 54 | `journalctl -u nginx` | Display logs for a service. |
| 55 | `journalctl -u nginx -f` | Follow service logs in real time. |
| 56 | `crontab -l` | List the current user's scheduled cron jobs. |
| 57 | `tar -czf backup.tar.gz directory/` | Create a compressed archive. |
| 58 | `tar -xzf backup.tar.gz` | Extract a compressed archive. |
| 59 | `ssh user@server` | Connect securely to a remote server. |
| 60 | `scp file.txt user@server:/tmp/` | Copy a file to a remote server. |