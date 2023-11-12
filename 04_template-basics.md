Template Basics
===============

In this lesson, we’ll go through the most common operations you would use in the `<template>`.

*   Attribute Binding
*   Conditional Rendering
*   List Rendering
*   List Rendering with Conditional

* * *

Setting up the layout
---------------------

But first, we have to set up some basic layout for the page:

📃 **src/App.vue**

    <template>
      <div class="nav"></div>
      <div class="product-display">
        <div class="product-container">
          <div class="product-image">
          </div>
          <div class="product-info">
            <h1>{{ product }}</h1>
          </div>
        </div>
      </div>
    </template>
    

The class names are used for connecting to the CSS in **main.css**.

Now it looks like this in the browser:

![browser.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1668107515241.jpg?alt=media&token=c3134291-ca18-4f09-8cfd-c26464e75fb9)

* * *

Attribute Binding
-----------------

We want to put an image in this container:

📃 **src/App.vue**

    <div class="product-image">
    </div>
    

It will appear in here:

![product-image.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F2.1668107515242.jpg?alt=media&token=dc654e15-f312-45bf-8c65-76c0cf6ad1ca)

Remember we have some images that we downloaded back in Lesson 2?

We’re going to import and use one of them:

📃 **src/App.vue**

    import socksGreenImage from './assets/images/socks_green.jpeg'
    
    ...
    <div class="product-image">
      <img v-bind:src="socksGreenImage">
    </div>
    

We’re importing the image directly from the image path. This import syntax is supported out of the box.

And we’re binding the image path to the image element using `v-bind:src`.

You can think of `v-bind` as a special syntax for creating a bond between the `src` attribute and the JavaScript variable `socksGreenImage`.

The content inside the attribute value for `v-bind:src` will be treated as a JavaScript expression. In this case, it’s the variable `socksGreenImage`. Having JavaScript code embedded in an attribute like this is a common theme in Vue.js.

Aside from `src`, this `v-bind` directive can be applied on other attributes, such as `class` and `style`. We’ll see how that works in a future lesson.

If you check browser, you should see a basic two-column layout is coming along:

![layout.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F3.1668107521203.jpg?alt=media&token=33cd4834-96f0-4977-b96f-f1568eaaa3fc)

We’ve used the double curly braces in the previous lesson. The `v-bind` directive is like the double curly braces, but for attributes.

But since `socksGreenImage` is not a reactive variable, it’s never going to change, so this binding is not very interesting.

We can make the image path reactive like this:

📃 **src/App.vue**

    const image = ref(socksGreenImage)
    ...
    <img v-bind:src="image">
    

We’re passing the `socksGreenImage` variable through `ref()` to get a new state.

Now, if we change the `value` of the `image` ref to another path, the `<img>` element will get updated accordingly.

Alternatively, `v-bind:` can be written with just the _colon_ as a shorthand syntax.

    <img :src="image">
    

* * *

Conditional Rendering
---------------------

Now, let’s talk about using conditional logic in `<template>`.

Here, we have a new ref called `inStock`:

📃 **src/App.vue**

    const inStock = ref(true)
    

And we can use `inStock` to conditionally render “In Stock” and “Out of Stock”:

📃 **src/App.vue**

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
    </div>
    

`v-if` and `v-else` have to be used on elements right next to each other. Just like with `v-bind`, the attribute value of `v-if` will be interpreted as JavaScript code.

* * *

Unsurprisingly, `v-if` can be used alone all by itself:

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock</p>
    </div>
    

There is another conditional directive called `v-show`:

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-show="inStock">In Stock</p>
    </div>
    

It’s similar to `v-if`, but `v-show` will still render the element but just hide it using `display: none;`. This means it’s a more performant option and is a good choice for pieces of a template that you know will need to appear/disappear very frequently.

* * *

Chaining Conditional Logic
--------------------------

We can also use `v-else-if` along with `v-if` and `v-else`.

For example, if we change `inStock` to inventory:

    const inventory = ref(8)
    

We can use this number ref to conditionally render one of the three different elements:

    <div class="product-info">
      ...
      <p v-if="inventory > 10">In Stock</p>
      <p v-else-if="inventory <= 10 && inventory > 0">Out of Stock</p>
      <p v-else>Out of Stock</p>
    </div>
    

Now that we’ve learned _conditional rendering_, let’s move on to _rendering a list of items_.

* * *

List Rendering
--------------

Let’s first create an array `ref`:

📃 **src/App.vue**

    const details = ref(['50% cotton', '30% wool', '20% polyester'])
    

In the template, we can render the array in a `<ul>` using `v-for`:

📃 **src/App.vue**

    <div class="product-info">
      ...
      <ul>
        <li v-for="detail in details">{{ detail }}</li>
      </ul>
    </div>
    

The list should show up like this:

![list-1.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F4.1668107523651.jpg?alt=media&token=0ffdbacc-d649-42cd-a6e7-65a11f085717)

* * *

As long as your data is iterable, `v-for` will be able to work with it.

In our case, we’re using the array value from the `details` ref:

    <li v-for="detail in details">{{ detail }}</li>
    

And the variable `detail` is created on each iteration to represent each item in the array.

You can think of `v-for` as a conveyor belt. It takes each item from the array and render them one by one.

![Screen Shot 2022-09-28 at 9.57.40 AM.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F5.1668107527783.jpg?alt=media&token=6b5e3d10-a660-4bff-ac9b-8f634b21b379)

* * *

Next, let’s create an array of objects and use `v-for` on it:

📃 **src/App.vue**

    const variants = ref([
      { id: 2234, color: 'green' },
      { id: 2235, color: 'blue' },
    ])
    

We don’t have to always use `v-for` with `<li>`, we can also use it with a `<div>`:

📃 **src/App.vue**

    <div class="product-info">
      ...
      <div v-for="variant in variants">{{ variant.color }}</div>
    </div>
    

![list.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F6.1668107527784.jpg?alt=media&token=3a87850b-48b7-40ff-a10f-c1d984740360)

And just like in React, we have to set a key on each element:

📃 **src/App.vue**

    <div class="product-info">
      ...
      <div v-for="variant in variants" :key="variant.id">{{ variant.color }}</div>
    </div>
    

That’s because Vue.js relies on _Virtual DOM_ just like React does.

* * *

v-for with v-if
---------------

`v-for` and `v-if` can be used together on the same element, but there is a caveat.

For example, if you have this:

    <div v-for="..." v-if="...">...</div>
    

The order in which they appear on the same element doesn’t matter. `v-if` will always be processed before `v-for`. The fact that `v-if` is placed behind `v-for` doesn’t change anything.

If you want `v-for` to be processed first, you have to put them in different elements:

    <div v-for="...">
      <div v-if="...">...</div>
    </div>
    

* * *

Coming Up Next
--------------

Now that we’re equipped with some templating basics, we’re ready to move on to the next lesson where we’ll add some interactivity to the page using event handling.

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L4-start)
    
*   [Ending Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L4-end)
