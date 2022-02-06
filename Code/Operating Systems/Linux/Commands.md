# Commands
## Why use commands?
- To have greater control
- To be faster
- For automation
- To use headless clients
- For cloud computing
- ...


## Most popular
Manual
> man "command" 
> help "command"

*Most commands have a manual, but some like 'cd' do not. They do however have help pages. This goes for all of [built-in-shell commands](https://www.computerhope.com/unix/bash/index.htm).* 

Print Working Directory
> pwd

Print user id
> whoami

Show who is logged in
> who

List
> ls

Change directory
> cd

Clear terminal
> clear

Make folder
> mkdir

Remove empty folder
> rmdir

Make file / update timestamp
> touch "filename"

Edit file
> vim "filename"

Remove file or folder
> rm

Open file or folder
> xdg-open "filename"

???
> ps auxww





## Nono's
- Delete everything (including root)
>sudo rm -R -f -no-preserve-root /
- Fork bomb:
>:(){ :|:& };:
- Fork bomb:
>fu{ fu | fu & }; fu

---
#Linux