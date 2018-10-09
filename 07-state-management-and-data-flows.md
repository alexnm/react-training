# State Management and Data Flows
Since frontend code became a separate project/application, complexity grew and architectural patterns evolved. We looked in depth at the UI side of the frontend stack, but now we'll have a look at how **state management** is done in modern web applications. The following two chapters are not necesarily related to the React ecosystem. All the ideas here are easily implemented with other frontend frameworks.

## UI vs App State
Before we dive deep into a couple of ideas, let's try to separate state. A frontend application mainly handle two types of state objects/values:
* **UI State** (ex: activeTab, showButton, loginFormValues)
* **App State** (ex: session, products, images)

Unfortunately it's almost impossible to draw an exact line and define a strict rule of what is app state and what is UI state. It will always be a thing of judgement and preference, of architecture and design. One good example is the form state, the object behind a form. You could argue that it is UI state, because it is mapped 1:1 to the inputs, but you could also argue that it represents a business object so it belongs in the app state.

For the UI state, we've seen how React can handle the state at the component level. There's no ground rule on this, but in general, the UI state should be encapsulated in the components that you are building. Remember that components should work in any context, with as few external dependencies as possible.

Application state can be regarded as easily accessible information (ex: objects, values) that is kept in memory and has it's own encapsulated management system (changes, transforms). Application state should not (if possible) leak as a global object. A very naïve approach is to consider the application state as the "immediate backend" for the frontend.

## Immutability and Pure Functions
Coming from the world of functional programming, the concepts of immutability and pure functions gradually were introduced into frameworks and libraries in JavaScript. The language itself does not have immutable data structures, so any operation on arrays and objects are just modifying the existing data structure. One of the disadvantages of mutating objects is that the state becomes less predictive and harder to share between multiple subsystems.

While not being a mandatory rule, immutability is prefered when dealing with state management in modern frontend. Immutability means that we can easily compare different state objects and subtrees of the same state object in different points in time. The shift towards a declarative UI and libraries which always re-render the entire virtual DOM is also welcoming immutable data structures because of the speed of the comparisons (checking if the state changed becomes an O(1) operation).

## Unidirectional Flows
One of the major drawbacks of the early frontend frameworks (backbone, angular.js, knockout) was the use of two-directional flows. Any part of the application could directly change any object in the state part (ex: angular services, backbone models). This often lead to unwanted side-effects, with object references passed by accident between the two layers.

Most of the modern frontend framework recognized these early issues, so the community came up with a lot of libraries that are doing state mangement in a simple unidirectional way.

![Flux](https://facebook.github.io/flux/img/flux-simple-f8-diagram-1300w.png)
Source: https://facebook.github.io

Flux is an architecture developed by facebook in the early days of React and is aimed at offering a predictable and easily reproduceable state. It is unidirectional because the UI cannot directly modify the state (store), but can only dispatch actions that will **eventually** update the state. So all the **data flows** in a **unidirectional** way through the architecture.

## Actions/Events
Most of the flux libraries, including Redux, which we will take a look at in the coming chapter, are heavily relying on actions/events to communicate between the two layers (UI, state).

**Actions** are simple **objects** which have a `type` and a `payload`. They describe the change that needs to be applied to the state. Example:
```javascript
{
  type: "ADD_TO_CART",
  payload: {
     productId: 123
  }
}
``` 

The **UI** will usually **listen** for **events** coming from the state (ex: state updated) and will trigger its mechanism for updating the DOM.

The way state is managed in uni-directional architectures has some similarities with the [event sourcing](https://martinfowler.com/eaaDev/EventSourcing.html) architecture model.

**References**
* [What is a pure function](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976)
* [Immutable data structures in JS](https://www.youtube.com/watch?v=noBDly9LuSs)
* [Flux Architecture](https://facebook.github.io/flux/)
