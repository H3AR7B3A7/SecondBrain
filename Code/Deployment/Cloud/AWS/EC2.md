# EC2

## Connect to instance:

### Putty:

- Make sure Putty is up to date
- Make sure to use a .ppk
	- Convert key to ppk if needed with: puttygen and SSH-1 (RSA)

### SSH:

```
ssh -i C:\Users\Admin\.ssh\AWStest.pem INSTANCE_IPV4_DNS.amazonaws.com
```

### AWS CLI:

- Make sure a user exists with a `aws_access_key_id` and `aws_secret_access_key`
- run aws configure and set `aws_access_key_id`, `aws_secret_access_key` and zone
	- Or change them in: `C:\Users\Admin\.aws\credentials`
- In IAM assign `AdministratorAccess` permission to the user

```
aws ec2-instance-connect ssh --instance-id INSTANCE_ID --private-key-file PATH_TO_PRIVATE_KEY
```

### Session Manager:

- Create a new role in IAM
- AWS service: EC2
- Permission policy: AmazonSSMManagedInstanceCore
- Give it a name
- Create

## Copy files to EC2 instance

```
scp -i "C:\Users\Admin\.ssh\AWStest.pem" FILE_LOCATION INSTANCE_IPV4_DNS.amazonaws.com:/home/ec2-user
```


## Create SystemD Service

In `/etc/systemd/system/`:

> sudo nano demo-app.service 

```
[Unit]
Description=My Demo App
After=syslog.target network.target

[Service]
WorkingDirectory=/home/ec2-user
ExecStart=/usr/bin/java -jar demo-1.jar
KillMode=process
User=ec2-user
Restart=on-failure

[Install]
WantedBy=multi-user.target

```


> sudo systemctl start demo-app



---

#Cloud #AWS #EC2
