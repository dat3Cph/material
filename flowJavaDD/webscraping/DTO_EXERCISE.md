### DTO When, How, and Why

#### The Problem

You have a model that you want to return to the client. You have a few options:

1. Return the model directly.
2. Return a DTO.

Which one should you choose? When should you choose one over the other? How do you know which one to choose?

#### The Solution

The answer is simple: **it depends**.
You should use a DTO when you want to return a subset of the model's attributes.
You should use a model when you want to return all the model's attributes.

#### Scenario Return the Model Directly

You have a model called `City` with the following attributes:

* `town` - string
* `zip_code` - string
* `state` - string
* `country` - string

You have a controller method called `show` that returns a `City` object.

```java
public City show() {
    return new City("New York", "10001", "NY", "USA");
}
```

You have a view that renders the `City` object.

```html
<h1>City</h1>
<p>City: {{city.town}}</p>
<p>Zip Code: {{city.zipCode}}</p>
<p>State: {{city.state}}</p>
<p>Country: {{city.country}}</p>
```

#### Scenario Return a DTO

You have a model called `City` with the following attributes:

* `town` - string
* `zip_code` - string
* `state` - string
* `country` - string
* `full_name` - string
* `full_address` - string
* `full_name_and_address` - string

You have a controller method called `show` that returns a `City` object.

```java
public City show() {
    return new City("New York", "10001", "NY", "USA");
}
```

You have a view that renders the `City` object.

```html
<h1>City</h1>
<p>City: {{city.fullName}}</p>
<p>Zip Code: {{city.fullAddress}}</p>
<p>State: {{city.fullNameAndAddress}}</p>
```

#### Common Mistakes

- Returning a model directly when you should be returning a DTO.
- Creating a DTO that is a direct copy of a model.
- Creating a DTO that is a direct copy of a database table.
- Creating to many DTOs that are all very similar.
- Add business logic to a DTO.

This exercise is designed to help you understand the difference between a DTO and a model.
It is also designed to help you understand the difference between a model and a database table. 

#### Quick Review

- A DTO is a data transfer object.
- A DTO is a class that is used to transfer data between different layers of an application.
- A DTO are objects that carry data between processes in order to reduce the number of method calls.
- The pattern was interpreted as a way to encapsulate data transfer in a single object.
- The pattern was first introduced by Martin Fowler in 1998. https://martinfowler.com/books/eaa.html


#### The Exercise

You are given a model called `User` with the following attributes:

* `id` - integer
* `first_name` - string
* `last_name` - string
* `email` - string

You are given a model called `BankAccount` with the following attributes:

* `id` - integer
* `user_id` - integer
* `account_number` - string
* `balance` - double
* `created_at` - date
* `updated_at` - date

Task 1: Create a DTO called `UserDTO` with the following attributes:

* `fullName` - string
* `email` - string

Task 2: Create a main method that creates a `User` object and a `UserDTO` object.

Task 3: Print out the fullName from the `UserDTO` object.

Task 4: Create a DTO called `BankAccountDTO` with the following attributes:

* `accountNumber` - string
* `balance` - double
* `createdAt` - date

Task 5: In the main method create a `BankAccount` object and a `BankAccountDTO` object.

Task 6: Create a DTO called `BankAccountWithUserDTO` with the following attributes:

* `accountNumber` - string
* `balance` - double
* `fullName` - string
* `email` - string

Task 7: In the main method create a `BankAccountWithUserDTO` object with help from the User and BankAccount objects.

Task 8: Print out the fullName and balance from the `BankAccountWithUserDTO` object.





