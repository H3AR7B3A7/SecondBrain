# Windows Terminal

[Official Documentation](https://docs.microsoft.com/en-gb/windows/terminal/) [Download](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab)  
  
Windows Terminal is a multi-tabbed command-line front-end that Microsoft has developed for [[Windows]] as a replacement for Windows Console. It can run any command-line app, including all Windows terminal emulators, in a separate tab. It is pre-configured to run Command Prompt, [[PowerShell]], WSL, SSH, and [[Azure]] Cloud Shell Connector.
  

### Profiles

  
Other shells that were added include: PowerShell 7, Git Bash, Python, JShell  
These tools and/or languages will have to be installed separately.  
  
- [Powershell 7](https://github.com/PowerShell/PowerShell)  
- [Git Bash](https://git-scm.com/downloads)  
- [Python Shell](https://www.python.org/downloads/)  
- [JShell](https://www.oracle.com/java/technologies/javase-downloads.html)  
  
  

### Use as Administrator

  
To start your terminal elevated from your taskbar just create a shortcut with the following as location:  
  
 C:\Windows\System32\cmd.exe /c start /b wt  
Icons modified to make your terminal look better, are provided in the [img](https://github.com/H3AR7B3A7/WindowsTerminalAndPowershell/tree/master/img) folder of this repository as well.  
  

### Start with Keyboard Shortcut

Find the location to wt.exe:

![[Pasted image 20240501210201.png]]

Create a shortcut to it in:
> C:/ProgramData/Microsoft/Windows/Start Menu/Programs

_Edit the properties to set a keyboard shortcut._


### Quake

Under `settings > actions`: Find the open/close quake shortcut


### Running .bat Files in Terminal

In regedit navigate to:  
  
 HKEY_CLASSES_ROOT\batfile\shell\open\command  
Change the default value to:  
  
 "C:\Users\StevenD'Hondt\AppData\Local\Microsoft\WindowsApps\wt.exe" -d . -p "Command Prompt" "%1" %*  
  

### Settings

```json
{  
  "$schema": "https://aka.ms/terminal-profiles-schema",  
  
  "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",  
  
  // You can add more global application settings here.  
  // To learn more about global settings, visit https://aka.ms/terminal-global-settings  
  
  // If enabled, selections are automatically copied to your clipboard.  
  "copyOnSelect": false,  
  
  // If enabled, formatted data is also copied to your clipboard  
  "copyFormatting": false,  
  
  // A profile specifies a command to execute paired with information about how it should look and feel.  
  // Each one of them will appear in the 'New Tab' dropdown,  
  //   and can be invoked from the commandline with `wt.exe -p xxx`  
 // To learn more about profiles, visit https://aka.ms/terminal-profile-settings  
  "profiles": {  
    "defaults": {  
      // Put settings here that you want to apply to all profiles.  
      "acrylicOpacity": 0.5,  
      "useAcrylic": true,  
      "colorScheme": "Tango Dark",  
      "backgroundImage": "C:\\Users\\Admin\\Pictures\\Saved Pictures\\terminalBG.png",  
      "backgroundImageOpacity": 0.5,  
      "padding": "0, 0, 0, 0",  
      "closeOnExit": true,  
      "fontFace": "Consolas",  
      "fontSize": 12,  
      "cursorShape": "bar",  
      "cursorColor": "#FFFFFF",  
      "snapOnInput": true,  
      "historySize": 9001,  
      "startingDirectory": "C:\\" //"%USERPROFILE%"  
    },  
    "list": [  
 {  
        // Make changes here to the POWERSHELL 7 profile.  
        "tabTitle": "POWERSHELL",  
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",  
        "hidden": false,  
        "name": "PowerShell 7",  
        "commandline": "pwsh.exe -NoLogo",  
        "source": "Windows.Terminal.PowershellCore"  
      },  
      {  
        // Make changes here to the OLD POWERSHELL profile.  
        "tabTitle": "POWERSHELL (OLD)",  
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",  
        "name": "PowerShell (OLD)",  
        "commandline": "powershell.exe -NoLogo",  
        "hidden": false  
      },  
      {  
        // Make changes here to the CMD profile.  
        "tabTitle": "CMD",  
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",  
        "name": "Command Prompt",  
        "commandline": "cmd.exe",  
        "hidden": false  
      },  
      {  
        // Make changes here to the AZURE CLOUD SHELL profile.  
        "tabTitle": "AZURE CLOUD",  
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",  
        "name": "Azure Cloud Shell",  
        "hidden": false,  
        "source": "Windows.Terminal.Azure"  
      },  
      {  
        // Make changes here to the GIT BASH profile.  
        "tabTitle": "GIT BASH",  
        "guid": "{00000000-0000-0000-0000-000000012345}",  
        "name": "Git Bash",  
        "commandline": "\"%PROGRAMFILES%\\git\\bin\\bash.exe\" --login -i -l",  
        "colorScheme": "GitBash",  
        "icon": "%PROGRAMFILES%/git/mingw64/share/git/git-for-windows.ico"  
      },  
      {  
        // Make changes here to the Python Shell  
        "tabTitle": "PYTHON",  
        "guid": "{1850e97f-16dc-4281-9ea9-0100c4e852c5}",  
        "commandline": "py.exe",  
        "icon": "C:/Users/Admin/AppData/Local/Programs/Python/Python38/Lib/test/imghdrdata/python.png",  
        "name": "Python"  
      },  
      {  
        // Make changes here to the JShell  
        "tabTitle": "JSHELL",  
        "guid": "{e1840119-35c4-4dcc-a456-ecdf38222fa0}",  
        "commandline": "jshell.exe",  
        "icon": "C:\\Users\\Admin\\Pictures\\Saved Pictures\\java.png",  
        "name": "JShell"  
      }  
    ]  
 },  
  
  // Add custom color schemes to this array.  
  // To learn more about color schemes, visit https://aka.ms/terminal-color-schemes  
  "schemes": [  
 {  
      "name": "GitBash",  
      "background": "#000000",  
      "black": "#0C0C0C",  
      "blue": "#6060ff",  
      "brightBlack": "#767676",  
      "brightBlue": "#3B78FF",  
      "brightCyan": "#61D6D6",  
      "brightGreen": "#16C60C",  
      "brightPurple": "#B4009E",  
      "brightRed": "#E74856",  
      "brightWhite": "#F2F2F2",  
      "brightYellow": "#F9F1A5",  
      "cyan": "#3A96DD",  
      "foreground": "#bfbfbf",  
      "green": "#00a400",  
      "purple": "#bf00bf",  
      "red": "#bf0000",  
      "white": "#ffffff",  
      "yellow": "#bfbf00",  
      "grey": "#bfbfbf"  
    }  
  ],  
  
  // Add custom keybindings to this array.  
  // To unbind a key combination from your defaults.json, set the command to "unbound".  
  // To learn more about keybindings, visit https://aka.ms/terminal-keybindings  
  "keybindings": [  
    // Copy and paste are bound to Ctrl+Shift+C and Ctrl+Shift+V in your defaults.json.  
    // These two lines additionally bind them to Ctrl+C and Ctrl+V.  
    // To learn more about selection, visit https://aka.ms/terminal-selection  
    {  
      "command": {  
        "action": "copy",  
        "singleLine": false  
      },  
      "keys": "ctrl+c"  
    },  
    {  
      "command": "paste",  
      "keys": "ctrl+v"  
    },  
  
 // Press Ctrl+Shift+F to open the search box { "command": "find", "keys": "ctrl+shift+f" },  
 // Press Alt+Shift+D to open a new pane. // - "split": "auto" makes this pane open in the direction that provides the most surface area. // - "splitMode": "duplicate" makes the new pane use the focused pane's profile. // To learn more about panes, visit https://aka.ms/terminal-panes { "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" } ]  
}
```

## Shortcuts

- <kbd>Ctrl</kbd> + <kbd>L</kbd> &nbsp; - &nbsp; Clear the pane  

- <kbd>Alt</kbd> + <kbd>Arrow Key</kbd> &nbsp; - &nbsp; Change active pane  

- <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>Arrow Key</kbd> &nbsp; - &nbsp; Resize current pane  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>W</kbd> &nbsp; - &nbsp; Close the pane  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>D</kbd> &nbsp; - &nbsp; Open new tab  

- <kbd>Ctrl</kbd> + <kbd>Tab</kbd> &nbsp; - &nbsp; Next tab  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>1</kbd> &nbsp; - &nbsp; Open new tab with #1 shell (2: #2 shell, ...)  

- <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>D</kbd> &nbsp; - &nbsp; New pane  

- <kbd>Alt</kbd> + <kbd>Shift</kbd> + &nbsp; <kbd>+</kbd> &nbsp; - &nbsp; Split horizontally  

- <kbd>Alt</kbd> + <kbd>Shift</kbd> + &nbsp; <kbd>-</kbd> &nbsp; - &nbsp; Split vertically  

- <kbd>F11</kbd> &nbsp; - &nbsp; Full screen  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>PgUp</kbd> &nbsp; - &nbsp; Scroll up one page  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>PgDn</kbd> &nbsp; - &nbsp; Scroll down one page  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Home</kbd> &nbsp; - &nbsp; Scroll to start of history  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>End</kbd> &nbsp; - &nbsp; Scroll to end of history  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>N</kbd> &nbsp; - &nbsp; New window  

- <kbd>Ctrl</kbd> + &nbsp; <kbd>+</kbd> (Numpad) &nbsp; - &nbsp; Increase font size  

- <kbd>Ctrl</kbd> + &nbsp; <kbd>-</kbd> (Numpad) &nbsp; - &nbsp; Decrease font size  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>F</kbd> &nbsp; - &nbsp; Find  

- <kbd>Ctrl</kbd> + <kbd>,</kbd> &nbsp; - &nbsp; Open Settings  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> &nbsp; - &nbsp; Open command palette



---
#Windows #Terminal