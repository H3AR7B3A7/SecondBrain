# Gradle

## What Is Gradle?

- A powerful and flexible build automation tool.
- Builds on the concepts of Ant and Maven.
- Uses a Domain Specific Language (DSL) based on Groovy or Kotlin for build scripts.
- Manages dependencies and project structure.

## Why Use Gradle?

- **Flexibility:** Gradle is highly customizable. You can easily extend it to fit your project's needs.
- **Performance:** Gradle is fast. It uses a build cache and incremental builds to avoid unnecessary work.
- **Concise DSL:** The Groovy or Kotlin DSL is more concise and readable than Maven's XML.
- **IDE Support:** Excellent support in major IDEs like IntelliJ IDEA and Android Studio.
- **Growing Ecosystem:** A large and growing number of plugins are available.

## Maven vs Gradle

| Feature | Maven | Gradle |
| :--- | :--- | :--- |
| **Build Script** | XML | Groovy or Kotlin DSL |
| **Flexibility** | Convention over configuration | Highly flexible and customizable |
| **Performance** | Slower | Faster (caching, incremental builds) |
| **Readability** | Verbose | Concise and readable |
| **Learning Curve** | Easier for beginners | Steeper learning curve |

## Installation

To use Gradle from the command line:

- Download the binary from the [Gradle website](https://gradle.org/releases/).
- Unzip it to your hard drive.
- Set the `GRADLE_HOME` environment variable and add `$GRADLE_HOME/bin` to your `PATH`.

You can find more information [here](https://gradle.org/install/).

*Many projects use the Gradle Wrapper (`gradlew`), which automatically downloads and uses the correct Gradle version for the project.*

## Build Script (build.gradle)

Basic example using the Groovy DSL:

```groovy
plugins {
    id 'java'
}

group = 'be.dog.d.steven'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.apache.commons:commons-lang3:3.12.0'
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.8.1'
    testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.8.1'
}

test {
    useJUnitPlatform()
}
```

## Common Tasks

- **build:** Assembles and tests the project.
  > `gradle build`
- **clean:** Deletes the build directory.
  > `gradle clean`
- **test:** Runs the unit tests.
  > `gradle test`
- **run:** Runs the application.
  > `gradle run`

## Project Structure

Gradle uses a similar default project structure to Maven:

- `src/main/java`
- `src/main/resources`
- `src/test/java`
- `src/test/resources`
- `build.gradle` (or `build.gradle.kts`)
- `settings.gradle` (or `settings.gradle.kts`)
- `build/` (output directory)

## Dependencies

Dependencies are declared in the `dependencies` block.

```groovy
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.12.0'
}
```

### Configurations (Scopes)

Gradle uses "configurations" to group dependencies. Some common configurations provided by the Java plugin are:

- **`implementation`**: The dependency is used at compile time and at runtime. It's not exposed to consumers of the library.
- **`api`**: The dependency is part of the library's API and is exposed to consumers.
- **`compileOnly`**: The dependency is used only at compile time and is not included in the runtime classpath.
- **`runtimeOnly`**: The dependency is needed only at runtime.
- **`testImplementation`**: The dependency is used for compiling and running tests.

## Plugins

Plugins add new tasks, configurations, and other features to your build.

You can apply plugins using the `plugins` block:

```groovy
plugins {
    id 'java'
    id 'application'
}
```

The `application` plugin, for example, adds the `run` task.

---
#Gradle #BuildTool
