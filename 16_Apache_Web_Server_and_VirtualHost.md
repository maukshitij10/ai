# Q: Configure basic Apache server  /  Apache virtual host

## A. Basic Apache
```bash
dnf install httpd -y
systemctl enable --now httpd
systemctl status httpd
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
echo "<h1>Welcome to my Apache Server</h1>" > /var/www/html/index.html
curl http://localhost
```
Open browser: `http://<server-ip>`.
Main config: `/etc/httpd/conf/httpd.conf`, document root: `/var/www/html`, logs: `/var/log/httpd/`.
If page forbidden: `restorecon -Rv /var/www/html` ; `setenforce 0` (temp, for testing only).

## B. Virtual host (name based)
```bash
mkdir -p /var/www/site1.com/html
echo "<h1>Site 1 Working</h1>" > /var/www/site1.com/html/index.html
mkdir -p /var/www/site2.com/html
echo "<h1>Site 2 Working</h1>" > /var/www/site2.com/html/index.html
restorecon -Rv /var/www
```
Create `/etc/httpd/conf.d/site1.conf`:
```
<VirtualHost *:80>
    ServerName site1.com
    ServerAlias www.site1.com
    DocumentRoot /var/www/site1.com/html
    ErrorLog /var/log/httpd/site1_error.log
    CustomLog /var/log/httpd/site1_access.log combined
</VirtualHost>
```
Same for `site2.conf` with site2.com.
```bash
echo "<server-ip> site1.com site2.com" >> /etc/hosts     # name resolution
httpd -t                       # Syntax OK
systemctl restart httpd
curl http://site1.com
curl http://site2.com
```
## Viva
- Name-based vhosts: many sites on one IP. Port 80 HTTP / 443 HTTPS. Service name `httpd`.
