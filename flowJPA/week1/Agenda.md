# Agenda JPA 1 thursday
1. Update entity
2. Lazy loading vs Eager loading
3. Lifecycle annotations
```java
    @PrePersist
    private void prePersist() {
        this.createdAt = LocalDateTime.now();
        if (!validatePhoneNumber(this.phoneNumber)) {
            throw new IllegalArgumentException("Phone number could not be validated");
        }
    }

    @PreUpdate
    public void preUpdate() {
        this.updatedAt = LocalDateTime.now();
        if (!validatePhoneNumber(this.phoneNumber)) {
            throw new IllegalArgumentException("Phone number could not be validated");
        }
    }
```
4. jUnit
5. JPQL
```java
    TypedQuery<Hotel> query = em.createQuery("SELECT h FROM Hotel h WHERE h.city = :city", Hotel.class);
    query.setParameter("city", "Stockholm");
    List<Hotel> hotels = query.getResultList();
```
and with group by
```java
    TypedQuery<Object[]> query = em.createQuery("SELECT h.city, COUNT(h) FROM Hotel h GROUP BY h.city", Object[].class);
    List<Object[]> results = query.getResultList();
    for (Object[] result : results) {
        System.out.println(result[0] + ": " + result[1]);
    }
```
and with order by
```java
    TypedQuery<Hotel> query = em.createQuery("SELECT h FROM Hotel h ORDER BY h.name", Hotel.class);
    List<Hotel> hotels = query.getResultList();
```
and with new DTO
```java
    TypedQuery<HotelDTO> query = em.createQuery("SELECT new com.example.HotelDTO(h.name, h.city) FROM Hotel h", HotelDTO.class);
    List<HotelDTO> dtos = query.getResultList();
```
6. Named Queries