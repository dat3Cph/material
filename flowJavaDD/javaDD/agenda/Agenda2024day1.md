# Agenda 2024 day 1
### Lambda
- Syntax
```java
Function<Integer, Integer> square = (x) -> x * x;
```
and
```java
Arrays.asList(1, 2, 3, 4, 5).stream().map(x -> x * x).forEach(System.out::println);
```

### Streams
- topics:
  - `map`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      List<Integer> squares = numbers.stream().map(x -> x * x).collect(Collectors.toList());
      ```
  - `filter`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      List<Integer> evenNumbers = numbers.stream().filter(x -> x % 2 == 0).collect(Collectors.toList());
      ```
  - `reduce`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      int sum = numbers.stream().reduce(0, (x, y) -> x + y);
      ```
  - `collect`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      List<Integer> squares = numbers.stream().map(x -> x * x).collect(Collectors.toList());
      ```
  - `distinct`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 1, 2, 3);
      List<Integer> distinctNumbers = numbers.stream().distinct().collect(Collectors.toList());
      ```
  - `sorted`
    - ```java
      List<Integer> numbers = Arrays.asList(5, 3, 1, 4, 2);
      List<Integer> sortedNumbers = numbers.stream().sorted().collect(Collectors.toList());
      ```
  - `limit`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      List<Integer> limitedNumbers = numbers.stream().limit(3).collect(Collectors.toList());
      ```
  - `skip`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      List<Integer> skippedNumbers = numbers.stream().skip(2).collect(Collectors.toList());
      ```
  - `forEach`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      numbers.stream().forEach(System.out::println);
      ```
  - `count`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      long count = numbers.stream().count();
      ```
  - `min`
    - ```java
      List<Integer> numbers = Arrays.asList(5, 3, 1, 4, 2);
      Optional<Integer> minNumber = numbers.stream().min(Integer::compareTo);
      ```
  - `max`
    - ```java
      List<Integer> numbers = Arrays.asList(5, 3, 1, 4, 2);
      Optional<Integer> maxNumber = numbers.stream().max((x, y) -> x.compareTo(y));
      ```
  - `anyMatch`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      boolean anyMatch = numbers.stream().anyMatch(x -> x % 2 == 0);
      ```
  - `allMatch`
    - ```java
      List<Integer> numbers = Arrays.asList(2, 4, 6, 8, 10);
      boolean allMatch = numbers.stream().allMatch(x -> x % 2 == 0);
      ```
  - `noneMatch`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 3, 5, 7, 9);
      boolean noneMatch = numbers.stream().noneMatch(x -> x % 2 == 0);
      ```
  - `findFirst`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      Optional<Integer> firstNumber = numbers.stream().findFirst();
      ```
  - `findAny`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      Optional<Integer> anyNumber = numbers.stream().findAny();
      ```
  - `toArray`
    - ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
      Integer[] numbersArray = numbers.stream().toArray(Integer[]::new);
      ```

### Java Time API
- [java.time API](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html)
- [Examples](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/demos/day2/ClassDemoTimeAPI.java)
  1. `LocalDate`
  2. `LocalTime`
  3. `LocalDateTime`
  4. `Period`
  5. `Duration`
  6. `Instant`
  7. `ZoneId`
  8. `ZonedDateTime`
