# IPs & Ports

## Apache Tomcat

```
sudo sed -i 's/8080/9090/g' apache-tomcat-8.5.53/conf/server.xml
```

```
sudo ./apache-tomcat-8.5.53/bin/startup.sh
```

## Flask

```
sudo sed -i 's/0.0.0.0/127.0.0.1/g;s/8080/5000/g' /opt/simple-webapp-flask/app.py;
```

```
cd /opt/simple-webapp-flask/; nohup python app.py &
```

```
sudo sed -i 's/127.0.0.1/0.0.0.0/g' /opt/simple-webapp-flask/app.py
```

```
pkill python; cd /opt/simple-webapp-flask/; nohup python app.py &
```

```
curl app01:5000
```

```
sudo sed -i 's/172.16.239.30/0.0.0.0/g' /opt/simple-webapp-flask/app.py; sudo pkill python; cd /opt/simple-webapp-flask/; nohup python app.py &
```

```
curl app01:5000 ; curl 172.16.239.30:5000
```

