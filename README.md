# React

#### To be able to access variables in other Javascript files
```javascript
//Take note that React is a variable from the react library
//For library name please refer to package.json
import React from 'react';
import ReactDOM from 'react-dom';
```

#### **Component** is used to generate HTML.
```javascript
//This is a class of a component not an instance
const App = () => {
  return <div>Hi</div>
}
//This is an instance
<App></App>
```

#### To render a component we have to attach it to the DOM
```javascript
ReactDOM.render(<App />, document.querySelector(".container"));
```

#### **JSX** allows us to write what looks like HTML tags in Javascript
```javascript
const App = () => {
  return <div>Hi</div>
}
```

#### **JSX** code gets transpiled by Babel to normal Javascript. Try https://babeljs.io/repl/
```javascript
"use strict";

var App = function App() {
  return React.createElement( //createElement creates an instance of the component class. i.e. div
    "div",
    null,
    "Hi"
  );
};
```

# NPM

#### To install new packages and include in package.json
`npm install --save youtube-api-search`
