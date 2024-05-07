# Common Installations on Linux Machines

## Install Java

In /opt:

```
sudo curl https://download.java.net/java/GA/jdk20/bdc68b4b9cbc4ebcb30745c85038d91d/36/GPL/openjdk-20_linux-x64_bin.tar.gz --output /opt/openjdk-20_linux-x64_bin.tar.gz
```

```
sudo tar -xf /opt/openjdk-20_linux-x64_bin.tar.gz -C /opt/
```

```
/opt/jdk-20/bin/java -version
```

_"/usr/local/*" is typically used for installing software that has been built locally._

Set path variable:

```
export PATH=$PATH:/opt/jdk-20/bin
```

## Install Ant

```
sudo yum install -y ant
```

```
sudo ant
```

## Install Maven

```
sudo yum install -y maven
```

```
sudo mvn package
```

```
java -cp /opt/maven/my-app/target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App
```

## Install Node 14

```
curl -sL https://rpm.nodesource.com/setup_14.x | sudo bash -
```

```
sudo yum install -y nodejs
```

```
node -v
```

```
npm -v
```

## Install Python 3.6

```
sudo yum install -y python36
```

```
sudo pip install -r requirements.txt
```

## Install Apache Webserver

```
sudo yum install -y httpd
```

```
sudo systemctl start httpd
```

## Install Apache Tomcat

```
curl https://downloads.apache.org/tomcat/tomcat-8/v8.5.100/bin/apache-tomcat-8.5.100.tar.gz -o apache-tomcat-8.5.100.tar.gz
```

```
sudo tar -xvf apache-tomcat-8.5.100.tar.gz
```

```
sudo mv apache-tomcat-8.5.100 /opt/apache-tomcat-8
```

```
sudo /opt/apache-tomcat-8/bin/startup.sh
```

```
curl localhost:8081; ps -ef | grep tomcat
```

To change the port :
  
```
sudo sed -i 's/8081/9090/g' /opt/apache-tomcat-8/conf/server.xml;
```  
  
```
sudo /opt/apache-tomcat-8/bin/shutdown.sh
```  

```
sudo /opt/apache-tomcat-8/bin/startup.sh
```  
  
```
curl localhost:9090; ps -ef | grep tomcat
```

```
sudo mv /opt/sample.war /opt/apache-tomcat-8/webapps/
```

## NodeJs

```
sudo npm i -g pm2
```

```
pm2 start app.js
```

```
pm2 delete app.js
```

```
pm2 start app.js -i 4
```

## Install MariaDB Server:

```
sudo yum install mariadb-server
```

```
sudo service mariadb start
```

```
mysql -u root
```

and then run the following queries:

```
USE mysql;
```

```
UPDATE user SET password=PASSWORD('P@ssw0rd123') WHERE User='root' AND Host = 'localhost';
```

```
FLUSH PRIVILEGES;
```

```
USE kk_db;
```

```
SHOW Tables;
```

```
CREATE USER 'kk_user'@'localhost' IDENTIFIED BY 'S3cure#3214';
```

```
GRANT ALL PRIVILEGES ON kk_db.* TO 'kk_user'@'localhost';
```

## Install MySQL Server:

```
sudo yum install https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
```

```
sudo yum install mysql-community-server
```

```
sudo service mysqld start
```

```
sudo grep 'temporary password' /var/log/mysqld.log
```

```
mysql -u root -p
```

```
sudo grep 'temporary password' /var/log/mysqld.log
```

and then run the following queries:

```
SET PASSWORD = PASSWORD('P@ssw0rd123');
```

```
FLUSH PRIVILEGES;
```


---
#Linux
