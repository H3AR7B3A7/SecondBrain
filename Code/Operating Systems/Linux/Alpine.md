# About Alpine  
Alpine Linux is a [[Linux]] distribution based on musl and BusyBox, designed for security, simplicity, and resource efficiency.   
It uses OpenRC for its init system and compiles all user-space binaries as position-independent executables with stack-smashing protection.  
  
*Because of its small size, it is commonly used in containers providing quick boot-up times.*  
  
## GUI  
By default, Alpine doesn't include any GUI.  
  
## Terminal  
By default, there is no terminal, just the sh shell (no bash).  
  
## Package Manager  
APK

## Installations  
### Before Starting  
#### Update APT  
> apk update  
  
  
### Common Commands  
#### Install Package  
> apk add package-name package-name ...  
  
#### Download Package  
> apk fetch package-name package-name ...  
  
#### Remove Package  
> apk del package-name package-name ...  
  
#### Clean Up Downloaded Packages  
*Alpine cleans up packages automatically.*


---
#Linux