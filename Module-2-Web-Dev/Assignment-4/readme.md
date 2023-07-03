# Assignment-4 Questions & Solutions

💡 **Question-1:** Explain Hoisting in JavaScript.

💬 **Solution-1:** 

Hoisting in JavaScript is a behavior that allows variables and function declarations to be moved to the top of their respective scopes during the compilation phase, before the code is executed. This means that regardless of where declarations appear in the code, they are effectively "hoisted" to the top of their scope.

Hoisting applies to both variable declarations and function declarations, but it works slightly differently for each.

1. **Variable Hoisting**:
When variables are declared using the `var` keyword, they are hoisted to the top of their scope, but their assignments are not hoisted. This means that the variable names are moved to the top, but their values remain undefined until the actual assignment statement is encountered during runtime.

   ```js
   console.log(x); // undefined
   var x = 10;
   ```

   In the above example, even though the `console.log` statement appears before the variable declaration and assignment, it doesn't throw an error. This is because the variable declaration is hoisted to the top, and `x` is initialized with the value `undefined` by default. Therefore, the output will be `undefined`.

2. **Function Hoisting**:
   Function declarations are also hoisted to the top of their scope, and they can be called before they appear in the code. This allows you to define functions after they are used in the code. For example:

   ```js
   foo(); // "Hello, world!"

   function foo() {
     console.log("Hello, world!");
   }
   ```

   In above example, the function `foo` is called before its declaration, but it still works without any errors. This is because the function declaration is hoisted to the top of its scope.

<hr/>

💡 **Question-2:** Explain Temporal Dead Zone?

💬 **Solution-2:** 

The Temporal Dead Zone (TDZ) is a behavior in JavaScript that occurs when variables declared with `let` and `const` are accessed before they are initialized within their respective scopes. During the TDZ, if you try to access such variables, a `ReferenceError` is thrown.

The TDZ is a concept introduced with the introduction of `let` and `const` in ECMAScript 2015 (ES6).

Example:

```js
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 10;
```

When we try to access the variable `x` before its initialization, a `ReferenceError` is thrown. This happens because the variable `x` is in the TDZ until the point of initialization, which is after the `let` statement.

The TDZ starts at the beginning of the scope and continues until the variable is declared and assigned a value.

<hr/>

💡 **Question-3:** Difference between var & let?

💬 **Solution-3:** 

The main difference between `var` and `let` in JavaScript is the scope and hoisting behavior.

1. Scope:
   - `var`: Variables declared with `var` have function scope or global scope, meaning they are accessible throughout the entire function or global context.
   - `let`: Variables declared with `let` have block scope, meaning they are limited to the nearest enclosing block, which could be a statement, loop, or a block defined by curly braces `{}`.

   Example:

   ```js
   function example() {
     var x = 10;
     let y = 20;

     if (true) {
       var x = 30; // Same variable as outer "x"
       let y = 40; // New variable, different from outer "y"

       console.log(x); // 30
       console.log(y); // 40
     }

     console.log(x); // 30
     console.log(y); // 20
   }

   example();
   ```

   In this example, the `var` declaration of `x` is function-scoped, so modifying it inside the `if` block affects its value outside as well. On the other hand, the `let` declaration of `y` is block-scoped, so the inner `y` is a separate variable from the outer `y`.

2. Hoisting:
   - `var`: Variable declarations using `var` are hoisted to the top of their scope during the compilation phase. However, only the declarations are hoisted, not the assignments. This means you can access the variable before its declaration, and it will have the value `undefined`.
   - `let`: Variable declarations using `let` are also hoisted to the top of their scope, but unlike `var`, they are not initialized. Accessing a variable declared with `let` before its declaration results in a `ReferenceError` within the Temporal Dead Zone (TDZ).

   Example:

   ```js
   console.log(x); // undefined
   var x = 10;

   console.log(y); // ReferenceError: Cannot access 'y' before initialization
   let y = 20;
   ```

   In this example, the `var` declaration of `x` is hoisted, so accessing it before the declaration is valid but returns `undefined`. However, the `let` declaration of `y` is also hoisted but cannot be accessed until it is initialized, resulting in a `ReferenceError`.

<hr/>

💡 **Question-4:** What are the major features introduced in ECMAScript 6?

💬 **Solution-4:**

Here are some of the major features introduced in ECMAScript 6:

1. **Arrow Functions**: A concise syntax for defining anonymous functions, using the `=>` arrow notation. Arrow functions provide lexical scoping of `this` and have implicit returns for one-line expressions.

2. **Block-Scoped Variables**: The `let` and `const` keywords were introduced to declare block-scoped variables, replacing the function-scoped variables of `var`. Block-scoped variables are more predictable and less prone to bugs.

3. **Classes**: The `class` syntax provides a more traditional object-oriented programming (OOP) approach to creating objects and defining classes in JavaScript, simplifying the process of creating constructor functions and prototypes.

4. **Modules**: ES6 introduced a standardized module system using the `import` and `export` keywords. This allows JavaScript code to be split into separate modules, each with its own scope and dependencies, promoting modularity and reusability.

5. **Template Literals**: Template literals are an enhanced string syntax that allows for multiline strings, string interpolation, and expressions inside strings using the `${}` syntax.

6. **Destructuring Assignment**: Destructuring assignment enables extracting values from arrays or objects and assigning them to variables in a more concise and readable way. It simplifies variable assignment and parameter handling.

7. **Enhanced Object Literals**: Object literals gained new syntax and capabilities, such as shorthand property and method definitions, computed property names, and the ability to define setters and getters.

8. **Default Parameters**: Function parameters can now have default values assigned, allowing for more flexibility and eliminating the need for manual checks and fallbacks.

9. **Spread and Rest Operators**: The spread operator (`...`) allows the expansion of an array or an object into individual elements, while the rest parameter syntax allows the gathering of multiple function arguments into an array.

10. **Promises**: Promises were introduced as a native way to handle asynchronous operations, providing better control flow and error handling compared to traditional callback-based approaches.

<hr/>

💡 **Question-5:**  What is the difference between let and const in ES6?

💬 **Solution-5:** 

1. `let`: Variables declared with `let` allow for block scoping, which means they are limited to the block in which they are defined (a block can be a statement, loop, or a block defined by curly braces `{}`). `let` variables can be reassigned with a new value, allowing them to change over time.

   ```js
   let x = 10;
   x = 20; // Valid, x can be reassigned
   ```

   With `let`, you can redeclare a variable within different blocks:

   ```js
   let x = 10;
   if (true) {
     let x = 20; // Different variable, separate scope
     console.log(x); // Output: 20
   }
   console.log(x); // Output: 10
   ```

   The block scope of `let` variables provides better predictability and avoids common issues associated with function-scoped variables declared with `var`.

2. `const`: Variables declared with `const` also have block scoping, just like `let`, but they have an additional feature: they are constants and cannot be reassigned once they are initialized. The value of a `const` variable remains constant throughout its lifetime.

   ```js
   const x = 10;
   x = 20; // Invalid, cannot reassign a const variable
   ```

   When using `const`, you must initialize the variable with a value at the time of declaration. Once assigned, the value cannot be changed.

   ```js
   const x = 10;
   const y; // Invalid, const variables must be initialized

   if (true) {
     const z = 20;
     console.log(z); // Output: 20
   }
   console.log(z); // ReferenceError: z is not defined
   ```

   `const` is useful when you want to declare variables that should not be reassigned and maintain their value throughout the program execution. It also helps in preventing accidental changes to important values.

<hr/>

💡 **Question-6:**  What is template literals in ES6 and how do you use them?

💬 **Solution-6:** 

Template literals allows for multiline strings, string interpolation, and expression embedding, providing a more expressive and flexible syntax compared to traditional string concatenation.

To define a template literal, enclose the string within backticks (` `) instead of single quotes or double quotes.

Example:

```js
const name = 'Alice';
const age = 25;

const message = `Hello, my name is ${name} and I am ${age} years old.`;
console.log(message);
```

*Output*:

```
Hello, my name is Alice and I am 25 years old.
```

Features:

1. String Interpolation: Variables and expressions can be embedded within the string using `${}` notation. This allows you to directly include variables, function calls, or expressions inside the template literal, without the need for explicit concatenation or string manipulation.

2. Multiline Strings: Template literals can span multiple lines without requiring explicit line breaks or escape characters. This makes it easier to work with multiline strings and improves code readability.

3. Expression Embedding: Besides variables, you can embed any JavaScript expression within `${}` notation. This allows for complex expressions, function calls, or even inline conditional statements within the template literal.

<hr/>

💡 **Question-7:** What’s difference between map & forEach?

💬 **Solution-7:** 

1. `forEach()`:
   - `forEach()` is a method that iterates over each element of an array and executes a provided callback function for each element.
   - It does not return a new array.
   - The primary purpose of `forEach()` is to perform an action or operation on each element of the array.
   - It is useful when you want to iterate over an array without the need to create a new array or modify the existing one.

   Example:

   ```js
   const numbers = [1, 2, 3, 4, 5];

   numbers.forEach((number) => {
     console.log(number);
   });
   ```


2. `map()`:
   - `map()` is a method that iterates over each element of an array and applies a provided callback function to each element, creating a new array with the results.
   - It returns a new array with the same length as the original array, where each element is the result of the callback function applied to the corresponding element in the original array.
   - The primary purpose of `map()` is to transform or modify the array elements and create a new array based on the transformations.
   - It is useful when you want to create a new array with modified elements, without modifying the original array.

   Example:

   ```js
   const numbers = [1, 2, 3, 4, 5];

   const doubledNumbers = numbers.map((number) => {
     return number * 2;
   });

   console.log(doubledNumbers);
   ```


<hr/>

💡 **Question-8:**  How can you destructure objects and arrays in ES6?

💬 **Solution-8:** 

1. Object Destructuring:
   Object destructuring allows to extract values from an object and assign them to variables with matching property names. The syntax involves enclosing the desired variable names in curly braces `{}` and providing the object from which the values should be extracted.

   Example:

   ```js
   const person = { name: 'Alice', age: 25, city: 'New York' };

   const { name, age, city } = person;

   console.log(name); // Output: Alice
   console.log(age); // Output: 25
   console.log(city); // Output: New York
   ```

   In the example, the values of the `name`, `age`, and `city` properties from the `person` object are extracted and assigned to corresponding variables with the same names.

2. Array Destructuring:
   Array destructuring allows to extract values from an array and assign them to variables based on their positions. The syntax involves enclosing the desired variable names in square brackets `[]` and providing the array from which the values should be extracted.

   Example:

   ```js
   const numbers = [1, 2, 3, 4, 5];

   const [first, second, ...rest] = numbers;

   console.log(first); // Output: 1
   console.log(second); // Output: 2
   console.log(rest); // Output: [3, 4, 5]
   ```

   In the example, the values at the corresponding positions in the `numbers` array are assigned to the `first` and `second` variables. The rest of the values are gathered into the `rest` variable using the rest syntax (`...`).
 

<hr/>

💡 **Question-9:** How can you define default parameter values in ES6 functions?

💬 **Solution-9:** 

In ECMAScript 6 (ES6), we can define default parameter values for function parameters, which allows to specify a default value that will be used if no argument is provided or if the argument is `undefined`. Here's how to define default parameter values in ES6 functions:

```js
function greet(name = 'Anonymous') {
  console.log(`Hello, ${name}!`);
}

greet(); // Output: Hello, Anonymous!
greet('Alice'); // Output: Hello, Alice!
```

In the example, the `greet` function has a single parameter `name` with a default value of `'Anonymous'`. If no argument is passed when calling `greet()`, or if `undefined` is passed, the default value `'Anonymous'` will be used. If an argument is provided, such as `'Alice'`, the provided value will override the default value.

Can be defined default values for multiple parameters:

```js
function addNumbers(a, b = 0, c = 0) {
  return a + b + c;
}

console.log(addNumbers(1, 2, 3)); // Output: 6
console.log(addNumbers(1, 2)); // Output: 3
console.log(addNumbers(1)); // Output: 1
```

In this example, the `addNumbers` function has three parameters (`a`, `b`, and `c`). The parameters `b` and `c` have default values of `0`. If no argument is provided for `b` or `c`, the default value of `0` will be used.

<hr/>
 
💡 **Question-10:**  What is the purpose of the spread operator (...) in ES6?

💬 **Solution-10:** 

In ECMAScript 6 (ES6), the spread operator (`...`) serves multiple purposes and provides a convenient syntax for working with arrays, objects, and function arguments. The spread operator allows to expand or spread the elements of an iterable (like an array or an object) into various contexts. Here are some common use cases for the spread operator:

1. Array Spread:
   - When used with an array, the spread operator allows you to create a new array by expanding the elements of an existing array.
   - It is useful for creating copies of arrays, merging arrays, or extracting specific elements from an array.
   - Example:

     ```js
     const numbers = [1, 2, 3];
     const newArray = [...numbers, 4, 5]; // Spread the elements of 'numbers' and add additional elements

     console.log(newArray); // Output: [1, 2, 3, 4, 5]
     ```

2. Object Spread:
   - The spread operator can also be used with objects to create a new object by expanding the properties of an existing object.
   - It is useful for creating copies of objects, merging objects, or adding new properties to an object.
   - Example:

     ```js
     const person = { name: 'Alice', age: 25 };
     const newPerson = { ...person, city: 'New York' }; // Spread the properties of 'person' and add a new property

     console.log(newPerson); // Output: { name: 'Alice', age: 25, city: 'New York' }
     ```

3. Function Arguments:
   - The spread operator can be used to pass an array of values as individual arguments to a function.
   - It is useful when you have an array and want to call a function that expects individual arguments.
   - Example:

     ```js
     function addNumbers(a, b, c) {
       return a + b + c;
     }

     const numbers = [1, 2, 3];
     const sum = addNumbers(...numbers); // Spread 'numbers' as individual arguments

     console.log(sum); // Output: 6
     ```

4. Rest Parameters:
   - The spread operator can be used as part of function parameter syntax to capture multiple arguments as an array.
   - It is useful when you want to define a function that can accept a variable number of arguments.
   - Example:

     ```js
     function concatenateStrings(...strings) {
       return strings.join(' ');
     }

     const result = concatenateStrings('Hello', 'world', '!', 'Welcome');

     console.log(result); // Output: 'Hello world ! Welcome'
     ```

<hr/>