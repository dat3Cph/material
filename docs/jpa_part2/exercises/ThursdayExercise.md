# Order system

## Object Relational Mapping with JPA

This model represents an initial domain model for a system that can
handle orders. Order refers to a customer and a number of order lines.
Each order line has a quantity and it refers to a product.
The product has a name, a description and a price. 
The price for each order line is the quantity times the price.
The total price for an order is the sum of all its order lines.

![Domain model](../../images/JPA_Order_Exercise_Domain.svg)

1. Examine and understand the model.
2. Create a Maven Java Application with IntelliJ, and use Object Relational Mapping (JPA) to implement the OO classes and the corresponding Database Tables [^1] [^2].
3. Create a DAO and implement as many of the methods below as you have time for, not necessarily in the given order [^3].
    1. Create a Customer.
    2. Find a Customer.
    3. Get all Customers
    4. Create a Product
    5. Find a Product
    6. Create an Order and Add it to a Customer
    7. Create an OrderLine for a specific Product, and add it to an Order
    8. Find all Orders, for a specific Customer
    9. Find the total price of an order (tricky - but create a dto for the result and use the `new` keyword in a jpql statement)

[^1]: You don't necessarily need to implement all Entity-classes
before you begin on part-3. Do it as you go along.
[^2]: Customer to Order should probably be bi-directional while
Order to OrderLine should probably be uni-directional. Why?
[^3]: Use TDD to execute and test your methods
