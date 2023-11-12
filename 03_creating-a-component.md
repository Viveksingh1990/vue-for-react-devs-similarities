Creating a component
====================

Some Prep Work
--------------

In this lesson, we’re finally going to write some Vue code.

Let’s first remove all the default files in the **src/components** folder.

Also remove all the code inside the **src/App.vue** file. We’re going to create our first Vue.js component from scratch.

* * *

The Structure of a Single-File Component:
-----------------------------------------

Similar to a React component, there are two distinct parts of a Vue component. The script part and the template part. Optionally, there’s a style part for your CSS code, but for now let’s just focus on the script and the template.

📃 **src/App.vue**

    <script>
    </script>
    
    <template>
    </template>
    

To use the latest syntax in `<script>`, we have to add the `setup` attribute. (I’ll explain the syntactical differences between the new and old later in the lesson)

📃 **src/App.vue**

    <script setup>
    </script>
    

We’re going to put all the component’s logic in the `<script>` section, and put the template code in the `<template>` section.

* * *

ref: Vue’s version of “useState”
--------------------------------

First let’s create a state.

We have to import `ref` and use it to initialize a state:

📃 **src/App.vue**

    <script setup>
    import { ref } from 'vue'
    
    const product = ref('Socks')
    
    </script>
    

So what exactly is `ref`? As you can discern, `ref` is the Vue.js equivalent of `useState`.

“ref” stands for reference. The idea is that a value such as a string or a number is not a reference, but we need a reference object to facilitate reactivity in a Vue component.

For example, a variable with a string value:

    let product = 'Socks'
    

If we’re using this variable as a state, changing it means reassigning it:

    product = 'New Socks'
    

The problem is that the original value `"Socks"` would be lost after the reassignment. If the original value is lost, reactivity is lost as well.

Vue’s way of getting around this problem is to wrap the value in an object with `ref`:

    const product = ref('Socks')
    

So our state is technically the `ref` object, not the string value it contains.

* * *

Now to render this ref state, we’ll use the _double curly braces_ in the template to create a binding:

📃 **src/App.vue**

    <template>
      <h1>{{ product }}</h1>
    </template>
    

So whenever `product` is changed, the `<h1>` will be updated with its new value.

If you check the browser, you should see “Socks”:

![socks.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1668106685756.jpg?alt=media&token=cd1bc789-9989-4d08-932e-2fe29be1d65b)

* * *

The Double-Curly Braces
-----------------------

The double curly braces are similar to React’s single curly braces with JSX. Technically you put any JavaScript expression inside them, it doesn’t have to be a variable.

* * *

value: Vue’s version of “state” and “setState”
----------------------------------------------

If we want to access or change the value of the ref in `<script>`, we have to use the `value` property on the ref:

📃 **src/App.vue**

    setTimeout(() => {
      product.value = "New Socks"
    }, 1000)
    

The `value` property is used for both read and write. So it’s the _Vue.js equivalent of state and setState_.

In the example here, we’re assigning `value` to a new string to change the state.

In the browser, you should see the value changing after the one-second timeout.

![new_socks.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F2.1668106685757.jpg?alt=media&token=1a0a56dd-c6a6-4695-8cad-5c20a6d2ab33)

But in the `<template>`, you don’t have to use the `value` property because it will be added for you automatically.

* * *

Reactive
--------

Another way to create a state in Vue is to use `reactive()`, but this is intended for object-type data:

📃 **src/App.vue**

    import { reactive } from 'vue'
    
    // pass an object to reactive()
    const product = reactive({
      name: 'Socks'
    })
    
    ...
    <h1>{{ product.name }}</h1>
    

The main difference is that you don’t have to use the `value` property to access and change its content in both the `<script>` and the `<template>`.

📃 **src/App.vue**

    setTimeout(() => {
      product.name = "New Socks"
    }, 1000)
    

To use `ref()` or `reactive()`, it all depends on your need. If you just need a state for a simple value, then `ref()` should be fine. If you have a bunch of related data that usually go together, you might want to put them in the same object using `reactive()`.

* * *

Other Script Syntax
-------------------

As I mentioned previously, using the `setup` attribute on the `<script>` tag means we’re using the latest syntax for the component script.

This is called the **Composition API** with the `script setup` syntax:

    <script setup>
    import { ref } from 'vue'
    
    const product = ref('Socks')
      
    setTimeout(() => {
      product.value = "New Socks"
    }, 1000)
    
    </script>
    
    <template>
      <h1>{{ product }}</h1>
    </template>
    

The above is basically a simplified syntax for the **classic Composition API** syntax\*\*:\*\*

    <script>
    import { ref } from 'vue'
    
    export default {
      setup() {
        const product = ref('Socks')
    
        setTimeout(() => {
          product.value = "New Socks"
        }, 1000)
    
        return { product }
      }
    }
    </script>
    
    <template>
      <h1>{{ product }}</h1>
    </template>
    

As you can see, this is tedious to read/write. That’s why we’re using the `script setup` syntax instead.

So from now on I’m going to refer to the `script setup` syntax as the **Composition API** syntax.

* * *

In contrast to the Composition API, there’s the **Options API**. It’s yet another way for constructing the component logic.

    <script>
    export default {
      data() {
        return {
          product: 'Socks'
        }
      },
      created() {
        setTimeout(() => {
          this.product = "New Socks"
        }, 1000)
      }
    }
    </script>
    

In fact, this is the main syntax that Vue developers had been using for years before the **Composition API** came along.

But because the **Composition API** is now the _officially recommended syntax_, we’re going to use that in this course.

To explore the evolution of how the script setup became the recommended way to compose Vue components, you can check out the Vue Mastery article on [A Brief History of Vue’s Script Setup](https://www.vuemastery.com/blog/a-brief-history-of-vue-script-setup).

* * *

Custom Hook
-----------

You can think of the **Composition API** as the _Vue.js equivalent of React Hooks_.

You can think of the **Options API** as the _Vue.js equivalent of React’s class-based API_.

That means using the Composition API, we can create _custom hooks_. But in the Vue.js world, we call them _composables_.

It’s the same concept. If you’ve created custom hooks in React, this should feel right at home.

📃 **src/App.vue**

    // a composable that changes the value after a specified delay
    const useChangeWithDelay = function (state, newVal, delay) {
      setTimeout(() => {
        state.value = newVal
      }, delay)
    }
    
    const product = ref('Socks')
      
    useChangeWithDelay(product, 'New Socks', 1000)
    

We’re using the “use” prefix to name the composable just like the naming convention of a React hook.

If you want to learn more about creating composables, you can check out the _[Coding Better Composables](https://www.vuemastery.com/courses/coding-better-composables)_ course.

* * *

Coming Up Next
--------------

So far, we’ve talked about the various ways to write code in the `<script>` section. In the next lesson, we’ll shift our focus to the `<template>` section. We’ll talk about how to render things with conditionals and loops.

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/tailwind-tutorial/tree/L5-Start)
    
*   [Ending Code](https://github.com/Code-Pop/tailwind-tutorial/tree/L5-End)
