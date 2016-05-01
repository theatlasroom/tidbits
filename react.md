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

## Data
* Data is managed by state, props or context
* State is available through this.state, defaults to null
  - You can set state in a constructor, dont do it anywhere else
  - State only should be used when a component has a internal value that only effects that component nothing else
  - when state changes on a component, the component is updated and re-rendered
  - change state using this.setState({});
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

## Flux
* A pattern for building react frameworks
* Components fire actions or listen to stores (collections/services of data)
  - update when a store updates
  - components listen stores for updates to information
    * components can query a store for data
  - actions pipe data to a dispatcher
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

## Helpers
* react-html-attrs - transpiles class attributes to be className
