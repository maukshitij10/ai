# Q: Script: date, hostname, CPU load, memory usage, selected processes

`vi report.sh`
```bash
#!/bin/bash
echo "Date     : $(date)"
echo "Hostname : $(hostname)"
echo "----- CPU load -----"
uptime                       # load averages
top -bn1 | head -5
echo "----- Memory -----"
free -h
echo "----- Selected running processes -----"
ps aux | grep -E "sshd|crond|NetworkManager" | grep -v grep
echo "----- Top 5 memory processes -----"
ps -eo pid,comm,%mem,%cpu --sort=-%mem | head -6
```
```bash
chmod +x report.sh
./report.sh
```
Alternative CPU load: `cat /proc/loadavg`, `mpstat` (sysstat).
