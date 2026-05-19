<h1>DevOps Infrastructure Technical Scenario Analysis</h1>
<p><strong>System Environment:</strong> Linux Mint Debian Edition 7 (LMDE 7)</p>

<h2>File Management Scenarios</h2>

<h3>1. Relocating a Misplaced File</h3>
<ul>
  <li><strong>Scenario:</strong> A file was accidentally generated in an incorrect directory path.</li>
  <li><strong>Solution:</strong> Use the <code>mv</code> (move) utility to relocate the target file to the designated path.</li>
</ul>
<pre><code>mv filename.txt /home/ubuntu/projects/</code></pre>

<h3>2. Nested Single-Command Directory Creation</h3>
<ul>
  <li><strong>Scenario:</strong> The environment requires a uniform directory architecture setup for logs, scripts, and backups.</li>
  <li><strong>Solution:</strong> Execute <code>mkdir</code> with brace expansion to evaluate and spin up the folders in one command.</li>
</ul>
<pre><code>mkdir -p /path/to/project/{logs,scripts,backups}</code></pre>

<h3>3. Storage Optimization: Locate, Relocate, and Purge</h3>
<ul>
  <li><strong>Scenario:</strong> A large backup archive is saturating storage block space.</li>
  <li><strong>Solution:</strong> Use find to track the resource, copy it to backups, and purge the source.</li>
</ul>
<pre><code># Locate the large file by size (looking for files over 40MB)
find . -type f -size +40M

# Copy the target file to the backup directory
cp huge_backup.tar.gz backups/

# Purge the original file to reclaim disk blocks
rm huge_backup.tar.gz</code></pre>

<h3>4. Live Production Application Log Tailing</h3>
<ul>
  <li><strong>Scenario:</strong> A web application is failing. The logs are stored in: /var/log/app.log. How would you view the latest logs and continuously monitor updates?</li>
  <li><strong>Solution:</strong> Use the <code>tail</code> utility to see the bottom of the file, and apply the <code>-f</code> flag to track live adjustments stream-side.</li>
</ul>
<pre><code># View the latest log entries
tail /var/log/app.log

# Continuously monitor updates live
tail -f /var/log/app.log</code></pre>

<h3>5. Scanning for Target Database Failures</h3>
<ul>
  <li><strong>Scenario:</strong> You suspect the application has database errors. How would you search the log file for ERROR?</li>
  <li><strong>Solution:</strong> Filter the log entries with the <code>grep</code> utility to scan the target log file and pull out only the lines containing the specific failure token.</li>
</ul>
<pre><code>grep "ERROR" logs/app.log</code></pre>

<h3>6. Interactive Large-File Pagination Inspection</h3>
<ul>
  <li><strong>Scenario:</strong> A configuration file is very large, which command would help you scroll through it page by page?</li>
  <li><strong>Solution:</strong> Pass the target configuration file to the <code>less</code> utility to scroll through data cleanly.</li>
</ul>
<pre><code>less logs/app.log</code></pre>

<h2>Permissions & Ownership Scenarios</h2>

<h3>7. Execution Permission Denied Resolution</h3>
<ul>
  <li><strong>Scenario:</strong> A deployment script called deploy.sh fails with: Permission denied. How would you fix it?</li>
  <li><strong>Solution:</strong> Modify the file mode bits using the <code>chmod</code> utility with the <code>+x</code> flag to grant explicit execution permissions.</li>
</ul>
<pre><code>chmod +x scripts/deploy.sh</code></pre>
<p><img src="screenshots/task7_permissions.png" alt="Task 7 Permissions" /></p>

<h3>8. System Resource Ownership Alteration</h3>
<ul>
  <li><strong>Scenario:</strong> You need to change the owner of a file named report.txt to a user named developer. How would you do that?</li>
  <li><strong>Solution:</strong> Execute the <code>chown</code> utility prefixed with <code>sudo</code> administrative privileges to reassign user ownership.</li>
</ul>
<pre><code>sudo chown developer report.txt</code></pre>
<p><img src="screenshots/task8_ownership.png" alt="Task 8 Ownership" /></p>

<h3>9. Absolute File Permissions Mask Configuration</h3>
<ul>
  <li><strong>Scenario:</strong> How would you grant read, write, and execute permissions to the owner, but only read permissions to everyone else for a file named secure.txt?</li>
  <li><strong>Solution:</strong> Apply the absolute numeric permissions mask <code>744</code> using the <code>chmod</code> utility.</li>
</ul>
<pre><code>chmod 744 secure.txt</code></pre>
<p><img src="screenshots/Scenarios 9_permissions.png" alt="Task 9 Permissions" /></p>

<h3>10. Group Infrastructure Ownership Modification</h3>
<ul>
  <li><strong>Scenario:</strong> You want to make a directory named shared accessible to a group named devs. How would you change the group ownership of this directory?</li>
  <li><strong>Solution:</strong> Utilize the <code>chgrp</code> utility prefixed with <code>sudo</code> administrative privileges.</li>
</ul>
<pre><code>sudo chgrp devs shared</code></pre>
<p><img src="screenshots/scenarios 10.png" alt="Task 10 Group" /></p>

<h2>System Information & Process Management Scenarios</h2>

<h3>11. Real-Time System Resource Monitoring</h3>
<ul>
  <li><strong>Scenario:</strong> Your server is running slow. Which command would you use to see running processes and resource usage in real-time?</li>
  <li><strong>Solution:</strong> Launch the interactive <code>htop</code> or <code>top</code> utility to view an active administrative process dashboard.</li>
</ul>
<pre><code>htop</code></pre>
<p><img src="screenshots/Scenarios11_monitoring.png" alt="Task 11 Monitoring" /></p>

<h3>12. Human-Readable Storage Volume Inspection</h3>
<ul>
  <li><strong>Scenario:</strong> How do you check the available disk space on your Linux system in a human-readable format?</li>
  <li><strong>Solution:</strong> Execute the <code>df</code> utility with the <code>-h</code> human-readable flag.</li>
</ul>
<pre><code>df -h</code></pre>
<p><img src="screenshots/Scenarios12_disk_space_.png" alt="Task 12 Disk Space" /></p>

<h3>13. Granular Directory Storage Footprint Analysis</h3>
<ul>
  <li><strong>Scenario:</strong> How can you view the size of a specific directory and all its contents?</li>
  <li><strong>Solution:</strong> Invoke the <code>du</code> utility with the <code>-sh</code> flags to compute storage footprint block allocation.</li>
</ul>
<pre><code>du -sh ~/devops-project</code></pre>
<p><img src="screenshots/Scenario13_diskusage_.png" alt="Task 13 Disk Usage" /></p>

<h3>14. Unresponsive Process Force Termination</h3>
<ul>
  <li><strong>Scenario:</strong> A process with ID 1234 is frozen and needs to be stopped immediately. Which command would you use?</li>
  <li><strong>Solution:</strong> Issue the <code>kill</code> utility configured with the <code>-9</code> SIGKILL signal flag.</li>
</ul>
<pre><code>kill -9 1234</code></pre>

<h3>15. Real-Time Memory Capacity Volatility Check</h3>
<ul>
  <li><strong>Scenario:</strong> You need to check how much free RAM (memory) is available on the server. Which command would you run?</li>
  <li><strong>Solution:</strong> Execute the <code>free</code> utility modified with the <code>-h</code> flag.</li>
</ul>
<pre><code>free -h</code></pre>
<p><img src="screenshots/Scenarios15_free memory.png" alt="Task 15 Free Memory" /></p>

<h2>Networking & Connectivity Scenarios</h2>

<h3>16. Remote Host Network Layer Reachability Verification</h3>
<ul>
  <li><strong>Scenario:</strong> You want to check if a remote server at IP address 192.168.1.50 is reachable. Which utility would you use?</li>
  <li><strong>Solution:</strong> Deploy the <code>ping</code> utility to transmit ICMP Echo Requests and assess connectivity metrics.</li>
</ul>
<pre><code>ping -c 6 8.8.8.8</code></pre>
<p><img src="screenshots/Scenario16_ping.png" alt="Task 16 Ping" /></p>

<h3>17. Remote Resource Command-Line Ingestion</h3>
<ul>
  <li><strong>Scenario:</strong> How would you download a file from a URL like http://example.com/file.tar.gz using the command line?</li>
  <li><strong>Solution:</strong> Invoke the <code>wget</code> network download utility against the remote uniform resource locator.</li>
</ul>
<pre><code>wget http://example.com/file.tar.gz</code></pre>

<h3>18. Active Network Socket and Listening Port Extraction</h3>
<ul>
  <li><strong>Scenario:</strong> You need to see all active network connections and listening ports on your machine. Which command would you use?</li>
  <li><strong>Solution:</strong> Execute the <code>ss</code> utility with the <code>-tuln</code> flags to display listening transport layer sockets.</li>
</ul>
<pre><code>ss -tuln</code></pre>
<p><img src="screenshots/Scenario 17_18 Network Connections.png" alt="Task 17/18 Network Connections" /></p>

<h3>19. Kernel Routing Table Inspection and Configuration</h3>
<ul>
  <li><strong>Scenario:</strong> How would you add a static routing entry or check the kernel routing table on your Linux machine?</li>
  <li><strong>Solution:</strong> Use the <code>ip route</code> utility to show active routes, or append arguments to insert a static route.</li>
</ul>
<pre><code># To view the table:
ip route show

# To add a static route:
sudo ip route add 192.168.2.0/24 via 192.168.1.1</code></pre>
<p><img src="screenshots/Scenario19_routing.png" alt="Task 19 Routing" /></p>

<h3>20. Domain Name System Record Resolution</h3>
<ul>
  <li><strong>Scenario:</strong> How do you look up the DNS records (like the IP address) of a domain name such as google.com from the terminal?</li>
  <li><strong>Solution:</strong> Execute the <code>dig</code> utility against the target domain name to query name servers.</li>
</ul>
<pre><code>dig google.com</code></pre>
<p><img src="screenshots/Scenario20_dnslookup.png" alt="Task 20 DNS Lookup" /></p>

<h2>Archiving, Backup, & Package Management Scenarios</h2>

<h3>21. Compressed File System Archive Creation</h3>
<ul>
  <li><strong>Scenario:</strong> How would you create a compressed backup archive of a directory named logs into a file called logs_backup.tar.gz?</li>
  <li><strong>Solution:</strong> Deploy the <code>tar</code> utility configured with creation and gzip compression flags (<code>-czvf</code>).</li>
</ul>
<pre><code>tar -czvf logs_backup.tar.gz logs</code></pre>

<h3>22. Compressed File System Archive Extraction</h3>
<ul>
  <li><strong>Scenario:</strong> You have a compressed archive file named backup.tar.gz. How would you extract its contents into the current directory?</li>
  <li><strong>Solution:</strong> Execute the <code>tar</code> utility configured with extraction and gzip decompression flags (<code>-xzvf</code>).</li>
</ul>
<pre><code>tar -xzvf backup.tar.gz</code></pre>

<h3>23. Package Repository Package Index Synchronization</h3>
<ul>
  <li><strong>Scenario:</strong> You want to update your Linux system's package list to make sure you can install the latest versions of software. Which command do you run on Ubuntu/Debian?</li>
  <li><strong>Solution:</strong> Invoke the <code>apt</code> package manager with the <code>update</code> command argument, prefixed with <code>sudo</code>.</li>
</ul>
<pre><code>sudo apt update</code></pre>

<h3>24. System-Wide Software Package Upgrade Execution</h3>
<ul>
  <li><strong>Scenario:</strong> After updating the package list, how do you actually upgrade all installed packages on an Ubuntu/Debian system to their latest versions?</li>
  <li><strong>Solution:</strong> Execute the <code>apt</code> package manager using the <code>upgrade</code> command modifier combined with <code>sudo</code>.</li>
</ul>
<pre><code>sudo apt upgrade -y</code></pre>

<h3>25. Target Software Package Installation</h3>
<ul>
  <li><strong>Scenario:</strong> How do you install a new package, such as the network tool curl, on an Ubuntu system?</li>
  <li><strong>Solution:</strong> Deploy the <code>apt</code> package utility with the <code>install</code> command, elevated by <code>sudo</code> privileges.</li>
</ul>
<pre><code>sudo apt install -y curl</code></pre>
<p><img src="screenshots/Scenarios 21_25.png" alt="Task 21-25" /></p>
