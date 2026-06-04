---
# EC2 SSH Command Reference

Essential Linux commands for students connected to AWS EC2 via SSH.

---

# 1. System Info

### OS & Kernel Info
See which Linux distro and kernel version is running.

```bash
uname -a && cat /etc/os-release
```

### CPU Info
List CPU cores and architecture.

```bash
lscpu
```

### RAM Usage
Check total and available memory.

```bash
free -h
```

### System Uptime
How long the server has been running.

```bash
uptime
```

### Environment Variables
List all environment variables set in the session.

```bash
printenv
```

---

# 2. Files & Directories

### List Files
Show all files including hidden ones with details.

```bash
ls -lah
```

### Current Directory
Print working directory.

```bash
pwd
```

### Create & Edit File
Create a file and write to it.

```bash
echo 'Hello Cloud' > myfile.txt
cat myfile.txt
```

### Find Files
Search for files by name recursively.

```bash
find / -name '*.log' 2>/dev/null
```

### File Permissions
Change file permissions.

```bash
chmod 755 myfile.txt
ls -l myfile.txt
```

### Copy/Move Files
Copy and move files between directories.

```bash
cp myfile.txt /tmp/
mv /tmp/myfile.txt /tmp/backup.txt
```

### Compress Files
Create a tar.gz archive.

```bash
tar -czvf archive.tar.gz /var/log/*.log
```

---

# 3. Processes

### Running Processes
Show all currently running processes.

```bash
ps aux
```

### Live Process Monitor
Real-time CPU and memory usage.

```bash
top
```

### Check Service Status
Check if a service like nginx is running.

```bash
systemctl status nginx
```

---

# 4. Networking

### IP Address
Show network interfaces and IP addresses.

```bash
ip addr show
```

### Open Ports
List all listening ports.

```bash
ss -tuln
```

### Test Connectivity
Ping a host to check internet access.

```bash
ping -c 4 google.com
```

### DNS Lookup
Resolve a hostname to IP.

```bash
nslookup example.com
```

### Trace Route
Trace hops to a destination.

```bash
traceroute google.com
```

### HTTP Request Test
Test an HTTP endpoint (useful for APIs).

```bash
curl -I https://google.com
```

---

# 5. Disk & Storage

### Disk Usage Summary
See total disk space used per partition.

```bash
df -h
```

### Folder Size
Find which folders use the most space.

```bash
du -sh /var/* 2>/dev/null | sort -rh | head -10
```

### List Block Devices
Show all attached disks and EBS volumes.

```bash
lsblk
```

---

# 6. Users & Permissions

### Current User
Who am I logged in as?

```bash
whoami
```

### All Users
List all users on the system.

```bash
cat /etc/passwd | cut -d: -f1
```

### Add a User
Create a new Linux user.

```bash
sudo adduser student1
```
