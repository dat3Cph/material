# Code Standard 3 semester 2024

1. **Naming Conventions**:
    - **Classes, Interfaces**: Use UpperCamelCase (e.g., `CustomerAccount`, `DataProcessor`).
    - **Interfaces implementations**: Use UpperCamelCase and `Impl`(e.g., `CustomerAccountImpl`, `DataProcessorImpl`)
    ```java
     interface CustomerAccount {
        // interface blueprint
     }
     class CustomerAccountImpl {
        // interface implementation
     }
    ```
    - **Methods and Variables**: Use lowerCamelCase (e.g., `calculateTotal`, `orderId`).
    - **Constants**: Use all uppercase letters with words separated by underscores (e.g., `MAX_BUFFER_SIZE`).
    - Use english for all naming conventions. (class, methods, interfaces osv.)


2. **Indentation and Spacing**:
    - Use 4 spaces per indentation level. Do not use tabs.
    - Ensure consistent spacing between operators and after commas for readability.

   ```java
   int sum = a + b;
   ```

3. **Braces Placement**:
    - Place opening braces `{` on the same line as the statement, and closing braces `}` on a new line.

   ```java
   if (condition) {
       // code
   } else {
       // code
   }
   ```

4. **Line Length**:
    - Limit each line of code to **80-100** characters to enhance readability.

5. **Class Structure**:
    - Follow this order: class variables, constructors, methods (public first, then protected, private last).

6. **Avoid Magic Numbers**:
    - Replace magic numbers with named constants to make the code more readable and maintainable.

   ```java
   final int MAX_USERS = 100;
   ```

7. **Use Proper Access Modifiers**:
    - Encapsulate class fields by making them private and provide access via public getters and setters if needed.

8. **Use Annotations**:
    - Use annotations like `@Override`, `@Deprecated`, and `@SuppressWarnings` properly to clarify code behavior.

9. **Method Length**:
    - Keep methods short and focused on a single task. Ideally, methods should not exceed 20-30 lines.

10. **Consistent Use of `this` Keyword**:
    - Use `this` keyword explicitly to refer to instance variables when necessary, especially in constructors and setters.

11. **Documentation and Comments**:
    - Use Javadoc comments for public APIs. Inline comments should be used sparingly and only to explain complex logic.

12. **Use of Generics**:
    - Utilize generics to write type-safe code, avoiding unnecessary casting.

    ```java
    List<String> names = new ArrayList<>();
    ```

13. **Exception Handling**:
    - Handle exceptions specifically rather than using generic `catch (Exception e)`. Use meaningful exception messages.

14. **Immutability**:
    - Prefer immutability by making fields `final` where possible and avoiding setters unless necessary.

15. **Testing**:
    - Write unit tests for your code using JUnit or a similar framework. Ensure your tests cover edge cases and are regularly maintained.

These conventions help create clean, maintainable, and robust Java code.