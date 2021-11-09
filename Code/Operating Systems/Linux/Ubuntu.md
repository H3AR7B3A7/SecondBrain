# Ubuntu  
Ubuntu is a Linux distribution based on [[Debian]] and composed mostly of free and open-source software.  
Ubuntu is officially released in three editions: Desktop, Server, and Core for Internet of things devices and robots.  
All the editions can run on the computer alone, or in a virtual machine. Ubuntu is a popular operating system  
for cloud computing, with support for OpenStack. Ubuntu's default desktop has been GNOME, since version 17.10.  
  
  
## Ubuntu Server  
Like other distributions, Ubuntu comes in two editions:  
- Desktop  
- Server  
  
The server edition has no GUI, instead it only uses the shell.  
It is a lean (1 GB of disc space) efficient operating system, ideally only rarely requiring updates.  
It has the same release schedule, but only LTS releases should be considered for server stability.  
  
The installation differs significantly from the desktop version. However, it offers a lot of build in functionality,  
like security and different software (to set up: webserver, mail server, files server, ...).  
  
OpenSSH allows for controlling the server securely from a different machine.  
  
## GUI  
Ubuntu uses GNOME as desktop environment by default for most installations, which is loosely based on the Apple ecosystem.  
  
## Terminal  
Ubuntu uses GNOME Terminal by default.  
  
## Package Manager  
APT

## Installations  
### Before Starting  
When uncertain about a packet name we can use:  
> apt search name  
  
Installing files can only be done by a super user.  
We can either elevate our command temporarily by using:  
> sudo  
  
Or by elevating ourselves to super user (not recommended):  
> sudo su  
  
#### Updating  
Before installing anything we might want to update the *advanced packaging tool*:  
> sudo apt-get update   
Our packages:    
> sudo apt-get upgrade -y   
Our OS:  
> sudo apt-get dist-upgrade -y  
  
  
### Common Commands  
#### Installing Packages  
> sudo apt-get install package-name package-name ...  
  
#### Installing DEB Packages  
> sudo dpkg -i path_to_deb_file.deb  
  
#### Download Packages  
> sudo apt-get install --download-only package-name package-name ...  
  
#### Removing Software  
To remove packages installed with APT:  
> sudo apt-get remove package-name package-name ...  
  
#### Clean Up Downloaded Packages  
> sudo apt-get clean  
  
  
### Common Installations  
#### Git  
> sudo apt-get install git  
  
#### Java  
[Download Oracle JDK for Debian](https://www.oracle.com/java/technologies/javase-downloads.html)  
  
> sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-16.0.1/bin/java 1  
  
> sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-16.0.1/bin/javac 1  
  
Or just check your version and follow instructions for OpenJDK:  
> java --version  
  
#### NodeJS & NPM  
> sudo apt-get install nodejs  
  
> sudo apt-get install npm  
  
Updating:  
> sudo npm install npm@latest -g  
  
> sudo npm install nodejs@latest -g  
  
#### NGINX  
> sudo apt-get install nginx  
  
#### OpenSSH  
Server:  
> sudo apt-get install openssh-server  
  
Client:  
> sudo apt-get install openssh-client  
  
#### Terminator  
> sudo apt-get install terminator  
  
#### ZSH + Oh My ZSH  
> sudo apt-get install zsh  
  
> chsh -s $(which zsh)  
  
> sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"  
  
For more customization tips go [here](https://maxim-danilov.github.io/make-linux-terminal-great-again/).  
  
#### Powerline Fonts  
> sudo apt-get install fonts-powerline

## Practical Examples  
An arbitrary list of practical working examples on an Ubuntu system.  
  
### Hosting a Website Using NGiNX  
```  
sudo mkdir -p /var/www/mysite.net  
cd IdeaProjects/MySite  
sudo cp -r * /var/www/mysite.net/  
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/mysite.net  
sudo nano /etc/nginx/sites-available/mysite.net  
sudo ln -s /etc/nginx/sites-available/mysite.net /etc/nginx/sites-enabled/  
sudo rm /etc/nginx/sites-enabled/default  
sudo ls /etc/nginx/sites-enabled/mysite.net  
sudo service nginx restart  
```  
  
  
### Connecting to Server Using SSH Key  
```  
ssh-keygen -b 2048 -t rsa -C name@company.com  
ls .ssh  
cat .ssh/id_rsa.pub  
ssh-copy-id -i .ssh/id_rsa.pub name@172.16.141.186  
ssh name@172.16.141.186  
```  
  
  
### Securely Transferring Files to Server Using SSH and SCP  
Remote:  
```  
nano /etc/nginx/sites-available/mysite.net  
sudo chmod a+w /etc/nginx/sites-available/  
sudo chmod a+x /etc/nginx/sites-available/  
scp /home/name/mysite.net name@172.16.141.186:/etc/nginx/sites-available  
```  
  
Server:  
```  
ls -l /etc/nginx/sites-available/  
sudo chown root /etc/nginx/sites-available/mysite.net  
sudo ln /etc/nginx/sites-available/mysite.net /etc/nginx/sites-enabled/  
sudo rm /etc/nginx/sites-enabled/default  
sudo ls /etc/nginx/sites-enabled/  
sudo service nginx restart  
```  
  
#### Using SSH Config  
Remote:  
```  
touch .ssh/config  
nano .ssh/config  
```  
  
Nano:  
```  
Host myServer  
	HostName        172.16.141.186
	User            name
	IdentityFile    ~/.ssh/id_rsa
```  
  
Remote Server:  
```  
ssh myServer  
sudo mkdir -p /var/www  
sudo chmod a+w /var/www/  
sudo chmod a+x /var/www/  
```  
Remote:  
```  
scp -r /var/www/mysite.net myServer:/var/www/mysite.net/  
```



---
#Ubuntu