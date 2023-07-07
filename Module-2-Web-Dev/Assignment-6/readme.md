# Assignment-6 Questions & Solutions

💡 **Question-1:**  What’s Constructor And Its Purpose?

💬 **Solution-1:** 

In JavaScript, a constructor is a special method that is used for creating and initializing objects created from a class. Constructors are defined within class declarations or class expressions and are automatically called when a new instance of the class is created using the `new` keyword.

Here's an example of a constructor in JavaScript:

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const john = new Person("John", 30);
console.log(john.name);  // Output: John
console.log(john.age);   // Output: 30
```

In this example, the `Person` class has a constructor that takes two parameters (`name` and `age`). Inside the constructor, the properties `name` and `age` are assigned using the `this` keyword, which refers to the instance of the object being created. When a new instance of the `Person` class is created using the `new` keyword, the constructor is automatically invoked with the provided arguments, and the object is initialized with the specified values.

<hr/>

💡 **Question-2:** Explain This Keyword and Its Purpose?

💬 **Solution-2:** 

In JavaScript, the `this` keyword refers to the object that is currently being executed or the context in which a function is invoked. Its value is dynamically determined at runtime based on how a function is called or how an object method is accessed.

The purpose of the `this` keyword is to provide a convenient way to access and manipulate object properties within methods and to establish the context in which a function operates.

Here are some common use cases and behaviors of the `this` keyword:

1. **Method Invocation**:
When a function is called as a method of an object, the `this` keyword refers to the object itself. It allows methods to access and manipulate the object's properties and other methods.

```js
const person = {
  name: "John",
  greet: function() {
    console.log("Hello, my name is", this.name);
  }
};

person.greet(); // Output: Hello, my name is John
```

Here `greet` function is defined within the `person` object. When the `greet` method is invoked using `person.greet()`, `this` inside the method refers to the `person` object, allowing it to access and use the `name` property of the object.

2. **Function Invocation**:
When a standalone function is called without any explicit binding, `this` typically refers to the global object (`window` in browsers, `global` in Node.js) in non-strict mode. In strict mode, it is `undefined`.

```js
function displayMessage() {
  console.log("Message:", this.message);
}

const message = "Hello!";
displayMessage(); // Output: Message: Hello!
```

Here `displayMessage` function is called without any specific object context. As a result, `this` inside the function refers to the global object (`window` in a browser context) and can access the global `message` variable.

3. **Constructor Invocation**:
When a function is used as a constructor using the `new` keyword, a new instance of an object is created, and `this` refers to the newly created object. The constructor function sets up the object's initial state by assigning properties to `this`.

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const john = new Person("John", 30);
console.log(john.name); // Output: John
console.log(john.age);  // Output: 30
```

Here `Person` function is used as a constructor to create new instances of `Person` objects. Inside the constructor function, `this` refers to the newly created object, and the properties `name` and `age` are assigned to `this`, setting up the initial state of the object.

4. **Explicit Function Binding**:
We can explicitly bind the `this` value using methods such as `call()`, `apply()`, or `bind()`. These methods allows to specify the desired object as the context for a function.

```js
const person = {
  name: "John"
};

function greet() {
  console.log("Hello, my name is", this.name);
}

greet.call(person); // Output: Hello, my name is John
```

Here, the `call()` method is used to invoke the `greet` function and explicitly bind `this` to the `person` object. As a result, `this` inside the `greet` function refers to the `person` object, enabling access to the `name` property.

<hr/>

💡 **Question-3:** What’s Call Apply Bind Method & Difference Between them.

💬 **Solution-3:** 

In JavaScript, the `call()`, `apply()`, and `bind()` are methods available on function objects that allows to explicitly set the `this` value and optionally pass arguments to the function. They provide control over the execution context of a function and allows to borrow methods from other objects, set the `this` value for function invocation, and create new functions with a bound context.

Here's an explanation of each method and their differences:

1. **`call()`**:
The `call()` method is used to invoke a function with a specified `this` value and individual arguments passed directly as comma-separated values. It accepts an object as its first argument, which becomes the `this` value inside the function, followed by any additional arguments.

```js
function greet(message) {
  console.log(message + ", " + this.name);
}

const person = { name: "John" };

greet.call(person, "Hello"); // Output: Hello, John
```

Here, `call()` is used to invoke the `greet` function with the `person` object as the `this` value and the message "Hello" as an argument.

2. **`apply()`**:
The `apply()` method is similar to `call()`, but it accepts an array or an array-like object as its second argument to pass arguments to the function. The first argument is the `this` value.

```js
function greet(message) {
  console.log(message + ", " + this.name);
}

const person = { name: "John" };

greet.apply(person, ["Hello"]); // Output: Hello, John
```

Here, `apply()` is used to invoke the `greet` function with the `person` object as the `this` value and the message "Hello" passed as an array.

3. **`bind()`**:
The `bind()` method creates a new function with a specified `this` value and any provided arguments permanently bound to it. It returns a new function that can be invoked later. Unlike `call()` and `apply()`, `bind()` doesn't immediately invoke the function.

```js
function greet(message) {
  console.log(message + ", " + this.name);
}

const person = { name: "John" };

const greetPerson = greet.bind(person);
greetPerson("Hello"); // Output: Hello, John
```

Here, `bind()` is used to create a new function `greetPerson` with the `person` object as the `this` value permanently bound to it. When `greetPerson` is invoked, the `this` value is automatically set to `person`, and the message "Hello" is passed as an argument.

<hr/>

💡 **Question-4:** Explain OOPS ? 

💬 **Solution-4:** 

OOPS stands for Object-Oriented Programming Paradigm, which is a programming approach based on the concept of objects. It is a way to structure and design software applications by representing real-world entities as objects that have properties (attributes) and behaviors (methods). OOPS provides a set of principles and concepts that enable modular, scalable, and maintainable code.

Here are some key concepts of OOPS:

1. **Classes and Objects**:
A class is a blueprint or template that defines the structure and behavior of objects. It encapsulates data (attributes) and functionality (methods) related to a specific entity. Objects are instances of classes, representing individual entities that can interact with each other.

2. **Encapsulation**:
Encapsulation is the practice of bundling related data and methods together within a class, hiding the internal implementation details from external access. It allows for data abstraction and provides controlled access to object properties, ensuring data integrity and security.

3. **Inheritance**:
Inheritance is a mechanism that allows a class (child/subclass) to inherit properties and methods from another class (parent/superclass). It promotes code reuse and establishes a hierarchical relationship between classes, enabling the creation of specialized classes based on existing ones.

4. **Polymorphism**:
Polymorphism means the ability of objects to take on different forms or behaviors. It allows objects of different classes to be treated as instances of a common superclass. Polymorphism enables flexibility, extensibility, and the ability to write generic code that can work with objects of different types.

5. **Abstraction**:
Abstraction is the process of simplifying complex systems by identifying essential features and ignoring irrelevant details. It allows the creation of abstract classes and interfaces that define common behavior and provide a blueprint for concrete implementations.

6. **Association, Aggregation, and Composition**:
These are different types of relationships between objects. Association represents a loosely coupled relationship between objects, where one object can refer to another. Aggregation represents a "has-a" relationship, where an object contains other objects but can exist independently.

<hr/>

💡 **Question-5:**  Whats Abstraction and Its Purpose?

💬 **Solution-5:** 

Abstraction is a fundamental concept in object-oriented programming (OOP) that involves simplifying complex systems by identifying and focusing on essential features while ignoring unnecessary details. It provides a higher-level representation of objects and their behavior, allowing programmers to work with simplified models of complex entities.

Here are some key aspects and benefits of abstraction:

1. **Hiding Implementation Details**: Abstraction allows to hide internal implementation details of an object and expose only the relevant information and functionality to the outside world. By concealing complex internal mechanisms, we can create simpler and more intuitive interfaces for interacting with objects.

2. **Creating Abstract Classes and Interfaces**: Abstraction enables the creation of abstract classes and interfaces that define a common set of properties and methods for a group of related objects. These abstract entities serve as blueprints or contracts for concrete implementations, allowing us to define a common behavior and establish a level of consistency across different objects.

3. **Promoting Code Reusability**: Abstraction supports the reuse of code by defining abstract classes and interfaces that can be extended or implemented by multiple concrete classes. This allows to create generic code that operates on abstract entities, providing flexibility to handle different types of objects.

4. **Simplifying Complexity**: Abstraction allows to focus on the essential aspects of an object or system while hiding unnecessary details. By abstracting away low-level implementation complexities, we can work at a higher level of understanding and tackle larger-scale problems without getting bogged down in intricate implementation details.

5. **Enhancing Maintainability**: Abstraction improves code maintainability by providing a clear separation between the interface and the implementation. Changes made to the internal implementation details of an object or class do not affect the code that depends on its abstract interface.

<hr/>

💡 **Question-6:** Whats Polymorphism and Purpose of it?

💬 **Solution-6:** 

Polymorphism is a fundamental concept in object-oriented programming (OOP) that allows objects of different classes to be treated as instances of a common superclass. It enables a single interface to be used to represent multiple types of objects, providing flexibility, extensibility, and the ability to write generic code that can work with objects of different types.

Here are some key aspects and benefits of polymorphism:

1. **Code Reusability**: Polymorphism enables the reuse of code by defining common interfaces, abstract classes, or base classes that can be inherited or implemented by multiple derived classes. Code written to interact with the common interface can be used with any object that adheres to that interface.

2. **Flexibility and Extensibility**: Polymorphism allows for easy extensibility of code. New classes can be added to the system without modifying the existing code that relies on the common interface. This promotes the Open-Closed Principle, one of the SOLID principles, which states that software entities (classes, modules, functions) should be open for extension but closed for modification.

3. **Method Overriding**: Polymorphism enables method overriding, which allows a subclass to provide its own implementation of a method defined in its superclass. When a method is called on an object, the actual implementation is determined dynamically at runtime based on the object's type.

4. **Run-Time Polymorphism**: Polymorphism in OOP is typically achieved through dynamic or run-time polymorphism. This means that the specific method implementation to be executed is determined at runtime based on the actual type of the object.

5. **Simplifying Code and Improving Readability**: Polymorphism helps in simplifying code by operating at a higher level of abstraction. By working with common interfaces, the code becomes more generic and easier to read and understand.

<hr/>

💡 **Question-7:**  Whats Inheritance and Purpose of it?

💬 **Solution-7:** 

Inheritance is a fundamental concept in object-oriented programming (OOP) that allows a class (child/subclass) to inherit properties and methods from another class (parent/superclass). It establishes a hierarchical relationship between classes, enabling the creation of specialized classes based on existing ones.

Here are some key aspects and benefits of inheritance:

1. **Code Reusability**: Inheritance promotes code reuse by allowing classes to inherit properties and methods from a superclass. Instead of writing the same code in multiple classes, we can define common behaviors and attributes in a parent class and have the child classes inherit them.

2. **Code Organization**: Inheritance helps in organizing and structuring code by establishing a hierarchical relationship between classes. Related classes can be grouped together, making the codebase more modular and easier to navigate.

3. **Specialization and Extension**: Inheritance allows for specialization and extension of classes. Child classes can add new properties and methods or override existing ones inherited from the parent class to provide specialized behavior.

4. **Polymorphism**: Inheritance is closely related to polymorphism. Polymorphism allows objects of different classes to be treated as instances of a common superclass. By using inheritance, we can write code that works with a superclass or interface and can be used with any subclass that adheres to that interface.

5. **Inheritance Hierarchies**: Inheritance can be used to create hierarchical structures or inheritance hierarchies. Classes can have multiple levels of inheritance, where a child class can become a parent class for other derived classes.

<hr/>

💡 **Question-8:** Whats Encapsulation and Purpose of it ?

💬 **Solution-8:** 

Encapsulation is a fundamental concept in object-oriented programming (OOP) that involves bundling related data (attributes) and methods (functions) together within a class, and controlling access to them from outside the class. It provides a way to hide the internal implementation details of an object and expose only necessary information and functionality through well-defined interfaces.

Here are some key aspects and benefits of encapsulation:

1. **Data Protection and Access Control**: Encapsulation allows to protect the internal state (data) of an object by making it private or hidden from the outside world. Access to the data is provided through public methods (getters and setters) that encapsulate the logic for accessing or modifying the data. This ensures that the object's state remains consistent and controlled.

2. **Information Hiding and Abstraction**: Encapsulation hides the internal implementation details of an object, exposing only essential information and functionality through well-defined interfaces. By encapsulating data and methods, we can abstract away the complexity and provide a simpler and more intuitive way to interact with objects.

3. **Modularity and Code Organization**: Encapsulation promotes modularity and code organization by grouping related data and methods within a class. By encapsulating related functionality, we can create self-contained and reusable components that are easier to understand, maintain, and extend. Encapsulation helps in achieving the Single Responsibility Principle, one of the SOLID principles, which states that a class should have only one reason to change.

4. **Code Maintenance and Versioning**: Encapsulation improves code maintenance and versioning by providing a clear separation between the internal implementation and the external interface. Changes made to the internal implementation of a class do not affect the code that depends on its public interface. This allows for easier updates, bug fixes, and enhancements, as long as the public interface remains unchanged.

5. **Information Security**: Encapsulation contributes to information security by restricting direct access to sensitive data within an object. By encapsulating data and providing controlled access through methods, we can enforce validation, access restrictions, and ensure the integrity and security of the data.

<hr/>

💡 **Question-9:** Explain Class in JavaScript?

💬 **Solution-9:** 

In JavaScript, a class is a blueprint or template for creating objects. It is a syntactical construct introduced in ECMAScript 2015 (ES6) that provides a more structured and convenient way to define objects and their behaviors. JavaScript classes are built on top of JavaScript's existing prototype-based inheritance model.

Here's an example of defining a class in JavaScript:

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

In this example, the `Person` class is defined using the `class` keyword. It has a `constructor` method that is automatically called when creating a new instance of the class. The `constructor` method is used to initialize the object's properties (`name` and `age`) based on the provided arguments.

The class also has a `greet` method, which can be called on instances of the class to display a greeting message. Note that methods defined inside the class do not need the `function` keyword and can directly use `this` to refer to the instance of the class.

To create objects from the class, we use the `new` keyword:

```js
const john = new Person("John", 30);
john.greet(); // Output: Hello, my name is John
```

In this example, `john` is an instance of the `Person` class created using the `new` keyword. The `name` and `age` properties are set based on the arguments passed to the `Person` constructor. The `greet` method is then called on the `john` object, invoking the behavior defined in the class.

JavaScript classes support inheritance, allowing us to create subclasses that inherit properties and methods from a parent class. The `extends` keyword is used to define a subclass:

```js
class Employee extends Person {
  constructor(name, age, employeeId) {
    super(name, age); // Call the constructor of the parent class
    this.employeeId = employeeId;
  }

  getInfo() {
    console.log(`Employee ID: ${this.employeeId}`);
  }
}
```

In this example, the `Employee` class is a subclass of `Person`, as indicated by `extends Person`. The `super()` function is used in the constructor to call the constructor of the parent class and initialize the inherited properties. The `getInfo` method is specific to the `Employee` class and can be called on `Employee` instances.

<hr/>

💡 **Question-10:**  What’s Super Keyword & What it does?

💬 **Solution-10:** 

In JavaScript, the `super` keyword is used to call functions on an object's parent or superclass. It is typically used within subclasses to access and invoke methods or constructors defined in the parent class.

Here are two common uses of the `super` keyword:

1. **Accessing Parent Class Methods**: In a subclass, the `super` keyword can be used to call a method defined in the parent class with the same name. This allows the subclass to extend or override the behavior of the parent class while still accessing and invoking the parent class's implementation of the method.

```js
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Cat extends Animal {
  speak() {
    super.speak(); // Call the speak() method of the parent class
    console.log("Cat meows");
  }
}

const cat = new Cat();
cat.speak();
// Output:
// Animal speaks
// Cat meows
```

In this example, the `Cat` class extends the `Animal` class and overrides its `speak()` method. The `super.speak()` call inside the `speak()` method of `Cat` invokes the `speak()` method of the parent class (`Animal`), allowing both the parent and child behaviors to be executed.

2. **Calling Parent Class Constructor**: In a subclass, the `super` keyword can also be used to call the constructor of the parent class. This is done using `super()` as the first statement inside the constructor of the subclass. It allows the subclass to inherit and initialize properties from the parent class.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Cat extends Animal {
  constructor(name, color) {
    super(name); // Call the constructor of the parent class
    this.color = color;
  }
}

const cat = new Cat("Fluffy", "gray");
console.log(cat.name);  // Output: Fluffy
console.log(cat.color); // Output: gray
```

In this example, the `Cat` class extends the `Animal` class and has its own constructor. The `super(name)` call inside the `Cat` constructor invokes the `Animal` constructor, allowing the `name` property to be initialized in the parent class. The `color` property is specific to the `Cat` class and is assigned within the subclass constructor.

<hr/>