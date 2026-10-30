# Q: Demonstrate ACL - assigning and displaying (also read-only ACL for specific users)

```bash
useradd user1 ; useradd user2 ; passwd user1 ; passwd user2
mkdir /project ; touch /project/data.txt
chmod 660 /project/data.txt

getfacl /project/data.txt                       # display
setfacl -m u:user1:rw /project/data.txt         # give user1 read/write
setfacl -m u:user2:r /project/data.txt          # read-only for user2
setfacl -m g:wheel:r /project/data.txt          # group ACL
getfacl /project/data.txt
ls -l /project/data.txt                         # '+' sign shows ACL present
```
Test: `su - user2 -c "cat /project/data.txt"` works; `su - user2 -c "echo x >> /project/data.txt"` -> Permission denied.

Default ACL on a directory (inherited by new files):
```bash
setfacl -m d:u:user1:rwx /project
```
Remove:
```bash
setfacl -x u:user2 /project/data.txt     # remove one entry
setfacl -b /project/data.txt             # remove all ACLs
```
Backup/restore: `getfacl -R /project > acl.bak ; setfacl --restore=acl.bak`
Note: filesystem must support ACL (XFS and ext4 do by default).
