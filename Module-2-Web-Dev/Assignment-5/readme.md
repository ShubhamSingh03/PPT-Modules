# Assignment-5 Questions & Solutions

💡 **Question-1:** What’s difference between Synchronous and Asynchronous?

💬 **Solution-1:** 

In JavaScript, synchronous and asynchronous are two different ways of executing code and handling operations.

1. Synchronous:
Synchronous execution means that each operation is performed one after the other in a sequential manner. When a synchronous operation is initiated, the program waits for it to complete before moving on to the next operation. This means that the execution of code blocks in JavaScript is blocking, and the program cannot continue until the current operation is finished.

Here's an example of synchronous code execution:

```js
console.log("Start");

function wait(ms) {
  const start = Date.now();
  while (Date.now() - start < ms) {}
}

wait(2000); // Pause execution for 2 seconds
console.log("End");
```

This program logs "Start," then pauses execution for 2 seconds using the `wait` function, and finally logs "End." During the 2-second pause, the program is blocked, and nothing else can happen.

2. Asynchronous:
Asynchronous execution, on the other hand, allows multiple operations to be initiated without waiting for each operation to complete before moving on to the next one. Asynchronous operations are non-blocking, meaning that the program can continue its execution while waiting for a certain operation to finish.

Here's an example of asynchronous code execution using callbacks:

```js
console.log("Start");

setTimeout(function() {
  console.log("Timeout completed");
}, 2000); // Asynchronous pause for 2 seconds

console.log("End");
```

This program logs "Start," initiates a 2-second asynchronous pause using the `setTimeout` function, and then logs "End" immediately. After the 2-second delay, the callback function is executed, and "Timeout completed" is logged.

JavaScript also introduced Promises and async/await syntax to handle asynchronous operations. Promises allows to write asynchronous code that looks more like synchronous code, and async/await provides a syntactic sugar on top of promises to make asynchronous code appear more linear and easier to follow.

<hr/>

💡 **Question-2:**  What are Web Apis ?

💬 **Solution-2:** 

Web APIs, also known as Application Programming Interfaces, are sets of rules and protocols that allow different software applications to communicate and interact with each other over the web. Web APIs enable developers to access and utilize the functionality of other software systems, libraries, or services to enhance their own applications.

Web APIs are widely used in web development to perform various tasks and access resources from external sources. Web APIs are typically based on the HTTP protocol and use a combination of endpoints, request methods, and data formats (such as JSON or XML) to enable communication.

There are different types of Web APIs, including:

1. **HTTP APIs**: These are APIs that expose a set of endpoints that can be accessed using HTTP methods (GET, POST, PUT, DELETE, etc.). They are often used to retrieve, create, update, or delete data on a server. Common examples include RESTful APIs and SOAP APIs.

2. **JavaScript APIs**: These are APIs built into web browsers that provide additional functionality to web applications. They allow developers to interact with various aspects of the web browser and its environment, such as manipulating the DOM, making AJAX requests, accessing geolocation information, working with local storage, and more. Examples include the Document Object Model (DOM) API, Fetch API, and Geolocation API.

3. **Third-party APIs**: These are APIs provided by external services or platforms that developers can integrate into their applications. They offer access to specific features or data from the service provider. Examples include social media APIs (e.g., Twitter API, Facebook Graph API), payment gateways (e.g., PayPal API), mapping services (e.g., Google Maps API), and many others.

<hr/>

💡 **Question-3:** Explain SetTimeOut and setInterval ?

💬 **Solution-3:** 

1. `setTimeout`:
The `setTimeout` function is used to execute a specified piece of code (callback function) after a designated delay. It takes two arguments: the callback function to be executed and the delay time in milliseconds.

Here's an example usage of `setTimeout`:

```js
console.log("Before setTimeout");

setTimeout(function() {
  console.log("Inside setTimeout");
}, 2000); // Executes the callback function after a 2-second delay

console.log("After setTimeout");
```

The program logs "Before setTimeout," then schedules the callback function to be executed after a 2-second delay using `setTimeout`, and finally logs "After setTimeout." After the 2-second delay, the callback function is executed, and "Inside setTimeout" is logged.

2. `setInterval`:
The `setInterval` function is used to repeatedly execute a specified piece of code (callback function) at a defined interval. It also takes two arguments: the callback function and the interval time in milliseconds.

Here's an example usage of `setInterval`:

```js
var counter = 0;

var intervalId = setInterval(function() {
  console.log("Counter:", counter);
  counter++;

  if (counter === 5) {
    clearInterval(intervalId); // Stops the interval after the counter reaches 5
  }
}, 1000); // Executes the callback function every 1 second

```

The program initializes a `counter` variable and sets up an interval using `setInterval`. The callback function logs the current value of the counter and increments it. If the counter reaches 5, the interval is stopped using `clearInterval`. The callback function is executed every 1 second, logging the counter value until it reaches 5.

<hr/>

💡 **Question-4:**  How can you handle Async code in JavaScript ?

💬 **Solution-4:** 

In JavaScript, there are several approaches to handle asynchronous code and ensure proper execution and coordination of operations. Here are some commonly used techniques:

1. Callbacks:
Callbacks are a traditional way of handling asynchronous code in JavaScript. With callbacks, we pass a function as an argument to an asynchronous operation, and that function is executed once the operation completes.

```js
function fetchData(callback) {
  // Simulating an asynchronous operation
  setTimeout(function() {
    const data = "Some data";
    callback(data); // Call the callback function with the result
  }, 2000);
}

function handleData(data) {
  console.log("Received data:", data);
}

fetchData(handleData);
```

In this example, the `fetchData` function simulates an asynchronous operation using `setTimeout`. It takes a callback function as an argument and invokes it with the result (`data`) once the operation completes. The `handleData` function is defined separately and passed as the callback function to `fetchData`. When the data is received, the `handleData` function is executed, logging the received data.

2. Promises:
Promises provide a more structured and readable way to handle asynchronous operations and their results. Promises represent the eventual completion (or failure) of an asynchronous operation and allows to chain actions using `.then()` and handle errors with `.catch()`.

```js
function fetchData() {
  return new Promise(function(resolve, reject) {
    // Simulating an asynchronous operation
    setTimeout(function() {
      const data = "Some data";
      resolve(data); // Resolve the promise with the result
    }, 2000);
  });
}

fetchData()
  .then(function(data) {
    console.log("Received data:", data);
  })
  .catch(function(error) {
    console.error("Error:", error);
  });
```

In this example, the `fetchData` function returns a new Promise object. Inside the Promise, the asynchronous operation is simulated with `setTimeout`, and when the operation completes successfully, the promise is resolved with the result (`data`). The resolved value can then be accessed using `.then()` and handled in the corresponding callback function. Errors can be caught using `.catch()`.

3. Async/await:
Async/await is a modern syntax introduced in ECMAScript 2017 (ES8) that provides a more concise and synchronous-like way to handle asynchronous code. It is built on top of promises and allows us to write asynchronous code that looks and behaves more like synchronous code.

```js
function fetchData() {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      const data = "Some data";
      resolve(data);
    }, 2000);
  });
}

async function getData() {
  try {
    const data = await fetchData(); // Await the promise to resolve
    console.log("Received data:", data);
  } catch (error) {
    console.error("Error:", error);
  }
}

getData();
```

In this example, the `fetchData` function returns a promise as before. The `getData` function is declared as `async` to enable the usage of `await` inside it. With `await`, the promise returned by `fetchData` is awaited, and the resolved value (`data`) is assigned to the `data` variable. Errors can be caught using a `try-catch` block.

Async/await offers a more straightforward and synchronous-looking code structure while still preserving the benefits of asynchronous execution and error handling.

<hr/>

💡 **Question-5:** What are Callbacks &  Callback Hell ?

💬 **Solution-5:** 

Callbacks in JavaScript are functions that are passed as arguments to other functions. They are commonly used to handle asynchronous operations and execute code after a certain task or event completes.

Here's an example of a callback function:

```js
function greeting(name, callback) {
  console.log("Hello, " + name);
  callback();
}

function sayGoodbye() {
  console.log("Goodbye!");
}

greeting("Alice", sayGoodbye);
```

Here `greeting` function takes two arguments: `name` and `callback`. It logs a greeting message followed by calling the callback function. The `sayGoodbye` function is defined separately and passed as the callback function to `greeting`. When `greeting` is called, it logs "Hello, Alice" and then executes the callback function, which logs "Goodbye!".

**Callback Hell**, also known as the Pyramid of Doom, is a situation that arises when we have multiple nested callbacks, resulting in code that becomes difficult to read and maintain. It often occurs when dealing with complex asynchronous operations or when handling multiple asynchronous tasks sequentially.

Here's an example of callback hell:

```js
asyncOperation1(function(result1) {
  asyncOperation2(result1, function(result2) {
    asyncOperation3(result2, function(result3) {
      // More nested callbacks...
    });
  });
});
```

In this example, each asynchronous operation depends on the result of the previous operation, so they are nested inside each other. As the number of operations grows, the nesting becomes deeper, making the code harder to understand and prone to errors.

To mitigate callback hell, there are a few techniques available:

1. Modularization: Break down the code into smaller, reusable functions to improve readability and separate concerns. This can reduce the depth of nesting.

2. Promises: Use Promises to handle asynchronous operations in a more structured and readable way. Promises allows to chain operations using `.then()` and handle errors with `.catch()`, reducing the need for deeply nested callbacks.

3. Async/await: Utilize the async/await syntax, which provides a more synchronous-like coding style for handling asynchronous code.

Here's an example of using Promises to handle the same asynchronous operations:

```js
asyncOperation1()
  .then(function(result1) {
    return asyncOperation2(result1);
  })
  .then(function(result2) {
    return asyncOperation3(result2);
  })
  .then(function(result3) {
    // ...
  })
  .catch(function(error) {
    // Handle errors
  });
```

<hr/>

💡 **Question-6:**  What are Promises & Explain Some Three Methods of Promise

💬 **Solution-6:** 

Promises are objects in JavaScript that represent the eventual completion or failure of an asynchronous operation and allows to handle the result or error in a more structured and readable manner. Promises provide a way to write asynchronous code that is easier to reason about and avoids the pitfalls of callback hell.

A Promise can be in one of three states:

1. **Pending**: The initial state when the Promise is still undergoing the asynchronous operation and has not yet been fulfilled or rejected.
2. **Fulfilled**: The state when the Promise successfully completes the operation, resulting in a resolved value.
3. **Rejected**: The state when the Promise encounters an error or fails to complete the operation, resulting in a rejection reason.

Promises have three main methods that allows to interact with and handle the asynchronous operation:

1. **`then()`**: The `then()` method is used to handle the fulfillment of a Promise. It takes two optional arguments: a success callback function that handles the resolved value, and a failure callback function that handles any potential rejection. The `then()` method returns a new Promise, allowing for chaining.

```js
asyncOperation()
  .then(function(result) {
    console.log("Operation succeeded:", result);
  })
  .catch(function(error) {
    console.log("Operation failed:", error);
  });
```

Here `then()` method is used to handle the successful completion of the `asyncOperation()`. The success callback function receives the resolved value as an argument and logs a success message. If an error occurs during the operation and the Promise is rejected, the `catch()` method is used to handle the error.

2. **`catch()`**: The `catch()` method is used to handle the rejection of a Promise. It takes a callback function that handles the rejection reason. It is typically used at the end of a Promise chain to catch any errors that occur during the asynchronous operation.

```js
asyncOperation()
  .then(function(result) {
    console.log("Operation succeeded:", result);
  })
  .catch(function(error) {
    console.log("Operation failed:", error);
  });
```

Here `catch()` method is used to handle any rejections that occur during the `asyncOperation()`. If an error occurs, the rejection callback function logs an error message.

3. **`finally()`**: The `finally()` method is used to specify a callback function that is always executed, regardless of whether the Promise is fulfilled or rejected. It is commonly used to perform cleanup operations or final actions.

```js
asyncOperation()
  .then(function(result) {
    console.log("Operation succeeded:", result);
  })
  .catch(function(error) {
    console.log("Operation failed:", error);
  })
  .finally(function() {
    console.log("Cleanup or final action");
  });
```

Here `finally()` method is used to define a callback function that will be executed no matter the outcome of the Promise. It can be used to perform cleanup tasks, release resources, or execute final actions.

<hr/>

💡 **Question-7:** What’s async & await Keyword in JavaScript

💬 **Solution-7:** 

1. `async`:
The `async` keyword is used to declare an asynchronous function. When a function is marked as `async`, it automatically returns a Promise, allowing to use `await` inside the function to pause its execution and wait for a Promise to resolve before continuing.

Here's an example of an asynchronous function using the `async` keyword:

```js
async function fetchData() {
  // Asynchronous operation
  return await someAsyncOperation();
}
```

Here `fetchData` function is marked as `async`. It performs an asynchronous operation using `someAsyncOperation()`, and the `await` keyword is used to pause the execution of the function until the Promise returned by `someAsyncOperation()` is resolved.

2. `await`:
The `await` keyword is used inside an asynchronous function to pause the execution until a Promise is resolved. It can only be used within an `async` function. When encountering an `await` expression, the function will pause, and control will be returned to the calling context until the Promise resolves.

Here's an example of using `await` inside an `async` function:

```js
async function fetchData() {
  const result = await someAsyncOperation();
  // Further code execution after the Promise is resolved
  return result;
}
```

Here `await` keyword is used to wait for the resolution of the Promise returned by `someAsyncOperation()`. The function will be paused until the Promise is resolved, and the resolved value will be assigned to the `result` variable. After that, the function continues its execution.

Here's an example showcasing the usage of `async` and `await` with error handling:

```js
async function fetchData() {
  try {
    const result = await someAsyncOperation();
    console.log("Operation succeeded:", result);
    return result;
  } catch (error) {
    console.log("Operation failed:", error);
    throw error;
  }
}
```

Here `try-catch` block is used to handle errors that may occur during the asynchronous operation. If an error is thrown or a rejected Promise is encountered within the `try` block, control is transferred to the `catch` block, where the error is logged and potentially rethrown.

<hr/>

💡 **Question-8:** Explain Purpose of Try and Catch Block & Why do we need it?

💬 **Solution-8:** 

The `try` and `catch` blocks are used in JavaScript for error handling and exception handling. They allows us to write code that gracefully handles potential errors and provides a way to recover from them or perform alternative actions when exceptions occur.

The purpose of the `catch` block is to handle the caught exception. It contains the code that executes when an exception occurs within the corresponding `try` block. The `catch` block takes an error object as a parameter, which can be used to access information about the error, such as its type or message.

Here's an example that demonstrates the usage of `try` and `catch` blocks:

```js
function divide(a, b) {
  try {
    if (b === 0) {
      throw new Error("Division by zero is not allowed");
    }

    const result = a / b;
    console.log("Result:", result);
  } catch (error) {
    console.log("Error:", error.message);
  }
}

divide(10, 2);    // Result: 5
divide(10, 0);    // Error: Division by zero is not allowed
divide("10", 2);  // Error: Invalid operands to divide
```

Here `divide` function attempts to perform division by dividing `a` by `b`. The `try` block is used to enclose the division operation, and if an exception is thrown (e.g., division by zero or invalid operands), the control is transferred to the `catch` block. In the `catch` block, the error object is accessed, and an appropriate action is taken (in this case, logging the error message).

The `try-catch` mechanism provides several benefits:

1. **Error Handling**: The primary purpose is to catch and handle exceptions that may occur during the execution of a block of code.

2. **Robustness**: By using `try-catch`, we can safeguard critical sections of code and handle exceptional situations, ensuring the program can continue running even in the face of errors.

3. **Debugging**: `try-catch` blocks provide a way to capture and log errors, making it easier to identify and debug issues during development.

4. **Fallback or Alternative Actions**: The `catch` block can be used to execute alternative code or fallback actions when an error occurs.

<hr/>

💡 **Question-9:**  Explain fetch in Js.

💬 **Solution-9:** 

In JavaScript, the `fetch` function is used to make network requests and retrieve resources from a specified URL. It provides a modern and flexible way to perform asynchronous HTTP requests, typically for fetching data from an API or making AJAX calls.

Here's a basic example of using the `fetch` function:

```js
fetch('https://api.example.com/data')
  .then(function(response) {
    // Process the response
    return response.json(); // Parse the response body as JSON
  })
  .then(function(data) {
    // Work with the parsed data
    console.log(data);
  })
  .catch(function(error) {
    // Handle errors
    console.error(error);
  });
```

In this example, the `fetch` function is used to make a GET request to the specified URL (`https://api.example.com/data`). The response is obtained in the first `then` block, where the `response.json()` method is used to parse the response body as JSON. The parsed data is then processed in the second `then` block. Any errors that occur during the request or parsing are caught in the `catch` block.

The `fetch` function can accept additional parameters to customize the request, such as setting headers, specifying the request method, including request data, etc. Here's an example:

```js
fetch('https://api.example.com/data', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token123'
  },
  body: JSON.stringify({ name: 'John', age: 30 })
})
  .then(function(response) {
    // Process the response
  })
  .catch(function(error) {
    // Handle errors
  });
```

In this example, a POST request is made to the specified URL with additional parameters specified in the options object. The request includes headers for content type and authorization, and the body is sent as JSON-encoded data.

<hr/>

💡 **Question-10:**  How do you define an asynchronous function in JavaScript using async/await?

💬 **Solution-10:** 

To define an asynchronous function using `async/await` in JavaScript, we simply need to prefix the function declaration with the `async` keyword. This marks the function as asynchronous and allows to use the `await` keyword inside the function to pause its execution until a Promise is resolved.

Here's an example of defining an asynchronous function using `async/await`:

```js
async function fetchData() {
  // Asynchronous operations using await
  const result1 = await someAsyncOperation1();
  const result2 = await someAsyncOperation2();
  // ...
  return result2;
}
```

Here `fetchData` function is declared as `async`, indicating that it is an asynchronous function. Inside the function body, we can use the `await` keyword to pause the execution of the function until a Promise is resolved. The result of each awaited operation is assigned to a variable (`result1`, `result2`, etc.), and the function can perform further operations or computations with those values.

The `await` keyword is used before the Promise-based asynchronous operation that want to wait for. It ensures that the function does not proceed until the Promise resolves and returns the resolved value. Note that the `await` keyword can only be used within an `async` function.

An important thing to keep in mind is that using `await` with an asynchronous operation effectively pauses the execution of the function until that operation is complete. This means that subsequent lines of code will not be executed until the awaited operation has finished and its result is available.

<hr/>