# JPA Week 2

## Learning Objectives

### Monday

1. JPQL Query types
   - Be able to explain the purpose of JPQL and how it differs from SQL.
   - What is the difference between `TypedQuery` and `Query` and when to use them.
   - Be able to demonstrate and explain how to use `NamedQueries`.
   - Be able to demonstrate `native queries` and explain the purpose.

2. JPQL result types
   - Be able to explain the difference between the methods `getResultList` and `getSingleResult`.
   - Be able to explain the difference between the methods `setFirstResult` and `setMaxResults`.
   - Be able to explain `getFirstResult` and `getMaxResults` methods.

3. JPA relations between entities (1)
   - Be able to explain and demonstrate the use of the annotations `@OneToOne`, `@OneToMany`, `@ManyToOne`.

4. JPA relations between entities (2)
   - Be able to explain the concepts `identifying` and `non-identifying` relationships.
   - Be able to explain and show the difference between `uni-directional` and `bi-directional` relationships. 
   - Explain the use of `@MapsId` annotation.

5. JPA annotations.
   - explain and demonstrate the use of `Enumerated` annotation to map Java enum types to database columns.
   - explain and demonstrate the use of `Temporal` annotation to map Java Date and Calendar types to database columns.
   - explain the use of `@Transient` annotation.

6. JPQL
  - Be able to explain the difference between the methods `setParameter` and `setParameters`.
  - Be able to explain the difference between the methods `executeUpdate` and `executeQuery`.
  - Be able to explain the methods `isBound`.

7. Cascading and data fetching.
    - explain and demonstrate the difference between `FetchType.EAGER` and `FetchType.LAZY`.
    - explain and demonstrate the difference between `CascadeType.ALL` and `CascadeType.PERSIST`.
    - explain and demonstrate the difference between `orphanRemoval=true` and `orphanRemoval=false`.

### Wednesday

1. Be able to explain and demonstrate JPA relation `@ManyToMany`.
   - explain the `@ManyToMany` annotation.
   - explain and demonstrate the difference between `owning` and `inverse` side of a relationship.
   - explain and demonstrate the `@JoinColumn` annotation to specify the foreign key column name.

2. DTO projections in JPQL
   - Explain what an DTO is
   - Explain and demonstrate the use of DTO projections in JPQL queries
