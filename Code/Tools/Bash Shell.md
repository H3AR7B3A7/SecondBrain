# Bash Shell 
Bash commands with some of their arguments on the consecutive lines.  
  
We can get a list of commands using help:  
  
> help  
  
We can also get more information on arguments using help as an argument:  
  
> command --help  
  
Or the version of the software providing a specific command, if any:  
  
> command --version > command --v  
  
  
## Terminal Shortcuts  
- <kbd>Arrow Up / Down</kbd> : Navigate command history    

- <kbd>Tab</kbd> : Autocomplete    

- <kbd>Alt</kbd> + <kbd>F10</kbd> : Maximize window    

- <kbd>Ctrl</kbd> + <kbd>L</kbd> : Clear    

- <kbd>Ctrl</kbd> + <kbd>C</kbd> : Kill current running task    

- <kbd>Ctrl</kbd> + <kbd>D</kbd> : Exit shell    

- <kbd>Ctrl</kbd> + <kbd>Z</kbd> : Current running task to background    

- <kbd>Alt</kbd> + <kbd>F</kbd> : Move cursor forward one word    

- <kbd>Alt</kbd> + <kbd>B</kbd> : Move cursor back one word    

- <kbd>Esc</kbd> + <kbd>T</kbd> : Swap last two words before cursor    

- <kbd>Ctrl</kbd> + <kbd>A</kbd> : Go to the beginning of the line    

- <kbd>Ctrl</kbd> + <kbd>E</kbd> : Go to the end of the line    

- <kbd>Ctrl</kbd> + <kbd>W</kbd> : Delete word before cursor    

- <kbd>Ctrl</kbd> + <kbd>K</kbd> : Clear line behind cursor    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>T</kbd> : Open new tab    
  
  
## Terminator Specific Shortcuts  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>E</kbd> : Vertical split    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>O</kbd> : Horizontal split    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> : Previous screen    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>N</kbd> : Next screen    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>W</kbd> : Close screen    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Q</kbd> : Quit terminal    

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>X</kbd> : Enlarge current screen  
  
  
## Common Commands  
### System  
#### Open New Tab in Console  
> --tab
  
#### Exit Console  
> exit  
  
#### Reboot System  
> reboot  
  
#### Shutdown System  
> shutdown  
> -h  
  
#### Change Timezone  
> rm /etc/localtime  
  
> ln -s /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime  
  
  
### Information  
  
#### Username:  
> whoami  
  
#### System name:  
> hostname  
  
#### Current date:  
> date  
  
#### Calendar  
> cal  
  
#### Manual:  
> sudo apt-get install man-db  
  
> man > ls > ...  
  
#### Network routing:  
> ip rout show  
  
#### Check for DHCP server in network:  
> sudo dhclient  
  
#### Lookup IP address:  
> ip addr  
  
#### Network interfaces and usage  
> netstat -i  
  
#### Open and listening ports  
> netstat -l  
  
> ss -i  
  
#### Get DNS ip  
> host google.com  
  
#### Check if network address is live  
> ping 8.8.8.8  
  
#### Current DNS configurations  
> systemd-resolve --status  
  
  
### Navigate & Open  
  
#### List content:  
> ls > /bin/p* > -a > -l -G > -C -b > -R  
  
> ll  
  
> dir  
  
#### Print working directory:  
> pwd  
  
#### Change directory  
> cd  
  
#### Locate file  
> sudo apt-get install mlocate  
  
> locate filename  
  
#### Print files to screen  
> cat  
  
#### Print last X lines of file  
> tail > file.txt > -n 1 > -f  
  
#### Print file in pages  
> less  
  
Shortcuts in less:  
- Forward / backward one page    
    f  
    b  
- Forward / backward half a page    
    Ctrl + D    
    Ctrl + U  
- Beginning / end of file    
    Shift + <    
Shift + >  
- Search for pattern    
    /  
- Mark letter (x)    
mx  
- Goto marked letter (x)    
'x  
  
#### Search directory tree  
> find > pattern > -maxdepth 2 > -mindepth 1  
> -type f  
> -perm 775  
> -user name  
> -exec cp '{}' /some_path \;  
  
#### Filter / search  
> grep > filename > phrase > -w > -i  
  
#### List loaded modules  
> lsmod  
  
#### Load module  
> modprobe name  
  
  
### Create & Alter  
  
#### Elevating to super user  
> sudo su  
  
To drop elevation:  
> exit  
  
#### Non-Interactive Download  
> wget  
> wordpress.org/latest.tar.gz  
  
#### Creating (symbolic) link  
> ln /target name  
  
> ln -s /some/very/long/path /target  
  
#### Changing file rights  
> chmod > 777 file.txt  
  
![Chmod](img/chmod.png)  
  
#### Changing owner  
> chown > username  
  
#### Create file  
> touch > file.txt  
  
#### Edit file  
> vi > file.txt  
  
> vim > file.txt  
  
*More info: [Vim cheatsheet](https://vim.rtorr.com)  
  
> nano > file.txt  
  
#### Edit stream  
> sed > -i > 's/regex/replace/g' filename  
  
#### Scan for pattern and process text  
> awk > -F " " 'BEGIN { print "Date\t\tPrice\t\tVolume" }; NR > 1 { print $1 "\t" $2 "\t" $7 } ' filename  
```  
# AWK Script  
BEGIN {  
 FS=" "; OFS="\t\t"; print Date\t\tPrice\t\tVolume" print "----\t\t-----\t\t-----"};  
NR > 1 {  
 print $1, $2, $7;};  
```  
> awk -f awk_script  
  
#### Zip / Unzip file  
Zip:  
> zip name.zip filename filename ...  
  
> unzip name.zip  
  
Gzip:  
> gzip filename  
  
> gunzip filename  
  
Tar:  
> tar cvzf name.tar fileOrFoldername  
  
> tar -xvf name.tar  
  
> tar cvzf name.tar.gz fileOrFoldername  
  
> tar -xvf name.tar.gz  
  
> tar cvzf name.tgz fileOrFoldername  
  
> tar -xvf name.tgz  
  
*More info: [Zip Format Differences](https://upengareri.github.io/compression_and_archiving/)  
  
  
## Command Insertion  
List kernel module files for current kernel version.  
> ls /lib/modules\`uname -r\`  
  
  
## Command Chaining  
Append contents of group filtering only lines with username to file.  
> cat /etc/group | grep name >> file  
  
Overwrite contents of group filtering only lines with username to file.  
> cat /etc/group | grep name > file  
  
Cut contents using colon as field delimiter keeping the 3d field and sorting them in natural order.  
> cut -d: -f3 /etc/group | sort -n  
  
Cut contents using colon as field delimiter keeping the 3d field and sorting them in descending order.  
> cut -d: -f3 /etc/group | sort -rn  
  
Find everything in /var/log starting with syslog of type file, print with null chars for new line and individually run each with an elevated command to grant read permission to all users.  
> find /var/log/syslog* -type f -print0 | xargs -0 sudo chmod a+r  
  
Find everything in /var/log starting with syslog and ending on .gz of type file, print with null chars for new line and individually run each with an elevated command to unzip.  
> find /var/log/syslog*.gz -type f -print0 | xargs -0 sudo gunzip  
  
Find everything in /var/log starting with syslog of type file, print with null chars for new line and individually run each to concatenate in one long string and look for matching lines for "NetworkManager" that are warnings.  
> find /var/log/syslog* -type f -print0 | xargs -0 cat | grep "NetworkManager.*warn"  
  
Get IP-addresses from network interfaces, in the first result merge spaces, cut in string parts on the spaces and give me the 3d string.  
> ifconfig | grep "inet " | head -n 1 | tr -s ' ' | cut -d ' ' -f 3  
  
  
## Standard Streams  
- Standard Input (stdin): 1  
- Standard Output (stdout): 1  
- Standard Error (stderr): 2