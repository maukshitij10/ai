# Q: Shell script to automate or monitor tasks/processes

`vi monitor.sh`
```bash
#!/bin/bash
# Monitor a process; restart it if not running
PROC="httpd"
echo "Monitoring started at $(date)"
if pgrep -x "$PROC" > /dev/null
then
    echo "$PROC is running (PID: $(pgrep -x $PROC | head -1))"
else
    echo "$PROC is NOT running. Starting..."
    systemctl start $PROC
fi
echo "---- Top 5 CPU processes ----"
ps -eo pid,user,%cpu,%mem,comm --sort=-%cpu | head -6
echo "---- Disk usage ----"
df -h /
```
Run:
```bash
chmod +x monitor.sh
./monitor.sh
```
Automate every 5 min: `*/5 * * * * /root/monitor.sh >> /var/log/monitor.log`
