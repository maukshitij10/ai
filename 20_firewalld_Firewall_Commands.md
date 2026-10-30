# Q: firewalld - status, zones, allow HTTP/SSH, verify

```bash
systemctl status firewalld                     # a
systemctl enable --now firewalld               # if not running
firewall-cmd --state                           # running
firewall-cmd --get-active-zones                # b
firewall-cmd --get-default-zone
firewall-cmd --list-all                        # rules of active zone (public)
firewall-cmd --permanent --add-service=http    # c
firewall-cmd --permanent --add-service=ssh
firewall-cmd --reload
firewall-cmd --list-services                   # d verify
firewall-cmd --list-all
```
Other: `--add-port=8080/tcp`, `--remove-service=http`, `--get-services`, `--zone=public`.
Without `--permanent` the rule is runtime only and lost on reload/reboot.
