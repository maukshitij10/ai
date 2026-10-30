# Q: Memory, block devices, mounted FS, disk usage
(Question header says "process management" but commands are system/disk commands)

## a. Used and free memory in KB and MB
```bash
free            # default KB
free -k         # KB
free -m         # MB
free -h         # human readable
cat /proc/meminfo | head
```

## b. Block devices: tree and ordinary structure
```bash
lsblk           # tree structure
lsblk -l        # list (ordinary) format
```

## c. Information about block devices
```bash
blkid                       # UUID, TYPE, LABEL
lsblk -f                    # filesystem info
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT
fdisk -l                    # partition table details
```

## d. Currently mounted file systems
```bash
mount
findmnt
df -hT
cat /proc/mounts
```

## e. Detailed report of disk space usage
```bash
df -h           # human readable
df -hT          # with FS type
df -i           # inode usage
```

## f. Space used by files in a directory
```bash
du -sh /home            # total summary
du -h /var/log          # per sub-directory
du -sh *                # each item in current dir
du -ah /etc | sort -rh | head
```
## Viva
- `df` reports filesystem-level usage; `du` reports file/directory-level usage.
