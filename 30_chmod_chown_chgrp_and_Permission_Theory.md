# Q: chmod, chown, chgrp; significance of user/group/other permissions

```bash
mkdir testdir ; touch testfile
ls -ld testdir ; ls -l testfile
chmod 755 testdir                  # rwxr-xr-x
chmod 640 testfile                 # rw-r-----
chmod u+x,g-r,o-r testfile
chmod -R 750 testdir
useradd user1 ; groupadd team1
chown user1 testfile               # change owner
chgrp team1 testfile               # change group
chown user1:team1 testdir          # both
chown -R user1:team1 testdir
ls -l
```
## Significance
Permission string `-rwxr-xr--` = type | user | group | others.
| | File | Directory |
|---|---|---|
| r (4) | read contents | list contents (ls) |
| w (2) | modify | create/delete files inside |
| x (1) | execute | enter (cd) |
- **User (u)**: owner of file. **Group (g)**: members of file's group. **Others (o)**: everyone else.
- Default permissions come from `umask` (022 -> files 644, dirs 755).
