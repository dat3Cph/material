# Exercise hints for Java Deep Dive week

## The map function

In functional programming, the `map` method is a higher-order function commonly used to transform the elements of a collection (such as an array, list, or any iterable data structure) by applying a given function to each element and returning a new collection with the transformed values. The `map` function is a fundamental building block for many functional programming operations and is particularly useful for working with lists or arrays of data.

Here's a general description of how the `map` function works:

1. Input:
   - A function (often referred to as a mapping function or transformation function): This function takes one element from the original collection as its input and returns a transformed or mapped value.
   - A collection (e.g., an array or list) of elements that you want to transform.

2. Operation:
   - The `map` function iterates over each element in the input collection.
   - For each element, it applies the provided mapping function to transform the element.
   - It collects the transformed values and stores them in a new collection (typically an array or list).

3. Output:
   - The `map` function returns a new collection containing the transformed values. The length of this collection is typically the same as the length of the original collection.

## The filter function

In functional programming, the `filter` function is another higher-order function used to work with collections (e.g., arrays, lists) by selecting elements that satisfy a given condition and returning a new collection containing only those elements. The `filter` function is particularly useful for creating a new collection of elements that meet specific criteria.

Here's a general description of how the `filter` function works:

1. Input:
   - A predicate function: This function takes an element from the original collection as its input and returns a boolean value (true or false) based on whether the element satisfies a given condition.
   - A collection of elements that you want to filter.

2. Operation:
   - The `filter` function iterates over each element in the input collection.
   - For each element, it applies the provided predicate function to check if the element meets the specified condition.
   - It collects the elements that satisfy the condition and stores them in a new collection.

3. Output:
   - The `filter` function returns a new collection containing only the elements that satisfy the condition specified by the predicate function.
