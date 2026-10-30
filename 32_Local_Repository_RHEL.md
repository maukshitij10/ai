# Q: Configure a local software repository on RHEL and install from it

## a. Prepare directory with RPMs + metadata
Easiest: use the RHEL ISO attached to the VM (VM Settings > CD/DVD > "Connected").
```bash
mkdir /mnt/rhel_iso
mount /dev/sr0 /mnt/rhel_iso
mkdir /localrepo
cp -r /mnt/rhel_iso/AppStream/Packages/*  /localrepo/ 2>/dev/null   # or copy only a few RPMs
dnf install createrepo_c -y
createrepo /localrepo                      # creates repodata/ metadata
ls /localrepo/repodata
```
## b. Configure repo
```bash
vi /etc/yum.repos.d/local.repo
```
```
[local-repo]
name=Local Repository
baseurl=file:///localrepo
enabled=1
gpgcheck=0
```
(Or directly use ISO: baseurl=file:///mnt/rhel_iso/BaseOS and another for AppStream; add the mount to /etc/fstab: `/dev/sr0 /mnt/rhel_iso iso9660 defaults 0 0`.)

## c. Verify and search
```bash
dnf clean all
dnf repolist
dnf search tree
dnf info tree
```
## d. Install and verify
```bash
dnf install tree --disablerepo="*" --enablerepo="local-repo" -y
rpm -q tree
tree --version
```
