# Patterns in React
Before we dive deeper into the React ecosystem, let's look at a set of common patterns and practices used by the community.

## Component Design
The purpose of these patterns is to improve the readability, simplicity or the performance of your React components.

### Conditional Rendering
When people think of React and JSX, they still think in terms of HTML and JavaScript. But remember! JSX is just JavaScript! So when we need to render something based on some condition, the first idea is to compute that output with a ternary operator:
```const content = show ? <h1>Hello {name}!</h1> : null;```

But we can also leverage the power of boolean expressions in JavaScript. If the left-hand operator is `true`, the `JSX` will be rendered!
```javascript
render() {
    const { name, show } = this.props;
    return (
        <div>
            <p>Before text</p>
            {show && <h1>Hello {name}!</h1>}
            <p>After text</p>
        </div>
    );
}
```

**[Full Example](https://codesandbox.io/s/l4v80652ol)**

### Stateless functional components
When `render` is the only function needed and the component does not rely on internal state, a simpler form of writing can be used. The component does not rely on state, so we call it a **stateless** component. When we have such a situation, the component pretty much acts as a **pure function**: it takes some input parameters (showName, showMessage, name) and returns some output (the JSX code). If we render this component with the same props, it will **always** return the same output.

So React allows you to write components as simple functions:

```javascript
const Message = ({ name, showName, showMessage }) => (
    <div>
        {showName && <h1>Hello {name}!</h1>}
        {showMessage && <h2>How are you today?</h2>}
    </div>
);
```

Functional stateless components have the following characteristics:
* They don’t create an actual `React` component object in memory
* They don’t have `this` as a reference
* They have no **lifecycle hooks** and re-render **everytime** the parent component re-renders
* They receive the `props` object as the first parameter

**[Full Example](https://codesandbox.io/s/18o6z78nm3)**

### State Lifting
When building complex structures with `React`, there's always the question: where should this state be placed? It will often be a matter of taste, of mixing stateless and stateful component. But in one particular situation you need to resolve to a pattern known as **state lifting**. This pattern usually involves handling the `state` value in a parent component and sending an `onChange/onUpdate` function `prop` to the child component.

**[Full Example](https://codesandbox.io/s/qvz0qr29l6)**

The React documentation covers this use case with a more [complex scenario](https://reactjs.org/docs/lifting-state-up.html).

### Children Props
React provides a `children` prop that represents the content rendered inside the component. In other words, you can write something like that to render the inner content of a component:

```javascript
const WithBorder = ({ children }) => (
  <div style={{ border: "1px solid red" }}>
    {children}
  </div>
);

const App = (
  <WithBorder>
    <p>Hello world!</p>
  </WithBorder>
);
```

This very simple pattern also allows composability:
```javascript
const App = (
  <WithBorder>
    <WithBorder>
      <p>Hello world!</p>
    </WithBorder>
  </WithBorder>
);
```

**[Full Example](https://codesandbox.io/s/8xj528p53j)**

## Reusability and Composition
Below are a couple of well known patterns that are widely used in the React community. However, getting in depth into them is beyond the scope of this introductory course. These are, however, good references for continuing the learning path with React. They also require a bit of hands-on experience with React to be properly understood and for them to make sense.

### Higher Order Components
Starting from the concept of [higher-order functions](https://eloquentjavascript.net/05_higher_order.html), the community developed the concept of higher order component (or HOC) that is nothing more than a function which accepts a component as a parameter and returns a modified version of that component. They are also called *decorators* or *enhancers* because of the similarities with the decorator pattern.

A few examples can be found in [this sandbox](https://codesandbox.io/s/vv198n1y00).

HOCs are providing **static composition** and are useful when implementing [cross-cutting concerns](https://en.wikipedia.org/wiki/Cross-cutting_concern) (logging, authorization, 3rd party integration, etc.). HOCs are used by a lot of libraries in the React ecosystem, most notably react-redux, recompose, redux-forms, etc.

### Render Props
Another pattern for reusing bits of functionality, the idea behind the render prop pattern is to send a **function prop** to a child component and to expect that component to call the function and place the resulting JSX (the render prop should return some JSX) inside its own **render** function.

A few examples can be found [here](https://codesandbox.io/s/nk9jvnp3wp).

Render props are providing **dynamic composition** allowing you to share small pieces of logic between components. The pattern is also used in libraries in the React ecosystem: react-motion, react-router, formik, etc.

### React Context
React has a 3rd way of handling data and an additional way of passing data between components (other than props). It is called the **context** and has not been a widely used functionality because it was mostly considered experimental and aimed at helping library creators. However, since **React 16.3**, a nice syntax was standardized and the **Context API** can be used today following [the documentation](https://reactjs.org/docs/context.html).

**References**
* [React Patterns](https://reactpatterns.com/)
* [Evolving patterns in React](https://medium.freecodecamp.org/evolving-patterns-in-react-116140e5fe8f)
* [Never use another HOC](https://www.youtube.com/watch?v=BcVAq3YFiuc) - advocating for using the render props pattern
* [React ContextAPI](https://medium.com/dailyjs/reacts-%EF%B8%8F-new-context-api-70c9fe01596b)
