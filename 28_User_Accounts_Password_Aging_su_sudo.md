# Q: Local users, passwords, group, password aging, su, sudo and root account

```bash
useradd user1 ; useradd user2                  # a
passwd user1 ; passwd user2
groupadd devteam                               # b
usermod -aG devteam user1
usermod -aG devteam user2
id user1 ; grep devteam /etc/group
```
## c. Modify user and password aging
```bash
usermod -c "Test User One" -s /bin/bash user1    # comment, shell
usermod -L user1 ; usermod -U user1              # lock / unlock
chage -l user1                                   # view aging
chage -M 90 -m 7 -W 14 user1                     # max 90 days, min 7, warn 14
chage -E 2026-12-31 user1                        # account expiry
chage -d 0 user1                                 # force password change at next login
passwd -x 90 -n 7 -w 14 user1                    # alternative
```
## d. su, sudo, root
```bash
su - user1            # switch user with login environment
whoami ; exit
su -                  # switch to root (needs root password)
```
- **root**: UID 0 superuser, unrestricted. Avoid direct root login.
- **su**: switch user (needs the target user's password).
- **sudo**: run one command as root using *your own* password; logged in /var/log/secure; controlled by /etc/sudoers.
```bash
usermod -aG wheel user1          # wheel group = sudo access on RHEL
su - user1
sudo whoami                      # prints root
visudo                           # safely edit sudoers
```
Specific command only (in visudo):
`user2 ALL=(ALL) /usr/bin/systemctl restart httpd, /usr/bin/yum`
Verify: `sudo -l -U user2`.
