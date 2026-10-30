# Q: ps, top, kill; job control (jobs, bg, fg); tuned-adm; sudo + yum

## ps / top
```bash
ps ; ps -ef ; ps aux
ps aux --sort=-%cpu | head
top            # q to quit; k kill; r renice; M sort memory; P sort CPU
htop           # optional (EPEL)
pgrep sleep ; pstree
```
## Job control
```bash
sleep 500 &            # background job
jobs                   # list jobs
sleep 600              # Ctrl+Z to suspend
bg %2                  # resume in background
fg %1                  # bring to foreground
kill %1                # kill a job
```
## Identify CPU-intensive process and kill
```bash
yes > /dev/null &      # CPU hog
top                    # spot it at top (or: ps aux --sort=-%cpu | head -3)
kill <PID>             # SIGTERM
kill -9 <PID>          # force
pkill yes ; killall yes
```
## tuned-adm
```bash
dnf install tuned -y ; systemctl enable --now tuned
tuned-adm active                # current profile
tuned-adm list                  # available profiles
tuned-adm profile throughput-performance    # switch (optional)
tuned-adm recommend
```
## Add new disk
See file 34.
