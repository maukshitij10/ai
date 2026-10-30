# Q: Demonstrate various network management commands

```bash
ip addr show                    # IP addresses (or: ip a)
ip link show                    # interfaces and state
ip route show                   # routing table / default gateway
ifconfig                        # (dnf install net-tools)
hostname ; hostname -I          # hostname and IPs
hostnamectl                     # detailed host info
ping -c 4 8.8.8.8               # connectivity test
ping -c 4 google.com            # DNS + connectivity
traceroute google.com           # (dnf install traceroute)
tracepath google.com
ss -tuln                        # listening ports
netstat -tulnp                  # (net-tools)
nslookup google.com             # (dnf install bind-utils)
dig google.com
host google.com
nmcli device status             # NetworkManager devices
nmcli connection show           # connection profiles
nmcli general status
nmtui                           # text UI
arp -a / ip neigh               # ARP table
curl -I http://example.com      # HTTP header test
systemctl status NetworkManager
systemctl restart NetworkManager
cat /etc/resolv.conf            # DNS servers
cat /etc/hosts
```
## Viva
- `ip` replaces older `ifconfig`/`route`; `ss` replaces `netstat`.
