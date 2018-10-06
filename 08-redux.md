# Redux
By far the most popular state management library in the React ecosystem, Redux offers a simple and efficient pattern through which you do state management. Learning Redux is pretty easy, as the library itself can be written in several lines of code. But there's a huge ecosystem around Redux which tends to get rather complex and has a very steep learning curve. Today the community is debating a lot on using Redux and the Redux ecosystem, but all in all it is a widely used solution and it is definitely a good learning step before moving to something else.

One word of advice, before we begin: Redux or any state management library does not need to be there from the beginning. Maybe an early stage project doesn't need a separate state management library. Make sure you take that into account when decided on the tech stack for a new project.

## Single state object
Redux has a single state object, called **store**. The object is created/initialized with the `createStore` function provided by Redux.

The only condition for the store object is to be a serializable object, so it can contain anything from arrays, sub-objects, booleans, numbers and strings. Shapping the state object is entirely in the hands of the developer.

Let's consider a simple store object keeping info about the session
```javascript
{
  isAuthenticated: false
  username: null
}
```

The ground rule of redux is that you treat the store as an **immutable** object and its state is **readonly** for the UI layer.

## Actions and Reducers
In order to be able to change the state, we need to introduce the undirectional flow we've been discussing in the previous chapter. Redux has two fundamental constructs: **actions** and **reducers**.

Actions are simple objects with a fixed format. They all must have a `type` property, which is an unique string literal identifying the action, an action name if you want. The common practice is to use UPPER_SNAKE_CASE to define the actions, but in larger applications you can also prefix the action with the business object is refers to, ex: "product/ADD_TO_CART". Another practice is to put the rest of the action values into a `payload` property, but this is absolutely optional and depends on the design and architecture decisions of the system.

Example action:
```javascript
{
  type: "LOGIN",
  payload: {
    username: "alice"
  }
}
```

An action is triggered with the `store.dispatch` function (see below).

Reducers are **pure functions** that take the **current state**, the **action** being dispatched and return the **new state** based on that action. In the simplest form, the reducer is a switch statement that acts acording to the action type. Keep in mind that the state should not be directly mutated inside the reducers, but a new state should be created with each pass.

The function looks like this: `const reducer = (state, action) => state`.

You can think of the Redux store as a state machine, with an infinite number of possible states, but with a very easy way to visualize both the current state **N** and all the previous **N-1** states, because of the predictibility of the actions/reducers system.

## Redux API
As mentioned before, Redux is a very simple library

Here's an example of a Redux store in action
```javascript
const initialState = 0;

const increment = {
    type: "INCREMENT",
};

const decrement = {
    type: "DECREMENT",
};

const reducer = (state, action) => {
    switch (action.type) {
        case "INCREMENT":
            return state + 1;
        case "DECREMENT":
            return state - 1;
        default:
            return state;
    }
};

const store = createStore(reducer, initialState);
store.dispatch(increment);
store.dispatch(decrement);
```

### createStore
This is called once when Redux is initialized and is creating a store instance object. It requires a reducer to function and can optionally take the initialState as a second param.

### getState
The store object has a function `getState` which retrieves the entire state shape. It can be called anywhere you have access to the store object.

### dispatch
The store object also has a function `dispatch` which is used to send each individual action to the reducer(s). Dispatch always has a single parameter, the action object which it dispatches. Inside the dispatch function, Redux calls the reducer function with the existing state and the action it receives as a param.

Check out [this example](https://codesandbox.io/s/1qq39yk0n4) which implements the code we discussed so far.

### combineReducers
Having a single reducer for the entire application is not really scalable, because you end up with a monster switch with tens/hundreds of cases. So Redux also offers a handy function, `combineReducers`, with which you can break down the reducers into multiple smaller functions that handle a certain part of the entire state shape.

You can check the official docs for a very good example of this (slighly adapted):
```javascript
function visibilityFilterReducer(state, action) {
  /* ... */
}

function todosReducer(state, action) {
  /* ... */
}

const reducer = combineReducers({
  visibilityFilter: visibilityFilterReducer,
  todos: todosReducer
})
```

## Middlewares
The Redux ecosystem is built on top of the middleware pattern, which allows you basically to override the dispatch function and add intermediate steps to the whole flow.

A middleware is a [curried function](https://hackernoon.com/currying-in-js-d9ddc64f162e) of the form:
```javascript
const middleware = store => next => action => {
  /* perform operations before the dispatch */
  next( action ); // this will actually call the original dispatch
  /* perform operations after the dispatch */
}
```

Check out a simple [custom logger example here](https://codesandbox.io/s/zxv1lv5xx).

A few examples of widely used middlewares:
* [redux-thunk](https://github.com/reduxjs/redux-thunk)
* [redux-saga](https://github.com/redux-saga/redux-saga)
* [redux-logger](https://github.com/evgenyrodionov/redux-logger)
* [redux-persist](https://github.com/rt2zz/redux-persist)

**References**
* [Redux tutorial by Dan Abramov](https://egghead.io/courses/getting-started-with-redux)
