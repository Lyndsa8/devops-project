
## Task 9 — Explain Permissions

Linux file system security relies on a 3-digit octal notation system. Each digit manages access for a specific tier of users in a strict hierarchical order:
1. **First Digit:** The **User** (Individual account that owns the file)
2. **Second Digit:** The **Group** (Users assigned to the file's primary group)
3. **Third Digit:** **Others** (Any other global account on the local system)

The access rights are calculated mathematically by summing the binary bitmask values of the desired capabilities:
* **Read (r)** = `4`
* **Write (w)** = `2`
* **Execute (x)** = `1`
* **No Permission (-)** = `0`

---

### 1. Code `755` (`rwxr-xr-x`)
* **User Allocation ($4+2+1=7$):** Granted full Read, Write, and Execution privileges.
* **Group Allocation ($4+0+1=5$):** Granted Read and Execution access; denied modification capabilities.
* **Others Allocation ($4+0+1=5$):** Granted global Read and Execution access; denied modification capabilities.
* **DevOps Engineering Blueprint:** This configuration is standard for shared utility software, scripts (like our `deploy.sh`), and directory structures. It allows non-root service accounts and general system processes to execute the program without permitting them to alter or corrupt the underlying source code.

### 2. Code `644` (`rw-r--r--`)
* **User Allocation ($4+2+0=6$):** Granted Read and Write access; cannot be executed as an application.
* **Group Allocation ($4+0+0=4$):** Isolated to a Read-Only state.
* **Others Allocation ($4+0+0=4$):** Isolated to a Read-Only state globally.
* **DevOps Engineering Blueprint:** The baseline default for standard system files, text documentation, and public web assets. It permits web servers (like Nginx or Apache) to read and host the file contents while locking out all edit privileges to anyone except the owner.

### 3. Code `600` (`rw-------`)
* **User Allocation ($4+2+0=6$):** Granted absolute Read and Write capabilities to safely interact with the file.
* **Group Allocation ($0$):** Total access denial.
* **Others Allocation ($0$):** Total access denial.
* **DevOps Engineering Blueprint:** Critical high-security credential lockdown. This is required for safeguarding infrastructure connection configurations (like our `app.conf`), internal private keys, and application environment variables. It directly enforces the security principle of least privilege, preventing horizontal data visibility or local privilege escalation breaches.

---

### Verified Permissions Environment
The screenshot below confirms the successful implementation of the permission states configured during Tasks 7 and 8:

![POSIX File Permissions Verification](screenshots/task9_permissions.png)

### Task 10 — Start Background Process
To simulate a long-running, continuous application or service without locking up the active terminal user interface, the `sleep` utility was executed and pushed directly into the background using the trailing ampersand (`&`) operator:
```bash
sleep 600 &```

### Task 11 — Identify Process
To trace and verify the execution state of our background operation, the global system process table was audited using the Process Status (`ps aux`) tool combined with a pipeline filter (`grep`) to isolate its specific Process ID (PID) and command mapping:
```bash
ps aux | grep "sleep 600"
```
Identified Process Name: sleep 600

Identified PID: 3844

---
### Task 12 — Terminate Process
Using the validated PID (`3844`), a standard termination signal (`SIGTERM`) was delivered directly to the target background thread to stop it cleanly:
```bash
kill 3844
```
![Process Management Verification](screenshots/task10_12_process.png)
### Task 13 — Monitor System
To inspect global system resource performance and running kernel threads on the host machine, the interactive real-time system monitor tool was executed:

```bash
top```

###Task 14 — Find Server IP

To discover the local system identity and its network addressing properties for hostname and query ip address respectively is 
```bash
hostname
hostname -I```

### Task 15 — Test Connectivity
To verify external internet access from the local virtual machine, a 4-packet ICMP echo request was sent to Google's public DNS:
```bash
ping -c 4 google.com```

###Task 16 - Verify Listening Ports
To confirm that local gateway ports such as SSH service(Port 22) and Webserver(port 80/443) are listening, socket connections were queried:
```Bash
ss -tuln```

---

## PART 6 — SSH & SCP

### Task 17 — Remote Access (Local to Remote)
To establish a secure remote administrative session with the cloud-hosted AWS EC2 Ubuntu instance, local private key permissions were securely restricted, and the SSH transport tunnel was initialized:

```bash
# Set secure read-only permission on the downloaded private key
chmod 400 ~/Downloads/devops-key.pem

# Securely connect to the AWS instance
ssh -i ~/Downloads/devops-key.pem ubuntu@16.170.233.94```

### Task 18 — Secure File Transfer
The entire local workspace repository (`devops-project/`) was securely and recursively uploaded over an encrypted network channel to the remote AWS EC2 instance home directory using Secure Copy (`scp`):

```bash
scp -i ~/Downloads/devops-key.pem -r ~/devops-project ubuntu@16.170.233.94:~/
```
### Task 19 — Retrieve File (Remote to Local)
To verify file retrieval capabilities from the cloud infrastructure, a specific application log archive was securely downloaded from the remote AWS host back to a dedicated local workspace subdirectory:

```bash
# Download target log file from AWS EC2 instance
scp -i ~/Downloads/devops-key.pem ubuntu@16.170.233.94:~/devops-project/logs/app.log ~/Downloads/restored-files/
```
---

## PART 7 — DISK & SYSTEM INFORMATION

### Task 20 — Resource Monitoring & System Metrics
To evaluate the host infrastructure's operating conditions, storage allocation, memory consumption, and active network sockets, the standard administrative diagnostics suite was executed:

```bash
# Display human-readable file system disk space usage
df -h

# Display total and available system memory metrics in megabytes
free -m

# Output current system uptime, logged-in sessions, and load averages
uptime

# Audit active listening TCP/UDP network ports and sockets
sudo ss -tuln```

(screenshots/task20_system_info.png)
---

### Task 21 to 23 — Log Auditing, Session Tracking & Package Management
To finalize the host infrastructure review, authentication logs were inspected for anomalies, active user administrative sessions were mapped, and system repository update lines were verified:

```bash
# Task 21: View the final 20 lines of security authentication logs
sudo tail -n 20 /var/log/auth.log

# Task 22: List currently authenticated user sessions
who

# Task 23: Audit system repositories for available security updates
sudo apt update && apt list --upgradable
