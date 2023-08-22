# JPA Week 2

## Learning Objectives

### Monday

1. JPQL
   - Be able to explain the purpose of JPQL and how it differs from SQL.
   - What is the difference between TypedQuery and Query and when to use them.
   - Be able to demonstrate and explain how to use NamedQueries.
   - Be able to explain the difference between the methods `createQuery` and `createNamedQuery`.
   - Be able to explain the difference between the methods `getResultList` and `getSingleResult`.

2. JPQL queries
   - Be able to demonstrate code with complex JPQL queries using joins, aggregate functions, group by, order by, having, subqueries and native queries.
   - Be able to explain the difference between the methods `createQuery` and `createNamedQuery`.
   - Be able to explain the difference between the methods `getResultList` and `getSingleResult`.
   - Be able to explain the difference between the methods `getFirstResult` and `setMaxResults`.
   - Be able to explain the difference between the methods `getSingleResult` and `getResultList`.

3. JPA relations between entities
   - Be able to explain and demonstrate the use of the annotations @OneToMany, @ManyToOne, @OneToOne, @ManyToMany and @JoinColumn.
   - Be able to explain the difference between unidirectional and bidirectional relationships.
   - Be able to explain the difference between eager and lazy loading.
   - Be able to explain and demonstrate cascading and orphan removal.

4. JPQL and JPA annotations.
   - explain and demonstrate the use of Enumerated annotation to map Java enum types to database columns.
   - explain and demonstrate the use of Temporal annotation to map Java Date and Calendar types to database columns.
   - Be able to explain the difference between the methods `setParameter` and `setParameters`.
   - Be able to explain the difference between the methods `executeUpdate` and `executeQuery`.

5. Cascading and data fetching.
    - explain and demonstrate the difference between FetchType.EAGER and FetchType.LAZY.
    - explain and demonstrate the difference between CascadeType.ALL and CascadeType.PERSIST.
    - explain and demonstrate the difference between orphanRemoval=true and orphanRemoval=false.


### Wednesday

1. Be able to explain and demonstrate JPA relation OneToOne.
   - explain and demonstrate the difference between unidirectional and bidirectional relationships.
   - explain and demonstrate the difference between owning and inverse side of a relationship.
   - explain and demonstrate the @JoinColumn annotation to specify the foreign key column name.

2. Be able to explain and demonstrate JPA relation OneToMany.
   - explain and demonstrate the difference between unidirectional and bidirectional relationships.
   - explain and demonstrate the difference between owning and inverse side of a relationship.
   - explain and demonstrate the @JoinColumn annotation to specify the foreign key column name.

3. Be able to explain and demonstrate JPA relation ManyToOne.
   - explain and demonstrate the difference between unidirectional and bidirectional relationships.
   - explain and demonstrate the difference between owning and inverse side of a relationship.
   - explain and demonstrate the @JoinColumn annotation to specify the foreign key column name.

4. Be able to explain and demonstrate JPA relation ManyToMany.
   - explain and demonstrate the difference between unidirectional and bidirectional relationships.
   - explain and demonstrate the difference between owning and inverse side of a relationship.
   - explain and demonstrate the @JoinTable annotation to specify the join table name and columns.
