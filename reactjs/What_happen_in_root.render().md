# What happened in root.render() function?

## Overview

When we are using reacts the first code snippet we see majority is the `index.js`

```js
import * as React from "react";
import { createRoot } from "react-dom";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

const root = createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

In here we can see it use `createRoot` to generate a `root` and then use `root.render` to render the code we wrote. But what happened  in `root.render`? In this article, we will explore its implementation.

## createRoot

Before we go through `root.render` we should know what happened in `createRoot` function call and how does it mount a render function into root itself.

ReactDOM.js

```js
function createRoot(
  container: Element | DocumentFragment,
  options?: CreateRootOptions
): RootType {
  return createRootImpl(container, options);
}

```

ReactDOMRoot.js

```js
export function createRoot(
  container: Element | DocumentFragment,
  options?: CreateRootOptions
): RootType {
  ...
  return new ReactDOMRoot(root);
}
```

In the above two files we can find `createRoot` will return a `ReactDOMRoot` class object. Then what is the `ReactDOMRoot` class?

```js
function ReactDOMRoot(internalRoot: FiberRoot) {
  this._internalRoot = internalRoot;
}
```

We can see the `ReactDOMRoot` class constructor function receive a `FiberRoot` as parameter and mount it into the `_internalRoot`. 

The `render` function is mounted on the prototype of  `ReactDOMRoot`

```js
ReactDOMRoot.prototype.render =
  function (children: ReactNodeList): void {
    const root = this._internalRoot;
    if (root === null) {
      throw new Error("Cannot update an unmounted root.");
    }
    updateContainer(children, root, null, null);
  };
```

## render

