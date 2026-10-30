# Q: Perform the installation of Red Hat Linux on a Virtual Machine (VMware)

## Requirements
- VMware Workstation / Player installed
- RHEL 9 ISO (free Developer subscription from developers.redhat.com)
- Min: 2 CPU, 2-4 GB RAM, 20 GB disk

## Steps
1. Open VMware -> **File > New Virtual Machine** -> **Typical** -> Next.
2. Select **Installer disc image file (iso)** -> Browse to the RHEL ISO -> Next.
3. Guest OS: **Linux**, Version: **Red Hat Enterprise Linux 9 64-bit** -> Next.
4. Name the VM (e.g. `RHEL9`) and choose location -> Next.
5. Disk size: **20 GB**, "Store as single file" -> Next -> **Finish** (customise hardware: RAM 2048 MB, CPU 2).
6. Power on the VM -> choose **Install Red Hat Enterprise Linux 9** -> Enter.
7. Select language (English) -> **Continue**.
8. On **Installation Summary** configure:
   - **Installation Destination** -> select disk -> Automatic -> Done
   - **Network & Host Name** -> turn Ethernet **ON**, set hostname (e.g. `rhel9.example.com`) -> Apply
   - **Software Selection** -> *Server with GUI* (needed for workspaces) -> Done
   - **Root Password** -> set password, tick "Allow root SSH login with password" (for practice)
   - **User Creation** -> create a user (e.g. `guest`) and tick "Make this user administrator"
   - **Time & Date** -> Asia/Kolkata
9. Click **Begin Installation** (10-20 min).
10. Click **Reboot System** -> accept license -> finish setup.
11. Log in and verify:
```bash
cat /etc/redhat-release
uname -r
hostnamectl
```
12. (Optional) Register: `subscription-manager register --username <id>`

## Viva points
- RHEL = Red Hat Enterprise Linux, commercial, uses RPM/dnf, SELinux, firewalld, systemd.
- Default filesystem: XFS. Default partitioning uses LVM.
