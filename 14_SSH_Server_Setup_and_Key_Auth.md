# Q: Enable and configure SSH server / steps for remote access / key-based authentication

## 1. Install, enable and start
```bash
dnf install openssh-server openssh-clients -y
systemctl enable --now sshd
systemctl status sshd
ss -tlnp | grep 22
```
## 2. Firewall
```bash
firewall-cmd --permanent --add-service=ssh
firewall-cmd --reload
```
## 3. Configure /etc/ssh/sshd_config
```bash
vi /etc/ssh/sshd_config
```
Useful settings:
```
Port 22
PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes
AllowUsers guest
```
```bash
sshd -t                      # syntax check
systemctl restart sshd
```
If you change the port: `semanage port -a -t ssh_port_t -p tcp 2222` and open it in firewall.

## 4. Connect from client (second VM or host)
```bash
ip a                         # IP of server
ssh guest@<server-ip>
ssh -p 2222 guest@<server-ip>
exit
```
## 5. Key-based authentication (on client)
```bash
ssh-keygen -t rsa -b 4096           # (ed25519 also fine) enter a passphrase
ssh-copy-id guest@<server-ip>       # copies public key to ~/.ssh/authorized_keys
ssh guest@<server-ip>               # logs in with key (asks key passphrase only)
```
Manual alternative: append `~/.ssh/id_rsa.pub` to server's `~/.ssh/authorized_keys` with permissions `chmod 700 ~/.ssh; chmod 600 ~/.ssh/authorized_keys`.

Optional hardening: set `PasswordAuthentication no` and restart sshd (only after key login works!).

Other: `scp file guest@ip:/tmp`, `sftp guest@ip`.
## Viva
- SSH port 22/TCP, encrypted replacement for telnet. Private key stays on client; public key goes to server.
