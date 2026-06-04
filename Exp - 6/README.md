# Accessing EC2 Instances

When launching EC2 instances in the default us-east-1 Region in this environment, choose the option to use the existing key pair named **vockey** at the time of launch.

Then:

- Choose the **AWS Details** link above these instructions.

### If you are using a Windows desktop or laptop

- Choose the **Download PPK** button and save the `labsuser.ppk` file.
- You can use this file to connect via SSH to a Linux EC2 instance or Windows EC2 instance, typically using a tool such as PuTTY.

### If you are using a MacOS desktop or laptop

- Choose the **Download PEM** button and save the `labsuser.pem` file.
- You can use this file to connect via SSH to a Linux EC2 instance or Windows EC2 instance, typically using a terminal window.

---

## To connect via Remote Desktop to a Windows EC2 instance

1. In the EC2 Console, choose **Instances** and choose the instance you want to connect to.
2. From the **Actions** menu choose **Get Windows Password**.
3. Next to **Key Pair Path** choose **Browse**.
4. Browse to and select the `labsuser.pem` file you downloaded earlier.
5. Choose **Decrypt Password**.
6. The connection information will now display, including:
   - The instance's Public DNS
   - Administrator user name
   - The decrypted password
7. Use a Remote Desktop Protocol (RDP) client to connect to the desktop of the EC2 instance using these connection details.

To connect using SSH to a Linux instance, see the next section.

---

# SSH access to an EC2 Instance you launch

The steps below describe how to use the SSH key to connect to your instance.

> **Tip:** Assuming you launched the instance with the `vockey` key pair, and that you have opened TCP port 22 in the instance's security group, you can also SSH to an EC2 instance by using the terminal to the side of these instructions.

Simply enter the command:

```bash
ssh -i ~/.ssh/labsuser.pem ec2-user@<public-ip>
```

where `<public-ip>` is the actual IPv4 public address of the instance.

---

# Windows Users: Using SSH to Connect

These instructions are for Windows users only.

## Download needed software

You will use PuTTY to SSH to Amazon EC2 instances.

If you do not have PuTTY installed on your computer, download it here.

---

## Open putty.exe

### Configure PuTTY to not timeout

1. Choose **Connection**.
2. Set **Seconds between keepalives** to `30`.

This allows you to keep the PuTTY session open for a longer period of time.

---

## Configure your PuTTY session

1. Choose **Session**.
2. In **Host Name (or IP address)**:
   - Copy and paste the IPv4 Public IP address for the instance.
   - To find it:
     - Return to the EC2 Console.
     - Choose **Instances**.
     - Check the box next to the instance.
     - In the **Description** tab copy the **IPv4 Public IP** value.

3. Back in PuTTY:
   - In the **Connection** list, expand **SSH**.
   - Choose **Auth** (don't expand it).
   - Choose **Browse**.
   - Browse to and select the `.ppk` file that you downloaded.
   - Choose **Open** to select it.

4. Choose **Open**.

5. Choose **Yes**, to trust the host and connect to it.

6. When prompted:

```text
login as: ec2-user
```

This will connect you to the EC2 instance.


--- 
# EC2 SSH Command Reference

Essential Linux commands for students connected to AWS EC2 via SSH.

## Difficulty Levels

- Beginner
- Intermediate
- Advanced

---

# 1. System Info

## OS & Kernel Info
See which Linux distro and kernel version is running.

```bash
uname -a && cat /etc/os-release
```

**Level:** Beginner

### CPU Info
List CPU cores and architecture.

```bash
lscpu
```

**Level:** Beginner

### RAM Usage
Check total and available memory.

```bash
free -h
```

**Level:** Beginner

### System Uptime
How long the server has been running.

```bash
uptime
```

**Level:** Beginner

### Environment Variables
List all environment variables set in the session.

```bash
printenv
```

**Level:** Beginner

---

# 2. Files & Directories

### List Files
Show all files including hidden ones with details.

```bash
ls -lah
```

**Level:** Beginner

### Current Directory
Print working directory.

```bash
pwd
```

**Level:** Beginner

### Create & Edit File
Create a file and write to it.

```bash
echo 'Hello Cloud' > myfile.txt
cat myfile.txt
```

**Level:** Beginner

### Find Files
Search for files by name recursively.

```bash
find / -name '*.log' 2>/dev/null
```

**Level:** Intermediate

### File Permissions
Change file permissions.

```bash
chmod 755 myfile.txt
ls -l myfile.txt
```

**Level:** Intermediate

### Copy/Move Files
Copy and move files between directories.

```bash
cp myfile.txt /tmp/
mv /tmp/myfile.txt /tmp/backup.txt
```

**Level:** Beginner

### Compress Files
Create a tar.gz archive.

```bash
tar -czvf archive.tar.gz /var/log/*.log
```

**Level:** Intermediate

---

# 3. Processes

### Running Processes
Show all currently running processes.

```bash
ps aux
```

**Level:** Beginner

### Live Process Monitor
Real-time CPU and memory usage.

```bash
top
```

**Level:** Beginner

### Check Service Status
Check if a service like nginx is running.

```bash
systemctl status nginx
```

**Level:** Beginner

---

# 4. Networking

### IP Address
Show network interfaces and IP addresses.

```bash
ip addr show
```

**Level:** Beginner

### Open Ports
List all listening ports.

```bash
ss -tuln
```

**Level:** Intermediate

### Test Connectivity
Ping a host to check internet access.

```bash
ping -c 4 google.com
```

**Level:** Beginner

### DNS Lookup
Resolve a hostname to IP.

```bash
nslookup example.com
```

**Level:** Beginner

### Trace Route
Trace hops to a destination.

```bash
traceroute google.com
```

**Level:** Intermediate

### HTTP Request Test
Test an HTTP endpoint (useful for APIs).

```bash
curl -I https://google.com
```

**Level:** Intermediate

---

# 5. Disk & Storage

### Disk Usage Summary
See total disk space used per partition.

```bash
df -h
```

**Level:** Beginner

### Folder Size
Find which folders use the most space.

```bash
du -sh /var/* 2>/dev/null | sort -rh | head -10
```

**Level:** Intermediate

### List Block Devices
Show all attached disks and EBS volumes.

```bash
lsblk
```

**Level:** Beginner

---

# 6. Users & Permissions

### Current User
Who am I logged in as?

```bash
whoami
```

**Level:** Beginner

### All Users
List all users on the system.

```bash
cat /etc/passwd | cut -d: -f1
```

**Level:** Beginner

### Add a User
Create a new Linux user.

```bash
sudo adduser student1
```
