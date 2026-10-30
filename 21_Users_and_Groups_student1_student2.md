# Q: Create users student1/student2, groups group1/group2, secondary groups

```bash
useradd student1 ; useradd student2                 # a
passwd student1 ; passwd student2
groupadd group1 ; groupadd group2                   # b
usermod -aG group2 student1                         # c secondary group (-a = append!)
usermod -aG group1 student2                         # d
id student1                                         # e
id student2
groups student1 student2
grep -E "group1|group2" /etc/group
```
Other: `gpasswd -a student1 group2`, `userdel -r student1`, `groupdel group1`, `groupmems -g group1 -l`.
Files: /etc/passwd, /etc/shadow, /etc/group.
Warning: `usermod -G` without `-a` replaces all secondary groups.
