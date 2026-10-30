# Q: Configure file permissions and ACLs to allow specific users read-only access

```bash
useradd alice ; useradd bob ; useradd carol ; passwd alice ; passwd bob ; passwd carol
echo "Confidential report" > /srv/report.txt
chown root:root /srv/report.txt
chmod 600 /srv/report.txt                 # only root
setfacl -m u:alice:r /srv/report.txt      # alice read-only
setfacl -m u:bob:r /srv/report.txt        # bob read-only
getfacl /srv/report.txt
ls -l /srv/report.txt                     # note '+'
```
Test:
```bash
su - alice -c "cat /srv/report.txt"                 # works
su - alice -c "echo hack >> /srv/report.txt"        # Permission denied
su - carol -c "cat /srv/report.txt"                 # Permission denied
```
Remove: `setfacl -x u:bob /srv/report.txt`; `setfacl -b file`.
Note: the ACL "mask" limits effective permissions; check `getfacl` output for `#effective`.
