# Q: Process management
a. Start a process, send to background, bring back to foreground
b. Parent-child relationship
c. top: renice, change priority, kill

## a. Background / foreground
```bash
sleep 300            # runs in foreground
# press Ctrl+Z  -> stops (suspends) it
jobs                 # shows [1]+ Stopped sleep 300
bg %1                # resume in background
jobs                 # [1]+ Running sleep 300 &
fg %1                # bring back to foreground
# Ctrl+C to stop it
sleep 400 &          # start directly in background
```

## b. Parent-child relationship
```bash
echo $$              # PID of current shell (parent)
bash                 # start a child shell
echo $$              # new PID (child)
echo $PPID           # parent PID = previous shell PID
ps -f                # PPID column shows parent
pstree -p            # tree view
sleep 500 &
ps -o pid,ppid,cmd -p $!     # PPID of the sleep = shell PID
exit                 # return to parent shell
```

## c. top - renice, priority, kill
```bash
sleep 1000 &
sleep 2000 &
yes > /dev/null &    # CPU hungry process
top
```
Inside top:
- Press **r** -> enter PID -> enter new nice value (e.g. `10`) -> Enter (renice). Only root can set negative values (-20 to 19).
- Press **k** -> enter PID -> signal `15` (or `9`) -> Enter (kill).
- Press **q** to quit. Press **u** to filter by user, **P** sort by CPU.

Command-line equivalents:
```bash
ps -o pid,ni,cmd -p <PID>
renice -n 10 -p <PID>
nice -n 5 sleep 600 &        # start with a nice value
kill -9 <PID>
pkill sleep
```
## Viva
- Nice range -20 (highest priority) to +19 (lowest). Default 0.
- Ctrl+Z = SIGTSTP, Ctrl+C = SIGINT, kill = SIGTERM(15), kill -9 = SIGKILL.
