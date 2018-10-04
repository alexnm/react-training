# Client side routing

In order to start building relevant web applications with React, we must have a way of showing different components based on the url visited by the user, otherwise known as **routing**.

Traditionally routing has been handled by the backend, so each route change meant a full page reload, a new HTML basically taking the place of the old one. With client side routing we can work our way around this, changing the components (pages) on the fly and changing the url (based on the strategy used) while keeping the same root HTML in place.

There are multiple libraries that are handling routing functionalities in React and there's no official library built by the core team, as there is the case of Vue.js. However, [react-router](https://reacttraining.com/react-router/) is pretty much the standard approach today. Other notable libraries are: [reach-router](https://github.com/reach/router) - accessible first routing library and [router5](https://router5.js.org/)(https://router5.js.org/).

## Browser History vs Hash Routing

There are two main options for configuring a router, `BrowserRouter` and `HashRouter`.

**BrowserRouter** relies on the HistoryAPI capabilities introduced in HTML5, on pushState, popState and replaceState. This is very convenient because the user doesn't see any difference compared to traditionally server rendered applications. For them, the url changes, the page changes. The only perceivable difference is in speed, because they don't get a new page load.

**HashRouter** relies on the hash part (ex: example.com/#about) of the url and can be convenient when you have a client application mounted inside a more complex server rendered application and you don't want to change the base url for that application.

## Router Setup

Here is the most basic setup for react-router involving 3 pages and using the browser history:

```javascript
<BrowserRouter>
    <div>
        <header>
            <Link to="/">Home</Link>
            <Link to="/about">About</Link>
            <Link to="/contact">Contact</Link>
        </header>
        <Route path="/" exact component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
    </div>
</BrowserRouter>
```

`BrowserRouter` can easily we swapped with `HashRouter` to enable **hash** navigation instead. the `Link` component simply renders an anchor tag which changes the url when clicked. However, this does not behave as a regular anchor tag and does not trigger a full page reload.

Complete solution [in codesandbox](https://codesandbox.io/s/jz8x6l30qv)

## Matching Routes

The `Route` component works on a very simple principle: If the url **matches**, the component is rendered in place. There are multiple props that you can use on a `Route`, but most importantly you would want to use `exact: true` or simply `exact` as an attribute. When `exact` is true, the url match is done using the string equality operation. When `exact` is false, which is the default value, the match is done using `indexOf`. This means that if you have two Routes defined next to each other, one with the path `/java` and one with `/java/script`, both components will be rendered one after another when the user ends on `/java`.

There's also a `<Switch>` tag which can be used, also part of `react-router` which forces a single component to be rendered at a time. This is useful when building a complex page routing, but you must be careful with the order of the routes, or you risk having a general route take precedence over a more specific one.

## Dynamic Routes

There are cases where you want the url to have a dynamic part (ex: an id, a permalink, a category). For those situations, the paths can be matched against dynamic routes:
```javascript
<Route path="/food/:foodType" component={Restaurant} />
```

At this point, any url starting with `/food` will match with this route: /food/pizza, /food/icecream.

Subsequently, when the `<Restaurant>` component will mount, it will receive the following props:
* `this.props.location` -> reference to the browser location object
* `this.props.history` -> reference to the browser history object
* `this.props.match` -> an object with the result of the route match, that among others has the params from the dynamic url

Hence, if you want to access the dynamic `:foodType` param, you would use: `this.props.match.params.foodType`. You can check out this full **example** on [codesandbox](https://codesandbox.io/s/84yk989mw2).

## Redirects

Another useful scenario is when you want a certain url to be redirected to another one, or you want to redirect somewhere based on a user action (ex: login). In those cases, you can use the `<Redirect>` component. When a `<Redirect>` is rendered, it immediately uses the history API to change the url to the specified location. When `<Redirect>` is specified in a list of routes, you need to send the `from` prop, for react-router to know when the redirect should happen. 

Check [this example](https://codesandbox.io/s/l53kl1mp2z) of using a Redirect component.

**References**
* [react-router official docs](https://reacttraining.com/react-router/)
* [react-router tutorial](https://medium.com/@pshrmn/a-simple-react-router-v4-tutorial-7f23ff27adf)
