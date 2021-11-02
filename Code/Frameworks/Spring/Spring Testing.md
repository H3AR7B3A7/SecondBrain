# Spring Testing
- Unit tests
- Integration tests

Dependency:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

- JUnit
- Mockito
- [[Spring]] Test (MockMVC)

@SpringBootTest:
- Convenient way to start up an application context to be used in a test

@WebMvcTest:
- Scans @Controller and @RestController
- Does NOT load the full application context
- Dependent beans must be mocked
- Speeds up testing by loading small portions of application

Mock environment:

*Springs @Mockbean annotation works well with mockito.*

TestRestTemplate:

```java
private TestRestTemplate restTemplate = new TestRestTemplate();
ResponseEntity<List> response = this.restTemplate.getForEntity(
        "http://localhost:" + port + "/tza/applications/", List.class);

assertThat(response.getStatusCode(), equalTo(HttpStatus.OK));
```


---
#Spring 