# Powershell

PowerShell or Microsoft PowerShell (formerly Windows PowerShell) is a task automation and configuration management program from [[Microsoft]], consisting of a command-line shell and the associated scripting language. Initially a [[Windows]] component only, known as Windows PowerShell, it was made open-source and cross-platform on 18 August 2016 with the introduction of PowerShell Core. The former is built on the .NET Framework, the latter on .NET Core. The name Windows PowerShell is still present on the latest versions of Windows 11 and 10, but the latest versions of PowerShell is called PowerShell or Microsoft PowerShell.

In PowerShell, administrative tasks are generally performed by cmdlets (pronounced command-lets), which are specialized .NET classes implementing a particular operation. These work by accessing data in different data stores, like the file system or registry, which are made available to PowerShell via providers. Third-party developers can add cmdlets and providers to PowerShell. Cmdlets may be used by scripts, which may in turn be packaged into modules.

PowerShell provides access to COM and WMI, enabling administrators to perform administrative tasks on both local and remote Windows systems as well as WS-Management and CIM enabling management of remote Linux systems and network devices. PowerShell also provides a hosting API with which the PowerShell runtime can be embedded inside other applications. These applications can then use PowerShell functionality to implement certain operations, including those exposed via the graphical interface. This capability has been used by Microsoft Exchange Server 2007 to expose its management functionality as PowerShell cmdlets and providers and implement the graphical management tools as PowerShell hosts which invoke the necessary cmdlets. Other Microsoft applications including Microsoft SQL Server 2008 also expose their management interface via PowerShell cmdlets.

PowerShell includes its own extensive, console-based help (similar to man pages in Unix shells) accessible via the `Get-Help` cmdlet. Updated local help contents can be retrieved from the Internet via the Update-Help cmdlet. Alternatively, help from the web can be acquired on a case-by-case basis via the -online switch to `Get-Help`.

## Instalation

### Using Installer

Download the installer [here](https://github.com/PowerShell/PowerShell) and follow the instructions.  
  
  

### Using Commandline

> iex "& { $(irm https://aka.ms/install-powershell.ps1) } -UseMSI"  
  
You can also use other installation parameters:  
- Destination – change the default PowerShell Core installation directory  
- Preview – install the latest Preview PowerShell version  
- Quiet – a quiet installation  
- AddToPath – adds a path to the PowerShell Core installation directory to the environment variables  
update powershell core 7.1 from command line  
  
  

### Using Chocolatey

If you have Chocolatey package manager installed, you can install or update your PowerShell version using the following commands:  
  
> choco upgrade pwsh -y  
  
> choco upgrade pwsh -y

## Commands

- **cd "path"** &nbsp; - &nbsp; Go to path  
- **cd ..** &nbsp; - &nbsp; Go up in file structure  
- **ls -r** &nbsp; - &nbsp; List children recursively  
- **ii.** &nbsp; - &nbsp; Open current folder in explorer  
- **Remove-Item fileName -f -r** &nbsp; - &nbsp; Force remove item  
- **pwd** &nbsp; - &nbsp; Get current full path  
- **clear** &nbsp; - &nbsp; Clear the window  
- **exit** &nbsp; - &nbsp; Close the window  
- **$Profile** &nbsp; - &nbsp; Find user profile location

## Custom PowerShell Functions

These can be added to the 'profile', find location by using following command:  
>$Profile  
  
If you haven't used it before we will have to create the file. The profile path will likely look like this:  
For the default Powershell:  
>C:\Users\<UserName>\Documents\WindowsPowerShell  

For Powershell 7:  
> C:\Users\<UserName>\Documents\PowerShell  

```bash
# Shorten the current directory path to just the folder
function prompt{
  $check = $pwd.drive
  if ( "$check`:\" -eq $pwd.path){
    "$pwd>"
  }else{
    $p = Split-Path -leaf -path (Get-Location)
    "~ $p\> "
  }
}

# Change or create files
function touch {
  Param(
    [Parameter(Mandatory=$true)]
    [string]$Path
  )

  if (Test-Path -LiteralPath $Path) {
    (Get-Item -Path $Path).LastWriteTime = Get-Date
  } else {
    New-Item -Type File -Path $Path
  }
}

# Encode
function encode([string]$arg){
    [Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($arg))
}

# Decode
function decode([string]$arg) {
    [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($arg))
}
```

## Oh My Posh

[Original docs](https://ohmyposh.dev/docs)

```
choco install oh-my-posh
```

Add this to `~\Documents\PowerShell\Microsoft.PowerShell_profile.ps1`:

```
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\if_tea.omp.json" | Invoke-Expression
```

_You can edit the theme to have a '\\n' new line..._

```
oh-my-posh install font
```

_Meslo config in windows terminal:_

```json
"profiles": {  
	"defaults": {  
		"font": {
			"face": "MesloLGM Nerd Font"  
		}  
	}  
}  
```


---
#Microsoft 