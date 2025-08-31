# IntelliJ IDEA  

[IntelliJ CE Repository](https://github.com/JetBrains/intellij-community)  
  
## Project files  
  
- The *.iml files are created for each IntelliJ module  
  - Can be added to VCS  
- The .idea folder is created for each project  
  - Can be added to VCS (excluding workspace.xml)  
- .idea/workspace.xml holds personal preferences  
  - Do NOT add it to VCS

## Live Reload  
  
To have a Spring project live reload your changes:  
  
- Add devtools dependencies to your pom.xml  
  
```xml  
 <dependency>
	 <groupId>org.springframework.boot</groupId>
	 <artifactId>spring-boot-devtools</artifactId>
	 <optional>true</optional>
	 <scope>runtime</scope>
 </dependency>  
 ```  
- In your intellij IDEA go to: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>S</kbd> ->build,execution,deployment->compiler  
  - Select build project automatically  
- In your intellij IDEA: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> +<kbd>A</kbd> ->registry  
  - Select compiler.automake.allow.when.app.running  
- Add LiveReload extension in your browser  
  - Enter a rule for html (e.g. localhost:8080)  
 - Enter a rule for css (e.g. localhost:8080/style.css)  
 - ...  
  
*PS: For war deployments with a TomCat Server, choose for an exploded war. In configurations select 'update classes and  
resources' for **on frame deactivation**. And in LiveReload enter the full path + application context as provided in the  
Deployment tab.*  
  
## Auto Imports  
  
- In your intellij IDEA go to: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>S</kbd> ->Editor->General->Auto Import  
  - Select optimize imports on the fly  
  
- In your intellij IDEA go to: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>S</kbd> ->Editor->Code Style->Java->Imports  
  - Set Class count to use imports with '*' to 9999  
  - Set Names count to use static imports with '*' to 9999  
  
## Requests  
  
We can create a scratch file by navigating to the project tab and creating a new file:  
  
<kbd>Alt</kbd> + <kbd>1</kbd> -> <kbd>Alt</kbd> + <kbd>Insert</kbd> -> Scratch file -> Http Request  
  
```http request  
GET localhost:8080/user?firstname=Bob&lastname=Builder&age=44  
Accept: application/json  
```  
  
*We can then run our requests by clicking the play button from the scratch file.*  
  
We can find more about using the HTTP client in Intellij  
IDEA [here](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)  
  
## Interesting Keyboard Shortcuts  

### Code Editing & Refactoring

|Shortcut|Action|
|---|---|
|Alt + Enter|Show inspections / intentions / fixes|
|Ctrl + Shift + Space|Code suggestions|
|Ctrl + P|Required parameters|
|Ctrl + Alt + P|Extract parameter|
|Ctrl + Shift + Enter|Complete current statement|
|Shift + Ctrl + Alt + T|Refactor menu|
|Ctrl + Alt + V|Extract variable|
|Ctrl + Alt + M|Extract method|
|Ctrl + Alt + F|Extract field|
|Shift + F6|Refactor name|
|Ctrl + I|Implement interface|
|Ctrl + Alt + L|Format file|
|Alt + Insert|Generate file or code|
|Ctrl + Alt + T|Surround with|

### Line & Block Operations

|Shortcut|Action|
|---|---|
|Alt + Shift + Up/Down|Move line|
|Ctrl + Shift + Up/Down|Move block|
|Ctrl + D|Duplicate line|
|Ctrl + /|Comment out / Uncomment|

### Selection Operations

|Shortcut|Action|
|---|---|
|Alt + J|Add next occurrence to selection|
|Alt + Shift + J|Remove last occurrence from selection|
|Alt + Ctrl + Shift + J|Add all occurrences to selection|
|Ctrl + W|Grow selection|
|Shift + Ctrl + Left/Right|Grow selection left/right|

### Navigation & View

| Shortcut         | Action                      |
| ---------------- | --------------------------- |
| Ctrl + M         | Scroll to center            |
| Alt + 1          | Project folder view         |
| Alt + 0          | Commit view                 |
| Alt + 9          | Git view                    |
| Ctrl + Alt + S   | Open Settings               |
| Ctrl + `         | Show quick switch list      |
| Ctrl + Shift + I | View source in popup window |
| F2               | Next highlighted error      |
| Shift + F2       | Previous highlighted error  |

### Search & Find

| Shortcut         | Action                      |
| ---------------- | --------------------------- |
| Ctrl + N         | Search classes              |
| Ctrl + Shift + N | Search files                |
| Ctrl + Shift + A | Search actions              |
| Ctrl + B         | Find usage/declaration      |
| Ctrl + Alt + B   | Find implementation         |
| Shift x2         | Search everywhere           |
| Ctrl + F         | Find in file                |
| Ctrl + Shift + F | Find in project             |
| Ctrl + R         | Find and replace in file    |
| Ctrl + Shift + R | Find and replace in project |
| Ctrl + F12       | Show members                |

### Bookmarks

|Shortcut|Action|
|---|---|
|F11|Bookmark|
|Ctrl + F11|Mnemonic bookmark|
|Shift + F11|Show bookmarks|

### Running

| Shortcut           | Action            |
| ------------------ | ----------------- |
| Shift + F10        | Run configuration |
| Ctrl + Shift + F10 | Run current block |

### Debugging

| Shortcut   | Action              |
| ---------- | ------------------- |
| Ctrl + F8  | Set breakpoint      |
| Shift + F9 | Debug configuration |
| F9         | Resume              |
| F8         | Step over           |
| F7         | Step into           |
| Shift + F8 | Step out            |

## Action Menus

|Shortcut|Action|
|---|---|
|Ctrl + Alt + Shift + T|Open refactor menu|
|Ctrl + Shift + A|Open action menu|

### Version Control

|Shortcut|Action|
|---|---|
|Ctrl + K|Commit|
|Ctrl + Shift + K|Push|
|Ctrl + Shift + µ|Open branch menu|

Some other functions do not have keyboard shortcuts, you might want to consider assigning some of these:  
  
- Extract to interface 
- Extract to abstract class
- Pull members up

*(Tip: <kbd>Alt</kbd> + <kbd>Numpad 0 - 9</kbd> makes for 10 easy extra shortcuts you can use to suit your needs.)*

## Macros

_We can also record macro's, in the action menu, choose start/stop macro. We can also bind the macro's to key bindings._

One interesting one is recording just a <kbd>→</kbd> and bind it to <kbd>Shift</kbd> + <kbd>Space</kbd>, because tab is relatively unreliable to jump out of brackets.

## Live Templates  
  
<kbd>Ctrl</kbd> + <kbd>J</kbd>: Show live templates  
  
- fori  
- if  
- ifn  
- sout  
- psvm  
- psfs  
- ...  
  
*Templates are contextually aware.*  
  
### Custom Live Templates  
  
- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>S</kbd> -> Live Template  
- Add group  
- Add Live Template  
  
Example:  
  
Abbreviation: pcm  
Description: public class method  
Applicable context: Java declaration  
  
```java  
public $RETURN_TYPE$ $NAME$($INPUT$) {  
    $END$}  
```

## Plugins
### Functional  
  
- CheckStyle IDEA  
- Easy l18n  
- GitHub Copilot  
- google-java-format  
- GWT  
- JPA Buddy  
- PlantUML integration  
- Spring Boot Assistant  
- UUID Generator  
- .ignore  
- Prettier  
- VisualVM Launcher  
- Key promoter  
- Save actions  
- Code with me  
- CommitPrefix  
- Pre Commit Hook Plugin
- Apache Camel
- AWS Toolkit
- ESLint Restart Service Action
- Nx Console
- MDX
- 
  
### Cosmetic  
  
- Atom Material Icons  
- Dark Purple Theme  
- Nyan Progress Bar  
- Rainbow Brackets  
- Presentation assistant
- CodeGlance
- Gitmoji
- 

## Interesting actions  
  
<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>A</kbd>  
  
- Color picker  
- Set Background image

---
#IDE #IntelliJ