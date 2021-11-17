# JUnit5
## New in JUnit Jupiter
-   Visibility
    -   Everything does not have to be public
-   Custom display names
    -   @DisplayName: spaces, special characters, emoji 👻
    -   DisplayNameGenerator
-   Tagging
    -   @Tag
    -   Tag expression language
-   Meta-annotation support
    -   Create your own custom composed annotations
    -   Combine annotations from Spring and JUnit
-   Conditional test execution
-   Dependency injection for constructors and methods
-   Lambda expressions and method references
-   Interface default methods and testing traits
-   @Nested test classes
-   @RepeatedTest, @ParameterizedTest, @TestFactory
-   @TestInstance lifecycle management
-   Implicit / Explicit conversions
-   Argument aggregation
-   New extension model
    -   Extension: marker interface
    -   APIs: org.junit.jupiter.api.extension
    -   @ExtendWith(...)
    -   @RegisterExtension
-   And more ...

## Architecture
![[JUnit5.png]]

## Dependencies
2 + 1 or more dependencies (depending on if you want legacy and/or 3d party engines):

```
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>${junit.jupiter.version}</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>${junit.jupiter.version}</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.vintage</groupId>
    <artifactId>junit-vintage-engine</artifactId>
    <version>5.4.2</version>
    <scope>test</scope>
</dependency>
```