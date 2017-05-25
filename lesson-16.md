# Passing Props to MyVuetable - Part 2

In this lesson, we will start working on refactoring our `MyVuetable` component to accept properties and make it work as the same.

As a summary, here are the list of properties that we are going to make:
- api-url
- fields
- multi-sort
- sort-order
- append-params

If you are new to Prop, check out the documentation on Vue.js Guide [here](https://vuejs.org/v2/guide/components.html#Props).

## Changes in MyVuetable.vue

### Declaring Props

First, we need to define that our component accepts those properties. We are going to borrow the same property names from Vuetable in this case.

```javascript
// MyVuetable.vue

//...
export default {
  name: 'my-vuetable',
  components: {
    //...
  },
  props: {
    apiUrl: {
      type: String,
      required: true
    },
    fields: {
      type: Array,
      required: true
    },
    sortOrder: {
      type: Array,
      default() {
        return []
      }
    },
    appendParams: {
      type: Object,
      default() {
        return {}
      }
    },
    detailRowComponent: {
      type: String
    }
  },
  //...
}
```

> Only the `api-url` and `fields` properties are required. So, we marked it with `required: true`.

### Modify template to use Props

Now, we modify the template to use our newly defined properties, like so.

```html
// MyVuetable.vue

  //...
  <vuetable ref="vuetable"
    :api-url="apiUrl"
    :fields="fields"
    pagination-path=""
    :per-page="10"
    :multi-sort="true"
    :sort-order="sortOrder"
    :append-params="appendParams"
    detail-row-component="detailRowComponent"
    //...
  ></vuetable>

```

> __Note__    
> The `per_page` has been changed from `20` to `10`.

### Clean up

We need to clean up the following as well:
- Looking at the `data` section, you will see that all the variables in this section are no longer needed as they will be passed in via our properties instead, so we can remove all of them here.

  ```javascript
  // MyVuetable.vue

    // you can even remove the data section itself
    data () {
      return {}
    },
    //...
  ```

- The `import` statements of `FieldDefs` and `DetailRow` are no longer needed here, so remove both of them. 

## Changes in App.vue

### Passing the Props 

Now we need to modify `App.vue`, so that all necessary data are declared and pass into `<my-vuetable>` via properties we've defined earlier. Here is what we need to do:
- Add `data` section and declare our variables
- Import field definition in here 
- Add prop to our App template

```vue
// App.vue

// 
```
