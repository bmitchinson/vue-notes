## Guide Notes

### [Intro](https://vuejs.org/v2/guide/)
#### Vue component properties:

`el:` Dom element selector. `#` corresponds to an element id.

`data:` Component data object. Can be altered straight from the console.

`methods:` A object of functions (can't be arrows?).

Directives `v-`: apply reactive behavior from component to dom

`v-bind`: binds component data to dom element property

`v-if`: renders the element if truthy

`v-for`: maps over an object
```
<li v-for="todo in todos">
  {{ todo.text }}
</li>
```

#### `v-on`: attaches event listeners
```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

`v-model`: makes two way binding stupid easy.
Ex: input box alters p text:
```
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vu!'
  }
})
```

#### Component organization and templating
" In Vue, a component is essentially a Vue instance with pre-defined options. "

```
// Define a new component called todo-item
Vue.component('todo-item', {
  template: '<li>This is a todo</li>'
})
```

but using the binding directives you can create dynamic components with props like
so:
```
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```

```
<div id="app-7">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```

### [The Vue Instance](https://vuejs.org/v2/guide/instance.html)

- "all Vue components are also Vue instances, and so accept the same options object (except for a few root-specific options)."
- "When a Vue instance is created, it adds all the properties found in its data object to Vue’s reactivity system. When the values of those properties change, the view will react, updating to match the new values."
  - (it seems like data is almost like state. It can be altered directly from 
  outside the component with an instance reference)
- The only data properties that will be reative are those defined on instantiation

#### Some basic instance properties and methods are exposed
[Full list](https://vuejs.org/v2/api/#Instance-Properties)

They're prefixed with $: `vm.$data`, `vm.$el`, 
`vm.$watch('a', function(){...})`

(watch assigns a callback function to anychange of `vm.a`. Again, you can't 
use arrow functions due to their anonymity)

#### Instance Lifecycle Hooks
There's `created`, `mounted`, `updated`, `destroyed`. None of them can
be anon!


