# React
* Focus on component based code
* Requires webpack
* Call super() in the component constructor
* use [es6](https://babeljs.io/blog/2015/06/07/react-on-es6-plus) - ignore everything else

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

* validators are: `React.PropTypes.array`, `..bool`, `..func`, `..object`, `..number`, `..string`, `..symbol`
  - `..node` - anything that can be rendered
  - `..element` - react element
  - `..arrayOf(type)` - array containing elements of the type specified
  - `..instanceOf` - uses JS instanceOf operator
  - `..oneOf(enum_of_types)` - specify an enum of types that are supported
  - `..oneOfType([types])` - array of types that the object could be
  - `..objectOf(type)` - object of a specific type
  - `..shape({ prop1, prop2... })` - an object taking a specific shape

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
* the components below the root dont get access automatically to a context, they must specify the items they are interested in using the **contextTypes** object
* not great for domain related models, they couple your code to the domain
* Some use cases include:
  - current user model
  - event bus
  - flux data store
  - session storage

## Component Spec + Lifecycle methods
* `render()` - required method that should return a single child element
  - returning **null** or **false** will not render anything
  - this function should be **pure**
* `getDefaultProps()` - invoked once and cached when the class is created
  - values in the mapping will be set on `this.props` if the prop i snot specified by the parent component
* **propTypes** - allows you to validate props being passed to your components
  - can be validated by using the `React.PropTypes`
* **statics** - the statics object allows you to define static methods that can be called on the component
  - methods defined here do not have access to props or states, pass them in as args
* **componentWillMount** - invoked on client and server before the initial rendering occurs
* **componentDidMount** - invoked once on the client after the initial rendering
  - you can access any refs to your children (to access underlying DOM)
  - children's componentDidMount is executed before the parent
  - good for AJAX request, settings timers, integrating other frameworks
* **componentWillReceiveProps** - invoked when a component is receive new props, not called for initial render
  - props have not changed yet at this point
  - allows you to react to a prop transition before render is called by updating the state
  - the **nextProps** are passed as and argument
* `componentWillUpdate()` - invoked immediately before rendering when new props or state are being received
  - you cannot update this.setState in here
* `componentDidUpdate()` - invoked after the components updates are flushed to the DOM
* `componentWillUnmount()` - invoked before a component is unmounted
  - good place to undo what was done in **componentDidMount**
* `shouldComponentUpdate()` - invoked before rendering when new props or state are being received
  - you can force a component not to update by returning false here
  - nextProps and nextState are passed as arguments
* `constructor()`
  - Setup your state object in the constructor, the value you assign to `this.state` will be used as the initial state - this replaces the **getInitialState** function
  - Bind event handlers in the constructor
    `this.tick = this.tick.bind(this)`

## Flux
### General
* A pattern for building react frameworks
* Components fire actions or listen to stores (collections/services of data)
  - update when a store updates
  - components listen stores for updates to information
    * components can query a store for data
  - actions pipe data to a dispatcher

### Stores
* Fat models, containing all the data and application logic for a domain
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
* Only knows there is a callback it has call if an event occurs
* Events should be in all caps "NEW_EVENT"
* flux has a dispatcher which can be used
  `import { Dispatcher } from "flux"`
* register() - register a new register
  - make sure to bind the store as this context
  `dispatcher.regsiter(myStore.handleActions.bind(myStore))`
* dispatch() - dispatch an action
  `dispatch({type: 'MY_EVENT', ... params});`

### Actions
* The entry point to the system for anything that needs to enter with the system (User input, api interactions)
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
* `waitFor()` used to sequence updates and allow for the creation of a hierarchy of stores

### Flux utils
Utility classes to help make flux easier.
Comes with 4 basic classes that can be imported from `flux/utils`

**Store** - cache data and expose public getters to provide access, they should respond to actions from the dispatcher and emit a change when their data changes
  - `.constructor(dispatcher)`: construct the store and register an instance with the given dispatcher
  - `.addListener(cb)`: adds a listener to the store to listen for the change event, a token is returned that can be used to remove the listener
**ReduceStore** -
  - **getInitialState**: constructs the initial state for this store
  - `reduce(state, action)`: reduces the current state and and action to the new state of this store. all subclasses must implement this method.
**MapStore** -
**Container** - React components that control a view, primarily to gather information from stores and save it in their state, they should have no props or UI logic
  - views should be controlled by a container, they contain UI and rendering logic and receive all information and callbacks as props


### Flux package - npm
* [Flux](https://www.npmjs.com/package/flux)

### Links
* [React w/ Flux](http://reactkungfu.com/2015/07/react-with-flux-by-example-simple-todo-list-dissected/)
* [scotch.io - flux](https://scotch.io/tutorials/build-a-react-flux-app-with-user-authentication)
* [Flux pattern](https://tonyspiro.com/building-a-simple-react-application-using-the-flux-pattern)
* [SurviveJS - webpack / react](http://survivejs.com/webpack/advanced-techniques/configuring-react/)

## Redux
### General
* A predictable state container for JS apps, providing:
  - a place to store application state (all the data of your application)
  - a mechanism to dispatch actions to modifiers of your applications state (reducers)
  - a mechanism to subscribe to state updates
* the redux instance is called a store and can be created:
  `import { createStore } from 'redux'
   const store = createStore(function(){})
   store.dispatch({type: SOME_ACTION })
   // or using an action creator
   someActionCreator = (val) => {type; 'SOME_ACTION', value: val}
   store.dispatch(someActionCreator('some_value'))`
  - `.createStore(reducerFunction)` expects a function that will reduce your state
  - `.combineReducers({ someSliceOfState: reducer ...})` combines different reducers, it takes a hash and returns a function, the function manages only one part of the total application state
  - `.getState()` returns the current state of the application
  - `.applyMiddleware(middlewares...) => function` lets reduce know of the middleware we will be using
    * the resulting function should be used with createStore to apply the middleware to the stores dispatch
  - `.subscribe(function(){...})` registers a callback to the state changes for the store

* [React redux](https://github.com/rackt/react-redux) simplifies binding redux to a react context


* Action creators -> Action -> Dispatcher -> Store -> Events -> Views
* **Action creators**: pure JS functions used to create an action
  `const action = () => {type: 'ACTION', ...}`
  - Action creators may also return a function
* **Actions**: The action is a JS object that contains a *type* property, which can be used for handling the action. Any additional data can also be passed along with the action
  - actions can inform us that something has happenend or that data needs to be updated
* **Dispatching**: sends the action to the parts of the application it applies to
  - handlers register with the dispatch function to be notified when an action is dispatched
  - Redux dispatches a *INIT* action to initialize the state of the application, the state initializes to `undefined`
    * using ES6 default params we can define a reducer with a default state `reducer(state={}, action)`
  - when an action is dispatched, each registered reducer is called with the state and the action
  - when dispatching asynchronous actions, return a function instead and pass the dispatch function into the action so it can call dispatch when it has completed execution
    * use middleware to ensure the function executes correctly
* **Reducers**: A subscriber to actions
  - *stateless* stores that receive the state each time they are called
  - a function that receives the current state of your application + an action, and returns a modified (reduced) state
    * Reducer(state, action) -> newState
  - when a reducer is called it receives 2 parameters `(state, action)`
  - reducers are passed to redux.createStore as action handlers  
  - there are no limits on the number of reducers we might have
* **Middleware**: functions that execute between parts of the application execution
  - Use middleware to help with dispatching async actions
  - `const someMiddleware = ({ dispatch, getState }) => {
      return function(next){
        return function(action){
          // middleware specific code here
        }
      }
    }`
  - [thunk middleware](https://github.com/gaearon/redux-thunk) is used for building async actions


## Helpers
* react-html-attrs - transpiles class attributes to be className

## Plugins
* `DefinePlugin()` - implements a regex that searches our source and replaces variables defiend in a key(name of variable)-value(name in the source code) object
  - by convention surround the replaced variables with 2 underscores either side ie NODE_ENV => __NODE_ENV__

## Basic setup
* [SurviveJS setup](http://survivejs.com/webpack/advanced-techniques/configuring-react/)
* react modules **npm install -S react react-dom babel-preset-react babel-preset-es2015 babel-loader babel-core react-router**
* testing: **npm install -D enzyme mocha karma**
* webpack: **npm install -D webpack-dev-server webpack react-hot-loader**

## Testing
### Enzyme
Wraps around react shallowrender to give a jquery like wrapper around the resulting tree
We can assert on events and state transitions
- mount: full dom rendering
- render: html rendering

## Links
* [*"Official"* react starter - facebook](http://github.com/facebookincubator/create-react-app)
* [MERN](http://mern.io/) - mongo, express, react, node
* [Communication between components without flux](http://andrewhfarmer.com/component-communication/)
* [Server side rendering + express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/#maintenance)
* [React + node](http://blog.yld.io/2015/06/10/getting-started-with-react-and-node-js/)
* [isomorphic js - react + node + flux](http://stefunk.github.io/2015/01/29/isormophic-javascript-blog-react-nodejs.html)
* [Redux tutorial](https://github.com/happypoulp/redux-tutorial.git)
* [Redux dev tools](https://github.com/gaearon/redux-devtools)
* [Redux thunk middleware](https://github.com/gaearon/redux-thunk)
* [React redux](https://github.com/rackt/react-redux)
* [Redux offline docs](https://github.com/paulkogel/redux-offline-docs)
