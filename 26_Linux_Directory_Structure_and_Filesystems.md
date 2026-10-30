# Q: Explore Linux directory structure and file systems

## Key directories
| Directory | Purpose |
|---|---|
| `/` | Root of the whole filesystem tree |
| `/etc` | System-wide configuration files (passwd, fstab, ssh/, httpd/) |
| `/home` | Home directories of normal users |
| `/var` | Variable data: logs (/var/log), mail, spool, web (/var/www) |
| `/usr` | User programs, libraries, docs (/usr/bin, /usr/lib) |
| `/bin /sbin` | Essential commands (symlinks to /usr/bin on RHEL 9) |
| `/root` | Home of root user |
| `/tmp` | Temporary files (sticky bit) |
| `/dev` | Device files (sda, null) |
| `/proc` | Virtual FS: kernel/process info |
| `/boot` | Kernel, initramfs, GRUB |
| `/mnt /media` | Mount points |
| `/opt` | Optional third-party software |
| `/lib /lib64` | Shared libraries |

```bash
ls /
ls -l /etc | head
ls -ld /home /var /usr /tmp
tree -L 1 /          # dnf install tree
man hier
```
## Filesystem details
```bash
ls -lah /
df -h
df -hT                # shows type (xfs, ext4)
mount | head
findmnt
lsblk -f
cat /etc/fstab
```
Filesystem types: XFS (RHEL default), ext4, vfat, NFS, tmpfs.
