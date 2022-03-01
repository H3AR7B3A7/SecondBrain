# IntelliJ IDEA  
  
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

- <kbd>Ctrl</kbd> + <kbd>K</kbd>: Commit  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + K</kbd>: Push  

- <kbd>Alt</kbd> + <kbd>1</kbd>: Project folder  

- <kbd>Alt</kbd> + <kbd>Insert</kbd>: Generate file or code  

- <kbd>Ctrl</kbd> + <kbd>I</kbd>: Implement interface  

- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + V</kbd>: Extract variable  

- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + M</kbd>: Extract method  

- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + F</kbd>: Extract field  

- <kbd>Ctrl</kbd> + <kbd>B</kbd>: Find usage in code  

- <kbd>Shift</kbd> + <kbd>F6</kbd>: Refactor name  

- <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + S</kbd>: Open Settings  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + Space</kbd>: Code suggestions  

- <kbd>Shift</kbd> x2: Search everywhere  

- <kbd>Ctrl</kbd> + <kbd>F</kbd>: Find in file  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + F</kbd>: Find in project / module / directory / scope  

- <kbd>Ctrl</kbd> + <kbd>R</kbd>: Find and replace in file  

- <kbd>Ctrl</kbd> + <kbd>ALt</kbd> + L</kbd>: Format file  

- <kbd>Alt</kbd> + <kbd>Shift</kbd> + Up/Down</kbd>: Move line  

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + Up/Down</kbd>: Move block

- <kbd>Ctrl</kbd> + <kbd>D</kbd>: Duplicate line

- <kbd>Ctrl</kbd> + <kbd>/</kbd>: Comment out / Uncomment  
  
Some other functions do not have keyboard shortcuts, you might want to consider assigning some of these:  
  
- Extract interface  
  
*(Tip: <kbd>Alt</kbd> + <kbd>Numpad 0 - 9</kbd> makes for 10 easy extra shortcuts you can use to suit your needs.)*

## Plugins
### Functional
- CheckStyle IDEA
- Easy l18n
- [[GitHub Copilot]]
- google-java-format
- GWT
- JPA Buddy
- PlantUML integration
- Spring Boot Assistant
- UUID Generator

Cosmetic
- Atom Material Icons
- Dark Purple Theme
- Nyan Progress Bar
- Rainbow Brackets

---
#IDE #IntelliJ