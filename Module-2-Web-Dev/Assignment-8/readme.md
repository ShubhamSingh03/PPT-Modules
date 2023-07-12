# Assignment-8 Questions & Solutions

💡 **Question-1:** Whats React and its pros and cons?

💬 **Solution-1:** 

React is an open-source JavaScript library that is widely used for building user interfaces (UIs) for web applications. It was developed by Facebook and provides developers with a declarative and efficient way to build interactive UI components.

**Pros of React**:

1. Virtual DOM: React utilizes a virtual DOM, which is an abstract representation of the actual DOM (Document Object Model) in memory. This allows React to efficiently update and render only the necessary components when there are changes, resulting in improved performance.

2. Component-based architecture: React promotes a modular approach to building UIs through its component-based architecture.

3. Declarative syntax: React uses a declarative syntax, where developers describe how the UI should look based on the current application state.

4. Rich ecosystem and community support: React has a large and active community, which means there is extensive documentation, tutorials, and libraries available.

**Cons of React**:

1. Tooling complexity: React itself is a library, not a full-fledged framework, so developers need to choose additional tools and libraries (e.g., bundlers, build tools, routers) to build a complete application. The complexity of configuring and managing these tools can be overwhelming, especially for beginners.

2. Abundance of options: The React ecosystem has numerous options for state management, routing, and other functionalities. While having choices is generally a good thing, it can also lead to decision paralysis or difficulty in determining the best approach for a particular project.

3. Performance considerations: Although React's virtual DOM improves performance in many cases, improper usage or inefficient component design can lead to performance issues. Care must be taken to optimize rendering and avoid unnecessary re-renders.

<hr/>

💡 **Question-2:** What do you understand by Virtual Dom?

💬 **Solution-2:** 

The Virtual DOM (Document Object Model) is a concept used in frameworks like React to optimize the updating and rendering of UI components. It is an abstraction or a representation of the actual DOM tree, which is the browser's internal representation of the HTML structure of a web page.

Here's how the Virtual DOM works:

1. When a React component's state or props change, it triggers a re-rendering of that component and its child components.

2. Instead of directly updating the actual DOM, React creates a new virtual representation of the UI components and compares it with the previous virtual DOM representation.

3. React then identifies the differences (known as "diffing" or "reconciliation") between the new virtual DOM and the previous one.

4. After determining the minimal set of changes required, React updates only those specific parts of the actual DOM that need to be changed. This process is known as "reconciliation" or "diffing."

By using the Virtual DOM, React can optimize the rendering process in several ways:

1. Performance optimization: React can batch multiple changes together and update the actual DOM in a single operation.

2. Efficient updates: React determines the minimal set of changes required by comparing the new virtual DOM with the previous one. This ensures that only the necessary parts of the UI are updated, improving performance.

3. Developer-friendly: Instead of manually manipulating the actual DOM, developers can work with the virtual representation of the UI components, which is easier to reason about and understand.

<hr/>

💡 **Question-3:** Difference between Virtual Dom vs Real Dom

💬 **Solution-3:** 

**Virtual DOM**:

1. Representation: The Virtual DOM is an abstraction or a virtual representation of the actual DOM structure. It is a lightweight copy of the real DOM tree.

2. Manipulation: When changes occur in a UI component, React updates the virtual DOM by creating a new virtual representation. The entire virtual DOM is then compared with the previous version to identify the minimal set of changes required.

3. Efficiency: By performing the diffing process on the virtual DOM, React optimizes the updates. It determines the specific parts of the virtual DOM that have changed and only applies those changes to the real DOM.

4. Updates: React updates the actual DOM based on the identified changes in the virtual DOM. It applies the necessary updates in a batch operation, reducing the overall computational cost.

**Real DOM**:

1. Representation: The Real DOM is the actual representation of the HTML structure of a web page. It is the browser's internal model that represents each element, its attributes, and the relationships between them.

2. Manipulation: When changes occur in a UI component, the Real DOM needs to be directly manipulated. This involves accessing and modifying the properties and attributes of specific elements in the actual DOM tree.

3. Efficiency: Updating the Real DOM can be computationally expensive because each change triggers a recalculation of the layout, reflow, and repaint processes in the browser.

4. Updates: When changes are made to the Real DOM, the browser updates the rendered web page accordingly. This involves modifying the structure, content, or styles of the actual HTML elements.

<hr/>

💡 **Question-4:** Whats component? Types of component

💬 **Solution-4:** 

A component is a reusable and self-contained piece of code that encapsulates the logic, structure, and styling of a UI element or a group of UI elements. Components are the building blocks of a React application, and they help organize and modularize the user interface.

In React, there are two main types of components:

1. Functional Components:
   - Functional components, also known as stateless components or presentational components, are defined as JavaScript functions.
   - They accept props (short for properties) as input and return JSX (JavaScript XML) elements as output to describe the UI.
   - Functional components are simple and primarily focused on rendering UI based on the received props.

Example:

```jsx
import React from 'react';

const MyComponent = (props) => {
  return <div>Hello, {props.name}!</div>;
};

export default MyComponent;
```

2. Class Components:
   - Class components, also known as stateful components or container components, are defined as ES6 classes that extend the React.Component class.
   - Class components have a more feature-rich API compared to functional components, as they can hold and manage their own internal state, use lifecycle methods, and handle events.
   - Class components are useful when more complex logic or state management is required.

Example:

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  handleClick = () => {
    this.setState((prevState) => ({ count: prevState.count + 1 }));
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}

export default MyComponent;
```

<hr/>

💡 **Question-5:** Difference between class & function based component

💬 **Solution-5:** 

Here are the key distinctions:

1. Syntax:
   - Class-based components are defined as ES6 classes that extend the `React.Component` class. They use the `render()` method to return the JSX representation of the component.
   - Function-based components are defined as JavaScript functions that take in props as input and return JSX elements as output.

2. State management:
   - Class-based components have their own internal state, which can be managed using the `setState()` method provided by the `React.Component` class. State allows components to store and update data over time.
   - Function-based components can also manage state using React Hooks, specifically the `useState` hook. Hooks provide a way to use state and other React features in functional components.

3. Lifecycle methods:
   - Class-based components have access to a range of lifecycle methods, such as `componentDidMount()`, `componentDidUpdate()`, and `componentWillUnmount()`. These methods allow developers to perform actions at specific points during the component's lifecycle, such as initializing data, making API requests, or cleaning up resources.
   - Function-based components can also utilize lifecycle methods using React Hooks. For example, the `useEffect` hook can be used to replicate the behavior of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` methods.

4. Code organization:
   - Class-based components can contain complex logic within methods defined in the class, such as event handlers or utility functions. This can lead to longer code files and potentially reduced readability.
   - Function-based components encourage a more modular and concise coding style. They can utilize custom hooks or separate functions for handling specific logic, which promotes code reusability and maintainability.

5. Performance:
   - Function-based components tend to have better performance compared to class-based components. This is because function components are simpler and have less overhead. With the introduction of React Hooks, function components can now manage state and use lifecycle methods efficiently, reducing the need for class components in many cases.

<hr/>

💡 **Question-6:** Explain react component life cycle 

💬 **Solution-6:** 

In React, component lifecycle refers to the series of phases and methods that a component goes through from its creation to its removal from the DOM. Each phase in the lifecycle provides specific opportunities to initialize, update, and clean up component state and perform certain actions. However with the introduction of React Hooks, there is a shift towards using functional components and the `useEffect` hook to handle component lifecycle behavior. Here is an overview of the three main phases of the React component lifecycle:

1. Mounting:
   - `constructor()`: This is the first method called when a component is instantiated. It is primarily used for initializing state and binding event handlers.
   - `render()`: The `render()` method is responsible for returning the JSX representation of the component. It is a mandatory method that should not cause any side effects.
   - `componentDidMount()`: This method is invoked immediately after the component is inserted into the DOM. It is commonly used for making API requests, setting up subscriptions, or performing other one-time initializations.

2. Updating:
   - `render()`: After the initial mounting, the `render()` method is called again whenever the component's state or props change. It is responsible for rendering the updated JSX representation of the component.
   - `componentDidUpdate(prevProps, prevState)`: This method is invoked immediately after an update occurs. It receives the previous props and state as parameters and can be used to perform actions based on the changes, such as updating the DOM or making additional API requests.
   - `shouldComponentUpdate(nextProps, nextState)`: This optional method is called before a component is re-rendered. It allows to optimize rendering by comparing the current props and state with the next props and state and returning a boolean value indicating whether an update should occur.

3. Unmounting:
   - `componentWillUnmount()`: This method is invoked just before a component is removed from the DOM. It is often used for cleaning up resources, canceling API requests, or unsubscribing from subscriptions.

<hr/>

💡 **Question-7:**  Explain Prop Drilling in React & Ways to avoid it

💬 **Solution-7:** 

Prop drilling is a term used in React to describe the scenario where props are passed through multiple intermediate components that do not need them, only to be finally used by a deeply nested component.

Example to illustrate prop drilling:

```jsx
// ParentComponent.js
import React from 'react';
import ChildComponent from './ChildComponent';

const ParentComponent = () => {
  const data = 'Some data';
  return <ChildComponent data={data} />;
};

// ChildComponent.js
import React from 'react';
import GrandchildComponent from './GrandchildComponent';

const ChildComponent = ({ data }) => {
  return <GrandchildComponent data={data} />;
};

// GrandchildComponent.js
import React from 'react';

const GrandchildComponent = ({ data }) => {
  return <div>{data}</div>;
};
```

In example, the `data` prop is passed from the `ParentComponent` to the `ChildComponent` and then to the `GrandchildComponent`. However, the `ChildComponent` itself does not need the `data` prop; it is simply used as a conduit to pass it down. This is an example of prop drilling.

To avoid prop drilling and make the codebase cleaner and more maintainable, we can consider the following approaches:

1. Context API: React's Context API allows to create a context that can be accessed by any component in the tree without the need for prop drilling. By defining a context at a higher level in the component hierarchy and providing values, we can consume those values in lower-level components without explicitly passing props through intermediaries.

2. Redux or other state management libraries: Redux is a popular state management library in the React ecosystem. It allows to store and manage the application state in a centralized store, eliminating the need to pass props through multiple components.

3. React Router: React Router provides a way to manage and access routing information across components without the need for prop drilling. The router maintains the current route information, allowing components to access it as needed.

4. Refactor component structure: Sometimes, prop drilling occurs because of the component structure itself. In such cases, consider restructuring the components to make the component hierarchy more logical and avoid unnecessary passing of props.

<hr/>

💡 **Question-8:** Create a Counter Web App using React

- Develop a web application using React that functions as a counter.
- Include two buttons in the UI:
    1. "Increment" button:
        - On clicking this button, the counter value should be incremented by one.
    2. "Decrement" button:
        - On clicking this button, the counter value should be decremented by one.
- Implement the counter logic using React's state management.
- Ensure that the counter value is displayed in the UI and updates in real-time when incremented or decremented.
- Use appropriate React components and hooks to manage the counter state and handle button click events.

💬 **Solution-8:** 

First step is to create CounterApp component in the React Application:

```jsx
import React, { useState } from 'react';

const CounterApp = () => {
  const [counter, setCounter] = useState(0);

  const incrementCounter = () => {
    setCounter(counter + 1);
  };

  const decrementCounter = () => {
    setCounter(counter - 1);
  };

  return (
    <div>
      <h1>Counter App</h1>
      <p>Counter: {counter}</p>
      <button onClick={incrementCounter}>Increment</button>
      <button onClick={decrementCounter}>Decrement</button>
    </div>
  );
};

export default CounterApp;
```

Next step is to use this CounterApp component, import it into index.js file and render it as a component in the desired location:

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import CounterApp from './CounterApp';

ReactDOM.render(<CounterApp />, document.getElementById('root'));
```

<hr/>

💡 **Question-9:** Develop a **GitHub User Finder** web application using **React** The application should allow users to enter a **GitHub username** and display relevant information about the user, including their avatar and name.

- Use Github Api to get User Data “https://api.github.com/users”

💬 **Solution-9:** 

```jsx
import React, { useState } from 'react';

const GitHubUserFinder = () => {
  const [username, setUsername] = useState('');
  const [userData, setUserData] = useState(null);

  const handleChange = (event) => {
    setUsername(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();

    fetch(`https://api.github.com/users/${username}`)
      .then((response) => response.json())
      .then((data) => setUserData(data))
      .catch((error) => {
        console.error('Error:', error);
        setUserData(null);
      });
  };

  return (
    <div>
      <h1>GitHub User Finder</h1>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={username}
          onChange={handleChange}
          placeholder="Enter a GitHub username"
          required
        />
        <button type="submit">Search</button>
      </form>
      {userData ? (
        <div>
          <img src={userData.avatar_url} alt="User Avatar" />
          <h2>{userData.name}</h2>
        </div>
      ) : (
        <p>No user data found.</p>
      )}
    </div>
  );
};

export default GitHubUserFinder;
```

To use this GitHubUserFinder component, import it into main React application file and render it as a component:

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import GitHubUserFinder from './GitHubUserFinder';

ReactDOM.render(<GitHubUserFinder />, document.getElementById('root'));
```

<hr/>

💡 **Question-10:** Develop a simple website using React, fetch and display products from the "https://fakestoreapi.com/products" API. The website should have the following features:

- Fetch product data from the "https://fakestoreapi.com/products" API.
- Display the products in a user-friendly UI.
- Show **Three products** in a single row for optimal visibility and layout.
- Use **React** to achieve the desired layout and functionality.
- Ensure that the UI is visually appealing and responsive.
- Implement error handling to handle any issues with API requests.
- Test the website thoroughly to ensure proper functionality and performance.
- Provide clear and concise documentation to guide users on how to interact with the website and understand its features.

💬 **Solution-10:** 

```jsx
App.js

import React, { useState, useEffect } from 'react';
import './style.css';

export function App(props) {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch('https://fakestoreapi.com/products')
      .then((response) => response.json())
      .then((data) => {
        setProducts(data);
        setLoading(false);
      })
      .catch((error) => {
        setError(error);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return <div className="loader">Loading...</div>;
  }

  if (error) {
    return <div className="error">Error: {error.message}</div>;
  }

  const handleAddToCart = (productId) => {
    console.log(`Added product with ID: ${productId} to cart`);
  };

  const handleBuyNow = (productId) => {
    console.log(`Clicked Buy Now for product with ID: ${productId}`);
  };

  return (
    <div className="product-list">
      {products.map((product) => (
        <div key={product.id} className="product">
          <img src={product.image} alt={product.title} className="product-image" />
          <h3 className="product-title">{product.title}</h3>
          <p className="product-price">${product.price}</p>
          <div className="button-row">
            <button onClick={() => handleAddToCart(product.id)}>Add to Cart</button>
            <button onClick={() => handleBuyNow(product.id)}>Buy Now</button>
          </div>
        </div>
      ))}
    </div>
  );
}
```

```css
style.css

.product-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.product {
  width: 300px;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  text-align: center;
}

.product-image {
  width: 200px;
  height: 200px;
  object-fit: contain;
  margin-bottom: 10px;
}

.product-title {
  font-size: 18px;
  margin-bottom: 5px;
}

.product-price {
  font-weight: bold;
}

.button-row {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.button-row button {
  margin: 0 5px;
}
```

```jsx
index.js

import React from 'react';
import ReactDOM from 'react-dom/client';

import { App } from './App.jsx'

ReactDOM.createRoot( 
  document.querySelector('#root')
).render(<App />)
```

**Screenshots**:

![assignment-8-webdev-answer-10-preview-react-io-image](./images/assignment-8-webdev-answer-10-preview-react-io.png)


<hr/>