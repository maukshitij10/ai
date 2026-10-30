# Q: NFS file sharing (export files lmn and xyz / share a directory and mount on client)
Two VMs: server (e.g. 192.168.1.10) and client (192.168.1.20). NFS exports directories, so put the files inside a shared directory.

## Server
```bash
dnf install nfs-utils -y
mkdir /share
touch /share/lmn /share/xyz ; echo "hello" > /share/lmn
chmod 777 /share
echo "/share  192.168.1.20(rw,sync,no_root_squash)" >> /etc/exports
# or for all: /share *(rw,sync)
systemctl enable --now nfs-server
exportfs -rav
exportfs -v
firewall-cmd --permanent --add-service={nfs,mountd,rpc-bind}
firewall-cmd --reload
```
## Client
```bash
dnf install nfs-utils -y
showmount -e 192.168.1.10               # list exported dirs
mkdir /mnt/nfs
mount -t nfs 192.168.1.10:/share /mnt/nfs
df -h | grep nfs
ls /mnt/nfs                              # lmn  xyz
touch /mnt/nfs/test                      # verify write access
umount /mnt/nfs
```
Permanent: `192.168.1.10:/share  /mnt/nfs  nfs  defaults  0 0` in /etc/fstab.
If denied: `setsebool -P nfs_export_all_rw 1`, or `setenforce 0` for testing.
Export options: rw/ro, sync, root_squash/no_root_squash. Ports: 2049.
