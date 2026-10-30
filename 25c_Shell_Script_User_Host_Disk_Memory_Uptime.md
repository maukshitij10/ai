# Q: Script: username & hostname, df -h, free -h, uptime; execute and verify

`vi sysinfo.sh`
```bash
#!/bin/bash
echo "Username : $(whoami)"
echo "Hostname : $(hostname)"
echo "----- Disk usage -----"
df -h
echo "----- Memory usage -----"
free -h
echo "----- Uptime -----"
uptime
```
```bash
chmod +x sysinfo.sh
./sysinfo.sh                 # execute
./sysinfo.sh | head          # verify against manual commands: whoami, hostname, df -h, free -h, uptime
```
