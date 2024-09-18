# Agenda 2024 day 2
## 3. semester
## 3. semester
### Functional Programming
- What is functional programming?
  - Higher order functions
  - Pure functions
  - Immutability
  - Declarative vs imperative code style
  - Functional interfaces in java
  - DEMO:
    - Show examples of functional [code](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/functional/DeclarativeStyle.java)
    - Show examples of pure functions [code](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/functional/PureFunction.java)
    - Show examples of functional interface [code](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/functional/CallbackInJava.java)
- 4 build-in functional interfaces in [Read the Docs of java.util.function](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)
  - `Predicate<T>`: `boolean test(T t)`
  - `Consumer<T>`: `void accept(T t)`
  - `Function<T, R>`: `R apply(T t)`
  - `Supplier<T>`: `T get()`
- DEMO:
  - Predicate
```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        // Predicate to check if a number is even
        Predicate<Integer> isEven = num -> num % 2 == 0;

        System.out.println(isEven.test(4));    // Output: true
        System.out.println(isEven.test(7));    // Output: false
    }
}
```
  - Consumer
```java
import java.util.List;
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        // Consumer to print each element in a list
        Consumer<String> printElement = element -> System.out.println(element);

        List<String> names = List.of("Alice", "Bob", "Charlie");
        names.forEach(printElement);    // Output: Alice, Bob, Charlie
    }
}
```
  - Function
```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Function to convert a string to its length
        Function<String, Integer> lengthFunction = str -> str.length();

        System.out.println(lengthFunction.apply("Java"));     // Output: 4
        System.out.println(lengthFunction.apply("Programming")); // Output: 11
    }
}
```
  - Supplier
```java
import java.util.Random;
import java.util.function.Supplier;

public class SupplierExample {
    public static void main(String[] args) {
        // Supplier to generate a random number
        Supplier<Integer> randomSupplier = () -> new Random().nextInt(100);

        System.out.println(randomSupplier.get());    // Output: Random number between 0 and 99
        System.out.println(randomSupplier.get());    // Another random number
    }
}
```

### Method References
[Demo](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/demos/day1/ClassDemo.java)
1. Static method reference `Arrays.sort(names, StaticMethodReferenceExample::compareNames);`
2. Instance method reference `Arrays.sort(names, new InstanceMethodReferenceExample()::compareNames);`
3. Constructor reference `Supplier<InstanceMethodReferenceExample> instanceMethodReferenceExampleSupplier = InstanceMethodReferenceExample::new;`



### Method References
[Demo](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/demos/day1/ClassDemo.java)
1. Static method reference `Arrays.sort(names, StaticMethodReferenceExample::compareNames);`
2. Instance method reference `Arrays.sort(names, new InstanceMethodReferenceExample()::compareNames);`
3. Constructor reference `Supplier<InstanceMethodReferenceExample> instanceMethodReferenceExampleSupplier = InstanceMethodReferenceExample::new;`

### Streams

### Colletors

### Generics
