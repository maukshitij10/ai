# Q: Configure sudo for specific commands; YUM install/update/remove; show repo configuration

## sudo for specific commands
```bash
useradd user1 ; passwd user1
visudo
```
Add:
```
user1 ALL=(ALL) /usr/bin/systemctl, /usr/bin/yum
```
Or put in drop-in: `echo "user1 ALL=(ALL) /usr/bin/systemctl restart httpd" > /etc/sudoers.d/user1 ; chmod 440 /etc/sudoers.d/user1`
Full admin: `usermod -aG wheel user1`.
Test: `su - user1` -> `sudo systemctl status sshd` (allowed), `sudo useradd x` (denied). `sudo -l` lists rights.

## YUM
```bash
yum repolist
cat /etc/yum.repos.d/*.repo
yum install tree -y
yum update tree
yum remove tree -y
```
Remaining items (ps/top/kill, jobs): see file 37.
