# Q: Sample system log file with 10+ lines; grep error/failed; cut/awk/sort; head/tail/wc

```bash
cat > syslog.txt <<'EOT'
Oct 30 10:00:01 server sshd[1001]: Accepted password for user1
Oct 30 10:01:12 server sshd[1002]: Failed password for root
Oct 30 10:02:20 server kernel: disk error on sdb
Oct 30 10:03:45 server httpd[2001]: started successfully
Oct 30 10:04:10 server crond[3001]: job executed
Oct 30 10:05:33 server sshd[1003]: Failed password for admin
Oct 30 10:06:41 server systemd[1]: network service started
Oct 30 10:07:02 server kernel: error writing block
Oct 30 10:08:15 server sshd[1004]: Accepted password for user2
Oct 30 10:09:50 server httpd[2002]: request failed
Oct 30 10:10:30 server crond[3002]: job executed
EOT
```
## grep
```bash
grep -i -E "error|failed" syslog.txt
grep -ic -E "error|failed" syslog.txt      # count
grep -n "Failed" syslog.txt
```
## cut / awk / sort
```bash
cut -d' ' -f1-3 syslog.txt                 # timestamp
cut -d' ' -f5 syslog.txt | sort | uniq -c  # process counts
awk '{print $3, $5}' syslog.txt            # time and process
awk '{print $5}' syslog.txt | sort
sort -k3 syslog.txt                        # sort by time column
sort -k5 syslog.txt
```
## head / tail / wc
```bash
head -n 3 syslog.txt
tail -n 3 syslog.txt
wc syslog.txt ; wc -l syslog.txt
```
