# Assignment 6: Sales Performance Report

## Description

In this assignment, you will design and implement a Python program that analyzes a fixed collection of product sales records and produces a sales performance report.

This is the first assignment in which **functions are a primary design requirement**.

The central goal is not simply to produce the correct output. You must organize the program as a **driver coordinating multiple well-designed functions** with clear responsibilities, explicit parameters, and appropriate return values.

You will continue to use collections, repetition, decisions, counters, accumulators, and formatted output. The important new step is learning to organize those operations into cooperating functions.

The primary programming concepts in this assignment include:

- function definition and function calls;
- `main()` as the program driver;
- parameters and arguments;
- return values;
- local variables and scope;
- function contracts;
- single-responsibility function design;
- function composition;
- functions calling other functions;
- passing collections to functions;
- avoiding unnecessary side effects;
- multiple-value returns using tuples;
- systematic testing of individual functions;
- incremental software development; and
- use of automated grading feedback during development.

> **Classroom 50 autograding is used extensively in this assignment.**
>
> The autograder may test individual functions directly in addition to checking the complete program output. Therefore, required function names, parameter lists, return values, and behavior are part of the program interface and must be followed exactly.

## Learning Objectives

By completing this assignment, you should be able to:

- explain the role of `main()` as a driver function;
- decompose a larger problem into coherent functional responsibilities;
- define and call functions correctly;
- distinguish parameters from arguments;
- pass data into functions through parameters;
- return calculated results to the caller;
- distinguish `return` from `print`;
- design computational functions that do not depend unnecessarily on global state;
- pass collections to functions without modifying them unintentionally;
- use one function from another function when the design naturally requires it;
- return multiple related values using a tuple;
- explain the contract of a function in terms of inputs, outputs, assumptions, and side effects;
- test individual functions using known inputs and expected outputs;
- develop software incrementally using meaningful Git commits;
- use Classroom 50 feedback as part of an iterative development process; and
- use generative AI while retaining responsibility for design, correctness, and verification.

## Background

Before beginning this assignment, you should have:

- completed **Assignment 5: Student Performance Report**;
- completed the collections material;
- watched **Functions Part I** and reviewed the accompanying **Functions Part I notes**;
- watched **Functions Part II** and reviewed the accompanying **Functions Part II notes**;
- reviewed the [Best Practices for Procedural Programming](https://katrompas.accprofessors.com/best-practice-procedural-programming);
- reviewed the course [Commenting Guidelines](https://katrompas.accprofessors.com/commenting);
- reviewed the [.gitignore guidelines](https://katrompas.accprofessors.com/gitignore-guidelines);
- reviewed the course [README Guidelines](https://katrompas.accprofessors.com/readme-guidelines); and
- reviewed the course [commit guidelines](https://katrompas.accprofessors.com/committing).

Do not begin this assignment before completing both functions lectures and notes. The assignment assumes that you understand:

- the purpose of functions;
- the difference between parameters and arguments;
- the difference between returning and printing a value;
- `main()` as a program driver;
- function contracts;
- local scope;
- mutability and side effects; and
- the course rule that each function has **one return statement**.

## Starter Repository

Your starter repository contains:

```text
ASSIGNMENT.md
ESSAY.md
```

You are responsible for creating the rest of the project.

At minimum, your completed repository must contain:

```text
ASSIGNMENT.md
ESSAY.md
main.py
README.md
.gitignore
```

Create `main.py` yourself.

Your program must use the standard course entry-point structure:

```python
if __name__ == "__main__":
    main()
```

The `main()` function is the **driver** of this program. It should coordinate the work by calling other functions rather than contain all of the detailed calculations itself.

## Required Data Collection

Your program must contain the following collection exactly as shown (declared in main):

```python
sales = [
    ("Laptop Stand", 12, 39.95),
    ("Wireless Mouse", 25, 24.50),
    ("USB-C Hub", 8, 54.95),
    ("Mechanical Keyboard", 15, 79.99),
    ("Webcam", 6, 89.50),
]
```

Each tuple contains:

```text
(product name, units sold, unit price)
```

Do not alter the names, order, quantities, or prices in the final submitted program.

The required sales collection must be created in `main()` and passed to functions as needed.

Do **not** create the sales collection as a global variable.

Your calculations must be performed from the collection at runtime. Do not hardcode calculated values such as total revenue, total units, the top product, or the performance classification.

Your functions should continue to work correctly if the contents of the collection are changed while preserving the same general record structure.

## Required Functions

Your program must contain the following functions with the exact names and parameter lists shown.

The autograder may test these functions individually.

### `calculate_revenue(units, unit_price)`

This function must:

- calculate the revenue for one product;
- use the supplied `units` and `unit_price` parameters;
- return the calculated revenue; and
- not print anything.

The relationship is:

```text
revenue = units sold × unit price
```

Example:

```python
calculate_revenue(10, 5.00)
```

must return:

```text
50.0
```

### `calculate_total_units(sales)`

This function must:

- receive the complete sales collection;
- traverse the collection;
- calculate the total number of units sold;
- return that total; and
- not print anything.

The function must not modify the `sales` collection.

### `calculate_total_revenue(sales)`

This function must:

- receive the complete sales collection;
- traverse the collection;
- calculate the total revenue for all products;
- use `calculate_revenue()` as part of that calculation;
- return the total revenue; and
- not print anything.

This requirement is intentional. It demonstrates that one function may call another function when the responsibilities naturally relate.

The function must not modify the `sales` collection.

### `find_top_product(sales)`

This function must:

- receive the complete sales collection;
- determine which product produced the greatest revenue;
- use `calculate_revenue()` when determining product revenue;
- return a tuple containing:

  ```text
  (product name, product revenue)
  ```

- not print anything; and
- not modify the `sales` collection.

For the required data, the returned result should represent:

```text
Mechanical Keyboard
1199.85
```

The supplied collection will contain at least one product.

Do not initialize the top revenue using an arbitrary large or small "magic" value. Establish the initial state using actual data from the collection.

### `classify_performance(total_revenue)`

This function must return one of three strings according to the following rules:

| Total Revenue | Performance |
| --- | --- |
| $3000.00 or greater | `Excellent` |
| $2000.00 through less than $3000.00 | `Satisfactory` |
| Less than $2000.00 | `Needs Improvement` |

The function must:

- receive the total revenue as a parameter;
- determine the correct classification;
- return the classification string; and
- not print anything.

Boundary behavior matters.

### `display_report(sales, total_units, total_revenue, top_product, performance)`

This function is responsible for displaying the final report.

It must:

- display the program title;
- display all product sales records in their original order;
- calculate each product's displayed revenue by calling `calculate_revenue()`;
- display the summary;
- use the values supplied through its parameters; and
- not return a calculated result.

The function must not recalculate values such as total units, total revenue, top product, or performance when those values are already supplied through parameters.

The function must not modify the `sales` collection.

### `main()`

`main()` is the program's **driver**.

It must:

1. create the required `sales` collection;
2. call the appropriate functions to perform the analysis;
3. receive and retain the returned values;
4. call `display_report()` with the information required to produce the report.

`main()` should primarily describe **what the program does**, while the other functions contain the detailed work.

Do not move the calculations back into `main()` merely to make the program work.

## Function Design Requirements

This assignment is specifically about function design. Producing the correct visible output is not sufficient by itself.

### One Coherent Responsibility

Each function should perform one coherent operation.

Do not combine unrelated responsibilities merely to reduce the number of functions.

Likewise, do not create meaningless functions such as:

```python
step1()
step2()
do_stuff()
process()
```

Function names and responsibilities should communicate what the program is doing.

### Parameters Make Dependencies Explicit

Functions should receive the information they need through parameters.

Do not use global variables to communicate program data between functions.

### Computational Functions Return Results

Functions whose purpose is to calculate or determine a value should return that value to the caller.

For example:

```python
revenue = calculate_revenue(units, price)
```

Do not replace a required return value with a `print()` statement.

Remember:

> `print()` communicates with a person.  
> `return` communicates a result back to the caller.

### Single-Return Rule

**Every function in this assignment must contain no more than one `return` statement.**

This is the course standard.

If a function returns a value, calculate or determine that value first and then return it through a single return statement.

For example:

```python
def classify_performance(total_revenue):
    performance = ""

    if total_revenue >= 3000:
        performance = "Excellent"
    elif total_revenue >= 2000:
        performance = "Satisfactory"
    else:
        performance = "Needs Improvement"

    return performance
```

Do not write multiple early returns such as:

```python
if condition:
    return value1
else:
    return value2
```

### Side Effects

The computational functions in this assignment should not modify the `sales` collection.

Passing a mutable collection to a function does not automatically create a copy. A parameter may refer to the same list object as the caller.

Your functions must therefore treat the supplied sales collection as data to read, not data to modify.

### Function Composition

At least the following required relationships must exist:

```text
calculate_total_revenue()
        |
        +-- calls calculate_revenue()

find_top_product()
        |
        +-- calls calculate_revenue()

display_report()
        |
        +-- calls calculate_revenue()
```

The assignment is testing whether you can design a program as cooperating functions rather than a set of unrelated function definitions.

## Program Requirements

For the required data set, the program must:

1. calculate the revenue for each product;
2. calculate the total units sold;
3. calculate total revenue;
4. determine the top product by revenue;
5. classify overall performance;
6. display all product records in their original order; and
7. display the final summary.

There is **no user input** in this assignment.

## Required Output

The completed program must produce:

```text
Sales Performance Report
Product Sales
Laptop Stand: 12 units @ $39.95 = $479.40
Wireless Mouse: 25 units @ $24.50 = $612.50
USB-C Hub: 8 units @ $54.95 = $439.60
Mechanical Keyboard: 15 units @ $79.99 = $1199.85
Webcam: 6 units @ $89.50 = $537.00
Summary
Products processed: 5
Units sold: 66
Total revenue: $3268.35
Top product: Mechanical Keyboard - $1199.85
Performance: Excellent
```

The required labels, capitalization, ordering, spaces, punctuation, and numeric formatting are part of the program interface.

All currency values must display exactly two digits after the decimal point.

`Products processed` must be determined from the collection rather than hardcoded.

## Autograding

> **IMPORTANT: Classroom 50 autograding is a major part of this assignment.**

The autograder may evaluate both:

1. the complete program output; and
2. the behavior of individual required functions.

This means that a program can appear to produce the correct final report and still fail automated tests if its functions do not follow the required interface.

For example, the grader may evaluate function behavior equivalent to:

```python
calculate_revenue(10, 5.00)
```

or may provide a different valid sales collection to:

```python
calculate_total_units(...)
calculate_total_revenue(...)
find_top_product(...)
```

It may also test `classify_performance()` at important boundaries.

Therefore:

- use the exact required function names;
- use the exact required parameter lists;
- return the required values;
- do not hardcode results for the supplied data set;
- do not make computational functions depend on global data;
- do not print from functions that are required to return values;
- do not modify collections that are supplied as arguments; and
- review Classroom 50 feedback after each meaningful push.

The autograder is intended to support incremental development.

**Autograder points represent tests passed, not your assignment grade.**

Passing all automated tests does not demonstrate that your function design, documentation, Git history, README, ESSAY, or understanding meet all assignment requirements.

## Programming Constraints

Use programming concepts introduced in the course.

For this assignment, do **not** use:

- user input;
- global variables for program data;
- additional functions beyond those required by the assignment unless there is a clear and defensible design reason;
- NumPy;
- external libraries;
- file input/output;
- classes;
- recursion;
- lambda expressions;
- list comprehensions;
- generator expressions;
- `sum()`;
- `min()`;
- `max()`;
- purposeful infinite loops such as `while True`;
- `break`; or
- `continue`.

Do not use multiple `return` statements in one function.

Generative AI may suggest techniques that have not yet been introduced in the course. Do not use unfamiliar or prohibited techniques simply because AI generated them.

**You are responsible for understanding every line of submitted code and every function interface you implement.**

## Testing

Testing is required, but you are **not** required to create a formal automated test suite for this assignment.

Formal testing frameworks will be covered later.

For now, use functions to make your program easier to test in small pieces.

During development, test individual functions with values for which you can determine the expected result independently.

Examples of useful tests include:

### `calculate_revenue()`

Test:

- ordinary values;
- zero units.

For example:

```python
calculate_revenue(10, 5.00)
```

should return:

```text
50.0
```

### `classify_performance()`

Test important boundaries:

```text
just below 2000
exactly 2000
just below 3000
exactly 3000
```

### `find_top_product()`

Temporarily test alternate collections where:

- the highest-revenue product is first;
- the highest-revenue product is last; and
- only one product exists.

### Collection Calculations

Temporarily change quantities and prices and verify that:

- total units change correctly;
- total revenue changes correctly; and
- the correct top product is identified.

After testing, **restore the exact required** `sales` collection before submission.

**Temporary test code should not remain in the final submitted program** unless it is part of the required program behavior.

Think about what each test is intended to demonstrate before running it.

## Development Process

Develop the program incrementally.

**Do not write all required functions at once and then submit the finished program as one development commit.**

Your repository history must contain **at least eight meaningful student-created program-development commits** showing the program being built incrementally.

Eight is the minimum, not the target.

A meaningful commit represents a coherent improvement to the working program.

Examples might include:

- creating the driver structure;
- implementing and verifying one calculation function;
- adding another coherent analysis capability;
- integrating functions through the driver;
- completing report behavior;
- correcting a discovered design or logic problem.

You are responsible for:

- choosing appropriate development stages;
- testing before committing;
- writing clear descriptive commit messages;
- pushing regularly;
- reviewing Classroom 50 feedback after pushes; and
- correcting problems revealed by your own testing or the autograder.

Each meaningful commit must follow the course [commit guidelines](https://katrompas.accprofessors.com/committing).

Commits made only to:

```text
README.md
ESSAY.md
.gitignore
```

do not count toward the eight required program-development commits.

Commits containing arbitrary fragments solely to increase the commit count are not meaningful development commits.

## Generative AI

Use of generative AI is required as part of the development process.

You may use the generative AI system of your choice as a:

- tutor;
- programming partner;
- design critic;
- debugging assistant;
- testing assistant;
- source of explanations; or
- aid in reasoning about function decomposition and contracts.

You may show the AI the complete assignment.

However, you are responsible for making and defending the final design decisions.

You should be able to explain:

- why `main()` is the driver;
- what responsibility belongs to each function;
- what each parameter represents;
- what each function returns;
- why returning a value differs from printing it;
- why the `sales` collection is passed as an argument;
- whether a function could modify that collection;
- where one function calls another and why;
- how you tested individual functions; and
- how you used Classroom 50 feedback to verify or improve the program.

Your use and verification of AI will be documented in `ESSAY.md`.

## Code Documentation

Your program must follow the course [Commenting Guidelines](https://katrompas.accprofessors.com/commenting).

Because functions are now a major part of the course, **function headers are especially important**.

Each function must have documentation that clearly communicates its interface, including as appropriate:

- purpose;
- parameters;
- return value;
- relevant assumptions or preconditions; and
- meaningful side effects.

Do not write comments that merely translate obvious Python statements into English.

The documentation should explain the function's **contract**, not narrate its implementation line by line.

Before submission, remove:

- debugging statements;
- commented-out code;
- temporary test data;
- temporary test calls;
- temporary code; and
- unnecessary comments.

## `README.md`

Create and complete `README.md` according to the course [README Guidelines](https://katrompas.accprofessors.com/readme-guidelines).

The README must accurately document the final program.

You are responsible for creating the complete Markdown structure yourself.

All Markdown files must be properly formatted and professional. Spelling, grammar, and writing quality count.

## `.gitignore`

Create an appropriate `.gitignore` file for this Python project.

Follow the course [.gitignore guidelines](https://katrompas.accprofessors.com/gitignore-guidelines).

The file must be present in the repository root before submission.

## `ESSAY.md`

Complete the supplied `ESSAY.md`.

The five questions will focus on:

- your use of generative AI;
- your decomposition of the program into functions;
- the role of `main()` as the driver;
- parameters, return values, mutability, and function contracts; and
- testing and verification of individual functions.

Each question is worth **2 points**, for a total of **10 points**.

Your answers must demonstrate **depth of thought and actual engagement with your work**. Short, vague, or trivial answers will not receive full credit.

Do not give answers such as:

> AI helped me write the functions.

or:

> I used functions because the assignment required them.

Instead, explain **what you did, why you did it, and what you learned or verified**.

Whenever possible, include a specific example from your program, your testing, Classroom 50 feedback, or your interaction with AI.

## Final Review and Submission

Before submitting the assignment, verify the complete repository.

### 1. Complete the Required Functions

Confirm that `main.py` contains:

```text
calculate_revenue(units, unit_price)
calculate_total_units(sales)
calculate_total_revenue(sales)
find_top_product(sales)
classify_performance(total_revenue)
display_report(sales, total_units, total_revenue, top_product, performance)
main()
```

Verify the exact names and parameter lists.

### 2. Check the Single-Return Rule

Review every function.

No function may contain more than one `return` statement.

### 3. Run the Complete Program

Run:

```bash
python3 main.py
```

Depending on your system configuration, the command may instead be:

```bash
python main.py
```

Verify that the complete output exactly matches the required output.

### 4. Restore the Required Data

If you temporarily changed the sales collection during testing, restore the exact required collection before submission.

### 5. Review Function Behavior

Verify that computational functions:

- receive required data through parameters;
- return required values;
- do not print unnecessarily;
- do not depend on global program data; and
- do not modify the sales collection.

### 6. Review Classroom 50

Push your final work and review the Classroom 50 feedback.

Do not assume that matching the visible final report means the program satisfies all function tests.

Remember:

> **Autograder points represent tests passed, not the assignment grade.**

### 7. Check Repository Status

Run:

```bash
git status
```

Your working tree should be clean.

### 8. Review Development History

Run:

```bash
git log --oneline
```

Verify that your history contains at least eight meaningful program-development commits and reflects incremental development.

### 9. Review the Project Structure

Confirm that the repository contains at least:

```text
ASSIGNMENT.md
ESSAY.md
main.py
README.md
.gitignore
```

### 10. Review GitHub

Open the repository on GitHub and confirm that:

- the final `main.py` is present;
- the required functions are present;
- the final required sales collection is present;
- `README.md` is complete and properly rendered;
- `ESSAY.md` is complete and properly rendered;
- `.gitignore` is present;
- Classroom 50 feedback has been reviewed; and
- all final changes have been pushed.

### 11. Submit through Blackboard

Copy the normal HTTPS URL for your GitHub repository and submit that URL in the Blackboard assignment.
