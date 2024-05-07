# Yum

The Yellowdog Updater Modified (YUM) is a free and open-source command-line package-management utility for computers running the Linux operating system using the RPM Package Manager. Though YUM has a command-line interface, several other tools provide graphical user interfaces to YUM functionality.

YUM allows for automatic updates and package and dependency management on RPM-based distributions. Like the Advanced Package Tool (APT) from Debian, YUM works with software repositories (collections of packages), which can be accessed locally or over a network connection.

```
yum repolist
```

```
yum install ansible
```

```
ls /etc/yum.repos.d/
```

```
cat /etc/yum.repos.d/CentOS-Base.repo
```

```
rpm -q openssh-server python3 ansible telnet
```

```
rpm -qa
```

```
sudo rpm -i /opt/ftp-0.17-67.el7.x86_64.rpm
```

```
rpm -qa | grep ftp
```

```
sudo rpm -e ftp-0.17-67.el7.x86_64
```

```
sudo rpm -e $(rpm -qa | grep ftp)
```

---
