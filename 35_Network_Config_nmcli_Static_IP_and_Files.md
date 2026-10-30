# Q: View IPv4/IPv6, configure static IP with nmcli/nmtui, DNS, config files, ping

## View
```bash
ip addr show
ip -4 addr ; ip -6 addr
nmcli device status                  # interfaces & status
nmcli connection show
ip route
```
## Configure static IPv4 (nmcli)  - assume connection ens160
```bash
nmcli connection modify ens160 ipv4.method manual \
  ipv4.addresses 192.168.1.50/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8 1.1.1.1"
nmcli connection up ens160           # activate
```
IPv6 example: `nmcli con mod ens160 ipv6.method manual ipv6.addresses fd00::50/64`
GUI: `nmtui` -> Edit a connection -> set IPv4 CONFIGURATION to Manual.
Back to DHCP: `nmcli con mod ens160 ipv4.method auto ipv4.addresses "" ipv4.gateway ""`.

## Verify
```bash
ip addr show ens160
ip route
cat /etc/resolv.conf
ping -c 4 192.168.1.1       # gateway
ping -c 4 8.8.8.8
ping -c 4 google.com        # DNS works
getent hosts google.com ; dig google.com ; hostname
```
## Manual config by editing file (RHEL 9)
Files are keyfiles: `/etc/NetworkManager/system-connections/ens160.nmconnection`
```
[ipv4]
method=manual
address1=192.168.1.50/24,192.168.1.1
dns=8.8.8.8;
```
```bash
chmod 600 /etc/NetworkManager/system-connections/ens160.nmconnection
nmcli connection reload
nmcli connection up ens160
```
(RHEL 7/8 legacy file: /etc/sysconfig/network-scripts/ifcfg-ens160 with BOOTPROTO=none, IPADDR, PREFIX, GATEWAY, DNS1; then `systemctl restart NetworkManager`.)
