Markdown
# DevOps Infrastructure Log Analysis Lab
**System Environment:** Linux Mint Debian Edition 7 (LMDE 7)  
**Objective:** Apply Linux text-processing and file-system discovery utilities (`find`, `locate`, `grep`, `awk`, `xargs`) to parse system, authentication, and application log metrics.

---

## PART 1 & 2 — File System Discovery (`find` & `locate`)

### Task 1: Find all `.log` files in the workspace
To scan the local tracking context for files ending with the log extension, the wildcard string was passed to the evaluation subsystem:
```bash
find . -name "*.log"```
Output captured:

Plaintext
./app.log
./auth.log
./system.log
Task 2: Match files containing "app" in the filename
```Bash
find . -name "*app*"```
Output captured:

Plaintext
./app.log
Task 3: Locate auth.log via indexing system
Because locate reads from a pre-built indexed database rather than scanning the physical disk live, the index database was refreshed before searching:
```
Bash
sudo updatedb
locate auth.log```
PART 3 — Pattern Matching (grep)
Task 4 & 5: Isolate ERROR and WARNING states from app.log
Bash
# Filter Error States
grep "ERROR" app.log

# Filter Warning Alerts
grep "WARNING" app.log
Output captured:

Plaintext
2026-05-12 08:05:11 ERROR Database connection failed
2026-05-12 08:15:22 ERROR Failed password attempt from 192.168.1.50
2026-05-12 08:25:41 ERROR API timeout from server1
2026-05-12 08:40:18 ERROR Disk write failure

2026-05-12 08:07:45 WARNING Disk usage at 85%
2026-05-12 08:30:55 WARNING High memory usage detected
Task 6: Quantitative Line Counting for Errors
By utilizing a pipe (|), the standard output stream of the matching routine was redirected to the line-counting engine:
```
Bash
grep "ERROR" app.log | wc -l```
Resulting Count: 4

PART 4 — Column Formatting & Token Extraction (awk)
Task 7: Isolate Structural Timestamps
awk processes lines as blank-space separated grids. The first two columns containing date and runtime markers were isolated:
```
Bash
awk '{print $1, $2}' app.log```
Output captured:

Plaintext
2026-05-12 08:00:01
2026-05-12 08:05:11
2026-05-12 08:07:45
...
Task 8: Extract Successful Authentications
```
Bash
grep "logged in" app.log | awk '{print $5}' ```
Extracted Principal User: john

Task 9: Extract Metric Arrays from System State Logs
```Bash
awk '{print $3}' system.log```
Collected Metrics:
45%
68%
91%
88%
92%
95%


PART 5 & 6 — Advanced Pipelines and Argument Bridging (xargs)
Task 10, 11 & 12: Chained Pipeline Redirection
```Bash
# Task 10: Count of Application Errors
grep "ERROR" app.log | wc -l

# Task 11: Alphabetical Sorting of Allowed Users
grep "Accepted" auth.log | awk '{print $8}' | sort

# Task 12: Frequency Counting of Failed Secure Shell Operations
grep "Failed" auth.log | awk '{print $9}' | sort | uniq -c
```
Task 11 Output:

Plaintext
devops
ubuntu
Task 12 Output:

Plaintext
      1 admin
      1 root
      1 testuser
Task 13, 14 & 15: Execution Argument Translation via xargs
A manifest tracking file named loglist.txt was verified. Because cat and grep process standard terminal strings as targeting arguments rather than linear text inputs, xargs was applied as an execution link:

# Task 14: Read list file entries and batch display raw log segments
```cat loglist.txt | xargs cat

# Task 15: Batch scan all log vectors listed inside the manifest file
cat loglist.txt | xargs grep "ERROR"
```
Task 15 Output:

Plaintext
app.log:2026-05-12 08:05:11 ERROR Database connection failed
app.log:2026-05-12 08:15:22 ERROR Failed password attempt from 192.168.1.50
app.log:2026-05-12 08:25:41 ERROR API timeout from server1
app.log:2026-05-12 08:40:18 ERROR Disk write failure
#ADVANCED CHALLENGE — SYSTEM UNSTABILITY ANALYSIS
1. Identify Disk Issue
Scanning the log targets explicitly highlights a severe storage boundary warning and subsequent physical writing anomalies:

system.log: Tracks a critical spike in system metrics up to Disk usage: 95%.

app.log: Records a catastrophic hardware execution block: ERROR Disk write failure.

2. Identify Failed Logins
Analyzing malicious access indicators inside auth.log maps a clear pattern of unauthorized credential testing:

Target targets: Three distinct bad authentications executed back-to-back targeting privileged system accounts (root, admin, and testuser).

3. Total Error Volume Metric
Running an integrated pipeline across all production assets shows that the system registers exactly 4 critical error entries, all concentrated within the application tier.

4. Locate Target Diagnostic Repositories
The active monitoring logs are structurally isolated within the specific workspace node:

Core path: ~/loglab/logs/

5. System Health Summary Statement
CRITICAL CONDITION ALERT: The server environment is structurally unstable. The primary operational bottleneck is localized to storage capacity saturation, which has escalated to a hard disk write failure (95% disk footprint threshold). Concurrently, the perimeter firewall shows trace patterns of a localized brute-force security threat via active authentication failures against system service processes. Immediate intervention required: expand the storage array partition and enforce active ip-blocking mechanics on active nodes.
