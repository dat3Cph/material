# Exercise TDD
![](../images/tdd.png)

## Steps
The purpose of this exercise is to train yourself in the art of TDD. 
It is not easy to do so practise it as often as you can.

- Open up your IDE and create a new maven project: tdd-koans
- Create a test class (That's right we start by creating the test NOT the source code)
- In the test class create tests for each of the 8 requirements found [here](https://github.com/testdouble/contributing-tests/wiki/Greeting-Kata)
- Hint for requirement 4: 
  - Use Object type for the parameter and
  - `if(o instanceof String)` and 
  - `if(o instanceof String[])`
- Whenever you write a new test, create the classes and methods needed for your test class to compile (Let your IDE auto create them with no implementation).
- Run the test and see that it fails.
- Implement the method so the test no longer fails.
- Run the test again to see that it is green.

When you have successfully written test cases for all 8 requirements and implemented the necessary source code (same ONE method for all requirements) reflect on this exercise compared to how you have been writing code previously. Do you see any benefits in doing it this way? Do you see any down sides?

For more practise exercises look [here](https://osherove.com/tdd-kata-1/)
