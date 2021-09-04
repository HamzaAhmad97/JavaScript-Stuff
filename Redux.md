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

* it is a good idea to use switch statement within the educer function to handle the different types of actions.

* A common practice when working with Redux is to assign action types as read-only constants, then reference these constants wherever they are used. You can refactor the code you're working with to write the action types as const declarations:

```
const LOGIN = 'LOGIN';
const LOGOUT= 'LOGOUT';
const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {

  switch (action.type) {
    case LOGIN: 
      return {
        authenticated: true
      }
    case LOGOUT: 
      return {
        authenticated: false
      }

    default:
      return state;

  }

};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: LOGIN
  }
};

const logoutUser = () => {
  return {
    type: LOGOUT
  }
};
```

* we use the method `subscribe()` for the store that takes a callback function, this method allows you to subscribe listener function to the store which are called whenever an action is dispatched against the store. One simple use for this method is to subscribe a function to your store that simply logs a message every time an action is received and the store is updated.

```
let count = 0;

const increment = () => {
  count = count + 1;
}
store.subscribe(increment);
```

* when we have a more complex state, instead of dividing the state into multiple pieces, we make use of reducer composition, you define multiple reducers to handle different pieces of your application's state, then compose these reducers together into one root reducer. The root reducer is then passed into the Redux createStore() method. In order to let us combine multiple reducers together, Redux provides the `combineReducers()` method. This method accepts an object as an argument in which you define properties which associate keys to specific reducer functions. The name you give to the keys will be used by Redux as the name for the associated piece of state:

```
const rootReducer = Redux.combineReducers({
  auth: authenticationReducer,
  notes: notesReducer
});
```

As an example, we create a reducer function for each piece of application state when they are distinct or unique, like authenticaton and handling user's input like notes here.

```
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

const counterReducer = (state = 0, action) => {
  switch(action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
};

const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const authReducer = (state = {authenticated: false}, action) => {
  switch(action.type) {
    case LOGIN:
      return {
        authenticated: true
      }
    case LOGOUT:
      return {
        authenticated: false
      }
    default:
      return state;
  }
};

const rootReducer = Redux.combineReducers({
  count: counterReducer, 
  auth: authReducer
})// Define the root reducer here

const store = Redux.createStore(rootReducer);
```

* You can also send specific data along with your actions other than 'type' since usually these actions originate from user interactions.

```
const addNoteText = (note) => {
  return ({
    type: ADD_NOTE,
    text: note,
  })
};
```

* for handling asynchronous endpoints in a redux app, you will need to use a middleware called *redux thunk middleware*. You pass it as an argument to `Redux.applyMiddleware()`. this whole statement is then passed as an optional parameter to the createStore() funtion. 

```
const store = Redux.createStore(
  asyncDataReducer,
  Redux.applyMiddleware(ReduxThunk.default)
);
```

Then, to create an asynchronous action, you return a function in the action creator that takes dispatch as an argument. Within this function, you can dispatch actions and perform asynchronous requests.

```
const REQUESTING_DATA = 'REQUESTING_DATA'
const RECEIVED_DATA = 'RECEIVED_DATA'

const requestingData = () => { return {type: REQUESTING_DATA} }
const receivedData = (data) => { return {type: RECEIVED_DATA, users: data.users} }

const handleAsync = () => {
  return function(dispatch) {
    // Dispatch request action here
    store.dispatch(requestingData());
    setTimeout(function() {
      let data = {
        users: ['Jeff', 'William', 'Alice']
      }
      // Dispatch received data action here
      store.dispatch(receivedData(data));
    }, 2500);
  }
};

const defaultState = {
  fetching: false,
  users: []
};

const asyncDataReducer = (state = defaultState, action) => {
  switch(action.type) {
    case REQUESTING_DATA:
      return {
        fetching: true,
        users: []
      }
    case RECEIVED_DATA:
      return {
        fetching: false,
        users: action.users
      }
    default:
      return state;
  }
};

const store = Redux.createStore(
  asyncDataReducer,
  Redux.applyMiddleware(ReduxThunk.default)
);
```

* to avoid mutating the state and returning a new one, we can use the spread operator to copy the previous state: `let newArray = [...myArray];`,  but it's important to note that it only makes a shallow copy of the array. That is to say, it only provides immutable array operations for one-dimensional arrays.

* we can use `concat()` and `slice()` to make copies and especially when you need to remove an item from an array: `[...state].slice(0,action.index).concat([...state].slice(action.index + 1))`.

* we can make use of `Object.assign()` to make copies from objects: `const newObject = Object.assign({}, obj1, obj2);`, where here the target object which is emppty, will have the properties in both the second and third objects.