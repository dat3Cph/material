# Learning Objectives for Java 8 Deep Dive week

## Day 1

### 1. Understand and use Java 8 streams

1.1 Understand and use Java 8 stream operations like `map`, `filter`, `reduce`, `collect`, `flatMap`, `peek`, `distinct`, `sorted`, `limit`, `skip`, `anyMatch`, `allMatch`, `noneMatch`, `findFirst`, `findAny`

1.2 Understand and use Java 8 parallel streams

1.3 Understand and use Java 8 stream collectors: `averagingDouble`, `averagingInt`, `averagingLong`, `collectingAndThen`, `counting`, `groupingBy`, `joining`, `mapping`, `maxBy`, `minBy`, `partitioningBy`, `reducing`, `summarizingDouble`, `summarizingInt`, `summarizingLong`, `summingDouble`, `summingInt`, `summingLong`, `toCollection`, `toList`, `toMap`, `toSet`
1.4 Understand and use Java 8 stream `reduce` operation

### 2. Understand and use Java Generics

1. **Understand the Purpose of Generics**: Learners should be able to explain why generics are used in Java, particularly how they help in writing type-safe code and reduce runtime errors by catching type mismatches at compile-time.

2. **Learn to Define and Use Generic Classes and Methods**: Learners should be able to define their own generic classes and methods, understanding how to create and utilize type parameters in these constructs.

3. **Master Bounded Type Parameters**: Learners should be able to use bounded type parameters (e.g., `<T extends Number>`) to restrict the types that can be passed to a generic class or method, and understand how to use wildcards (`? extends T`, `? super T`) to increase the flexibility of generics.

4. **Apply Generics in Common Data Structures**: Learners should be able to apply generics to commonly used Java data structures like `List`, `Set`, `Map`, etc., and understand the benefits and limitations of using generics with these collections.

5. **Understand Type Erasure**: Learners should have a basic understanding of type erasure in Java, including how generic type information is removed at runtime and the implications this has for using generics in Java.

### 3. Understand and use Java Collections E.g

    - `List`, `Set`, `Map`, `Queue`, `Deque`, `SortedSet`, `SortedMap`, `NavigableSet`, `NavigableMap`, `Collection`, `Iterable`, `Iterator`, `ListIterator`, `Comparator`, `Comparable`, `Enumeration`, `Dictionary`, `AbstractCollection`, `AbstractList`, `AbstractSequentialList`, `AbstractSet`, `LinkedList`, `ArrayList`, `Vector`, `Stack`, `HashSet`, `LinkedHashSet`, `TreeSet`, `HashMap`, `LinkedHashMap`, `TreeMap`, `WeakHashMap`, `IdentityHashMap`, `Collections`, `Arrays`.

## Day 2

### 1. Understand what functional programming is and how to use it in Java

1.1 Understand and illustrate principles of functional programming.

1.2 Understand and use Java 8 functional interfaces

1.3 Understand and use Java 8 labmda expressions

1.4 Understand and use Java 8 method references: `static`, `instance`, `constructor`

### 2. Understand and use Java 8 default and static interface methods

### 3. Understand and use Java 8 Date/Time API

3.1 Understand and use Java 8 Date/Time API classes: `Duration`, `Instant`, `LocalDate`, `LocalDateTime`, `LocalTime`, `MonthDay`, `OffsetDateTime`, `OffsetTime`, `Period`, `Year`, `YearMonth`, `ZonedDateTime`, `ZoneId`, `ZoneOffset`

3.2 Understand and use Java 8 Date/Time API methods: `between`, `from`, `now`, `of`...
