# Maven  

## What Is Maven  
  
- A build tool  
  - One artifact  
  - Manage dependencies  
- Project management tool  
  - Handles versioning/releases  
  - Describes project  
  - Produce Javadocs / site information  
  
## Why Use Maven  
  
- Repeatable builds  
- Transitive dependencies  
- Environment  
- Local repo  
- IDE and standalone  
- Preferred method for CI tools  
  
## Ant vs Maven  
  
Different mindset:  
Scripting tool <-> build tool  
  
### Ant  
  
- Replacement for Make  
- Cross-platform  
- Java and XML based  
  
Pro  
  
- Clear and straight forward  
- Quick to learn  
  
Con  
  
- No naming consistency between projects / organisations  
- A lot of copy / pasting, no inheritance  
- Large project size  
  
### Maven  
  
- Full features  
- Implicit  
- Consistency  
- Inheritance  
- Transitive dependencies  
- Versioned  
  
Pro  
  
- Convention over configuration  
- IDE integration  
- Less overhead  
-  
  
Con  
  
- Black box  
- Steeper learning curve  
  
## Installation  
  
To use maven from the command line:  
  
- Download binary files [here](https://maven.apache.org/download.cgi).  
- Unzip to hard-drive  
- Set JAVA_HOME and MAVEN_HOME environment variables  
  
We can find more information [here](https://maven.apache.org/install.html).  
  
*Maven is also built-in in IntelliJ IDEA.*  
  
## POM  
  
Basic example:  
  
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">  
    <groupId>be.dog.d.steven</groupId>
    <artifactId>HelloWorld</artifactId>
    <version>1.0-SNAPSHOT</version>
    <modelVersion>4.0.0</modelVersion>
    <packaging>jar</packaging>  
    <build>
	    <plugins>
		    <plugin>
			    <groupId>org.apachi.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.8.0</version>
				<configuration>
				    <release>12</release>
			    </configuration>
		    </plugin>
	    </plugins>
    </build>
</project>  
```  
  
## Commands / goals  
  
Clean  
> mvn clean  
  
Compile  
> mvn compile  
  
Package  
> mvn package  
  
Install (package + add to local repo)  
> mvn install  
  
Deploy (install + deploy to corporate or remote repo)  
> mvn deploy  
  
## Project Structure  
  
Project  
  
- src/main/java  
- src/test/java  
- pom.xml  
- target  
  
## Dependencies  
  
Required items:  
- groupId  
- artifactId  
- version  
  
```xml  
<dependencies>  
  <dependency>  
    <groupId>org.apache.commons</groupId>  
    <artifactId>commons-lang3</artifactId>  
    <version>3.8.1</version>  
  </dependency>  
</dependencies>  
```  
  
### Version  
  
Version naming conventions:  
- SNAPSHOT  
  - Latest in development  
  - Between version numbers  
  - Build is not reproducible  
- RC (Release Candidate) / M (Milestone Release)  
  - Approaching a release  
  - Not fully stable  
- RELEASE  
  
### Packaging Types  
  
- pom  
- jar  
- war  
- ear  
- maven-plugin  
  
### Transitive Dependencies  
  
Adding a dependency will also add all transitive dependencies.  
  
### Scopes  
  
- compile  
  - Default  
  - Available everywhere inside the application  
- provided  
  - Available throughout the entire build cycle  
  - Not included in final artifact(, because it is provided by the container)  
- runtime  
  - Not needed for compilation, but only for execution  
  - Only included in the final artifact  
- test  
  - Only available for test compilation and execution  
- system  
  - Hard codes the path to a jar in the file system  
  - Very brittle, do not use  
- import  
  - dependency management  
  - share resources across multiple pom files  
  
### Optional  
  
```xml  
<optional>true</optional>  
```  
  
When A declares B as optional dependency:  
  
```  
A -> B  
X -> A  
```  
  
Project B is not included in the classpath of X.  
  
### Exclusions  
  
Because of transitive dependencies it might be that an unwanted dependency is included.  
We can exclude them using exclusions.  
  
```xml  
<exclusions>  
  <exclusion>  
    <groupId>org.some.project</groupId>  
    <artifactId>some-project</artifactId>  
  </exclusion>  
</exclusions>  
```  
  
*To be used as a last resort.*