# React/Redux integration
The integration between the React components and the Redux state management part is done via the official bindings from Redux: [react-redux](https://react-redux.js.org/). This package has two main components that we will use in our regular React/Redux applications.

## Provider
The Provider is a top-level component that is added around your entire React app. 

```javascript
const store = createStore(reducer, initialState);
const app = (
    <Provider store={ reduxStore }>
        <Router>
            <App />
        </Router>
    </Provider>
);
```

Just as a reference, the `Provider` is implemented on top of React Context

This component gets the redux store as a parameter and then exposes the store to all the React components through the second abstraction we will be talking about next.

## Connect
In order to access the state of the store or to dispatch actions you need access at component level. This is done through the `connect` HOC provided by `react-redux`. Remember that HOCs are taking your input component and are returning a slightly modifed version of that component. In our case, `connect` is added props to the original component.

This is how you define a connect HOC around your component. Notice that this is a two-stage function, first you send the connect parameters and you get back another function where you send the component.
```javascript
const Counter = () => ( /* ... */ )

export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```

So what are `mapStateToProps` and `mapDispatchToProps`?

### mapStateToProps
This is a function that takes the entire state of the Redux store, obtained by `store.getState()`, and computes props or simply passes parts of that state as props for the components that is "connected". `mapStateToProps` should return an object, each key of the object will be a top level prop in the component. In case the function is not needed, `null` can be used.

Example:
```javascript
const mapStateToProps = (state) => ({
  todos: state.todos,
  filter: state.visibilityFilter
});
```

You can also map functions inside, so a function prop will be passed to your component:
```javascript
const mapStateToProps = (state) => ({
  userExists: (username) => state.users.contains(username) // function will be called inside the component
});
```

### mapDispatchToProps
This is another function, which now maps the actions that we want to dispatch from inside the component. Since the `dispatch` function is called on the Redux store and component don't have a direct reference to the store, we need to map the actions in advance and send the functions are props.

Example:
```javascript
const mapDispatchToProps = (dispatch) => ({
  increment: dispatch(actions.increment),
  decrement: dispatch(actions.decrement),
})
```

We're assuming here that actions are collected into an object (`actions`) because they are defined in different files. When we use action creators we have a simpler form for defining `mapDispatchToProps`, starting from the assumption that the params match the action creator params:
```javascript
const mapDispatchToProps = {
  increment: actions.increment,
  decrement: actions.decrement,
}
```
There are a bunch of patterns for mapDispatchToProps, trying to abstract and avoid code duplication or this kind of boilerplate code. However, I think that this offers more clarity into which actions are mapped and which are not. Feel free to document yourself more on how to use action creators directly as mapDispatchToProps or how to use `bindActionCreators`.

**[Full CodeSandbox example](https://codesandbox.io/s/ppnz28165x)** - check this full counter example.

**connect** is the critical glue between the React components and Redux, make sure you spend enough time understanding what is happening here.

Each dispatch to Redux will trigger the reducers to calculate the new state of the application, so each new state means that the two functions are called, so new props *might* be passed to the components, triggering a re-render. To get more in depth into the re-render mechanisms, check the documentation and look at the *pure* configuration option.

## Redux Selectors
Sometimes the raw state needs some sort of transformation in order to represent relevant data for the UI. One such example might be the cart total, in a shopping cart store. The total may not be kept as an exact value inside the store, but can be computed out of each new state based on the line items. A **selector** is a function that does that computation for you. When you define selectors on top of the Redux store, you eliminate the need to duplicate this logic inside each component where the computed data is needed. Selectors are simple functions that can be used inside `mapStateToProps`:
```javascript
const mapStateToProps = (state) => ({
  cartItems: state.items,
  cartTotal: computeCartTotal(state.items)
});
```

The Redux ecosystem has libraries that abstract some of the things we discussed about and [reselect](https://github.com/reduxjs/reselect) is one of them, handling the Redux selectors.

## Container vs Presentational Components
A common pattern is to separate components which are connected to Redux as **container components**. These components have the connect around them, maybe have some state and do data processing / event handling if needed. But they don't render too much JSX, only child components at most. The child components then become what is known as **presentational components**, they are heavy on the JSX side, but are not directly connected to Redux and they get all their props from the parent components.

## Scaling Redux
Scaling Redux and structuring a React/Redux app has been a hot topic for quite some time. It's an opinionated environment with a lot of pros and cons for various approaches.

In [this article](https://medium.freecodecamp.org/scaling-your-redux-app-with-ducks-6115955638be) that I wrote some time ago, I'm trying to paint a better picture for everyone who is new to React/Redux architectures.

**References**
* [Official binding docs](https://react-redux.js.org/docs/api)
* [Reselect](https://github.com/reduxjs/reselect)
* [The Re-ducks proposal](https://github.com/alexnm/re-ducks)
