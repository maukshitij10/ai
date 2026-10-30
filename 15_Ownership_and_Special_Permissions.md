# Q: linux.txt / minor.txt - ownership, group wheel, advanced (special) permissions

```bash
touch linux.txt                          # a
useradd guest ; passwd guest             # if missing
chown guest linux.txt                    # b  user owner
chgrp wheel linux.txt                    # c  group owner   (or: chown guest:wheel linux.txt)
ls -l linux.txt
```
## d. Advanced permissions (SUID, SGID, Sticky)
```bash
chmod u+s linux.txt        # SUID  (or chmod 4755)
chmod g+s linux.txt        # SGID  (or chmod 2755)
chmod o+t linux.txt        # Sticky (or chmod 1755)
ls -l linux.txt
chmod 7755 linux.txt       # all three together
ls -l
```
Meaning:
- **SUID (4)** - executable runs with file owner's privileges (e.g. /usr/bin/passwd). Shows `s` in user execute.
- **SGID (2)** - runs with group privileges; on a directory, new files inherit the group.
- **Sticky (1)** - on a directory, only owner can delete own files (e.g. /tmp). Shows `t`.
- Capital `S`/`T` means the execute bit is not set.
Remove: `chmod u-s,g-s,o-t linux.txt` or `chmod 755`.
