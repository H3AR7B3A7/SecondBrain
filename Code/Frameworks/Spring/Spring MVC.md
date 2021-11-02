# SPring MVC
## Spring MVC Annotations
- @RestController
  - @Controller
  - @ResponseBody
- @GetMapping
- ...

## ResponseEntity
Represents the entire http response:
- Status
  - 200: OK
  - 400: BAD_REQUEST
  - 409: CONFLICT
  - 404: NOT_FOUND
- Header
- Body

ResponseStatusException:
- Programmatic alternative to @ResponseStatus
- Provide HttpStatus and a reason and a cause
- Exceptions can be created programmatically
- Provides a default error mapping

## cURL
A tool to call api's from command line:

> curl http://localhost:8080/tza/applications

## Vocabulary
- SPA: Single Page Application
- DispatcherServlet: Entry point into the application
- Controller: Command Pattern Handler
- RequestMapping: URL and Request Type
- ViewResolver: Locates View to serve
- Servlet-config: Configuration file (Can also be done using java configuration)
- POJO: Plain Old Java Object
- Bean: [[Spring]] configured POJO

## Configuration
- pom.xml (dependencies)
- Config (XML or Java)
- Java (Controller, Model, Configuration etc.)
- View

## Model - View - Controller
![MVC](MVC.png)

## Application Layers
- Presentation Layer
- Business Logic
- Data Layer

## Components
- Controller
- Service
- Repository

## DispatcherServlet
The Application class extends SpringBootServletInitializer which tells the application server to create a DispatcherServlet.

The @SpringBootApplication annotation contains:
- @EnableAutoConfiguration
- @ComponentScan
- @Configuration

Because of the @Component scan the application will pick up on our controllers annotated with @Controller.

![DispatcherServlet](dispatcher-servlet.png)
![DispatcherServlet](dispatcher-servlet2.png)

## Interceptors
- Logging
- Security
- I18N
- Performance Monitoring

## JSR Bean Validation
Dependency:
```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

## Spring MVC with Client-side JavaScript Applications
@RestController: The heart of rest-services

Examples:
- [Default user](http://localhost:8080/conference/user)
- [Dan](http://localhost:8080/conference/user?firstname=Dan&lastname=Brown&age=25)
- [jQuery](http://localhost:8080/conference/user.html)



---
#Spring 