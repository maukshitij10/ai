# Q: Configure firewall with iptables to enable SSH, HTTP and FTP

RHEL uses firewalld by default - stop it and use iptables-services:
```bash
systemctl stop firewalld
systemctl disable firewalld
systemctl mask firewalld
dnf install iptables-services -y
systemctl enable --now iptables
iptables -L -n --line-numbers          # view
```
## Rules
```bash
iptables -F                                             # flush (do this on console, not over SSH)
iptables -A INPUT -i lo -j ACCEPT                       # loopback
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j ACCEPT           # SSH
iptables -A INPUT -p tcp --dport 80 -j ACCEPT           # HTTP
iptables -A INPUT -p tcp --dport 21 -j ACCEPT           # FTP
iptables -A INPUT -p icmp -j ACCEPT                     # ping (optional)
iptables -P INPUT DROP                                  # default deny
iptables -L -n -v
```
## Save permanently
```bash
service iptables save           # writes /etc/sysconfig/iptables
# or: iptables-save > /etc/sysconfig/iptables
systemctl restart iptables
```
Delete a rule: `iptables -D INPUT 3`.  Test from another machine with `nmap <ip>` or `telnet <ip> 80`.
Install FTP if needed: `dnf install vsftpd -y ; systemctl enable --now vsftpd`.
