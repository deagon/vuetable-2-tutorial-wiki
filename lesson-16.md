# Passing Props to MyVuetable - Part 2

In this lesson, we will start working on refactoring our `MyVuetable` component to accept properties and make it work as the same.

As a summary, here are the list of properties that we are going to make:
- api-url
- fields
- multi-sort
- sort-order
- append-params

First, we need to define that our component accepts those properties.

```javascript
// MyVuetable.vue

//..
export default {
  name: 'my-vuetable',
  components: {
    //..
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
  }
}
```
