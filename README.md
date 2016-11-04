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

#### To export component so that others maybe import
```javascript
export default SearchBar;
```

#### Difference between library imports and imports from personal files
```javascript
//Library are namespaced there will be only one copy of react in the node_modules folder that we installed to
import React from 'react';
import ReactDOM from 'react-dom';

//There may be dozens of search_bar.js in our folders hence we have to specify the relative path from which its being imported i.e. index.js
import SearchBar from './components/search_bar'
```

#### Functional component vs Class based component
```javascript
//functional component
import React from 'react';

const SearchBar = () => {
  return <input />;
}
```

```javascript
//class based component
import React, {Component} from 'react'; //syntatic sugar for const Component = React.Component

class SearchBar extends Component {
  //this is a method, notice there is no : after render?
  render() {
    return <input/>
  }
}
```

#### Handling events
```javascript
class SearchBar extends Component {
  //this is a method, notice there is no : after render?
  render() {
    return <input onChange={this.onInputChange}/>
  }
  onInputChange(event) {
    console.log(event.target.value)
  }
}
```


# NPM

#### To install new packages and include in package.json
`npm install --save youtube-api-search`
