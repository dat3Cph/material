---
title: Hamcrest Matchers
description: How to use Hamcrest for writing test cases
layout: default
parent: Test
grand_parent: Toolbox
nav_order: 4
permalink: /toolbox/test/hamcrest
---

# Hamcrest matchers

Here is a table summarizing some common Hamcrest matchers along with brief explanations of their usage:

| **Matcher**         | **Description**                                                                                             | **Example Usage**                                                                                             |
|---------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `is(T value)`       | Checks if the actual value is equal to the expected value. It is a shorthand for `equalTo()`.                | `assertThat(actual, is(5));`                                                                                  |
| `equalTo(T value)`  | Checks if the actual value is equal to the expected value.                                                   | `assertThat(actual, equalTo(5));`                                                                             |
| `not(Matcher<T> matcher)` | Asserts that the actual value does **not** match the given matcher.                                       | `assertThat(actual, not(equalTo(5)));`                                                                        |
| `greaterThan(T value)` | Asserts that the actual value is greater than the expected value.                                            | `assertThat(actual, greaterThan(5));`                                                                         |
| `lessThan(T value)` | Asserts that the actual value is less than the expected value.                                                | `assertThat(actual, lessThan(10));`                                                                           |
| `greaterThanOrEqualTo(T value)` | Asserts that the actual value is greater than or equal to the expected value.                               | `assertThat(actual, greaterThanOrEqualTo(5));`                                                                 |
| `lessThanOrEqualTo(T value)` | Asserts that the actual value is less than or equal to the expected value.                                  | `assertThat(actual, lessThanOrEqualTo(10));`                                                                  |
| `containsString(String substring)` | Checks if the actual string contains the specified substring.                                        | `assertThat(actual, containsString("example"));`                                                              |
| `startsWith(String prefix)` | Asserts that the actual string starts with the given prefix.                                              | `assertThat(actual, startsWith("Hello"));`                                                                    |
| `endsWith(String suffix)` | Asserts that the actual string ends with the given suffix.                                                 | `assertThat(actual, endsWith("World"));`                                                                      |
| `hasItem(T item)`   | Checks if a collection contains the specified item.                                                          | `assertThat(list, hasItem("item1"));`                                                                         |
| `hasItems(T... items)` | Checks if a collection contains all the specified items.                                                      | `assertThat(list, hasItems("item1", "item2"));`                                                               |
| `empty()`           | Asserts that a collection or array is empty.                                                                 | `assertThat(collection, is(empty()));`                                                                        |
| `notNullValue()`    | Asserts that the actual value is not `null`.                                                                 | `assertThat(actual, is(notNullValue()));`                                                                     |
| `nullValue()`       | Asserts that the actual value is `null`.                                                                     | `assertThat(actual, is(nullValue()));`                                                                        |
| `instanceOf(Class<?> clazz)` | Asserts that the actual value is an instance of the specified class.                                      | `assertThat(actual, is(instanceOf(String.class)));`                                                           |
| `allOf(Matcher<?>... matchers)` | Asserts that all of the provided matchers are satisfied.                                               | `assertThat(actual, allOf(startsWith("He"), containsString("el"), endsWith("lo")));`                           |
| `anyOf(Matcher<?>... matchers)` | Asserts that at least one of the provided matchers is satisfied.                                        | `assertThat(actual, anyOf(equalTo(5), equalTo(10)));`                                                         |

## Explanation

- **`is()` and `equalTo()`**: `is()` is a shorthand for `equalTo()`, used for simple equality comparisons.
- **`not()`**: Negates the result of a matcher.
- **Comparative matchers** (`greaterThan()`, `lessThan()`, etc.): Used for comparing numerical values.
- **String matchers** (`containsString()`, `startsWith()`, `endsWith()`): Used to assert conditions on strings.
- **Collection matchers** (`hasItem()`, `hasItems()`, `empty()`): Used for checking conditions on collections like lists or sets.
- **Null matchers** (`notNullValue()`, `nullValue()`): For asserting `null` or non-`null` values.
- **Type matcher** (`instanceOf()`): For asserting that an object is an instance of a specific class.
- **`allOf()` and `anyOf()`**: Logical matchers for combining multiple conditions.
