# JavaScript

- JavaScript is a synchronous, single-threaded language.
- The whole JavaScript executes in the "Global Execution Context".

## Execution Context

### Memory Allocation (Environment Variable)
- Executes code line by line and allocates memory for variables and functions.
- Sets the default value as `undefined` for variables and for functions sets the whole function code.

### Code (Thread of Execution)
- Executes code line by line and sets values to variables.
- For functions, it creates a new "execution context" inside the global execution context.
- The new execution context creates 2 parts: memory and code. Once its execution is complete, it finds the return keyword, which means it returns the control of execution to the upper execution context where the function was invoked.

## Call Stack

- Maintains the order of execution of "Execution Context".
- The execution of JavaScript follows the call stack. Every global execution context is put at the bottom of the stack, and once a new execution starts, it is pushed onto the stack. Once execution is complete, it will pop from the stack.
- The call stack is also known as the "Execution Context Stack," "Program Stack," "Control Stack," "Machine Stack," or "Runtime Stack."

## Hoisting

- Hoisting allows access to variables and functions before they are initialized.
- It returns `undefined` for variables and returns the whole function for functions.
- For arrow functions, it works as a variable, so it returns `undefined`.

### Example of Hoisting

```javascript
console.log(myVar); // Output: undefined
console.log(myFunc); // Output: [Function: myFunc]
console.log(myArrowFunc); // Output: undefined

var myVar = 10;

function myFunc() {
    console.log('This is my function.');
}

var myArrowFunc = () => {
    console.log('This is my arrow function.');
};

console.log(myVar); // Output: 10
myFunc(); // Output: This is my function.
myArrowFunc(); // Output: This is my arrow function.
```

In the example above:
- `myVar` is accessed before it is initialized, so it returns `undefined`.
- `myFunc` is accessed before it is defined, so it returns the whole function.
- `myArrowFunc` is accessed before it is initialized, so it returns `undefined`.

## Lexical Environment, Scope, and Scope Chain

### Lexical Environment

- A lexical environment is the environment in which variables and functions are physically written in the source code.
- It consists of the local memory (variable environment) and a reference to the parent lexical environment.

### Scope

- Scope determines the accessibility of variables and functions at various parts of the code.
- There are three types of scope:
  1. **Global Scope**: Variables declared outside any function have a global scope and can be accessed anywhere in the code.
  2. **Function Scope**: Variables declared within a function are only accessible within that function.
  3. **Block Scope**: Variables declared within a block (e.g., inside a loop or conditional statement) are only accessible within that block (introduced with `let` and `const` in ES6).

### Scope Chain

- The scope chain is used to resolve variable access in nested functions.
- It consists of references to its own lexical environment and its parent lexical environments up to the global environment.

### Example of Lexical Environment, Scope, and Scope Chain

```javascript
const globalVar = 'Global';

function outerFunc() {
    const outerVar = 'Outer';

    function innerFunc() {
        const innerVar = 'Inner';
        console.log(globalVar); // Output: Global
        console.log(outerVar);  // Output: Outer
        console.log(innerVar);  // Output: Inner
    }

    innerFunc();
    console.log(globalVar); // Output: Global
    console.log(outerVar);  // Output: Outer
    // console.log(innerVar); // Error: innerVar is not defined
}

outerFunc();
// console.log(outerVar); // Error: outerVar is not defined
// console.log(innerVar); // Error: innerVar is not defined
```
---

# Block and Block Scope in JavaScript

## Block

In JavaScript, a block is a statement enclosed in curly braces `{}`. Blocks are used to group statements together. Common places where blocks are used include control structures like `if`, `for`, `while` loops, and functions.

### Example:
```javascript
{
  // This is a block
  let x = 10;
  console.log(x); // Output: 10
}
```

## Block Scope

Block scope refers to the scope of variables declared within a block. In JavaScript, variables declared with `let` and `const` are block-scoped, meaning they are only accessible within the block in which they are declared. Variables declared with `var` are not block-scoped; they are function-scoped or globally scoped if declared outside a function.

### Example with `let` and `const`:
```javascript
if (true) {
  let a = 10;
  const b = 20;
  console.log(a); // Output: 10
  console.log(b); // Output: 20
}

// console.log(a); // ReferenceError: a is not defined
// console.log(b); // ReferenceError: b is not defined
```

### Example with `var`:
```javascript
if (true) {
  var c = 30;
  console.log(c); // Output: 30
}
console.log(c); // Output: 30 (var is not block-scoped, it is function-scoped or globally scoped)
```

## `let` and `const` in Loops

Block scope is particularly useful in loops where the loop variable should be limited to the loop's block.

### Example:
```javascript
for (let i = 0; i < 3; i++) {
  console.log(i); // Output: 0, 1, 2
}
// console.log(i); // ReferenceError: i is not defined
```

### Example with `var` (not block-scoped):
```javascript
for (var j = 0; j < 3; j++) {
  console.log(j); // Output: 0, 1, 2
}
console.log(j); // Output: 3 (var is not block-scoped)
```

## Function Scope vs. Block Scope

Understanding the difference between function scope and block scope is crucial for writing effective JavaScript code.

### Function Scope:
```javascript
function testFunction() {
  var x = 1;
  if (true) {
    var x = 2; // Same variable as above, due to function scope
    console.log(x); // Output: 2
  }
  console.log(x); // Output: 2
}
testFunction();
```

### Block Scope:
```javascript
function testBlockScope() {
  let y = 1;
  if (true) {
    let y = 2; // Different variable, due to block scope
    console.log(y); // Output: 2
  }
  console.log(y); // Output: 1
}
testBlockScope();
```

## Temporal Dead Zone (TDZ)

- The Temporal Dead Zone is the period between the start of the execution of a block and the point where a variable is declared and initialized.
- During this time, any reference to the variable will result in a `ReferenceError`.
Note : var store in gloabl space where let and const not store in separate memory space(script) so it's not accessible and gives refrence error
### Example of Temporal Dead Zone

```javascript
console.log(myVar); // Output: undefined (due to hoisting)
console.log(myLet); // Error: Cannot access 'myLet' before initialization
console.log(myConst); // Error: Cannot access 'myConst' before initialization

var myVar = 10;
let myLet = 20;
const myConst = 30;
```

### JavaScript Variable Declaration: `var`, `let`, and `const`

## `var`

`var` is used to declare variables in JavaScript. It has function scope, meaning it's accessible within the function it is declared in. It can be redeclared and updated.

### Example:
```javascript
var x = 10;
console.log(x); // Output: 10

var x = 20; // Redeclaration is allowed
console.log(x); // Output: 20

x = 30; // Updating the value is allowed
console.log(x); // Output: 30
```

## `let`

`let` is used to declare variables that are block-scoped. Variables declared with `let` can be updated but not redeclared within the same scope.

### Key Points:
- We cannot redeclare a `let` variable in the same scope.
- It is block-scoped.

### Example:
```javascript
let y = 10;
console.log(y); // Output: 10

// let y = 20; // SyntaxError: Identifier 'y' has already been declared

y = 20; // Updating the value is allowed
console.log(y); // Output: 20
```

## `const`

`const` is used to declare variables that are block-scoped and whose values cannot be reassigned. The variable must be initialized at the time of declaration.

### Key Points:
- We cannot redeclare a `const` variable in the same scope.
- We must assign a value at the time of declaration.
- The value of a `const` variable cannot be changed through reassignment, but if it's an object or array, the properties or elements can be modified.

### Example:
```javascript
const z = 10;
console.log(z); // Output: 10

// const z = 20; // SyntaxError: Identifier 'z' has already been declared

// z = 20; // TypeError: Assignment to constant variable

const obj = { key: 'value' };
obj.key = 'newValue'; // Allowed: Object properties can be modified
console.log(obj.key); // Output: 'newValue'

const arr = [1, 2, 3];
arr.push(4); // Allowed: Array elements can be modified
console.log(arr); // Output: [1, 2, 3, 4]
```

## Memory Location

Variables declared with `let` and `const` are stored in separate memory locations compared to `var`. This helps avoid hoisting issues and ensures block scoping.

### Example:
```javascript
if (true) {
  var a = 1; // Function-scoped or globally scoped
  let b = 2; // Block-scoped
  const c = 3; // Block-scoped
}
console.log(a); // Output: 1
// console.log(b); // ReferenceError: b is not defined
// console.log(c); // ReferenceError: c is not defined
```
---

# Common JavaScript Errors

JavaScript errors are categorized into different types, each indicating a specific kind of issue in your code. Here are some of the most common JavaScript errors:

## `SyntaxError`

A `SyntaxError` occurs when the code syntax is incorrect and cannot be parsed by the JavaScript engine.

### Example:
```javascript
// Missing closing parenthesis
console.log("Hello, world!" // SyntaxError: Unexpected end of input

// Using a reserved keyword as a variable name
var let = 10; // SyntaxError: Unexpected token let
```

## `ReferenceError`

A `ReferenceError` occurs when a variable that has not been declared is referenced in the code.

### Example:
```javascript
console.log(x); // ReferenceError: x is not defined

function test() {
  console.log(y); // ReferenceError: y is not defined
  let y = 5;
}
test();
```

## `TypeError`

A `TypeError` occurs when a value is not of the expected type or when an operation is performed on a value of the wrong type.

### Example:
```javascript
// Trying to call a non-function as a function
var x = 10;
x(); // TypeError: x is not a function

// Accessing a property on `undefined` or `null`
var obj = null;
console.log(obj.property); // TypeError: Cannot read property 'property' of null
```
## Handling Errors with `try...catch`

JavaScript provides the `try...catch` block to handle runtime errors gracefully.

### Example:
```javascript
try {
  // Code that may throw an error
  let result = riskyOperation();
  console.log(result);
} catch (error) {
  // Handling the error
  console.error('An error occurred:', error.message);
} finally {
  // Code that will run regardless of an error occurring or not
  console.log('This will always run');
}

function riskyOperation() {
  // Example function that throws an error
  throw new Error('Something went wrong!');
}
```

# Shadowing and Deep Copy in JavaScript

## Shadowing

Shadowing occurs when a variable declared within a certain scope (e.g., a block or function) has the same name as a variable declared in an outer scope. The inner variable "shadows" the outer variable, making the outer variable inaccessible within the inner scope.

### Example of Shadowing:
```javascript
let x = 10;

function shadowExample() {
  let x = 20; // This x shadows the outer x
  console.log(x); // Output: 20
}

shadowExample();
console.log(x); // Output: 10 (outer x is unaffected)
```

### Example with `var`:
```javascript
var y = 30;

if (true) {
  var y = 40; // This y shadows the outer y within the function scope
  console.log(y); // Output: 40
}

console.log(y); // Output: 40 (outer y is affected due to function scope)
```

## Deep Copy

A deep copy is a process where all levels of an object or array are copied. This means that nested objects and arrays are also duplicated, creating a completely independent copy. In contrast, a shallow copy only duplicates the top-level properties. This means only the top-level properties are copied, and nested objects are still referenced.

### Example of Shallow Copy:
```javascript
let original = { a: 1, b: { c: 2 } };
let shallowCopy = Object.assign({}, original);

shallowCopy.b.c = 3;
console.log(original.b.c); // Output: 3 (original object is affected)
```

### Example of Deep Copy:
```javascript
let original = { a: 1, b: { c: 2 } };

// Using JSON methods (not recommended for all cases due to loss of functions and undefined values)
let deepCopy = JSON.parse(JSON.stringify(original));

deepCopy.b.c = 3;
console.log(original.b.c); // Output: 2 (original object is unaffected)
```

## Practical Usage of Deep Copy

Deep copies are essential when working with complex data structures where changes to a copied object should not affect the original object. This is particularly important in state management, functional programming, and scenarios involving immutability.

### Example in State Management:
```javascript
let state = {
  user: { name: 'Alice', age: 25 },
  settings: { theme: 'dark', notifications: true }
};

let newState = deepCopy(state);
newState.user.name = 'Bob';

console.log(state.user.name); // Output: Alice (original state is unaffected)
console.log(newState.user.name); // Output: Bob
```
Certainly! Let's delve into closures in JavaScript from the perspective of lexical environments. 

## Lexical Environment and Closures

A lexical environment is the environment in which a function was created. It consists of any local variables that were in-scope at the time the function was defined.

### What is a Closure?

A closure is formed when an inner function is defined within an outer function and the inner function retains access to the outer function's variables even after the outer function has returned. This ability of the inner function to access the outer function’s scope is what constitutes a closure.
Funaction along with it's lexical scope which bundle together forms a closure.
### Lexical Environment

The lexical environment includes:
- The local environment where the function is defined (variables, constants, parameters).
- The outer environment (parent scopes up to the global scope).

### Example of Closure with Lexical Environment

Here’s an example that illustrates closures with lexical environments:

```javascript
function outerFunction() {
  let outerVariable = 'I am outside!';
  
  function innerFunction() {
    console.log(outerVariable); // Inner function can access outer function's variable
  }

  return innerFunction;
}

const myClosure = outerFunction();
myClosure(); // Output: I am outside!
```

### Lexical Environment Example with State

Let’s see a more complex example where closures help maintain state across function calls:

```javascript
function createCounter() {
  let count = 0; // Private variable

  return {
    increment: function() {
      count++;
      console.log(count);
    },
    decrement: function() {
      count--;
      console.log(count);
    },
    getCount: function() {
      return count;
    }
  };
}

const counter = createCounter();
counter.increment(); // Output: 1
counter.increment(); // Output: 2
counter.decrement(); // Output: 1
console.log(counter.getCount()); // Output: 1
```

Using closures in loops can sometimes be tricky due to how lexical environments work. Here’s an example with closures inside a loop:

```javascript
function createArrayOfClosures() {
  let closures = [];
  
  for (let i = 0; i < 3; i++) {
    closures.push(function() {
      console.log(i); // Each closure captures the current value of `i`
    });
  }

  return closures;
}

let myClosures = createArrayOfClosures();
myClosures[0](); // Output: 0
myClosures[1](); // Output: 1
myClosures[2](); // Output: 2
```
### Summary

- **Closures** allow functions to retain access to their lexical environment.
- **Lexical environments** consist of local variables and their parent scopes.
- **Example** demonstrates closures maintaining state and working within loops.

### setTimeout with closures
Using `setTimeout` with closures inside a loop can be tricky due to the way JavaScript handles variable scoping, particularly with the `var` keyword. Here's a common issue and how to solve it using closures:

### Problem with `var`

When using `var` in a loop, all instances of `setTimeout` end up referencing the same variable, resulting in unexpected behavior. For example:

```javascript
for (var i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, i * 1000);
}

// Output after 5 seconds: 6 6 6 6 6
```

All `setTimeout` callbacks print `6` because they all share the same `i` variable, which ends up being `6` after the loop completes.

### Solution with Closures

To fix this, you can use an IIFE (Immediately Invoked Function Expression) to create a new scope for each iteration, capturing the current value of `i`.

```javascript
for (var i = 1; i <= 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}

// Output: 1 2 3 4 5 (each logged one second apart)
```
### Solution with another function calling with var

To fix this, you can use an IIFE (Immediately Invoked Function Expression) to create a new scope for each iteration, capturing the current value of `i`.

```javascript
for (var i = 1; i <= 5; i++) {
  function close(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  };
close(i); // it pass i to close function and this time it remember new copy of i
}

// Output: 1 2 3 4 5 (each logged one second apart)
### Explanation

1. **IIFE**:
    - `(function(i) { ... })(i)` is an IIFE that creates a new function and immediately invokes it with the current value of `i`.
    - This captures the current value of `i` in a new scope, ensuring each `setTimeout` callback has its own copy of `i`.

2. **setTimeout**:
    - Inside the IIFE, `setTimeout` schedules the logging of `i` after `i * 1000` milliseconds.
    - Because each IIFE invocation creates a new scope, each `setTimeout` callback references a different `i` value.

### Using `let` (ES6+)

In ES6, you can use the `let` keyword to achieve the same result more cleanly, as `let` creates a new block scope for each iteration.

```javascript
for (let i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, i * 1000);
}

// Output: 1 2 3 4 5 (each logged one second apart)
```

### Explanation

- When using `let`, each iteration of the loop has its own `i` variable.
- The `setTimeout` callbacks correctly reference the `i` value from their respective iterations.

### advantages of clouser
- Used in function curring
- Used in higher order function line memoize and once
- used in data hiding and encapsulation
- Here are some advantages of closures in JavaScript, with a brief explanation of each:

1. **Function Currying**:
   - **Definition**: Currying is the process of transforming a function with multiple arguments into a sequence of functions each taking a single argument.
   - **Advantage**: Closures enable partial application of functions, allowing you to create new functions with some pre-set arguments. This enhances code reusability and can lead to more concise and readable code.
   - **Example**:
     ```javascript
     function add(x) {
       return function(y) {
         return x + y;
       };
     }
     const addFive = add(5);
     console.log(addFive(3)); // Outputs: 8
     ```

2. **Higher Order Functions (e.g., memoize and once)**:
   - **Definition**: Higher-order functions are functions that take other functions as arguments or return them as output.
   - **Advantage**: Closures allow these functions to maintain state between calls, making patterns like memoization (caching results of expensive function calls) and ensuring a function is only executed once possible.
   - **Example** (Memoize):
     ```javascript
     function memoize(fn) {
       const cache = {};
       return function(...args) {
         const key = JSON.stringify(args);
         if (cache[key]) {
           return cache[key];
         }
         const result = fn(...args);
         cache[key] = result;
         return result;
       };
     }
     const factorial = memoize(function(n) {
       if (n === 0) return 1;
       return n * factorial(n - 1);
     });
     console.log(factorial(5)); // Outputs: 120
     ```

3. **Data Hiding and Encapsulation**:
   - **Definition**: Encapsulation is the bundling of data with methods that operate on that data, and data hiding restricts access to some of the object's components.
   - **Advantage**: Closures provide a way to create private variables and functions that cannot be accessed from outside the enclosing function, improving data integrity and reducing unintended interactions.
   - **Example**:
     ```javascript
     function createCounter() {
       let count = 0;
       return {
         increment: function() {
           count++;
           return count;
         },
         decrement: function() {
           count--;
           return count;
         },
         getCount: function() {
           return count;
         }
       };
     }
     const counter = createCounter();
     console.log(counter.increment()); // Outputs: 1
     console.log(counter.decrement()); // Outputs: 0
     console.log(counter.getCount());  // Outputs: 0
     ```
### disadvantages of clouser
- it consume over size because every time it form new clouser
- Variables Not Garbage Collected
  While closures offer numerous benefits, they also have some disadvantages:

1. **Memory Consumption**:
   - **Issue**: Closures can consume more memory because every time a closure is created, it carries along the variables from its lexical scope.
   - **Explanation**: Since each closure maintains references to its own set of variables, it can lead to higher memory usage, especially if many closures are created and kept in memory simultaneously.
   - **Example**:
     ```javascript
     function createClosure() {
       let largeData = new Array(1000).fill('data');
       return function() {
         console.log(largeData.length);
       };
     }
     const closure1 = createClosure();
     const closure2 = createClosure();
     // Each closure carries its own copy of largeData, increasing memory usage.
     ```

2. **Variables Not Garbage Collected**:
   - **Issue**: Variables captured by closures are not garbage collected as long as the closure exists, which can lead to memory leaks.
   - **Explanation**: If a closure is kept around (for example, by being assigned to a global variable or kept in an event listener), the variables it references cannot be garbage collected, potentially leading to increased memory usage over time.
   - **Example**:
     ```javascript
     function createClosure() {
       let count = 0;
       return function() {
         count++;
         console.log(count);
       };
     }
     const closure = createClosure();
     // The count variable is not garbage collected as long as the closure exists.
     ```

3. **Debugging Complexity**:
   - **Issue**: Closures can make debugging more challenging because it may be unclear which context a variable belongs to.
   - **Explanation**: When dealing with deeply nested or multiple closures, tracking down the source of a variable or understanding the scope in which it is defined can be complex.
   - **Example**:
     ```javascript
     function outerFunction() {
       let outerVar = 'outer';
       function innerFunction() {
         let innerVar = 'inner';
         function nestedFunction() {
           console.log(outerVar); // Tracing the source of outerVar can be complex in larger codebases.
         }
         nestedFunction();
       }
       innerFunction();
     }
     outerFunction();
     ```

4. **Performance Overhead**:
   - **Issue**: Excessive use of closures can lead to performance issues, especially in loops or frequently called functions.
   - **Explanation**: Since each closure can create its own context, it might result in slower execution compared to non-closure approaches in performance-critical applications.
   - **Example**:
     ```javascript
     function createClosuresInLoop() {
       let closures = [];
       for (let i = 0; i < 1000; i++) {
         closures.push(function() {
           console.log(i);
         });
       }
       return closures;
     }
     const closures = createClosuresInLoop();
     closures[0](); // Excessive closure creation inside a loop.
     ```

### Anonymous Function
  Anonymous functions in JavaScript are functions that are defined without a name. 
  They are often used as arguments to other functions or as immediate values that do not need to be referenced later in the code.

### Key Points

1. **No Name**: Anonymous functions do not have a name identifier. They are typically used in contexts where a function is needed as a one-off.
2. **Usage in Callbacks**: Frequently used as callbacks for array methods like `.map()`, `.filter()`, `.reduce()`, and event handlers.
3. **Immediate Invocation**: Often used in Immediately Invoked Function Expressions (IIFE) to create a new scope.
4. **Arrow Functions**: Arrow functions can be anonymous and are a more concise way to write function expressions.

### Examples

#### 1. Using Anonymous Functions with Array Methods

```javascript
const numbers = [1, 2, 3, 4, 5];

// Using an anonymous function with map
const squares = numbers.map(function(number) {
  return number * number;
});

console.log(squares); // Outputs: [1, 4, 9, 16, 25]
```

#### 2. Anonymous Functions as Event Handlers

```javascript
document.getElementById('myButton').addEventListener('click', function() {
  alert('Button was clicked!');
});
```

#### 3. Immediately Invoked Function Expression (IIFE)

```javascript
(function() {
  console.log('This function runs immediately!');
})();
```

#### 4. Arrow Functions

Arrow functions provide a concise syntax for writing anonymous functions:

```javascript
// Using arrow function with map
const squares = numbers.map(number => number * number);

console.log(squares); // Outputs: [1, 4, 9, 16, 25]

// Arrow function as an event handler
document.getElementById('myButton').addEventListener('click', () => {
  alert('Button was clicked!');
});
```

#### 5. Returning Functions from Functions

```javascript
function createMultiplier(multiplier) {
  return function(x) {
    return x * multiplier;
  };
}

const double = createMultiplier(2);
console.log(double(5)); // Outputs: 10
```

### Advantages of Using Anonymous Functions

1. **Conciseness**: They make code more concise and readable, especially for simple operations.
2. **Encapsulation**: Anonymous functions can encapsulate logic that doesn't need to be reused elsewhere.
3. **Functional Programming**: Widely used in functional programming paradigms for higher-order functions.

### Disadvantages of Using Anonymous Functions

1. **Debugging**: Without a name, stack traces can be less informative when debugging.
2. **Reusability**: Anonymous functions are not reusable. If you need to use the same logic in multiple places, named functions are more appropriate.

### Functions
### Function Statement (Function Declaration)

A function statement or function declaration defines a function with the specified parameters and a function body.
It is hoisted to the top of its scope, meaning it can be called before it is defined in the code.

#### Syntax

```javascript
function functionName(parameters) {
  // function body
}
```

#### Example

```javascript
// Function declaration
function greet(name) {
  return `Hello, ${name}!`;
}

// Function call before declaration
console.log(greet('Alice')); // Outputs: "Hello, Alice!"
```

### Function Expression
A function expression defines a function as part of an expression.
It can be named or anonymous and is not hoisted, meaning it cannot be called before it is defined.

#### Syntax

```javascript
const functionName = function(parameters) {
  // function body
};
```

#### Example

```javascript
// Function expression
const greet = function(name) {
  return `Hello, ${name}!`;
};

// Function call after definition
console.log(greet('Bob')); // Outputs: "Hello, Bob!"
```

### Differences between Function Statements and Function Expressions

| Feature                | Function Statement (Declaration)    | Function Expression                |
|------------------------|-------------------------------------|------------------------------------|
| **Hoisting**           | Yes, hoisted to the top of the scope| No, not hoisted                    |
| **Naming**             | Must have a name                    | Can be named or anonymous          |
| **Execution Context**  | Available throughout the scope      | Available only after the definition|
| **Syntax**             | `function functionName(parameters) { ... }` | `const functionName = function(parameters) { ... };` |

### Named function expression
It is a type of function expression where the function is given a name.
This name can be used within the function itself for recursive calls or for identification in debugging, but the function name is not accessible outside the function expression.

### Syntax

```javascript
const variableName = function abc(parameters) {
  // function body
};
```

### Example

```javascript
const factorial = function fact(n) {
  if (n <= 1) {
    return 1;
  } else {
    return n * fact(n - 1);
  }
};

console.log(factorial(5)); // Outputs: 120
```

### Differences between Named Function Expressions and Anonymous Function Expressions

| Feature                | Named Function Expression            | Anonymous Function Expression       |
|------------------------|--------------------------------------|-------------------------------------|
| **Naming**             | Has a local name for recursion and debugging | No name                             |
| **Scope**              | The name is only accessible inside the function | Not applicable                      |
| **Debugging**          | Easier to identify in stack traces   | Harder to identify in stack traces  |

### Example Illustrating Differences

#### Named Function Expression

```javascript
const namedFactorial = function fact(n) {
  if (n <= 1) {
    return 1;
  } else {
    return n * fact(n - 1);
  }
};

console.log(namedFactorial(5)); // Outputs: 120
// console.log(fact); // ReferenceError: fact is not defined
```

### Anonymous Function Expression

```javascript
const anonymousFactorial = function(n) {
  if (n <= 1) {
    return 1;
  } else {
    return n * anonymousFactorial(n - 1); // This will cause an error
  }
};

console.log(anonymousFactorial(5)); // Outputs: 120
```

In the case of the anonymous function expression, the function cannot refer to itself by name, making recursion impossible unless the variable it is assigned to (`anonymousFactorial`) is used.

### First-Class Functions

1. **Assigning Functions to Variables**

   Functions can be assigned to variables, allowing them to be passed around and manipulated like any other data type.

   ```javascript
   const greet = function(name) {
     return `Hello, ${name}!`;
   };

   console.log(greet('Alice')); // Outputs: "Hello, Alice!"
   ```

2. **Passing Functions as Arguments**

   Functions can be passed as arguments to other functions. This is commonly used in higher-order functions such as array methods like `.map()`, `.filter()`, and `.reduce()`.

   ```javascript
   function sayHello() {
     console.log('Hello!');
   }

   function executeFunction(func) {
     func();
   }

   executeFunction(sayHello); // Outputs: "Hello!"
   ```

3. **Returning Functions from Other Functions**

   Functions can be returned from other functions, enabling the creation of function factories and other higher-order patterns.

   ```javascript
   function createGreeting(greeting) {
     return function(name) {
       return `${greeting}, ${name}!`;
     };
   }

   const sayHi = createGreeting('Hi');
   console.log(sayHi('Bob')); // Outputs: "Hi, Bob!"
   ```

4. **Storing Functions in Data Structures**

   Functions can be stored in arrays, objects, and other data structures.

   ```javascript
   const operations = {
     add: function(a, b) {
       return a + b;
     },
     subtract: function(a, b) {
       return a - b;
     }
   };

   console.log(operations.add(5, 3)); // Outputs: 8
   console.log(operations.subtract(5, 3)); // Outputs: 2
   ```

### Examples

#### Higher-Order Functions

Higher-order functions are functions that take other functions as arguments or return functions as their results.

```javascript
// Function that takes another function as an argument
function repeat(operation, num) {
  for (let i = 0; i < num; i++) {
    operation();
  }
}

function sayHello() {
  console.log('Hello!');
}

repeat(sayHello, 3); // Outputs: "Hello!" three times
```

#### Callback Functions

A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of action.

```javascript
function fetchData(callback) {
  setTimeout(function() {
    const data = { name: 'John Doe', age: 30 };
    callback(data);
  }, 1000);
}

function processData(data) {
  console.log(`Name: ${data.name}, Age: ${data.age}`);
}

fetchData(processData); // Outputs: "Name: John Doe, Age: 30" after 1 second
```

### Benefits of First-Class Functions

1. **Modularity**: Code can be broken down into smaller, reusable functions.
2. **Flexibility**: Functions can be passed around and manipulated, enabling powerful patterns like callbacks, higher-order functions, and function composition.
3. **Abstraction**: Higher-order functions and callbacks allow for abstracting repetitive or boilerplate code.

### Callback Functions

1. **Definition**: A callback function is a function passed into another function as an argument and is executed after some kind of event or task.
2. **Usage**: Callbacks are often used for asynchronous operations like handling user inputs, network requests, and timers.
3. **Flexibility**: Callbacks allow functions to be more flexible and reusable.

### Examples

#### Basic Callback Example

Here's a simple example to demonstrate the concept of a callback function:

```javascript
function greeting(name) {
  console.log(`Hello, ${name}!`);
}

function processUserInput(callback) {
  const name = 'Alice';
  callback(name);
}

processUserInput(greeting); // Outputs: "Hello, Alice!"
```

In this example, `greeting` is the callback function passed to `processUserInput` and is executed with the argument `name`.

#### Asynchronous Callback Example

Callbacks are particularly useful in asynchronous programming, such as with `setTimeout`:

```javascript
function sayHello() {
  console.log('Hello after 2 seconds!');
}

setTimeout(sayHello, 2000); // Outputs: "Hello after 2 seconds!" after 2 seconds
```

Here, `sayHello` is the callback function that `setTimeout` executes after 2000 milliseconds.

#### Handling Asynchronous Data

Callbacks are often used to handle asynchronous data, such as with HTTP requests. Using the `fetch` API, you can pass a callback to process the response:

```javascript
function fetchData(url, callback) {
  fetch(url)
    .then(response => response.json())
    .then(data => callback(data))
    .catch(error => console.error('Error:', error));
}

function processData(data) {
  console.log('Received data:', data);
}

fetchData('https://api.example.com/data', processData);
```

In this example, `processData` is the callback function that processes the data received from the API.

### Nested Callbacks (Callback Hell)

When dealing with multiple asynchronous operations, you might encounter nested callbacks, often referred to as "callback hell." This can lead to code that is difficult to read and maintain.

```javascript
function firstTask(callback) {
  setTimeout(() => {
    console.log('First task completed');
    callback();
  }, 1000);
}

function secondTask(callback) {
  setTimeout(() => {
    console.log('Second task completed');
    callback();
  }, 1000);
}

function thirdTask(callback) {
  setTimeout(() => {
    console.log('Third task completed');
    callback();
  }, 1000);
}

firstTask(() => {
  secondTask(() => {
    thirdTask(() => {
      console.log('All tasks completed');
    });
  });
});
```

### Promises and Async/Await

To avoid callback hell and make asynchronous code more readable, JavaScript provides Promises and the `async`/`await` syntax:

#### Using Promises

```javascript
function firstTask() {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('First task completed');
      resolve();
    }, 1000);
  });
}

function secondTask() {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('Second task completed');
      resolve();
    }, 1000);
  });
}

function thirdTask() {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('Third task completed');
      resolve();
    }, 1000);
  });
}

firstTask()
  .then(secondTask)
  .then(thirdTask)
  .then(() => {
    console.log('All tasks completed');
  });
```

#### Using Async/Await

```javascript
async function runTasks() {
  await firstTask();
  await secondTask();
  await thirdTask();
  console.log('All tasks completed');
}

runTasks();
```

### Event Loop
The event loop is a fundamental concept in JavaScript, especially when dealing with asynchronous operations. Understanding the event loop is crucial for writing efficient and non-blocking code. Here’s an overview of how it works:

### Overview

JavaScript is single-threaded, meaning it executes code in a single sequence of instructions. However, it can handle asynchronous operations, such as I/O tasks, without blocking the main thread. This is achieved through the event loop.

### How It Works

1. **Call Stack**: This is where your function calls are added and executed. It operates in a LIFO (Last In, First Out) manner. When you call a function, it gets pushed onto the stack, and when the function returns, it gets popped off the stack.

2. **Web APIs**: These are provided by the browser (or Node.js in server environments) and include functionalities like `setTimeout`, `fetch`, DOM events, etc. When you call an asynchronous function, it is handed off to the Web APIs.

3. **Task Queue**: Also known as the callback queue, this is where callbacks of asynchronous operations are queued once the Web APIs have completed their tasks. Tasks from the task queue are added to the call stack when the call stack is empty.

4. **Event Loop**: This is the mechanism that checks the call stack and the task queue. If the call stack is empty, the event loop pushes the first task from the task queue onto the call stack.

### Steps in the Event Loop

1. **Execution Phase**: The JavaScript engine starts executing the code from the top of the script file.
2. **Web APIs Phase**: When it encounters an asynchronous operation (like `setTimeout` or `fetch`), it offloads it to the Web APIs.
3. **Task Completion**: Once the Web APIs complete the task, the associated callback is moved to the task queue.
4. **Event Loop Phase**: The event loop continually checks if the call stack is empty. If it is, it moves the first task from the task queue to the call stack.
5. **Repeat**: This process continues, allowing JavaScript to handle asynchronous operations efficiently.

### Example

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout callback');
}, 2000);

console.log('End');
```

- **Step 1**: `console.log('Start')` is pushed to the call stack and executed.
- **Step 2**: `setTimeout` is called, and its callback is handed off to the Web APIs.
- **Step 3**: `console.log('End')` is pushed to the call stack and executed.
- **Step 4**: After 2000ms, the callback of `setTimeout` is moved to the task queue.
- **Step 5**: The event loop moves the callback from the task queue to the call stack, where it gets executed.

**Output**:
```
Start
End
Timeout callback
```

### Microtasks and Macrotasks

In addition to the task queue, there's also a microtask queue, which has higher priority than the task queue. Promises and other microtasks are handled in this queue.

- **Microtasks**: These include promises, `MutationObserver`, and process.nextTick in Node.js. They are executed immediately after the currently executing script and before any other tasks from the task queue.
- **Macrotasks**: These include `setTimeout`, `setInterval`, and I/O callbacks.

### Example with Microtasks

```javascript
console.log('Start');

setTimeout(() => {
  console.log('setTimeout callback');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise callback');
});

console.log('End');
```

**Output**:
```
Start
End
Promise callback
setTimeout callback
```

In this example, the promise callback (a microtask) executes before the `setTimeout` callback (a macrotask), even though `setTimeout` was scheduled with a delay of 0ms.

### Higher-Order Functions
Higher-order functions are a fundamental concept in JavaScript (and many other programming languages). A higher-order function is a function that either takes one or more functions as arguments or returns a function as its result. Higher-order functions enable a more functional programming style, which can lead to cleaner and more expressive code.

### Characteristics of Higher-Order Functions

1. **Accepts Functions as Arguments**: A higher-order function can take other functions as parameters.
2. **Returns Functions**: A higher-order function can return a new function.

### Common Higher-Order Functions

Here are some common higher-order functions used in JavaScript:

#### 1. `map`
The `map` function takes a function and applies it to each element of an array, returning a new array with the results.

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

#### 2. `filter`
The `filter` function takes a function that returns a boolean and uses it to filter elements of an array, returning a new array with only the elements that satisfy the condition.

```javascript
const numbers = [1, 2, 3, 4];
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4]
```

#### 3. `reduce`
The `reduce` function takes a function and an initial value, and applies the function to each element of the array, accumulating the result into a single value.

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```

#### 4. `forEach`
The `forEach` function takes a function and applies it to each element of an array. It doesn't return a new array, but it can be used for side effects like logging or updating values.

```javascript
const numbers = [1, 2, 3, 4];
numbers.forEach(num => console.log(num));
// 1
// 2
// 3
// 4
```

### Custom Higher-Order Functions

You can create your own higher-order functions. Here are some examples:

#### Function Returning a Function

```javascript
function createMultiplier(multiplier) {
  return function (num) {
    return num * multiplier;
  };
}

const double = createMultiplier(2);
console.log(double(5)); // 10

const triple = createMultiplier(3);
console.log(triple(5)); // 15
```

#### Function Taking a Function as an Argument

```javascript
function applyOperation(arr, operation) {
  return arr.map(operation);
}

const numbers = [1, 2, 3, 4];
const squared = applyOperation(numbers, num => num * num);
console.log(squared); // [1, 4, 9, 16]
```

### Benefits of Higher-Order Functions

1. **Code Reusability**: Higher-order functions promote the reuse of functions by abstracting common patterns.
2. **Modularity**: They help in creating more modular code, making it easier to test and maintain.
3. **Expressiveness**: Code written with higher-order functions can be more expressive and easier to understand.

### Functional programming (FP)
Functional programming (FP) is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing state or mutable data. It is a declarative programming style, where the focus is on what to solve rather than how to solve it. Here are the core principles and concepts of functional programming:

### Core Principles of Functional programming

1. **First-Class and Higher-Order Functions**: Functions are treated as first-class citizens, meaning they can be assigned to variables, passed as arguments, and returned from other functions. Higher-order functions take other functions as arguments or return them.

2. **Pure Functions**: Pure functions have no side effects. They always produce the same output given the same input and do not alter any state outside their scope.

3. **Immutability**: Data is immutable, meaning it cannot be changed once created. Instead of modifying data, new data structures are created.

4. **Function Composition**: Functions are composed together to build more complex functions. This is similar to the mathematical concept of composing functions.

5. **Avoiding Side Effects**: FP aims to avoid side effects, which are changes in state that do not depend on the function's input parameters.

6. **Declarative Code**: Functional programming focuses on what needs to be done rather than how it should be done, leading to more readable and concise code.

### Key Concepts

#### Pure Functions

A pure function does not have side effects and returns the same output for the same input.

```javascript
// Pure function
const add = (a, b) => a + b;

console.log(add(2, 3)); // 5
console.log(add(2, 3)); // 5 (always the same result)
```

#### Immutability

Data is not changed but new data is created instead.

```javascript
const arr = [1, 2, 3];

// Immutable update
const newArr = [...arr, 4];

console.log(arr); // [1, 2, 3]
console.log(newArr); // [1, 2, 3, 4]
```

#### Higher-Order Functions

Functions that take other functions as arguments or return functions.

```javascript
const map = (arr, fn) => {
  const result = [];
  for (const value of arr) {
    result.push(fn(value));
  }
  return result;
};

const numbers = [1, 2, 3, 4];
const doubled = map(numbers, num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

#### Function Composition

Combining functions to create more complex operations.

```javascript
const compose = (f, g) => x => f(g(x));

const add1 = x => x + 1;
const multiply2 = x => x * 2;

const add1ThenMultiply2 = compose(multiply2, add1);

console.log(add1ThenMultiply2(5)); // (5 + 1) * 2 = 12
```

#### Currying

Transforming a function that takes multiple arguments into a series of functions that each take a single argument.

```javascript
const add = (a, b) => a + b;
const curriedAdd = a => b => a + b;

const add5 = curriedAdd(5);
console.log(add5(3)); // 8
```

#### Recursion

Using recursion instead of loops for iteration.

```javascript
const factorial = n => {
  if (n === 0) return 1;
  return n * factorial(n - 1);
};

console.log(factorial(5)); // 120
```

### Benefits of Functional Programming

1. **Predictability**: Pure functions are predictable and easier to test.
2. **Modularity**: FP encourages small, reusable functions.
3. **Concurrency**: Immutable data structures make concurrent programming easier and less error-prone.
4. **Readability**: Declarative code can be more concise and easier to understand.

### Functional Programming in JavaScript

JavaScript supports functional programming and provides many built-in higher-order functions like `map`, `filter`, and `reduce`.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(num => num * 2);
const evenNumbers = numbers.filter(num => num % 2 === 0);
const sum = numbers.reduce((acc, num) => acc + num, 0);

console.log(doubled); // [2, 4, 6, 8]
console.log(evenNumbers); // [2, 4]
console.log(sum); // 10
```