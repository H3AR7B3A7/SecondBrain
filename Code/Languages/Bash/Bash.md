# Bash
Anything you can normally run on the command line can also be put into a script for repeated use.  
  
  
## Running Scripts  
A user will not have permission to run a saved script by default. We need to grant it first:  
  
>chmod a+x script.sh  
  
To run the script:  
>./script.sh  
  
  
## Scheduling Scripts  
To schedule scripts with CRON:  
>crontab -e  
  
Edit the file to run a script every minute:  
```  
* * * * * ~/script.sh  
```  
  
  
## Example Scripts  
### APT update automation  
```  
#!/bin/bash  
sudo apt-get udpate &&  
sudo apt-get upgrade -y &&  
sudo apt-get dist-upgrade -y  
```  
  
### Print sum of two inputs  
```  
#!/bin/bash  
declare -i number1  
declare -i number2  
declare -i total  
echo "Enter a number..."  
 read number1echo "Enter next number..."  
 read number2total=$number1+$number2  
echo "The sum of these numbers equals " $total  
exit 0  
```  
  
### Print index in a loop  
```  
#!/bin/bash  
for i in {0..10..2}  
 do echo "We've been through this $i times!" done```  
  
### Print to multiple files  
```  
#!/bin/bash  
for filename in file1 file2 file3  
 do echo "Uhn tiss..." >> $filename done```  
  
### If condition is true ... else ...  
```  
#!/bin/bash  
echo "What is your favorite color? "  
read text1  
echo "What is your friend's favorite color? "  
read text2  
 if test $text1 != $text2; then echo "I guess opposites attract." else echo "You two do think alike!" fiexit 0  
```  
  
### Print counter while counter is greater than 2  
```  
#!/bin/bash  
declare -i counter  
counter=10  
 while [ $counter -gt 2 ];do echo "The counter is $counter" counter=counter-1 doneexit 0  
```  
  
### Reply to input using a switch case  
```  
#!/bin/bash  
echo "What's the weather going to be like tomorrow?"  
read weather  
 case $weather in                sunny | warm ) echo "Nice! I love it when it's $weather."  
 ;; cloudy | cool ) echo "Not bad... $weather is ok." ;; rainy | cold ) echo "Yuk! $weather weather is depressing." ;; * ) echo "Sorry, I'm not familiar with that weather system." ;; esacexit 0  
```  
  
### Print IP  
```  
#!/bin/bash  
  
originalAddress=$(   ifconfig |   
                    grep "inet " |   
                    head -n 1 |   
                    tr -s ' ' |   
                    cut -d ' ' -f 3)  
  
echo $originalAddress >> ~/Desktop/ip.txt  
```  
  
### Print date and IP in an endless while loop  
```  
#!/bin/bash  
  
while [ : ]  
do  
  
 originalAddress=$(   ifconfig |                  grep "inet " |   
                  head -n 1 |   
                  tr -s ' ' |   
                  cut -d ' ' -f 3)  
  
 echo "$(date) $originalAddress" >> ~/Desktop/ip.txt    sleep 10  
done  
```  
To watch the output updating every 10s:  
>tail ip.txt -f



---
#Bash