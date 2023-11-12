Dynamic and Scoped Style
========================

In this lesson, we’re going to polish the design of the app using `:class` binding and `:style` binding.

First, we’re going to add the class `color-circle` to the `div` so that they become circles:

📃 **src/App.vue**

    <div 
      v-for="variant in variants" 
      ...
      class="color-circle"
    >
      {{ variant.color }}
    </div>
    

They look like this, which isn’t very pretty. Instead, we’ll want to use the names of the colors (”green” and “blue”) to dynamically set the color of the circle’s background.

![img-1.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1668110556099.jpg?alt=media&token=c356f9da-b3ef-4ac8-8d2f-f17f5785dd85)

To add dynamic style to each of the two circles so they have the right colors, we can use a style binding:

📃 **src/App.vue**

    <div 
      v-for="variant in variants" 
      ...
      class="color-circle"
      :style="{ backgroundColor: variant.color }"  
    >
      <!-- {{ variant.color }} --> 
    </div>
    

(We’re using the shorthand colon here in place of `v-bind:`)

Now we can just remove the text binding from the div.

The way we put CSS in the style binding is very similar to how you would do it in React, but instead of double curly braces, we use quotes and single curly braces:

**In Vue:**

    <div 
      ...
      :style="{ backgroundColor: variant.color }"  
    >
    </div>
    

**In React:**

    <div 
      ...
      style={{ backgroundColor: variant.color }}
    >
    </div>
    

* * *

Between the double quotation marks, it’s an object literal with a CSS property:

![Screen Shot 2022-09-28 at 9.13.47 AM.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F2.1668110556100.jpg?alt=media&token=d726100e-a2c3-4f07-8133-b549e499d6fa)

`variant.color` will be rendered as one of the color names:

![Screen Shot 2022-09-28 at 9.14.10 AM.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F3.1668110561932.jpg?alt=media&token=a5e662b5-aeab-4f7a-9a00-26a9dc471b4e)

The final rendering will be this:

![Screen Shot 2022-09-28 at 9.14.28 AM.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F4.1668110566232.jpg?alt=media&token=2321d272-1847-441e-88c7-552018b387c8)

Notice that the `:style` binding become the normal `style` attribute in the rendered HTML.

* * *

In the browser, the dynamically styled color circles should look like this:

![color-circles.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F5.1668110569548.jpg?alt=media&token=4290b186-08c2-4953-af5b-b2ebc1297c8b)

* * *

Class Binding
-------------

Next, we want to make the button _disabled_ whenever the `inStock` ref is `false`.

We can create another binding with the `disabled` attribute to make the button _unclickable_.

📃 **src/App.vue**

    <button
      ...          
      :disabled="!inStock"
    >
      Add to cart
    </button>
    

But to make it _look_ unclickable, we have to use CSS.

We already prepared the style in **src/assets/main.css**:

📃 **src/assets/main.css**

    .disabledButton {
      background-color: #d8d8d8;
      cursor: not-allowed;
    }
    

We just need to use this class in the template.

We’re going to create a binding with another class attribute:

📃 **src/App.vue**

    <button
      class="button" 
      :class="{ disabledButton: !inStock }"
      ...
    >
      Add to cart
    </button>
    

Similar to the style binding, we’re using an object literal. But different from the style binding, the property key is the class name, and the property value should be a boolean value. So if the value is `true`, the corresponding class will be rendered. If it’s `false`, the class will not be rendered.

Whenever a `:class` binding is used on the same element with a normal `class` attribute, they will be merged.

To demonstrate this, we’ll first have to set the `inStock` ref to `false`:

📃 **src/App.vue**

    const inStock = ref(false)
    

In the browser, the button will be disabled and also look disabled:

![disabled-button.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F6.1668110569549.jpg?alt=media&token=1db7b708-85e5-445b-8367-c78163955011)

And you can see that they’re merged in the DOM Inspector:

![class.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F7.1668110574188.jpg?alt=media&token=f8c4e5d3-8597-4b3c-b93d-410a09dd6bc4)

The class binding can also be used with an array; this alternate syntax can make it easier to use a bunch of string variables directly as classes.

    const color = 'text-dark'
    const bgColor = 'bg-white'
    const borderColor = 'border-dark'
    <div :class="[color, bgColor, borderColor]">
    

* * *

Scoped Style
------------

Finally, I want to wrap up this course with a mention of the optional `<style>` tag. It’s one of the three high-level tags along with `<script>` and `<template>`. Technically, `<script>` is also optional. So you can have `<template>` by itself if you don’t need any logic for your component. Or `<template>` with `<style>`.

    <template>
      <p>Hello world</p>
    </template>
    
    <style>
      p {
        border: 1px solid black;
      }
    </style>
    

The `<style>` section is simple, you just put CSS in it and it works.

To make it even more useful, you can use the `scoped` attribute:

    <template>
      <p>Hello world</p>
    </template>
    
    <style scoped>
      p {
        border: 1px solid black;
      }
    </style>
    

Now, the CSS will be scoped to only the current component and not affect its child components, except the root element of a child component.

For example, if we have a child component with one root element containing two other elements:

    <template>
      <p>
        <p>Hello</p>
        <p>world</p>
      </p>
    </template>
    

Import and use it in the parent component:

    <script>
    import ChildComponent from './ChildComponent.vue'
    </script>
    
    <template>
      <ChildComponent></ChildComponent>
    </template>
    
    <style scoped>
      p {
        border: 1px solid black;
      }
    </style>
    

Only the top-most `<p>` element of the child component will be affected by the black border style:

![border.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F8.1668110578303.jpg?alt=media&token=f4dba4f3-4dd4-468a-b6a7-b614d91ad4d7)

* * *

We’re not done just yet
-----------------------

Now that you’re equipped with some basics of Vue.js, you’re ready to move on the next course, _Vue For React Devs: Differences,_ where we’ll discuss more advanced concepts that are done differently in Vue.js compared to React.js, such as _props_ and _lifecycle hooks_.

I’ll see you there.

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L6-start)
    
*   [Ending Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L6-end)
