# Passing Scoped Slot to MyVuetable

In the last lesson, we have successfully create properties in our `MyVuetable` component allowing passing data in from the main component/instant. But the only remaining thing we are not able to do is the [scoped slots](https://vuejs.org/v2/guide/components.html#Scoped-Slots).

Scoped slots has been newly introduced in Vue 2.1 and it is a very powerful concept when working with Vue.js. It offers a more convenient way of flexible content distribution. Before the introduction of scope slots, you would have to create another component for the job. 

## The Problem

As of the current release of Vue 2.3, there is still no way to pass the scoped slot down into the component via template. The only way possible is to implement the `render` function where you'll have access to `scopedSlots` data object. This will allow you to pass down the scoped slot into your component. But this means you will have to give up the template and render your component using the `render` function only.

This seems like a daunting task. Luckily, in our case, this is not that hard but you will need some background knowledge before proceeding. Read the following topic in Vue documentation first, then come back to continue with the tutorial. You don't need to understand everything though.
- [Scope slots](https://vuejs.org/v2/guide/components.html#Scoped-Slots)
- [Render function](https://vuejs.org/v2/guide/render-function.html)


## Converting <template> to render function

