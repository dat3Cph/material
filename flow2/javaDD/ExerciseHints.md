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

## Supplier

Example of how to create Car objects where Car has a name and a price. The name is a String and the price is a double. The constructor takes these two values as parameters.

```java
public class Car {
    private String name;
    private double price;

    public Car(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
```
Creating 10 cars with random names and prices between 0 and 1000000:
```java

import java.util.ArrayList;
import java.util.List;
import java.util.Random;
import java.util.function.Supplier;


public class CarFactory {

    public static void main(String[] args) {
        List<String> carNames = Arrays.asList("Mercedes","BMW","Audi","Tesla","Ford","Fiat","Peugeot","Citroen","Renault","Toyota");
        Supplier<Car> carSupplier = () -> {
            Random random = new Random();
            int randomIndex = new Random().nextInt(carNames.size());
            String randomName = carNames.get(randomIndex);
            double randomPrice = random.nextDouble() * 1000000;
            return new Car(randomName, randomPrice);
        };
        List<Car> cars = createCars(10, carSupplier);
        cars.forEach(System.out::println);
    }

    public static List<Car> createCars(int numCars, Supplier<Car> supplier) {
        List<Car> cars = new ArrayList<>();
        for (int i = 0; i < numCars; i++) {
            cars.add(supplier.get());
        }
        return cars;
    }
}
```
