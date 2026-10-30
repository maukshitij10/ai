# Q: Demonstrate mounting a USB flash drive

## Connect the USB to the VM (VMware)
VM menu -> **Removable Devices > (your USB) > Connect (Disconnect from Host)**.

## Steps
```bash
lsblk                       # find device, e.g. sdb / sdb1
fdisk -l                    # confirm
blkid /dev/sdb1             # check filesystem type
mkdir /mnt/usb
mount /dev/sdb1 /mnt/usb
df -h | grep usb
ls /mnt/usb
```
If NTFS/exFAT: `dnf install ntfs-3g` (EPEL) and `mount -t ntfs-3g /dev/sdb1 /mnt/usb`. FAT: `mount -t vfat /dev/sdb1 /mnt/usb`.

## Unmount
```bash
cd /
umount /mnt/usb
lsblk
```
## Permanent mount (optional)
```bash
blkid /dev/sdb1
echo "UUID=<uuid>  /mnt/usb  vfat  defaults,nofail  0 0" >> /etc/fstab
mount -a
```
Note: GUI desktop automounts under `/run/media/<user>/`.
