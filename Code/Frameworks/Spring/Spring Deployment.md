# Spring Deployment
## Configuration
- External sources
  - Command line parameters
  - JNDI
  - OS environment variables
- Internal sources
  - Servlet parameters
  - Property files
  - Java configuration

Order of precedence:
1. Command line parameters
2. SPRING_APPLICATION_JSON args
3. Servlet Parameters
4. JNDI
5. Java System Properties
6. OS environment variables
7. Profile properties
8. Application properties
9. @PropertySource annotations
10. Default properties

*We should pick two sources. One will set the defaults, and one to overwrite the default to keep configuration in one of 2 places.*

## Run Maven with Environment Variables
Since Maven is not aware of environment variables, we need to provide them in the command line.
> maven -Dname=value clean install

## Common Application Properties
We can find common [[Spring]] properties [here](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html).

## Custom Auto Configuration
Example:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyAutoConfiguration {
  @Bean
  public someObject myMethod(){
    // ...
  }
}
```

Declaration in resources/META-INF/spring.factories to register autoconfiguration:

*org.springframework.boot.autoconfiguration.EnableAutoConfiguration=\com.mypackage.MyAutoConfiguration*

**Annotations**:
- @ConditionalOnClass
- @ConditionalOnMissingClass
- @ConditionalOnBean
- @ConditionalOnMissingBean
- @ConditionalOnProperty
- @ConditionalOnResource

## Embedded Servlet Container
By default, Spring Boot uses Tomcat as an embedded container.

But other options are supported:
- Jetty
- Undertow

We can swap them out by excluding Tomcat and adding the right dependency in the **pom.xml**:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

## JAR
We can build a jar with maven:
- **mvn package**

  Take the compiled code and package it in its distributable format, such as a JAR,

- **mvn install**

  Install the package into the local repository, for use as a dependency in other projects locally.

*Both of these maven commands will compile your code, clean the /target folder,
and will place a new packaged JAR or WAR into that /target folder.
It is just the *mvn install* command will also install the package into the local maven repository,
for use as a dependency in other projects locally.*

The jar can run by itself using the following command :
> java -DDB_URL=jdbc:postgresql://localhost:5432/conference_app -DUSERNAME=postgres -DPASSWORD=pass -jar .\conference-demo-0.0.1-SNAPSHOT.jar

## Cloud Supported Platforms
- Cloud Foundry
- Heroku
- Google Cloud
- Amazon Web Services
- Microsoft Azure

*For more flexibility we can **dockerize** the application.*

Considerations to make with using cloud offering:
- Logging (using a centralized logging service)
- Service integration (can differ from our regular Spring Boot config)
- Firewall and security (securing talking between services)

## Heroku Deployment
- Add a system.properties file to the root of the project

  ```properties
  java.runtime.version=15
  ```

- Go to [Heroku](https://www.heroku.com/) and create an account.
- Click 'add' to create a new project.
- Pick a deployment method (heroku / git / container ...)
- Set environment values:

  > heroku config:set DB_URL=jdbc:postgresql://localhost:5432/conference_app

  > heroku config:set USERNAME=postgres

  > heroku config:set PASSWORD=pass

  *Make sure to use the actual configuration provided by Heroku's datasource in resources tab.*

- Connect to the db using PGAdmin4 or any db manager and set up the database / data

Check the result:
- [Home](https://conf-spring.herokuapp.com/)
- [Swagger](https://conf-spring.herokuapp.com/swagger-ui.html)

## WAR Deployment
To deploy the application as a war file, we change the **pom.xml**:

```xml
...

<description>Blah blah</description>
<packaging>war</packaging>

...

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>

...
```

Copy the war to the *webapps* folder in an Apache Tomcat Container.

*JNDI is useful to look into for setting environment variables.*


---
#Spring