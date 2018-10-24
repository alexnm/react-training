# Modern Web Development
Before we dive deep into the React ecosystem, let's take a closer look at the current state of web development.

## Breaking the monolith
The traditional monolith is being replaced with a more specialized architecture. There are multiple approaches here and it's not the aim of this training to cover them, but the frontend ecosystem is being heavily impacted by this architectural shift
* The frontend code is no longer embedded into the backend web application framework (ex: RubyOnRails, ASP.NET MVC, Django)
* The backend has a clear interface through which it provides only data access (ex: REST API, GraphQL)
* The frontend code is not just a collection of modules that provide interactivity, but now has complex responsibility like: routing, templating, data management, etc.
* The frontend ecosystem is rich with build tools and libraries that compile the code to standard html, css and javascript (ex: Webpack, Babel, Gulp, TypeScript/Flowtype, CSS-in-JS)

**References**
* [Breaking the monolith](https://martinfowler.com/articles/break-monolith-into-microservices.html)
* [Again, this is a great article!](https://medium.com/@peterxjang/modern-javascript-explained-for-dinosaurs-f695e9747b70)

## Component Based UI
As a result of the FE ecosystem getting more and more complex, new ways of architecting the new idea of a "frontend application" had to be developed. While the initial push was towards the **MVC** approach ported on the FE as a **MVVM**-style architecture, later, framework developers realized that the UI interaction needs a different architecture. Slowly, each framework moved towards the component based architecture, where each individual UI component works as an MVC system inside, but encapsulates all that behavior and UI into a reusable piece of code.

![Classic Frontend](https://reactjs.org/static/thinking-in-react-mock-1071fbcc9eed01fddc115b41e193ec11-4dd91.png "Classic Frontend")
![Component Split](https://reactjs.org/static/thinking-in-react-components-eb8bda25806a89ebdc838813bdfa3601-82965.png "Component Split")

Source: https://reactjs.org/docs/thinking-in-react.html

**References**
* [Is MVC dead for the frontend?](https://medium.freecodecamp.org/is-mvc-dead-for-the-frontend-35b4d1fe39ec)
* [Thinking in React](https://reactjs.org/docs/thinking-in-react.html)

## Declarative vs Imperative UI
Together with these major shifts in web architecture, we have new ways of writing code. The jquery era favored the imperative approach of changing the DOM based on data flows and events. React and the new wave of frameworks favor a more declarative way of building UIs. We no longer have to deal with DOM selectors and direct DOM manipulation. This also makes way for faster and more reliable libraries that are handling the direct DOM changes for us.

Imperative DOM manipulation
```javascript
$("#button").click(function(event) {
    var value = $("#item").val();
    todos.push(value);
    $("ul").html("");
    render();
    $("#item").val("");
});

function render() {
    for (let index = 0; index < todos.length; index++) {
        $("ul").append(`<li>${todos[index]}</li>`);
    }
}
```

Declarative DOM
```javascript
onClick = () => {
    const newValue = inputRef.current.value;
    this.setState(state => ({
        todos: state.todos.concat(newValue),
    }));
    inputRef.current.value = "";
};

render() {
    return (
        <div>
            <h1>Hello React!</h1>
            <ul>{this.state.todos.map(todo => <li>{todo}</li>)}</ul>
            <input ref={inputRef} id="item" name="item" />
            <button onClick={this.onClick}>Click me!</button>
        </div>
    );
}
```

The fully working examples can be found [here](https://codesandbox.io/s/43np9vp839) and [here](https://codesandbox.io/s/oo0980nk99).

**References**
* [Declarative vs Imperative Programming](https://tylermcginnis.com/imperative-vs-declarative-programming/)
* [Making the DOM Declarative](https://www.youtube.com/watch?v=vyO5wKHlWZg)
