---
title: "Chapter_2:_JavaScript_Basics"
date: 2023-08-30T13:43:57-04:00
draft: false
---

III. Chapter 2: JavaScript Basics
# III. Chapter 2: JavaScript Basics

## A. Syntax and structure

### 1. Variables and data types
   a. Primitive data types (e.g., number, string, boolean)
   
   ```javascript
   let age = 25;
   let name = "John";
   let isStudent = true;
   ```

   b. Complex data types (e.g., object, array)
   
   ```javascript
   let person = {
      name: "John",
      age: 25,
      isStudent: true
   };

   let numbers = [1, 2, 3, 4, 5];
   ```

   c. Declaring and initializing variables
   
   ```javascript
   let x; // Declaring a variable without initializing it

   let y = 10; // Declaring and initializing a variable
   ```

### 2. Operators
   a. Arithmetic operators (e.g., +, -, *, /)
   
   ```javascript
   let result = 10 + 5; // Addition
   let result2 = 10 - 5; // Subtraction
   let result3 = 10 * 5; // Multiplication
   let result4 = 10 / 5; // Division
   ```

   b. Comparison operators (e.g., ==, ===, !=, !==)
   
   ```javascript
   let a = 5;
   let b = 10;

   let isEqual = a == b; // Equality check
   let isStrictEqual = a === b; // Strict equality check
   let isNotEqual = a != b; // Inequality check
   let isNotStrictEqual = a !== b; // Strict inequality check
   ```

   c. Logical operators (e.g., &&, ||, !)
   
   ```javascript
   let x = 5;
   let y = 10;
   let z = 15;

   let isTrue = x < y && y < z; // Logical AND
   let isFalse = x > y || y > z; // Logical OR
   let isNotTrue = !isTrue; // Logical NOT
   ```

   d. Assignment operators (e.g., =, +=, -=, *=, /=)
   
   ```javascript
   let x = 10;
   x += 5; // Equivalent to x = x + 5

   let y = 20;
   y -= 5; // Equivalent to y = y - 5

   let z = 30;
   z *= 2; // Equivalent to z = z * 2

   let w = 40;
   w /= 2; // Equivalent to w = w / 2
   ```

### 3. Comments
   a. Single-line comments
   
   ```javascript
   // This is a single-line comment
   ```

   b. Multi-line comments
   
   ```javascript
   /*
   This is a
   multi-line comment
   */
   ```
# B. Control Flow

Control flow refers to the order in which the statements in a program are executed. In JavaScript, control flow can be managed using conditional statements and looping constructs.

## 1. Conditional statements

Conditional statements allow us to make decisions in our code based on certain conditions. JavaScript provides several types of conditional statements.

### a. If statement

The `if` statement is the simplest conditional statement in JavaScript. It allows us to execute a block of code only if a specified condition is true.

Example:

```markdown
```javascript
let num = 10;

if (num > 0) {
  console.log("The number is positive.");
}
```
```
Output:
```
The number is positive.
```

### b. If-else statement

The `if-else` statement extends the functionality of the `if` statement by allowing us to execute a different block of code if the condition is false.

Example:

```markdown
```javascript
let num = -5;

if (num > 0) {
  console.log("The number is positive.");
} else {
  console.log("The number is non-positive.");
}
```
```
Output:
```
The number is non-positive.
```

### c. If-else if-else statement

The `if-else if-else` statement allows us to check multiple conditions and execute different blocks of code based on the conditions.

Example:

```markdown
```javascript
let num = 0;

if (num > 0) {
  console.log("The number is positive.");
} else if (num < 0) {
  console.log("The number is negative.");
} else {
  console.log("The number is zero.");
}
```
```
Output:
```
The number is zero.
```

### d. Switch statement

The `switch` statement provides an alternative way to handle multiple conditions. It allows us to evaluate an expression and execute different code blocks based on the value of the expression.

Example:

```markdown
```javascript
let day = "Monday";

switch (day) {
  case "Monday":
    console.log("Today is Monday.");
    break;
  case "Tuesday":
    console.log("Today is Tuesday.");
    break;
  default:
    console.log("Today is neither Monday nor Tuesday.");
}
```
```
Output:
```
Today is Monday.
```

## 2. Looping constructs

Looping constructs allow us to repeat a block of code multiple times. JavaScript provides several types of looping constructs.

### a. For loop

The `for` loop is commonly used when we know the number of iterations in advance. It allows us to repeat a block of code for a specified number of times.

Example:

```markdown
```javascript
for (let i = 0; i < 5; i++) {
  console.log("Iteration: " + i);
}
```
```
Output:
```
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
```

### b. While loop

The `while` loop is useful when we don't know the number of iterations in advance. It repeats a block of code as long as a specified condition is true.

Example:

```markdown
```javascript
let i = 0;

while (i < 5) {
  console.log("Iteration: " + i);
  i++;
}
```
```
Output:
```
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
```

### c. Do-while loop

The `do-while` loop is similar to the `while` loop, but it executes the block of code at least once before checking the condition.

Example:

```markdown
```javascript
let i = 0;

do {
  console.log("Iteration: " + i);
  i++;
} while (i < 5);
```
```
Output:
```
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
```

In this section, we have explored the control flow in JavaScript through conditional statements and looping constructs. Understanding control flow is essential for writing efficient and logical JavaScript code.
## C. Functions and Scope

### 1. Defining and Calling Functions

a. Function Declaration

A function declaration is a way to define a function in JavaScript. It starts with the keyword "function" followed by the function name and a pair of parentheses. The function body is enclosed in curly braces.

Here is an example of a function declaration:

```javascript
function greet() {
    console.log("Hello, world!");
}

greet(); // Output: Hello, world!
```

b. Function Expression

A function expression is another way to define a function in JavaScript. Instead of using the function declaration syntax, we assign the function to a variable.

Here is an example of a function expression:

```javascript
var greet = function() {
    console.log("Hello, world!");
};

greet(); // Output: Hello, world!
```

c. Anonymous Functions

Anonymous functions are functions without a name. They can be defined using either the function declaration syntax or the function expression syntax.

Here is an example of an anonymous function using the function expression syntax:

```javascript
var greet = function() {
    console.log("Hello, world!");
};

greet(); // Output: Hello, world!
```

d. Arrow Functions

Arrow functions are a shorthand syntax for writing functions in JavaScript. They provide a more concise way to define functions, especially when dealing with simple one-liners.

Here is an example of an arrow function:

```javascript
var greet = () => {
    console.log("Hello, world!");
};

greet(); // Output: Hello, world!
```

e. Function Parameters and Arguments

Functions can have parameters, which act as placeholders for values that are passed to the function when it is called. These values are called arguments.

Here is an example of a function with parameters and arguments:

```javascript
function greet(name) {
    console.log("Hello, " + name + "!");
}

greet("John"); // Output: Hello, John!
```

f. Returning Values from Functions

Functions can also return values using the "return" keyword. The returned value can be stored in a variable or used directly.

Here is an example of a function that returns a value:

```javascript
function multiply(a, b) {
    return a * b;
}

var result = multiply(2, 3);
console.log(result); // Output: 6
```

### 2. Scope and Variable Visibility

a. Global Scope

Variables declared outside of any function have global scope. They can be accessed from anywhere in the code, including inside functions.

Here is an example of a variable with global scope:

```javascript
var message = "Hello, world!";

function greet() {
    console.log(message);
}

greet(); // Output: Hello, world!
```

b. Local Scope

Variables declared inside a function have local scope. They can only be accessed within the function.

Here is an example of a variable with local scope:

```javascript
function greet() {
    var message = "Hello, world!";
    console.log(message);
}

greet(); // Output: Hello, world!
console.log(message); // Throws an error: message is not defined
```

c. Block Scope

Starting from ES6, variables declared with the "let" and "const" keywords have block scope. Block scope means that the variable is only accessible within the nearest pair of curly braces.

Here is an example of a variable with block scope:

```javascript
function greet() {
    if (true) {
        let message = "Hello, world!";
        console.log(message);
    }
    console.log(message); // Throws an error: message is not defined
}

greet(); // Output: Hello, world!
```

d. Hoisting

JavaScript has a concept called hoisting, which means that variable and function declarations are moved to the top of their containing scope during the compilation phase.

Here is an example of hoisting:

```javascript
console.log(message); // Output: undefined
var message = "Hello, world!";
```

In the above example, the variable declaration of "message" is hoisted to the top, but the value is not assigned yet.

This concludes the section on functions and scope in JavaScript. Understanding functions and scope is crucial for writing efficient and maintainable JavaScript code.
