# Introduction to React
Let's go through the basic elements of React

## JSX
`JSX is a syntax extension to JavaScript. It is similar to a template language, but it has full power of JavaScript. JSX gets compiled to React.createElement() calls which return plain JavaScript objects called “React elements”. To get a basic introduction to JSX see the docs here and find a more in-depth tutorial on JSX here. React DOM uses camelCase property naming convention instead of HTML attribute names. For example, tabindex becomes tabIndex in JSX. The attribute class is also written as className since class is a reserved word in JavaScript.`

Source: https://reactjs.org/docs/glossary.html#jsx

So JSX is nothing more than sugar syntax on top of JavaScript, allowing you to write what seems to be HTML-in-JS, but translating it into function calls, as you can see in this [babel live transpiler](https://babeljs.io/repl/#?babili=false&browsers=safari%20%3E%207&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgzgLgBAggBwTAvDAFASlQPgwKBhgB4ATASwDcZoBPAGwFMUBvOpiAXx0KJIAlG9eiBhgAhgFtmAIgDCIUowDK4sKQBGIAB4yYAeh58SACwBMOZVHEAnWIwpRyYAOYwooiI0Y0Q0mJLiLuTAMCbiSIxgMCwA5AA6AK5mAOxmAByxnMT65kYk-hSUPJgA3EA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=true&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=react%2Cenv&prettier=false&targets=&version=6.26.0&envVersion=1.6.2).

React can also run directly in the browser when added as a dependency, but you also have to add a jsx parser lib. In most of the cases, you will have a `webpack/babel` setup in your project that will automatically transpile **JavaScript** and **JSX** to standard JavaScript that can run in any browser.

JSX does not break separation of concerns, components are simply a new way of separating concerns based on function, not on technology!
![Separation of Concerns](https://pbs.twimg.com/media/Dcl2jTiWkAA0hnp.jpg:large)

## Custom Components
React components are created by extending the `React.Component` class. There are some alternatives to this, but we will check them out when we go a bit more in depth into React. For now, we create a class with a single function called `render`.

```javascript
class App extends React.Component {
    render() {
        return (
            <div>
                <h1 className="heading">Hello React!</h1>
                <p>This is a paragraph!</p>
                <p>This is another paragraph!</p>
            </div>
        );
    }
}
```

Working example [here](https://codesandbox.io/s/y0pz7jr901)

Each component creates a new <tag> which is available in your JSX code. Custom components should always start with a capital letter! The component behaves exactly like a regular tag. Feel free to inspect the DOM and install React Dev Tools to see the components in action!
  
```javascript
class App extends React.Component {
    render() {
        return (
            <div>
                <h1 className="heading">Hello React!</h1>
                <p>This is a paragraph!</p>
                <p>This is another paragraph!</p>
                <Greeting />
            </div>
        );
    }
}

class Greeting extends React.Component {
    render() {
        return <span>Hello Stranger!</span>;
    }
}
```

## Component Elements
Let's have a look at some of the basic elements that make up a React Component.

### Render function

### Props

### State

### Lifecycle Hooks

### Constructor (or not)

**References**
* [React Official Tutorial](https://reactjs.org/tutorial/tutorial.html)
* [Rethinking Best Practices](https://www.youtube.com/watch?v=x7cQ3mrcKaY)
* [Egghead Course](https://blog.kentcdodds.com/learn-react-fundamentals-and-advanced-patterns-eac90341c9db)
* [I wish I new these before diving into React](https://engineering.opsgenie.com/i-wish-i-knew-these-before-diving-into-react-301e0ee2e488)
* [React Dev Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
