## Exercise 1

```
sudo yum install -y mariadb-server
```

```
sudo systemctl start mariadb
```

```
sudo systemctl enable mariadb
```

```
sudo mysql
```

```
CREATE DATABASE ecomdb;
```

```
CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
```

```
GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
```

```
FLUSH PRIVILEGES;
```

```
sudo mysql < /opt/db-load-script.sql
```

```
sudo yum install -y httpd php php-mysqlnd
```

```
sudo sed -i 's/index.html/index.php/g' /etc/httpd/conf/httpd.conf
```

```
sudo systemctl start httpd ; sudo systemctl enable httpd
```

```
sudo yum install -y git; sudo git clone https://github.com/kodekloudhub/learning-app-ecommerce.git /var/www/html/
```

```
sudo sed -i 's/172.20.1.101/localhost/g' /var/www/html/index.php
```

## Exercise 2

```
ssh db
```

```
sudo yum install -y mariadb-server
```

```
sudo systemctl start mariadb
```

```
sudo systemctl enable mariadb
```

```
sudo mysql
```

```
CREATE DATABASE ecomdb;
```

```
CREATE USER 'ecomuser'@'%' IDENTIFIED BY 'ecompassword';
```

```
GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'%';
```

```
FLUSH PRIVILEGES;
```

```
sudo mysql < /opt/db-load-script.sql
```

```
exit
```

```
sudo yum install -y httpd php php-mysqlnd
```

```
sudo sed -i 's/index.html/index.php/g' /etc/httpd/conf/httpd.conf
```

```
sudo systemctl start httpd; sudo systemctl enable httpd
```

```
sudo yum install -y git; sudo git clone https://github.com/kodekloudhub/learning-app-ecommerce.git /var/www/html/
```

```
sudo sed -i 's/172.20.1.101/db/g' /var/www/html/index.php
```




---
