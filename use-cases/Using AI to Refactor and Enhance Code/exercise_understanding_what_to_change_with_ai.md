# Exercise: Understanding What to Change with AI

## Exercise 1: Code Readability Improvement (Java)

### Prompt Used

> I want to make this code more readable and maintainable. Please help me by:
>
> 1. Identifying parts that are difficult to understand
> 2. Suggesting better variable and function names
> 3. Recommending ways to break down complex sections
> 4. Pointing out any inconsistent style or formatting issues
>
> **Language/Framework:** Java
>
> **Team coding standards:** Standard Java naming conventions (camelCase for variables and methods, PascalCase for classes).

### AI Analysis

#### Readability Issues Identified

- Class names (`UserMgr`, `U`) are abbreviated and unclear.
- Method names (`a`, `f`) do not describe their purpose.
- Variable names (`un`, `pw`, `em`, `nu`, `res`) are too short and difficult to understand.
- SQL query is built through string concatenation, reducing readability and posing security risks.
- Validation logic, duplicate-user checking, and database operations are combined into one method.

#### Suggested Improvements

| Original | Suggested |
|----------|-----------|
| `UserMgr` | `UserManager` |
| `U` | `User` |
| `a()` | `addUser()` or `registerUser()` |
| `f()` | `findUserByUsername()` |
| `un` | `username` |
| `pw` | `password` |
| `em` | `email` |
| `nu` | `newUser` |
| `res` | `insertSuccessful` |
| `u_list` | `users` |
| `db` | `databaseConnection` |

#### Code Structure Improvements

- Extract user validation into a separate method.
- Create a helper method to check whether a username already exists.
- Use descriptive comments or JavaDoc.
- Replace SQL string concatenation with prepared statements.
- Apply consistent spacing and formatting.

#### Readability Issues I Might Have Missed

- Poor class naming.
- Mixing validation and database logic.
- SQL injection risk from concatenated SQL.
- Lack of documentation.



## Exercise 2: Function Refactoring (Python)

### Prompt Used

> I have a function that I think is doing too much. Please help me refactor it by:
>
> 1. Identifying the different responsibilities this function has
> 2. Suggesting how to break it into smaller, focused functions
> 3. Improving the organization and flow of the code
> 4. Pointing out any other issues you notice
>
> This function should process orders, update inventory, and track revenue.

### Responsibilities Identified

The function currently performs several independent tasks:

1. Validate inventory.
2. Validate customer information.
3. Calculate product prices.
4. Apply premium customer discounts.
5. Update inventory quantities.
6. Calculate shipping costs.
7. Calculate tax.
8. Calculate the final order price.
9. Update total revenue.
10. Create the processed order result.
11. Record processing errors.

### Suggested Smaller Functions

- `validate_order()`
- `calculate_price()`
- `apply_discount()`
- `calculate_shipping()`
- `calculate_tax()`
- `update_inventory()`
- `create_order_result()`

The main `process_orders()` function should coordinate these helper functions instead of handling every responsibility itself.

### Benefits of Refactoring

- Easier to understand.
- Easier to test each function independently.
- Easier to maintain and extend.
- Reduces code complexity.
- Makes debugging simpler.

### Comparison with My Own Ideas

Initially, I thought about separating only the validation logic. The AI also recommended extracting pricing, shipping, tax calculations, inventory updates, and result creation into separate helper functions, resulting in a cleaner and more maintainable design.



## Exercise 3: Code Duplication Detection (JavaScript)

### Prompt Used

> I suspect there might be repeated patterns in this code that could be consolidated. Please help me by:
>
> 1. Identifying similar code segments that appear multiple times
> 2. Suggesting ways to eliminate the duplication
> 3. Showing what the refactored code could look like
> 4. Explaining the benefits of the suggested changes

### Repeated Patterns Identified

The AI identified duplicated logic in:

- Average age calculation.
- Average income calculation.
- Average score calculation.
- Highest age calculation.
- Highest income calculation.
- Highest score calculation.

Each calculation uses nearly identical loops with only the property name changing.

### Suggested Refactoring

Create reusable helper functions such as:

- `calculateAverage(data, property)`
- `calculateHighest(data, property)`

The main function can then call these helper methods for each property rather than repeating the same logic.

### Benefits

- Eliminates duplicated code.
- Improves readability.
- Simplifies maintenance.
- Makes adding new statistics much easier.
- Reduces the chance of introducing bugs when making future changes.

### Best Approach for Junior Developers

Using helper functions like `calculateAverage()` and `calculateHighest()` provides the best balance between readability and maintainability. The functions clearly communicate their purpose while avoiding unnecessary complexity.



# Reflection Questions

## 1. Which prompting strategy did you find most useful? Why?

The **Function Refactoring** prompt was the most useful because it clearly identified the different responsibilities within a large function and suggested practical ways to divide it into smaller, reusable functions. This makes the code easier to understand, test, and maintain.

## 2. What kinds of improvements did the AI suggest that you might not have thought of?

The AI suggested:

- Using more descriptive class, method, and variable names.
- Extracting helper functions for repeated logic.
- Separating validation from business logic.
- Using prepared SQL statements instead of string concatenation.
- Adding documentation and improving formatting.

## 3. Were there any suggestions the AI made that you disagreed with? Why?

Most suggestions were useful. However, creating many small helper functions may be unnecessary for very small projects because it can increase complexity. For larger applications, however, the improvements make the code more maintainable.

## 4. How might you adapt these prompts for your specific codebase or tech stack?

I would specify the programming language, framework, coding standards, and project requirements. I would also ask the AI to preserve existing functionality, follow team coding standards, and recommend improvements that fit the project's architecture.

## 5. What safeguards would you put in place before applying AI-suggested refactoring to production code?

- Ensure automated tests are available before refactoring.
- Carefully review every AI suggestion.
- Verify that the application's functionality remains unchanged.
- Conduct code reviews with teammates.
- Test thoroughly in a development or staging environment before deploying to production.



# Next Steps

1. Apply these prompting strategies to personal or academic coding projects.
2. Build a personal library of effective AI prompts for refactoring and code improvement.
3. Continue practising refactoring to strengthen code quality and maintainability skills.
4. Always ensure tests are available before making changes to production code.
