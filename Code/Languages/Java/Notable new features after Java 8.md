### 1. Modularization of the JVM (Java 9)

Jdeps / Jlink

These can make the JVM significantly lighter by stripping it down to only the modules you need. This also make Java container images significantly smaller.

### 2. **Local-Variable Type Inference / `var`** (Java 10)

- **What you couldn’t do in Java 8**: You had to specify the type explicitly.
- **What you can do now**:

```java
// Using 'var' for local variables (Java 10+)
var message = "Hello, World!";  // Type is inferred as String
System.out.println(message);
// Output: Hello, World!`
```

---

### 3. **Enhanced Switch** (Java 12)

- **What you couldn’t do in Java 8**: Switch statements required `break` and could only handle single values, not returning values or using multiple labels in a case.
- **What you can do now** (Java 12+):

```java
// Enhanced switch with no 'break' and multiple case labels (Java 12+)
int dayOfWeek = 2;
String dayType = switch (dayOfWeek) {
	case 1, 7 -> "Weekend";
	case 2, 3, 4, 5, 6 -> "Weekday";
	default -> throw new IllegalArgumentException("Invalid day");
};
System.out.println(dayType); // Output: Weekday
```

---

### 4. **Text Blocks** (Java 13)

- **What you couldn’t do in Java 8**: Multiline strings required concatenation or escape sequences.
- **What you can do now**:

```java
// Text blocks for multiline strings (Java 13+)
String json = """
{
	"name": "Alice",
	"age": 30
}
""";
System.out.println(json);
```

---

### 5. **Records** (Java 14)

- **What you couldn’t do in Java 8**: You couldn’t easily create immutable data classes with automatic `toString`, `equals`, and `hashCode` methods.
- **What you can do now**:


``` java
// Record class definition (Java 14+)
public record Person(String name, int age) { }
Person person = new Person("Alice", 30);
System.out.println(person);
// Output: Person[name=Alice, age=30]
```

---

### 6. **Sealed Classes** (Java 15)

- **What you couldn’t do in Java 8**: You couldn’t restrict which classes can extend a particular class.
- **What you can do now**:

```java
// Sealed class with allowed subclasses (Java 15+)
public sealed class Shape permits Circle, Square { }
public final class Circle extends Shape { }
public final class Square extends Shape { }
```

---

### 7. **Pattern Matching**

#### - **For `instanceof` without casting** (Java 16)

- **What you couldn’t do in Java 8**: You had to cast the object after performing the `instanceof` check.
- **What you can do now**:

```java
Object obj = "Hello";
if (obj instanceof String str) {
	// No explicit cast needed
	System.out.println(str.length());
	// Output: 5 
}
```
#### - **For switch expressions (Java 17)

- **What you couldn’t do in Java 8**: Use pattern matching in a switch expression
- **What you can do now**:

```java
interface Shape { }
record Rectangle(double length, double width) implements Shape { }
record Circle(double radius) implements Shape { }

public static double getPerimeter(Shape shape) throws IllegalArgumentException {
	if (shape instanceof Rectangle r) { 
		return 2 * r.length() + 2 * r.width();
	} else if (shape instanceof Circle c) {
		return 2 * c.radius() * Math.PI;
	} else {
		throw new IllegalArgumentException("Unrecognized shape");
	}
}
```

---

### 8. **Virtual Threads (Loom)** (Java 20)

- **What you couldn’t do in Java 8**: Handling a large number of concurrent tasks with traditional threads could result in high overhead and scalability issues.
- **What you can do now**:

```java
// Virtual threads for lightweight concurrency (Java 19 Preview)
Thread.startVirtualThread(() -> {     
	System.out.println("Hello from a virtual thread!"); 
});
```

---

