# Backend Integration
One missing piece from the entire React/Redux flow is related to server data and how we integrate APIs into our frontend application. Neither React nor Redux have any standard way of introducing API calls into the workflow. Practices evolved in the community and opinions are still divided today.

## Native fetch
Before we start, let's a quick glimpse at the new `fetch API` which is implemented in modern day browsers. You can also use a [polyfill](https://github.com/github/fetch) to have support virtually everywhere.

There are several widely used libraries for making API calls: [superagent](https://github.com/visionmedia/superagent), [axios](https://github.com/axios/axios) or good old [jquery](https://jquery.com/), but **fetch** is good enough for most of your use cases and doesn't require any additional code (except for the polyfill which at some point would be removed)

Fetch is promise based and integrates nicely with newer syntax, including async/await.

A few examples of usage:
```javascript
// a GET request, response is serialized as JSON in the last then()
fetch(url).then(res => res.json()).then( /* ... */ ) 

// a POST is done also via the same function, just by setting the right headers/method
fetch(url, { method: "POST", headers: [...]}).then(res => res.json()).then( /* ... */ ) 
```

The simplest way of working with backend services may be simply to call the endpoints from the React components, for example from `componentDidMount`.

## Async Redux Actions
If we want to integrate async data into the Redux store, one option is to imagine the entire flow with **actions**. let's consider that we want to fetch a book from an endpoint. The action could be called `FETCH_BOOK`. But when is this action dispatched? We have three moments in an async call: when the call is sent, when the response is back and is successful, or when we have a failure. The common practice is to define the three moments as Redux actions: `FETCH_BOOK`, `FETCH_BOOK_COMPLETED`, `FETCH_BOOK_FAILED`. They would look like this:
```javascript
export const fetchBook = () => ({
    type: "FETCH_BOOK",
});

export const fetchBookCompleted = book => ({
    type: "FETCH_BOOK_COMPLETED",
    payload: {
        book: book,
    },
});

export const fetchBookFailed = err => ({
    type: "FETCH_BOOK_FAILED",
    payload: {
        err: err,
    },
});
```

Here's the [codesandbox example](https://codesandbox.io/s/ppkmw39yz7)

## redux-thunk
Fetching the data inside the component is fine, but in this case we are also managing the dispatches from the component and this tends to become repetitive. It would be nice if we could just dispatch a single action and let redux do its magic.

**redux-thunk** can help with that! This is a very simple middleware, but a very powerful one. It allows you to dispatch a function instead of an object. That function will always receive the `dispatch` reference as the first parameter. So when writing a `thunk`, we actually write an **action creator** which dispatches one or more simple actions.

Here's a quick example:
```javascript
const fetchBook = url => dispatch => {
    dispatch(fetchBookStarted());
    fetch(url)
        .then(res => res.json())
        .then(
            res => dispatch(fetchBookCompleted(res)),
            err => dispatch(fetchBookFailed(err))
        );
};
```

and the full [sandbox example](https://codesandbox.io/s/739x3z0w20).

Other alternatives for handling multiple dispatches for a single action are: redux-saga, redux-observables.

**References**
* [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
* [redux-thunk](https://github.com/reduxjs/redux-thunk)

## Future References
* Server render
* CSS in JS
* Async Rendering
* GraphQL
* Flow/TypeScript
