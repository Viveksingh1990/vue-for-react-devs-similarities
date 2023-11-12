Generating the app
==================

When it comes to creating an app from scratch, you don’t really want to create it from scratch. You would normally use a CLI program to generate the new app.

And it’s same with Vue.js. We’ll use the official Vue.js CLI called `create-vue`. This is _the Vue.js equivalent of create-react-app_.

    npx create-vue my-vue-app
    

We’ll go through a series of questions asked by _create-vue_:

    Add TypeScript?
    Add JSX Support?
    Add Vue Router for Single Page Application development?
    Add Pinia for state management?
    Add Vitest for Unit Testing?
    Add Cypress for both Unit and End-to-End testing?
    Add ESLint for code quality?
    

You can choose `no` for all of them.

Although JSX support is available for Vue.js, the standard way to write a Vue.js template is still using the _Vue.js template syntax_, which we’ll get to in the coming lessons.

Because Vue.js is a framework, it provides all the tools for your basic web development needs. You can use _Pinia_ for state management needs, use _Vue Router_ for your routing needs, etc.

But this course is going to be about the core Vue.js features, so we won’t get into _Pinia_ and _Vue Router_ here. If you want to learn about _Pinia_ or _Vue Router_, or _TypeScript for Vue.js_, you can check out the [Vue Mastery courses](https://www.vuemastery.com/courses) on these topics.

After generating the app folder, we have to install the packages:

    cd my-vue-app
    npm install
    

And finally, start the app server:

    npm run dev
    

You’ve probably noticed that the server got ready pretty quick. That’s because the app is powered by Vite.js instead of Webpack. The main feature of Vite is performance.

The default port is 5173. (it used to be port 3000 on some older versions of Vite).

You should see a welcome page like this at **localhost:5173**

![default.png](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1668106012392.jpg?alt=media&token=a045f603-d154-435b-8ba1-87ac8ed31b2c)

* * *

Project Files
-------------

Next, let’s cover a few important things inside the project directory.

Just like in a _create-react-app_ project, **src** is where you would put most of the code for the app, such as components and assets. And there’s a **main.js** file acting as the starting point for everything by mounting the `App` component.

📃 **/src/main.js**

    import { createApp } from 'vue'
    import App from './App.vue'
    
    import './assets/main.css'
    
    createApp(App).mount('#app')
    
    

* * *

**index.html** is where the App component will be mounted to (right inside `<div id="app"></div>`):

📃 **/index.html**

    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <link rel="icon" href="/favicon.ico" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Vite App</title>
      </head>
      <body>
        <div id="app"></div>
        <script type="module" src="/src/main.js"></script>
      </body>
    </html>
    

* * *

In **package.json**, you can see that the dependencies of this project are very concise. It’s basically just `vue` and `vite` (and a Vite plugin for Vue to make them work together).

📃 **/package.json**

      "dependencies": {
        "vue": "^3.2.38"
      },
      "devDependencies": {
        "@vitejs/plugin-vue": "^3.0.3",
        "vite": "^3.0.9"
      }
    

* * *

Legacy Mention - Vue CLI
------------------------

Although _create-vue_ is the current official Vue.js CLI, it came out in 2021. For years, Vue.js developers had been using another CLI tool called _Vue CLI_, which was the previous official Vue.js CLI.

I’m mentioning the _Vue CLI_ here because there are still many projects out there that were created with this older CLI tool.

The biggest difference between _Vue CLI_ and _create-vue_ is that the former is based on Webpack while the latter is based on Vite. So when you start the development server with a Vue CLI app, it’s noticeably slower.

If you want to learn more about why Vite is so fast, you should check out [Lightning Fast Builds w/ Vite](https://www.vuemastery.com/courses/lightning-fast-builds-with-vite/intro-to-vite) taught by Evan You, the creator of Vue.js and Vite.js.

* * *

Assets
------

Although we’re going to build an app from scratch, we still need some assets for the look and feel of the app, specifically the CSS and the images.

First, you’ll want to remove all the default files in **src/assets**.

Then go ahead and download the **main.css** and images folder from here:

[https://github.com/Code-Pop/vue-for-react-devs-similarities/tree/main/src/assets](https://github.com/Code-Pop/vue-for-react-devs-similarities/tree/main/src/assets)

Once you put them in the src/assets folder, you’re ready for the next step.

* * *

Next up…
--------

Now that we have all the assets ready, we’re ready to create our first Vue.js component in the next lesson.

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L2-start)
    
*   [Ending Code](https://github.com/Code-Pop/vue-for-react-devs/tree/L2-end)
