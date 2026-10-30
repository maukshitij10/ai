# Q: Create and manage user accounts with custom home directories and shell types

```bash
useradd -m -d /home/custom1 -s /bin/bash user1            # custom home + bash
useradd -m -d /data/user2home -s /bin/sh user2
useradd -d /opt/user3 -m -s /sbin/nologin user3           # no login shell (service account)
passwd user1
grep -E "user1|user2|user3" /etc/passwd                    # shows home & shell
ls -ld /home/custom1 /data/user2home
cat /etc/shells                                           # valid shells
```
## Manage
```bash
usermod -s /bin/zsh user1                  # change shell (if installed)
usermod -d /home/newhome -m user1          # change home and move files
usermod -c "Comment" user1
usermod -L user1 ; usermod -U user1
chsh -s /bin/bash user2
userdel user3 ; userdel -r user2           # -r removes home
id user1 ; su - user1 ; echo $SHELL ; pwd
```
Skeleton files copied from /etc/skel. Defaults: /etc/default/useradd, /etc/login.defs.
