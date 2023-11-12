Event Handling
==============

In this lesson, we’ll get into a very important aspect of building single page apps: _handling events_.

* * *

First, we’ll need some new elements to interact with.

Inside of our **App.vue** file, let’s add a new ref state `cart` in `<script>` and add a box right below the nav bar to show the cart state. This will display the number of items added to the shopping cart:

📃 **src/App.vue**

    const cart = ref(0)
    ...
    <div class="nav-bar"></div>
    <div class="cart">Cart({{ cart }})</div>
    

We also want a button so that we can add new items to the cart:

📃 **src/App.vue**

    <button class="button">Add to cart</button>
    

They look like this:

![cart_button.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1668108645485.jpg?alt=media&token=1e738b0c-4623-428c-a1dd-211d42ad471b)

To attach a `click` event to the button, we’ll use `v-on`:

📃 **src/App.vue**

    <button class="button" v-on:click="cart += 1">Add to cart</button>
    

Just like `v-bind`, the content inside the attribute value will be treated as JavaScript code. In this case, `cart += 1` means the cart state will get incremented.

Now when you click the button, the cart’s number will be updated:

![incremented.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F2.1668108645486.jpg?alt=media&token=87e081ea-4af6-4848-972e-1e3b7ad4e3de)

* * *

Optionally, you can add a function wrapper around the logic:

    <button class="button" v-on:click="(event) => cart += 1">Add to cart</button>
    

This is similar to how event handlers look like in React. But the function wrapper is optional.

So if you omit the function wrapper, it will get added for you automatically by the compiler:

    <button class="button" v-on:click="cart += 1">Add to cart</button>
    

If you don’t want too much logic in the template, you can also extract it to a function:

    const addToCart = () => cart.value += 1
    

(since we’re changing the `cart` ref inside `<script>`, we have to use `.value`.)

Then we’d use the function name in the template as the event handler:

    <button class="button" v-on:click="addToCart">Add to cart</button>
    

Just like `v-bind:` has the _colon_ as the shorthand syntax, `v-on:` can be replaced with the `@` sign:

    <button class="button" @click="addToCart">Add to cart</button>
    

* * *

Event Handling with Parameter
-----------------------------

Next, we want to add a mouseover event to the color names, so that the user can choose the color they want by hovering one these colors.

First, make sure you imported both the blue and the green images:

📃 **src/App.vue**

    import socksGreenImage from './assets/images/socks_green.jpeg'
    import socksBlueImage from './assets/images/socks_blue.jpeg'
    

And add both images to the variant array:

📃 **src/App.vue**

    const variants = ref([
      { id: 2234, color: 'green', image: socksGreenImage },
      { id: 2235, color: 'blue', image: socksBlueImage },
    ])
    

Now, let’s add the `mouseover` event to the variant element:

📃 **src/App.vue**

    <div 
      v-for="variant in variants" 
      key="variant.key"
      @mouseover="updateImage(variant.image)"
    >
      {{ variant.color }}
    </div>
    

When the event is triggered, we’ll pass the correct image to `updateImage`, which is a function we’ll create now:

📃 **src/App.vue**

    const updateImage = (variantImage) => {
      image.value = variantImage
    }
    

This function will take care of setting the correct image on the `image` ref.

Now, when we put the mouse on the color names, the image will get updated accordingly:

![mouseover.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F3.1668108650013.jpg?alt=media&token=4391a4d2-ad66-49db-8de5-5e956acd7641)

* * *

Event Modifiers
---------------

Because Vue.js is a framework, its event handling solution is much more feature-rich.

For instance, you can add modifiers to the event attribute:

`@click.once` means the event can be triggered only once on the same element.

`@click.prevent` is the Vue.js equivalent of using `event.preventDefault()`.

`@click.stop` will stop the event from propagating further up.

Modifiers are very useful when it comes to keyboard events such as keydown:

`@keydown:enter` will be triggered when the _Enter key_ is pressed.

You can check out the [Vue.js documentation](https://vuejs.org/guide/essentials/event-handling.html) to see the full list of modifiers you can use.

* * *

Up Next
-------

We’ve completed the _cycle of creating states, rendering them in the template using various tricks, and setting up events on the template to change the states_.

In the next and final lesson of this course, we’ll talk about the CSS-related features that you would need in a single page app project.

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L5-start)
    
*   [Ending Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L5-end)
