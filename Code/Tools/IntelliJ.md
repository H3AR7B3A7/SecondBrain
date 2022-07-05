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
 <dependency> <groupId>org.springframework.boot</groupId> <artifactId>spring-boot-devtools</artifactId> <optional>true</optional> <scope>runtime</scope> </dependency>  
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

- <kbd>Alt</kbd> + <kbd>Enter</kbd>: Show inspections / intentions / fixes  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Space</kbd>: Code suggestions  
- <kbd>Ctrl</kbd> + <kbd>P</kbd>: Required parameters  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd>: Complete current statement  
- <kbd>Shift</kbd> + <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd>: Refactor menu  
- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>V</kbd>: Extract variable  
- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>M</kbd>: Extract method  
- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>F</kbd>: Extract field  
- <kbd>Shift</kbd> + <kbd>F6</kbd>: Refactor name  
- <kbd>Ctrl</kbd> + <kbd>I</kbd>: Implement interface  
- <kbd>Ctrl</kbd> + <kbd>ALt</kbd> + <kbd>L</kbd>: Format file  
- <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>Up/Down</kbd>: Move line  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Up/Down</kbd>: Move block  
- <kbd>Ctrl</kbd> + <kbd>D</kbd>: Duplicate line  
- <kbd>Ctrl</kbd> + <kbd>/</kbd>: Comment out / Uncomment  
- <kbd>Alt</kbd> + <kbd>J</kbd>: Add next occurrence to selection  
- <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>J</kbd>: Remove last occurrence from selection  
- <kbd>Alt</kbd> + <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>J</kbd>: Add all occurrences to selection  
- <kbd>Ctrl</kbd> + <kbd>W</kbd>: Grow selection  
- <kbd>Shift</kbd> + <kbd>Ctrl</kbd> + <kbd>Left/Right</kbd>: Grow selection left/right  
  
- <kbd>Ctrl</kbd> + <kbd>K</kbd>: Commit  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + K</kbd>: Push  
- <kbd>Alt</kbd> + <kbd>1</kbd>: Project folder  
- <kbd>Alt</kbd> + <kbd>Insert</kbd>: Generate file or code  
- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>S</kbd>: Open Settings  
  
- <kbd>Ctrl</kbd> + <kbd>N</kbd>: Search classes  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>A</kbd>: Search actions  
- <kbd>Ctrl</kbd> + <kbd>B</kbd>: Find usage in code  
- <kbd>Shift</kbd> x2: Search everywhere  
- <kbd>Ctrl</kbd> + <kbd>F</kbd>: Find in file  
- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + F</kbd>: Find in project / module / directory / scope  
- <kbd>Ctrl</kbd> + <kbd>R</kbd>: Find and replace in file  
- <kbd>Ctrl</kbd> + <kbd>F12</kbd>: Show members  
- <kbd>F11</kbd> : Bookmark  
- <kbd>Ctrl</kbd> + <kbd>F11</kbd> : Mnemonic bookmark  
- <kbd>Shift</kbd> + <kbd>F11</kbd> : Show bookmarks  
- <kbd>Ctrl</kbd> + <kbd>`</kbd> : Show quick switch list
  
Some other functions do not have keyboard shortcuts, you might want to consider assigning some of these:  
  
- Extract interface  
  
*(Tip: <kbd>Alt</kbd> + <kbd>Numpad 0 - 9</kbd> makes for 10 easy extra shortcuts you can use to suit your needs.)*

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
  
### Cosmetic  
  
- Atom Material Icons  
- Dark Purple Theme  
- Nyan Progress Bar  
- Rainbow Brackets  
- Presentation assistant

## Interesting actions  
  
<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>A</kbd>  
  
- Color picker  
- Set Background image

---
#IDE #IntelliJ