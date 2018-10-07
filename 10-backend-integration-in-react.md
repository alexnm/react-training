# Backend Integration
One missing piece from the entire React/Redux flow is related to server data and how we integrate APIs into our frontend application. React nor Redux have any standard way of introducing API calls into the workflow. Practices evolved in the community and opinions are still divided today.

## Native fetch
Before we start, let's a quick glimpse at the new `fetch API` which is implemented in modern day browsers. You can also use a [polyfill](https://github.com/github/fetch) to have support virtually everywhere.

There are several widely used libraries for making API calls: [superagent](https://github.com/visionmedia/superagent), [axios](https://github.com/axios/axios) or good old [jquery](https://jquery.com/), but **fetch** is good enough for most of your use cases and doesn't require any additional code (except for the polyfill which at some point would be removed)

Fetch is promise based and integrates nicely with newer syntax, including async/await.

A few examples of usage:
```javascript
// a GET request, response is serialized as JSON in the last then()
fetch(url).then(res => res.json()).then( /* ... */ ) 

// a POST is done also via the same function, just be setting the right headers/method
fetch(url, { method: "POST", headers: [...]}).then(res => res.json()).then( /* ... */ ) 
```

The simplest way of working with backend services may be simply to call the endpoints from the React components, for example from `componentDidMount`.

## Async Redux Actions
If we want toto integrate async data into the Redux store, one option is to imagine the entire flow with **actions**. let's consider that we want to fetch a book from an endpoint. The action could be called `FETCH_BOOK`. But when is this action dispatched? When we integrate an async call we have three possible moments: when the call is sent, when the response is successful, or when we have a failure. The common practice is to define the three moments as Redux actions: `FETCH_BOOK`, `FETCH_BOOK_COMPLETED`, `FETCH_BOOK_FAILED`. They would look like this:
```javascript

```

## redux-thunk

**References**
* [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

## Future References
* Server render
* CSS in JS
* Async Rendering
* GraphQL
* Flow/TypeScript
