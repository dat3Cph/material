# Agenda 2024 day 2
## 3. semester

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

### Method References
[Demo](https://github.com/HartmannDemoCode/functional-demo/blob/main/src/main/java/demos/day1/ClassDemo.java)
1. Static method reference `Arrays.sort(names, StaticMethodReferenceExample::compareNames);`
2. Instance method reference `Arrays.sort(names, new InstanceMethodReferenceExample()::compareNames);`
3. Constructor reference `Supplier<InstanceMethodReferenceExample> instanceMethodReferenceExampleSupplier = InstanceMethodReferenceExample::new;`

### Streams

### Colletors

### Generics
