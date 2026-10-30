# Q: a. Login as root  b. 3 workspaces  c. active network connections  d. active processes to abc.txt  e. switch root -> guest

## a. Login as root
- GUI: on login screen click **Not listed?** -> username `root` -> password.
- Terminal: `su -` (enter root password) or `sudo -i`
```bash
whoami        # root
id
```

## b. Create 3 workspaces (GNOME desktop)
1. Press **Super (Windows) key** -> Activities overview.
2. Workspaces appear on the right side; drag a window to the empty workspace at the bottom to create a new one.
3. Repeat until 3 workspaces exist. Switch with **Ctrl+Alt+Up/Down** or **Super+PageUp/PageDown**.
(Settings > Multitasking > "Dynamic workspaces" or "Fixed number = 3")
```bash
gsettings set org.gnome.mutter dynamic-workspaces false
gsettings set org.gnome.desktop.wm.preferences num-workspaces 3
```

## c. Active network connections
```bash
ss -tuln          # listening sockets
ss -tup           # established connections
netstat -tuln     # (needs net-tools: dnf install net-tools)
nmcli connection show --active
```

## d. Active processes -> abc.txt
```bash
ps -ef > abc.txt
# or: ps aux > abc.txt
cat abc.txt | head
```

## e. Switch root -> guest
```bash
useradd guest 2>/dev/null; passwd guest     # if guest doesn't exist
su - guest
whoami            # guest
exit              # back to root
```
