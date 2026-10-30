# Q: rpm and yum/dnf - install/remove wget, mysql, nmap, ssh; repos; query; update

## YUM / DNF (yum is alias of dnf on RHEL 8/9)
```bash
yum repolist                       # configured repos
yum repolist all
cat /etc/yum.repos.d/*.repo
yum search wget                    # search
yum info wget                      # package info
yum install wget -y
yum install nmap -y
yum install openssh-server openssh-clients -y
yum install mysql-server -y        # (mysql / mariadb-server on older)
yum update wget                    # update one package
yum update -y                      # update all
yum remove wget nmap -y
yum list installed | grep wget
yum history
```
Verify: `wget --version`, `nmap --version`, `rpm -q wget`.

## RPM
```bash
rpm -qa                            # all installed packages
rpm -qa | grep wget
rpm -qi wget                       # info
rpm -ql wget                       # files in package
rpm -qf /usr/bin/wget              # which package owns file
rpm -ivh package.rpm               # install local file
rpm -Uvh package.rpm               # upgrade
rpm -e wget                        # remove
rpm -V wget                        # verify
```
Note: rpm does not resolve dependencies; yum/dnf does.
If no subscription, create a local repo (see file 32) using the RHEL ISO.
