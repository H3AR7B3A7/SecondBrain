# Linux

Linus Torvalds created his own kernel known as Linux. The kernel is the part of an OS that facilitates interactions between hardware and software.

At the time, many [[GNU]] 'pieces' were complete, but it lacked a kernel. Torvalds combined his kernel with the existing GNU components to create a full [[Unix]]-like operating system. It is considered [[Unix]]-like, because True-[[Unix]] was proprietary and Linux is open source.

Today there are nearly a thousand different Linux distributions (or distros) available:
- Fedora
- Debian
- Ubuntu
- Slackware
- ...

## Services

Start service

```
sudo systemctl start someService
```

Enable service to start on startup

```
sudo systemctl enable someService
```

Check the value for the directive `ExecStartPre` / `ExecStart` / ...

```
/usr/lib/systemd/system/app.service`  
```

```
systemctl cat app.service
```

## Switching and Routing

Assign new IPs to `app` servers.

```
ssh app01
```

```
sudo ip addr add 172.16.238.15/24 dev eth0
```


```
ssh app02
```

```
sudo ip addr add 172.16.238.16/24 dev eth0
```


```
ssh app03
```

```
sudo ip addr add 172.16.239.15/24 dev eth0
```


```
ssh app04
```

```
sudo ip addr add 172.16.239.16/24 dev eth0
```

Assign a new IP address `172.16.239.10/24` to `jump host`

```
sudo ip addr add 172.16.239.10/24 dev eth0
```

Add a routing table entry in app01 and app02 hosts so that these hosts can reach app03 and app04 hosts via jump host.
On app01 and app02:

```
sudo ip route add 172.16.239.0/24 via 172.16.238.10
```

Add a routing table entry in app03 and app04 hosts so that these hosts can reach app01 and app02 hosts via jump host.
On app03 and app04:

```
sudo ip route add 172.16.238.0/24 via 172.16.239.10
```

## DNS

Information about hosts:

```
sudo vi /etc/hosts
```

Information about dns server i.e nameserver

```
sudo vi /etc/resolv.conf
```

Getting information from the DNS server

```
nslookup [option] [domain]
```


---
#Linux