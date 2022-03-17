# Intro to Vue3

### Creating a Vue App

in a main.js file

```javascript
const app = Vue.createApp({});
```

Use an argument to pass in an object and add a data property. It is a function that returns another object, were you store your data.

```javascript
const app = Vue.createApp({
  data() {
    return {
      product: 'Apples',
    };
  },
});
```

### Import Vue App into the index.html file:

```javascript
<script src="./main.js"></script>
```

### Mount Vue App into the DOM:

```javascript
<script>const mountedApp = app.mount('#app')</script>
```

### Display the data:

```javascript
<div id="app">
  <h1>{{ product }}</h1>
</div>
```

# Vue Instances

The heart of a Vue App, is when the options object is passed in, and allows adding optional properties to configure the application.

### Vue uses double curly brace syntax (mustache syntax) to inject regular javascript into the HTML.

# Attribute Binding

To create a bond between HTML element and a value from the Vue app's data, you use a **Vue Directive** called _v-bind_

- Dynamically binds an attribute to an expression

```javascript
<img v-bind:src='image'>
```

- Shorthand:

```javascript
<img :src='image'>
```

# Conditional Rendering

This is how to display different HTML elements based upon a condition. Example:

main.js

```javascript
const app = Vue.createApp({
  data() {
    return {
      product: 'Apples',
      inventory: 100,
    };
  },
});
```

### The v-if directive with Chained Conditional Logic

add the v-if directive onto an element to render it based upon a condition.

index.html

```javascript
<p v-if="inventory > 10">In Stock</p>
<p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
<p v-else>Out of Stock</p>
```

### Show and Hide

The **v-show directive** is used for toggling an elements **visibility** instead of adding and removing the element from the DOM.

# List Rendering

To render an HTML list from an array of data, you can use the **v-for directive**

Think of it as a **For Loop** Example:

main.js

```javascript
const app = Vue.createApp({
    data() {
        return {
            ...
            kinds: ['Golden Delicious', 'Granny Smith', 'Fuji']
        }
    }
})
```

Create an unordered list in index.html, then add the **v-for** in the list item:

```javascript
<ul>
  <li v-for="kind in kinds">{{ kind }}</li>
</ul>
```

How this works:
Inside the **v-for** expression, we used _kind in kinds_. Here, the _kinds_ refers to the _kinds_ array in the data, and _kind_ is the alias for the current element from the array, and it loops through to print it out in a new **li**.

Each **li** will display that array element because the inner HTML is written in the expression: {{ kind }} to print each one.

## Important: add a key attribute, it is essential for list items that are an object inside of an array. Example:

main.js

```javascript
data() {
  return {
    ...
    kinds: ['Golden Delicious', 'Granny Smith', 'Fuji'],
    variants: [
      { id: 1, color: 'yellow'},
      { id: 2, color: 'green'},
      { id: 3, color: 'red green'},
    ]
  }
}
```

index.html

```javascript
<div v-for='variant in variants' :key='variant.id'>{{ variant.color }}</div>
```

Using dot notation to print out each _variant_ as it loops through the _variants_ array, then used the **v-bind** shorthand to bind the variant's id to the key attribute. This gives each DOM element a unique key so Vue does not lose track if it as the app updates.

# Event Handling

index.html

```javascript
<div class='cart'>Cart({{ cart }})</div>
...
<button class='button'>Add To Cart</button>
```

main.js

```javascript
data() {
  return {
    cart: 0,
    ...
  }
}
```

## Listening for Events

To know when a button is clicked, use another **Vue Directive** called **v-on**

```javascript
<button class="button" v-on:click="logic to run">
  Add to cart
</button>
```

The **v-on** is listening for a _click_ event. Inside the quotes add logic or a method name to run when that event happens.

index.html

```javascript
<button class='button' v-on:click='addToCart'>Add to cart</button>
<button class='button' v-on:click='removeFromCart'>Remove from cart</button>
```

main.js

```javascript
const app = Vue.createApp({
  data() {
    return {
      cart: 0
      ...
    }
  },
  methods: {
    addToCart() {
      this.cart += 1
    },
    removeFromCart() {
      if (this.cart >= 1 {
        this.cart -= 1
      })
    }
  }
})
```

In the methods option, and inside the addToCart and removeFromCart methods contain the logic for the on click event listener. this.cart refers to _this_ cart in _this_ Vue instance's data.

using the **v-on** added to an element, when a click happens, the addToCart and removeFromCart methods run when the buttons are clicked.

### Shorthand for **v-on**

**v-on** can be shortened to the **@** symbol:

```javascript
<button class='button' @click='addToCart'>Add to cart</button>
```
