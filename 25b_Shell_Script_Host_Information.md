# Q: Shell script to display host information

`vi hostinfo.sh`
```bash
#!/bin/bash
echo "======= HOST INFORMATION ======="
echo "Hostname      : $(hostname)"
echo "OS            : $(cat /etc/redhat-release)"
echo "Kernel        : $(uname -r)"
echo "Architecture  : $(uname -m)"
echo "IP Address    : $(hostname -I)"
echo "Logged User   : $(whoami)"
echo "Uptime        : $(uptime -p)"
echo "CPU           : $(lscpu | grep 'Model name' | cut -d: -f2 | xargs)"
echo "Memory        : $(free -h | awk '/Mem/{print $2}') total, $(free -h | awk '/Mem/{print $4}') free"
echo "Disk (/)      : $(df -h / | awk 'NR==2{print $3" used of "$2}')"
echo "Date          : $(date)"
```
```bash
chmod +x hostinfo.sh ; ./hostinfo.sh
```
