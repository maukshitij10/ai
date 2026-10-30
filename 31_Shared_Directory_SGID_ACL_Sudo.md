# Q: Shared directory with group ownership, SGID, ACL; switching users; sudo

```bash
useradd user1 ; useradd user2 ; passwd user1 ; passwd user2     # create users
groupadd devteam
usermod -aG devteam user1 ; usermod -aG devteam user2
id user1 user2

mkdir /shared                                   # shared directory
chgrp devteam /shared
chmod 2770 /shared                              # rwxrws--- (SGID=2)
ls -ld /shared                                  # drwxrws---

su - user1 -c "touch /shared/file1.txt"         # new file inherits group devteam
ls -l /shared

setfacl -m u:user3:r /shared/file1.txt          # ACL for a specific user (create user3 first)
getfacl /shared/file1.txt                       # verify ownership, permissions, ACL
ls -l /shared                                   # '+' indicates ACL
```
Verify access: `su - user2 -c "cat /shared/file1.txt"` (works - same group); `su - user3 -c "echo x >> /shared/file1.txt"` fails (read-only ACL).

## sudo / su admin access
```bash
usermod -aG wheel user1
su - user1
sudo systemctl status sshd
```
