# React

* React works by calling `ReactDOM.render(JSX, document.getElementById('root'))`. This function call is what places your JSX into React's own lightweight representation of the DOM. React then uses snapshots of its own DOM to optimize updating only specific parts of the actual DOM.

* Regarding JSX, it should only return a signle element, this parent element can wrap all nested elements. Note that we can also wrap everything in parantheses, but it is not strictly required.

* we use `{/* */}` to put comments inside a JSX.

* functional components are stateless, they are just functions that return either JSX or null. The function name should start with a capital letter just like constructor functions.

```
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

* we can use functional and class based components together since we only care about the returned JSX.

* functional components also have access to props, but we do not have to use `this`, props is just an object here so we can access the properties just like normal objects: `const Welcome = (props) => <h1>Hello, {props.user}!</h1>`.

* we can pass an array as props like this: `colors={["green", "blue", "red"]}`.

* you can define default values for components, so that if no value is provided for that property, it will get assigned a default value provided, for functional components, we define it outside the function like this: `MyComponent.defaultProps = { location: 'San Francisco' }`, you can also provide the value null. To override these default props, just assign them explicitly, as you define props in general.

* we use `propTypes` to tell that the passed values must be of that type, just like a schema, react will throw an error if the provided value does not match the set types: `MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }`, in this case, `.func` defines that this property is of type function, you can replace it with the other primitive types like `.bool` if the value is expected to be a boolean, and many other types that can be checked from the documentation, `isRequired` tells that this property is required, and react will throw a warning if this property is not provided. As of React v15.5.0, PropTypes is imported independently from React, like this: `import PropTypes from 'prop-types'`. Note that it is defined just like defaultProps.

* a **stateful component** is a class component that does maintain its own internal state. A common pattern is to try to minimize statefulness and to create stateless functional components wherever possible. This helps contain your state management to a specific area of your application. In turn, this improves development and maintenance of your app by making it easier to follow how changes to state affect its behavior.

* In the render() method, before the return statement, you can write JavaScript directly. For example, you could declare functions, access data from state or props, perform computations on this data, and so on. Then, you can assign any data to variables, which you have access to in the return statement.

* 