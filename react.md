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

* Sometimes you might need to know the previous state when updating the state. However, state updates may be asynchronous - this means React may batch multiple setState() calls into a single update. This means you can't rely on the previous value of this.state or this.props when calculating the next value. So, you should not use code like this: 

```
this.setState({
  counter: this.state.counter + this.props.increment
});
```
Instead, you should pass setState a function that allows you to access state and props.

```
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```
This method is guarnteed to work.

* from elements like input of type text and textarea maintain thier own state, but we want to move this state to be maintained by the component's state. That is, we make the component's state the single source of truth regarding the input data.

* complex stateful apps can be broken down into just a few, or maybe a single, stateful component. The rest of your components simply receive state from the parent as props, and render a UI from that state. It begins to create a separation where state management is handled in one part of code and UI rendering in another. 

* The componentWillMount() method is called before the render() method when a component is being mounted to the DOM. **The componentWillMount Lifecycle method will be deprecated in a future version of 16.X and removed in version 17.**.

* The best practice with React is to place API calls or any calls to your server in the lifecycle method `componentDidMount()`. Any calls to setState() here will trigger a re-rendering of your component. The componentDidMount() method is also the best place to attach any event listeners you need to add for specific functionality. We can do it like the regular way in javascript: `document.addEventListener()`.

* `componentWillUnmount()` is usually used to do any clean up on React components before they are unmounted and destroyed, so in the case of adding event listeners in componentDidMount, we can remove event listeners in this method: `document.removeEventListener()`.

* React provides a lifecycle method you can call when child components receive new state or props, and declare specifically if the components should update or not. The method is `shouldComponentUpdate()`, and it takes `nextProps` and `nextState` as parameters. This method is mainly used to optimize re-renders and increase performance. For example, the default behavior is that your component re-renders when it receives new props, even if the props haven't changed. You can use shouldComponentUpdate() to prevent this by comparing the props. The method must return a boolean value that tells React whether or not to update the component. You can compare the current props (this.props) to the next props (nextProps) to determine if you need to update or not, and return true or false accordingly. In this example we only allow the component to re-render only if the value of its new props is even:

```
shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    return nextProps.value % 2 === 0 ? true: false;
  }
```

* If you have a large set of styles and we are using inline styles, you can assign a style object to a constant to keep your code organized. Declare your styles constant as a global variable at the top of the file: ` <div style={styles}>Style Me!</div>`.

* 