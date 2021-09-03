# Redux

* In Redux, there is a single state object that's responsible for the entire state of your application. This means if you had a React app with ten components, and each component had its own local state, the entire state of your app would be defined by a single state object housed in the Redux **store**. The Redux store is the single source of truth when it comes to application state. This also means that any time any piece of your app wants to update state, it must do so through the Redux store. The unidirectional data flow makes it easier to track state management in your app.

* The Redux store is an object which holds and manages application state. There is a method called `createStore()` on the Redux object, which you use to create the Redux store. It takes the *reducer* funciton as a reuired argument: 

```
const reducer = (state = 5) => {
  return state;
}

let store = Redux.createStore(reducer);
```

* We can retrieve the current state using the method `getState()` on a store: 

```
const store = Redux.createStore(
  (state = 5) => state
);

let currentState = store.getState();
```

* In Redux, state updates are triggered by dispatching actions, **actions are simply javascript objects that contain information about an action event that has occured**. The Redux store receives these action objects, then updates its state accordingly. Sometimes a Redux action also carries some data. For example, the action carries a username after a user logs in. While the data is optional, actions must carry a type property that specifies the 'type' of action that occurred. We can think of Redux actions as messengers that deliver information about the actios that happen to the redux store. Writing redux actions is simply as writing simple objects that has at least the 'type' property, note that the value of this property can be anything the user sets:

```
let action = {
  type: 'LOGIN',
}
```

* To handle sending the actions to the Redux store, we use *action creators*, which are simply functions that return actions. In other words, action creators create objects that represent action events.

```
const action = {
  type: 'LOGIN'
}
function actionCreator() {
  return action;
}
```

* `dispatch` method is what you use to dispatch actions to the Redux store. Calling `store.dispatch()` and passing the value returned from an action creator sends an action back to the store.

```
store.dispatch(actionCreator());
store.dispatch({ type: 'LOGIN' });
```

Both of these lines are equivalent since the action creators return action objects.

* Once an action is created and dispatched, redux store needs to know how to respond to that action, thus comes the reducer function, it is responsible for state modification. It takes a state and action as arguments and always returns a new state, these are the only things that can be done inside this function.

* The state in redux is read-only the reducer function always returns a new copy of state and never modifies the state directly, thus it is a pure function that does not cause any side effects.

```
const reducer = (state = defaultState, action) => {
  if (action.type === 'LOGIN') {
    return {login: true};
  } else {
    return state;
  }
};
```

* 