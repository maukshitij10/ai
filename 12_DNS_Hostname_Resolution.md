# Q: Configure DNS / hostname resolution

## 1. Set hostname
```bash
hostnamectl set-hostname server1.example.com
hostname
```
## 2. Local resolution - /etc/hosts
```bash
ip a                                  # note your IP, e.g. 192.168.1.10
echo "192.168.1.10  server1.example.com  server1" >> /etc/hosts
ping -c 2 server1
getent hosts server1
```
## 3. DNS server for the connection (nmcli)
```bash
nmcli connection show                 # e.g. ens160
nmcli connection modify ens160 ipv4.dns "8.8.8.8 8.8.4.4"
nmcli connection modify ens160 ipv4.ignore-auto-dns yes
nmcli connection up ens160
cat /etc/resolv.conf
```
(Do not edit resolv.conf by hand - NetworkManager overwrites it.)

## 4. Name-service order
```bash
grep hosts /etc/nsswitch.conf         # files dns
```
## 5. Verify
```bash
nslookup google.com        # dnf install bind-utils
dig google.com
host google.com
ping -c 2 google.com
```
## Viva
- Order: /etc/hosts -> DNS (nsswitch.conf). DNS port 53. Config files: /etc/hosts, /etc/resolv.conf, /etc/hostname.
