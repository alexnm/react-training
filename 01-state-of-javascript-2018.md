# The State of JavaScript

## ES2015 and beyond
JavaScript is no longer the scripting language used to add some minimal interractivity to static websites. It's a rich syntax language with vast capabilities and a lot of new features that were standardized in 2015 and beyond. The **TC-39** committee is working on the language standardization on an yearly basis, so each year we get new features into the standard language. Furthermore, current tooling (webpack, babel) allows us to work with proposals/experimental features and ensure that we have full browser support while using the latest syntax into our source code. In other words, the code that we write does not end up in the same form on the browser, but rather goes through a **transpile/compile** step which ensures the browser support we need.

**References**
* [ECMAScript2015/ES6 features](http://es6-features.org/#Constants)
* [Egghead course on ES2015](https://egghead.io/courses/learn-es6-ecmascript-2015)
* [ES Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
* [TC-39's github org](https://github.com/tc39/ecma262) - Proposals are actively developed here

## Async JavaScript
The JS execution model is fundamental to understand how the language works. The main difference to other programming languages is the non-blocking / asynchrounous nature of the function calls. This is done via the powerful **event loop** mechanism which is explained in the talk below. Adding on top of the event loop, modern JS is finding ways of avoiding callback hells and callbacks in general with the **Promise** model/pattern and with the newer syntax of **async/await**.

**References**
* [Understand the event loop](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
* [Promises](https://scotch.io/tutorials/javascript-promises-for-dummies)
* [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
* [Async/Await full tutorial](https://egghead.io/courses/asynchronous-javascript-with-async-await)

## Modules
Finally, JavaScript is no longer a single file program, nor does it require you to work with global variables to ensure communication between multiple files. Starting from the **require.js** syntax which is behind node's file system, ES2015 also brought us **ESModules**, a very powerful and flexible **import/export** sytax which allows us to work with external dependencies (npm modules) or with other files in our setup.

**References**
* [Modern JS for Dinosaurs](https://medium.com/@peterxjang/modern-javascript-explained-for-dinosaurs-f695e9747b70)
* [Understanding ES Modules](https://www.sitepoint.com/understanding-es6-modules/)
* [ES Modules Deep Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
