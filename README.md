# React

#### To be able to access variables in other Javascript files
```javascript
//Take note that React is a variable from the react library
//For library name please refer to package.json
import React from 'react';
import ReactDOM from 'react-dom';
```

#### **Component** is used to generate HTML. To render this we have to attach it to the DOM
```javascript

```

#### **JSX** allows us to write what looks like HTML tags in Javascript
```javascript
const App = function() {
  return <div>Hi</div>
}
```

#### **JSX** code gets transpiled by Babel to normal Javascript. Try https://babeljs.io/repl/
```javascript
"use strict";

var App = function App() {
  return React.createElement(
    "div",
    null,
    "Hi"
  );
};
```
