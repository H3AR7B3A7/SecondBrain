# SSL & TLS

```
ssh-keygen -t rsa
```

```
cat /home/thor/.ssh/mykey
```

```
ssh-copy-id -i ~/.ssh/mykey.pub thor@app01
```

```
sudo yum install -y openssl
```

```
cd /etc/httpd/csr
```

```
sudo openssl req -new -newkey rsa:2048 -nodes -keyout app01.key -out app01.csr
```

```
openssl req -noout -text -in app01.csr
```

Self signed cert:

```
cd /etc/httpd/certs
```

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout app01.key -out app01.crt
```

```
sudo vi /etc/httpd/conf.d/ssl.conf
```

```
sudo service httpd restart
```



---
