# VueJS

## Testing

### Vue testing utils

- Allows for testing components in isolation by providing tools for _mounting_, _mocking_ and _asserting_ outputs
- Mounted components are returend inside a wrapper

#### Mounting

#### Selectors

- Any valid CSS selector can be used
- Vue components can be used as selectors
- The vue option object can be used to select by name

```javascript
// find by the name of the component
const buttonWrapper = wrapper.find({ name: "my-button" });
buttonWrapper.trigger("click");

// find by ref
const buttonWrapper = wrapper.find({ ref: "myButton" });
buttonWrapper.trigger("click");
```

#### Wrapper

- `vm` - the vue instance provides access to all the instances methods and properties of a vm
- `element` - the root DOM node of the wrapper
- `options`
  - _attachedToDocument_ - true if the component is attached to document when rendered
  - _sync_
- `.attributes(key)` - returns the value of DOM node attributes for the wrapper, if no key is specified all attributes are returend
  - returns `string | { [attribute]: value }`
- `.classes(name)` - returns an array of classnames, if a name is provided it returns a boolean if the class exists
- `.contains(selector)` - assert if a wrapper contains an element or component that matches a given selector
- `.destroy()` - destroy a vue component instance
  - if `attachToDocument` was set to true when mounted, the component DOM elements will also be removed from the document.
- `.emitted()` - returns an object with custom events emitted by the wrapper
  - the arguments to each invocation are added to the array for the relevant function in the emitted array

```javascript

console.log(wrapper.emitted())
=>
{
  // method, [first invocation, second invocation]
  foo: [[], [123]]
}

```

- `.emittedByOrder(function)` - returns an array of invocations of a method

```javascript
console.log(wrapper.emittedByOrder())
=>
[
  ({ name: "foo", args: [] }, { name: "bar", args: [123] })
];
```

- `.exists()` - assert existence of a wrapper or element
- `.find(selector)` - search for a the first DOM node or vue component matching the [selectors](#selectors)
- `.findAll(selector)` - returns an array of all nodes / components matching the given selector
- `.html()` - returns the rendered html
- `.is()` - assert the DOM node or vm matches the selector
- `.isEmpty()` - assert it cointains no child nodes
- `.isVisible()` - returns false if an ancestor of the node has `display: none` or `visibility: hidden`
- `.isVueInstance()`
- `.name()` - returns the name of a vue instance or the DOM node
- `.props(key)` - returns the props object, or the value of the prop if a key is provided
- `.setChecked()` - set the checked value of an input element of type checkbox or radio and update the v-model bound data
- `.setData(object)` - recursively calls `Vue.set` with each key value pair given
- `.setMethods({ method: stub / mock })` - sets methods and forces update
- `.setProps(object)` - set props
- `.setSelected()` - select an option and update the v-model bound data
- `.setValue(...)` - sets the text value of an input or select box and updates v-model data
- `.text()` - returns the text contents of a DOM node or element
- `.trigger(options)` - trigger an event on the wrapper, the options passed in are added to the Event

#### Examples

```javascript
// Assertions
expect(wrapper.attributes("id")).toBe("foo");
expect(wrapper.classes("bar")).toBe(true);
expect(wrapper.contains("p")).toBe(true);
expect(wrapper.exists()).toBe(true);
expect(wrapper.is("div")).toBe(true);

// assert event count
expect(wrapper.emitted().foo.length).toBe(2);

// assert event has been emitted
expect(wrapper.emitted().foo).toBeTruthy();

// assert event payload
expect(wrapper.emitted().foo[1]).toEqual([123]);
expect(wrapper.emitted("foo")[1]).toEqual([123]);

// set props
const wrapper = mount(Foo, { propsData: { foo: "bar" } });
// OR
const wrapper = mount(Foo);
wrapper.setProps({ foo: "bar" });
expect(wrapper.vm.foo).toBe("bar");

// Stub a method
const clickMethodStub = sinon.stub();
wrapper.setMethods({ clickMethod: clickMethodStub });
wrapper.find("button").trigger("click");
expect(clickMethodStub.called).toBe(true);

// Set a text box
const textInput = wrapper.find('input[type="text"]');
textInput.setValue("some value");

// Set option of a select box
const options = wrapper.find("select").findAll("option");
options.at(1).setSelected();
```

## i18n - Internationalization

## AST

- [AST Playground for vue](https://ast.js.org/#/plays/1)
- [vue-eslint-parser](https://github.com/mysticatea/vue-eslint-parser) - parser for the <template> section of .vue files

## Useful links

- [Testing guide](https://vue-test-utils.vuejs.org/guides/#getting-started)
- [Renderless components](https://adamwathan.me/renderless-components-in-vuejs/)
- [VueJS RFCs](https://github.com/vuejs/rfcs)
