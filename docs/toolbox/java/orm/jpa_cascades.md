---
title: JPA Cascades
description: crud examples 
layout: default
nav_order: 2
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/cascades/
---

# JPA - When to Use Cascades in JPA

Cascade types in JPA (Java Persistence API) can be tricky and, often perform operations that you may not intend, especially in more complex applications. However, they can be useful when dealing with certain parent-child relationships, where you want actions performed on an entity to propagate to its related entities.

## When to Use Cascade Types

Using cascade types pays off when you have strong, dependent relationships between entities, such as a one-to-many or many-to-one relationship where the lifecycle of one entity should control the lifecycle of another. Here are some scenarios where it makes sense:

1. **Simple Parent-Child Relationships**:
   - When you have entities like `Order` and `OrderLine` (where `Order` is the parent and `OrderLine` is the child), and you want any operations on the parent entity (like persist, remove, etc.) to automatically apply to the child. Using `CascadeType.ALL` makes sense here, as it simplifies the code by not requiring you to explicitly handle child entities every time you persist or delete an order.

2. **Avoiding Boilerplate Code**:
   - Without cascade operations, you'd need to manually persist, merge, or remove associated entities. This adds complexity and clutter to the code. Cascade types help streamline the persistence logic by automatically handling related entities.

3. **Aggregated Data**:
   - In scenarios where entities form a logical unit, like an aggregate in DDD (Domain-Driven Design), cascading persistence can be beneficial. For example, in a blog application, a `Post` may have `Comments`, and you'd want to cascade any operations from the `Post` to its `Comments`.

## Common Cascade Types and When They Apply

- **`CascadeType.PERSIST`**: Automatically saves child entities when the parent is saved. This is useful when child entities have no independent lifecycle (e.g., when creating a new parent-child relationship).
  
- **`CascadeType.MERGE`**: Updates child entities when the parent is updated. It’s useful when child entities are managed through the parent.

- **`CascadeType.REMOVE`**: Deletes child entities when the parent is deleted. This is often desirable when the child entities should not exist independently of the parent.

- **`CascadeType.DETACH`**: Detaches child entities when the parent is detached from the persistence context. This can be useful in some cases when you don’t want to continue managing child entities separately.

- **`CascadeType.REFRESH`**: Refreshes child entities when the parent is refreshed.

- **`CascadeType.ALL`**: Combines all the above types. While this is convenient in some scenarios, it’s also risky because it can lead to unintended behavior, especially with `REMOVE`.

## When Cascade Types Cause Problems

- **Unintentional Deletes**: Using `CascadeType.REMOVE` can be dangerous if not used carefully. For example, deleting a `Department` entity might unintentionally delete all `Employees` in that department, when you actually wanted to just dissociate them.
  
- **Performance Issues**: Cascading operations like `PERSIST` or `MERGE` can cause performance bottlenecks, as a single operation on a parent entity might trigger several database operations on related entities. In large datasets, this can lead to excessive database queries and slow performance.

- **Complex Relationships**: In cases of many-to-many relationships or bidirectional relationships, cascade types can lead to unexpected behavior, such as infinite loops, where JPA continuously tries to persist or merge entities.

## Best Practices

1. **Use Cascade Types Selectively**: Only use cascading where you are sure that the child entity’s lifecycle is completely dependent on the parent. In other cases, it’s safer to manage related entities manually.

2. **Prefer Explicit Operations**: Instead of relying on cascading, consider handling related entities explicitly in your service layer, especially for complex relationships. This gives you more control over how and when child entities are persisted, updated, or deleted.

3. **Be Cautious with `CascadeType.ALL`**: While it simplifies things in smaller, well-controlled applications, `CascadeType.ALL` can lead to unintended behavior as applications grow. It’s better to be explicit about which operations should cascade.

4. **Use `orphanRemoval` Carefully**: In conjunction with `CascadeType.REMOVE`, setting `orphanRemoval=true` ensures that when a child is removed from a parent’s collection, it is also deleted from the database. This is useful, but must be used with care to avoid unwanted deletions.

By understanding when cascading is useful and where it can lead to issues, you can apply it in a way that reduces code complexity without sacrificing control over your data's lifecycle.
