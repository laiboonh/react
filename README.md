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
    //to reference a javascript variable inside JSX we put it in braces {}
    return <input onChange={this.onInputChange}/>
  }
  onInputChange(event) {
    console.log(event.target.value)
  }
}
```

### State
#### "State is a plain Javascript object used to record and react to user events. Each class based component has its own state object. If the state object changes, the component will be re-rendered."

#### Initialize state
```javascript
class SearchBar extends Component {
  constructor(props) {
    super(props);
    this.state = { term : '' };
  }
  ...
}
```
#### Setting state
```javascript
class SearchBar extends Component {
  constructor(props) {
    super(props);
    this.state = { term : '' }; //this should be the only place where we use this.state=
  }
  render() {
    //use this.setState to change state -- good functional programming immutability practice
    return (
      <div>
        <input onChange={event => this.setState({term : event.target.value})}/>
        //to reference a javascript variable inside JSX we put it in braces {}
        Value of the input : {this.state.term}
      </div>
    );
  }
}
```

#### Controlled field is a form element whereby the value is set by the state and not the other way round
```javascript
class SearchBar extends Component {
  constructor(props) {
    super(props);
    this.state = { term : '' }; //this should be the only place where we use this.state=
  }
  render() {    
    return (
      <div>      
        <input onChange={event => this.setState({term : event.target.value})}/>
        //controlled field    
        <input value = {this.state.term} /> //declarative syntax another good functional programming practice
      </div>
    );
  }
}
```

#### "Downward data flow" - the common most parent component should be responsible for retrieving data
```javascript
//passing props from parent component to child component
//if the state changes, VideoList will be re-rendered with the new state
<VideoList videos={this.state.videos}/> //curly braces for referring to javascript variables within JSX
```

#### Applying styles to components
```javascript
const VideoList = (props) => {
  return (
    //notice we use className instead of class because class is a javascript keyword
    <ul className="col-md-4 list-group">
    </ul>
  );
}
```
# Redux
#### A Javascript object that contains the whole application state

### Reducers
#### A function that returns a piece of the application state
#### Note that state parameter is the part of the application state that it helped to produce in the first place.
#### Note that reducer will be called whenever an Action object is dispatched and passed into reducer via the action parameter.
```javascript
export default function(state, action) {
  return [
    {title : 'Javascript: The Good Parts'},
    {title : 'Harry Potter'},
    {title : 'The Dark Rower'},
    {title : 'Eloquent Ruby'}
  ];
}
```

### Container
#### A react "smart-component" that has a direct connection to the state managed by Redux
```javascript
import { connect } from 'react-redux';
//When application state changes, container will re-render
function mapStateToProps(state) {
  //Whatever is returned will show up as props in BookList
  return {
    books : state.books
  }
}
//connect is used to create a container (smart-component)
export default connect(mapStateToProps)(BookList);
```

#### An Action Creator is a function that returns an Action
#### To bind an Action Creator to a Container
```javascript
//Anything returned from this function will end up as props on the BookList container
function mapDispatchToProps(dispatch) {
  //Dispatch is in charged to passing Action to all Reducers.
  //When selectBook is called, the result (Action) should by passed to all Reducers via dispatch
  return bindActionCreators({ selectBook: selectBook }, dispatch);
}

//connect is used to create a container (smart-component)
export default connect(mapStateToProps, mapDispatchToProps)(BookList);
```

#### Action is a Javascript object that is automatically sent to ALL Reducers. Reducers can then choose to return a different piece of state depending on the Action. Because state changed, containers will re-render.
#### Consuming an Action in a Reducer
```javascript
export default function(state = null, action) {
  switch(action.type) {
    case 'BOOK_SELECTED' :
      return action.payload; //good functional practice to not mutate state, return fresh object
  }
  return state;
}
```

# ES6

#### If the key and value of an object are of the same variable name, we can condense it
```javascript
this.setState({ videos : videos });
//can be written as
this.setState({ videos });
```

#### If we simply want to work with a particular property from props
```javascript
const VideoListItem = (props) => {
  const video = props.video;
  return (
    <li className="list-group-item">Video</li>
  );
}
//can be condensed as
const VideoListItem = ({video}) => {
  return (
    <li className="list-group-item">Video</li>
  );
}
//if you want to access multiple properties
const VideoListItem = ({video, onVideoSelect}) => {
  return (
    <li className="list-group-item">Video</li>
  );
}
```

#### String interpolation
```javascript
const url = `https://www.youtube.com/embed/${videoId}`;
```

#### Handling undefined values
```javascript
//set state to null if its undefined
export default function(state = null, action) {
  ...
}
```

# Lodash

#### Throttling
```javascript
import _ from 'lodash';
//this function can only be called every 300ms
const videoSearch = _.debounce((term) => this.videoSearch(term),300);
```

# NPM

#### To install new packages and include in package.json
`npm install --save youtube-api-search`
