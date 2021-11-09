# Kali
Kali Linux is a [[Debian]]-derived [[Linux]] distribution designed for digital forensics and penetration testing.  
It is maintained and funded by Offensive Security.  
  
It was developed by Mati Aharoni and Devon Kearns of Offensive Security through the rewrite of BackTrack,  
their previous information security testing Linux distribution based on Knoppix.  
Originally, it was designed with a focus on kernel auditing, from which it got its name Kernel Auditing Linux.  
The name is sometimes incorrectly assumed to come from Kali the Hindu goddess. The third core developer,  
Raphaël Hertzog, joined them as a Debian expert.  
  
## Tools  
Kali Linux has around 600 pre-installed penetration-testing programs (tools), including:   
- **Armitage**: A graphical cyber-attack management tool  
- **Nmap**: A port scanner  
- **Wireshark**: A packet analyzer  
- **Metasploit**: A penetration testing framework, awarded as the best penetration testing software  
- **John the Ripper**: A password cracker  
- **Sqlmap**: An automatic SQL injection and database takeover tool  
- **Aircrack-ng**: A software suite for penetration-testing wireless LANs  
- **Burp suite** and **OWASP ZAP**: Web application security scanners  
- ...  
  
## GUI  
Kali Linux uses XFCE as desktop environment by default, but other options are available during the OS installation.  
  
## Terminal  
Kali Linux uses qTerminal by default, but other options are available during the OS installation.  
  
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
>sudo apt-get update  
  
Our packages:  
>sudo apt-get upgrade -y  
  
Our OS:  
>sudo apt-get dist-upgrade -y
  
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
#### Preload  
> sudo apt-get install preload  
  
#### Bleachbit  
> sudo apt-get install bleachbit  
  
#### Scrub  
> sudo apt-get install scrub   
#### Lolcat  
> sudo apt-get install lolcat  
  
#### Figlet + More Figlet Fonts  
> sudo apt-get install figlet  
  
> cd /usr/share  
  
> sudo git clone https://github.com/xero/figlet-fonts  
  
> sudo mv figlet-fonts/* figlet && sudo rm -rf figlet-fonts  
  
> showfigfonts  
  
#### Cmatrix  
> sudo apt-get install cmatrix  
  
#### Tor  
> sudo apt-get install tor  
  
#### Proxychains  
> sudo apt-get install proxychains  
  
> sudo updatedb  
  
#### Chkrootkit  
> sudo apt-get install chkrootkit  
  
#### Metagoofil  
> sudo apt-get install metagoofil  
  
#### Libre Office  
> sudo apt-get install libreoffice  
  
#### Discover  
> git clone https://github.com/leebaird/discover.git

## Practical Examples  
An arbitrary list of practical working examples on a Kali system.  
  
  
### Add Command Line Banner  
#### Kali 2021.1 and earlier  
>sudo chmod a+w /etc/bash.bashrc  
  
>nano /etc/bash.bashrc  
  
In nano append at bottom of file:  
```  
# Figlet banner  
figlet -f slant "H3AR7B3A7" | lolcat  
```  
  
#### Kali 2021.2  
>nano .zshrc  
  
In nano append at bottom of file:  
```  
# Figlet banner  
figlet -f slant "H3AR7B3A7" | lolcat  
```  
  
### (Re-)Configure SSH  
```  
cd /etc/ssh  
sudo mkdir old_ssh_keys  
sudo mv ssh_host_* old_ssh_keys  
sudo dpkg-reconfigure openssh-server  
service ssh start  
netstat -antp  
service ssh stop  
```  
  
### Using Tor & Proxychains  
```  
nano /etc/proxychains.conf  
```  
In nano:  
- Uncomment: dynamic_chain  
- Comment-out: strict_chain  
- Append at bottom: socks5  127.0.0.1 9050  
```  
service tor start  
service tor status  
proxychains firefox www.whatismyip.com  
service tor stop  
```


---
#Linux #Kali