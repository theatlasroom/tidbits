# React
* Focus on component based code
* Requires webpack
* Call super() in the component constructor

## Components
* Everything in react is a component
* Components return 1 DOM element
* Everything has to have just 1 DOM element, to return multiple elements from a render function, wrap them in a div (or other block level element)
* `{}` encloses content that is executed as normal javascript
  - attributes can be accessed using the `this.attr` syntax
* Capitalise components because its best to think of them as a constructor
* For a component that has a component within it, create a new folder. ie if the header has any components, create a header folder and put them in there
* componentWillMount() fires the first time the component is rendered to the dom. Use it to add event listener
  `TodoStore.on('change', () => {})`
* use componentWillUnmount to avoid memory leaks, use it to unbind listeners
 `getTodos(){
  this.setState({
    todos: TodoStore.getAll
  });
 }

 componentWillMount(){
  TodoStore.on("change", this.getTodos);
 }

 componentWillUnmount(){
  TodoStore.removeListener("change", this.getTodos);
 }`
 - if you listen to any event, make sure to unmount it

## Data
* Data is managed by state, props or context
* State is available through this.state, defaults to null
  - You can set state in a constructor, dont do it anywhere else
  - State only should be used when a component has a internal value that only effects that component nothing else
  - when state changes on a component, the component is updated and re-rendered
  - change state using this.setState({});
  - state should be used for a components internal values, a value that only effects that component
* Props can be injected into any component component
  `<component property='somevalue' />`
  - props can be injected from an outer / parent component
* When passing a function, make sure to bind(this), so you bind the correct context
  `changeTitle(title){

  }
  .
  .
  .
  <component changeTitle={this.changtitle.bind(this)} title={this.props.title}
  `
* DOM events can be used as handlers, such as onChange, onClick, onBlur etc
  - When you bind a value, make sure to also setup a change listener so that you can update the value when a change is triggered

### Proptypes
`React.propTypes` contain a range of validators, to ensure the passed in data is valid
`MyComponent.propTypes = {
  name: React.PropTypes.string.isRequired,
  id: React.PropTypes.number,
}`

## Routing
* [React Router](https://github.com/reactjs/react-router)
  - Render a router to your DOM
  - Routes should be defined within the router
  - IndexRoute defines the default route to use
    `ReactDOM.render(
      <Router>
        <Route path="/" component={Component}>
          <IndexRoute component={Component-1}></IndexRoute>
          <Route path="/component-2" component={Component-2}></Route>
        </Route>
      </Router>,
    app);
    `
  - *Link* provides a shorthand for hyperlinks
    `<Link to="somepage">Page</Link>`
    * elements link buttons can be rendered within the Link tags too
    * activeClassName='value' can be used to test for the current active class
    * using the hashHistory package, we can also use history.isActive('value')
  - render *this.props.children* in the layout where we want the route content to appear
  - Params can be added directly to the path attr of a <Route />. The params are *injected using this.props.params*
  - Query params can also be used, the will be *injected into this.props.location.query*
  - Optional params are wrapped in parens
    `<Route path="/resource(:id)"></Route>`
  - To render multiple copies of a component, create an array of the components
  `Words = ["this", "is", "a", "word"].map((title, i) => <Word key={i} title={title} />)
  .
  .
  .
  return (
    <div>
      {Words}
    </div>
  )
  `
    * Every child needs a unique key prop
  - History attribute - specifies the style to use for the urls, use browserHistory for server style urls, and hashHistory for `#` style urls
## contextTypes
* mechanism for passing data around to components
* the components below the root dont get access automatically to a context, they must specify the items they are interested in using the `contextTypes` object
* not great for domain related models, they couple your code to the domain
* Some use cases include:
  - current user model
  - event bus
  - flux data store
  - session storage

## Lifecycle methods
* componentWillUpdate
* shouldComponentUpdate

## Flux
### General
* A pattern for building react frameworks
* Components fire actions or listen to stores (collections/services of data)
  - update when a store updates
  - components listen stores for updates to information
    * components can query a store for data
  - actions pipe data to a dispatcher

### Stores
* Used to hold business logic
* When a store changes, it should emit a change event
  `this.emit('change')`
* A store exports an object
  - import EventEmitter from 'events' (standard js)
  - Your store should extend the EventEmitter
  `class TodoStore extends EventEmitter {
    constructor(){
      super()
    }
  }
  const todoStore = new TodoStore;
  export default todoStore;
  `
* The store should only respond to the events that it cares about

### Dispatcher
* Used to notify our store of actions
* Events should be in all caps "NEW_EVENT"
* flux has a dispatcher which can be used
  `import { Dispatcher } from "flux"`
* register() - register a new register
  - make sure to bind the store as this context
  `dispatcher.regsiter(myStore.handleActions.bind(myStore))`
* dispatch() - dispatch an action
  `dispatch({type: 'MY_EVENT', ... params});`

### Actions
* Should be housed in a seperate file for each store
  `export function createTodo(text){
    dispatcher.dispatch({    
      type: "CREATE_TODO",
      text
    });
  }
  `
* The component then fires the necessary actions when a DOM Event occurs
* For async actions, send out multiple events at different times
  - ie: BEGIN_FETCH_TODOS, RECEIVED_TODOS, FETCH_ERRORS
* the store should listen for the events and emit a change where needed

## Redux


## Helpers
* react-html-attrs - transpiles class attributes to be className

## Plugins
* `DefinePlugin()` - implements a regex that searches our source and replaces variables defiend in a key(name of variable)-value(name in the source code) object
  - by convention surround the replaced variables with 2 underscores either side ie NODE_ENV => __NODE_ENV__

## Basic setup
* [SurviveJS setup](http://survivejs.com/webpack/advanced-techniques/configuring-react/)
* react modules `npm install -S react react-dom babel-preset-react babel-preset-es2015 babel-loader babel-core react-router`
* testing: `npm install -D enzyme mocha karma`
* webpack: `npm install -D webpack-dev-server webpack react-hot-loader`

## Links
* [MERN](http://mern.io/) - mongo, express, react, node
* [Server side rendering + express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/#maintenance)
* [React + node](http://blog.yld.io/2015/06/10/getting-started-with-react-and-node-js/)
* [isomorphic js - react + node + flux](http://stefunk.github.io/2015/01/29/isormophic-javascript-blog-react-nodejs.html)
