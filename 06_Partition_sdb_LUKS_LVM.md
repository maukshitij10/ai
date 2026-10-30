# Q: Four partitions on /dev/sdb, encrypted volume (cryptvol), LVM logvol1 in VG vgroup

> Add a new virtual disk (e.g. 5 GB) in VMware: VM Settings -> Add -> Hard Disk. Reboot / rescan. Run everything as root.

## 0. Check disk and wipe old data
```bash
lsblk
umount /dev/sdb* 2>/dev/null
wipefs -a /dev/sdb          # wipes all signatures, partitions, LVM
```

## 1. Create four partitions (fdisk)
```bash
fdisk /dev/sdb
```
Inside fdisk:
```
g        (new GPT)   [or o for MBR]
n  Enter  Enter  +500M      -> partition 1 (primary on MBR: p, 1)
n  Enter  Enter  +500M      -> partition 2
n  Enter  Enter  +500M      -> partition 3
n  Enter  Enter  Enter      -> partition 4 (rest of disk)
w
```
*(With MBR: partition 4 needs `p` primary; 4 primaries is fine.)*
```bash
partprobe /dev/sdb
lsblk /dev/sdb
```

## 2. Encrypted volume on /dev/sdb1
```bash
dnf install cryptsetup -y
cryptsetup luksFormat /dev/sdb1        # type YES, set passphrase
cryptsetup luksOpen /dev/sdb1 cryptvol
ls /dev/mapper/
mkfs.ext4 /dev/mapper/cryptvol
mkdir /cryptvol
```
### Auto-mount at boot
```bash
blkid /dev/sdb1                         # note the UUID
echo "cryptvol  UUID=<sdb1-uuid>  none" >> /etc/crypttab
echo "/dev/mapper/cryptvol  /cryptvol  ext4  defaults  0 0" >> /etc/fstab
mount -a
df -h /cryptvol
```
(Passphrase is asked at boot. For keyfile: `dd if=/dev/urandom of=/root/keyfile bs=1024 count=4; chmod 600 /root/keyfile; cryptsetup luksAddKey /dev/sdb1 /root/keyfile` and use the keyfile path instead of `none` in crypttab.)

## 3. LVM on 4th partition (/dev/sdb4)
```bash
pvcreate /dev/sdb4
vgcreate vgroup /dev/sdb4
lvcreate -n logvol1 -l 100%FREE vgroup      # or -L 500M
mkfs.ext4 /dev/vgroup/logvol1
mkdir /logvol1
echo "/dev/vgroup/logvol1  /logvol1  ext4  defaults  0 0" >> /etc/fstab
mount -a
```

## 4. Verify
```bash
pvs ; vgs ; lvs
lsblk
df -hT | grep -E "cryptvol|logvol1"
systemctl daemon-reload
reboot       # confirm both mount after reboot
```
## Viva
- LUKS = Linux Unified Key Setup (disk encryption). PV -> VG -> LV is the LVM hierarchy.
- /etc/fstab = mounts at boot; /etc/crypttab = encrypted devices at boot.
