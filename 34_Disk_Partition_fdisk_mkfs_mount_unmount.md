# Q: List disks, create partition (fdisk/parted), format ext4/XFS, mount, verify, unmount, add new disk

> Add a new virtual disk in VMware (VM Settings > Add > Hard Disk, e.g. 2 GB) and reboot, or rescan:
> `echo "- - -" > /sys/class/scsi_host/host0/scan`

## a. Display disks
```bash
lsblk
fdisk -l
```
## b. Create partition (test disk /dev/sdb)
```bash
fdisk /dev/sdb
```
`n` -> `p` -> `1` -> Enter -> `+1G` -> `w`
```bash
partprobe /dev/sdb
lsblk /dev/sdb
```
Parted alternative: `parted /dev/sdb mklabel msdos mkpart primary 1MiB 1GiB`.
## c. Format
```bash
mkfs.ext4 /dev/sdb1          # or: mkfs.xfs /dev/sdb1
```
## d. Verify
```bash
blkid /dev/sdb1
lsblk -f
file -s /dev/sdb1
```
## Mount and verify access
```bash
mkdir /data
mount /dev/sdb1 /data
df -hT /data
touch /data/test.txt ; ls /data
```
## Unmount and verify
```bash
umount /data
lsblk                         # MOUNTPOINT empty
mount | grep sdb1             # no output
```
## Permanent mount (optional)
```bash
echo "UUID=$(blkid -s UUID -o value /dev/sdb1)  /data  ext4  defaults  0 0" >> /etc/fstab
mount -a
```
