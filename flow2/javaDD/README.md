# Week 4: Java 8 Deep Dive
## Content
Lambda, Functional Interfaces, Streams, Optionals, Collectors, Generics, Functional Programming and much more
Monday:
- [Part 1](Java8DeepDive.md)
- [Exercises](ClassExercises.md)

Wednesday:
- [Part 2](Java8DeepDive2.md)
- [Exercises](ClassExercises.md)

Friday:
- [Exercises](Week4Exercises.md)

## Learning Objectives for Java 8 week
1. Understand what functional programming is and how to use it in Java
    - Understand and use Java 8 functional interfaces
    - Understand and use Java 8 labmda expressions
    - Understand and use Java 8 method references: `static`, `instance`, `constructor`
2. Understand and use Java 8 streams
    - Understand and use Java 8 stream operations like `map`, `filter`, `reduce`, `collect`, `flatMap`, `peek`, `distinct`, `sorted`, `limit`, `skip`, `anyMatch`, `allMatch`, `noneMatch`, `findFirst`, `findAny`
    - Understand and use Java 8 parallel streams
    - Understand and use Java 8 stream collectors: `averagingDouble`, `averagingInt`, `averagingLong`, `collectingAndThen`, `counting`, `groupingBy`, `joining`, `mapping`, `maxBy`, `minBy`, `partitioningBy`, `reducing`, `summarizingDouble`, `summarizingInt`, `summarizingLong`, `summingDouble`, `summingInt`, `summingLong`, `toCollection`, `toList`, `toMap`, `toSet`
    - Understand and use Java 8 stream `reduce` operation
3. Understand and use Java 8 default and static interface methods
4. Understand and use Java 8 Optional
    - Understand and use Java 8 Optional methods: `empty`, `filter`, `flatMap`, `get`, `ifPresent`, `isPresent`, `map`, `of`, `ofNullable`, `orElse`, `orElseGet`, `orElseThrow`
    - 
5. Understand and use Java 8 Date/Time API
    - Understand and use Java 8 Date/Time API classes: `Clock`, `Duration`, `Instant`, `LocalDate`, `LocalDateTime`, `LocalTime`, `MonthDay`, `OffsetDateTime`, `OffsetTime`, `Period`, `Year`, `YearMonth`, `ZonedDateTime`, `ZoneId`, `ZoneOffset`
    - Understand and use Java 8 Date/Time API methods: `between`, `from`, `now`, `of`, `ofInstant`, `ofEpochSecond`, `parse`, `parseBest`, `parseUnresolved`, `parseBest`, `parseUnresolved`, `with`, `withDayOfMonth`, `withDayOfYear`, `withMonth`, `withYear`, `withHour`, `withMinute`, `withSecond`, `withNano`, `withZoneSameInstant`, `withZoneSameLocal`, `truncatedTo`, `toEpochSecond`, `toInstant`, `toLocalDate`, `toLocalDateTime`, `toLocalTime`, `toOffsetDateTime`, `toOffsetTime`, `toZonedDateTime`, `until`, `atOffset`, `atZone`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth`, `atDay`, `atStartOfDay`, `atTime`, `atYear`, `atMonth` or `atDay`
6. Understand and use Java Generics: `class`, `interface`, `method`, `constructor`, `wildcard`, `bounded wildcard`, `type parameter`, `type argument`, `type variable`, `type erasure`, `generic type`, `generic method`, `generic constructor`, `generic interface`, `generic class`, `generic type parameter`, `generic type argument`, `generic type variable`, `generic type erasure`, `generic method type parameter`, `generic method type argument`, `generic method type variable`, `generic method type erasure`, `generic constructor type parameter`, `generic constructor type argument`, `generic constructor type variable`, `generic constructor type erasure`, `generic interface type parameter`, `generic interface type argument`, `generic interface type variable`, `generic interface type erasure`, `generic class type parameter`, `generic class type argument`, `generic class type variable`, `generic class type erasure`
7. Understand and use Java Collections: 
    - `List`, `Set`, `Map`, `Queue`, `Deque`, `SortedSet`, `SortedMap`, `NavigableSet`, `NavigableMap`, `Collection`, `Iterable`, `Iterator`, `ListIterator`, `Comparator`, `Comparable`, `Enumeration`, `Dictionary`, `AbstractCollection`, `AbstractList`, `AbstractSequentialList`, `AbstractSet`, `LinkedList`, `ArrayList`, `Vector`, `Stack`, `HashSet`, `LinkedHashSet`, `TreeSet`, `HashMap`, `LinkedHashMap`, `TreeMap`, `WeakHashMap`, `IdentityHashMap`, `Collections`, `Arrays`.
8. Understand and use Java Concurrency
    - Understand and use Java Concurrency: `Thread`, `Runnable`, `Callable`, `Future`, `Executor`, `ExecutorService`, `Executors`, `CompletionService`, `ExecutorCompletionService`, `ScheduledExecutorService`, `ScheduledFuture`, `TimeUnit`, `Lock`, `ReadWriteLock`, `ReentrantLock`, `ReentrantReadWriteLock`, `Condition`, `Semaphore`, `CountDownLatch`, `CyclicBarrier`, `Phaser`, `Exchanger`, `ForkJoinPool`, `ForkJoinTask`, `ForkJoinWorkerThread`, `ForkJoinPool.ForkJoinWorkerThreadFactory`, `ForkJoinPool.ManagedBlocker`, `ThreadLocalRandom`, `ThreadFactory`, `Callable`, `Future`, `FutureTask`, `RecursiveAction`, `RecursiveTask`, `AbstractExecutorService`.