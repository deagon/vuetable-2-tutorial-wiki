# Pagination for Twitter's Bootstrap

Most CSS frameworks come with pagination style, however the markup looks different from one another. So, you may want rewrite your own pagination with the markup specific to your CSS framework of choice.

Luckily, this is quite easy because Vuetable comes with VuetablePaginationMixin which contains most of the functionality for pagination. In fact, if you look at the source code, both VuetablePagination and VuetablePaginationDropdown are using this mixin with a slight modification. So, you could just create a new pagination component that can work with Vuetable with ease by using this mixin as well.

This is the pagination markup for Bootstrap 3 as shown on its [website](https://getbootstrap.com/components/#pagination)

![image]()

However, it doesn't dictate how the pagination would be displayed if the number of pages is longer than 5. Let's say 100 pages, would it literally display buttons for page 1 up to page 100? 

That's definitely not what we want.

So let's see how VuetablePagination did with this situation?

## Sliding Window Pagination

VuetablePagination borrows the pagination idea from [Laravel](https://laravel.com), which employs sliding window pagination concept that display only a certain number of pagination links. 

This pagination window shifts when the user changes page, but the number of pagination links displayed stayed the same and the current page is displayed at the center almost all the time, except when the current page is near the start or end of the list. It also provides navigation links to jump to the first and last page of the list.

The pagination window size is calculated using `on-each-side` prop, which indicates how many items to be displayed on each side of the current page.

If you're satisfying with this logic of sliding window pagination, you can just write the template markup for the pagination according to the CSS framework and embedded the logic in there. It's just that!

## Creating Pagination for Bootstrap

Now, create a file `VuetablePaginationBootstrap.vue` in the `src/components` directory and paste the following code in.
```vue
<template>
  <ul class="pagination">
    <li :class="{'disabled': isOnFirstPage}">
      <a href="" @click.prevent="loadPage('prev')">
        <span>&laquo;</span>
      </a>
    </li>
    
    <template v-if="notEnoughPages">
      <li v-for="n in totalPage" :class="{'active': isCurrentPage(n)}">
        <a @click.prevent="loadPage(n)" v-html="n"></a>
      </li>
    </template>
    <template v-else>
      <li v-for="n in windowSize" :class="{'active': isCurrentPage(windowStart+n-1)}">
        <a @click.prevent="loadPage(windowStart+n-1)" v-html="windowStart+n-1"></a>
      </li>
    </template>

    <li :class="{'disabled': isOnLastPage}">
      <a href="" @click.prevent="loadPage('next')">
        <span>&raquo;</span>
      </a>
    </li>
  </ul>
</template>

<script>
import VuetablePaginationMixin from 'vuetable-2/src/components/VuetablePaginationMixin'
export default {
  mixins: [VuetablePaginationMixin]
}
</script>
```

Let's look at the `<script>` section first, you will see that we `import` VuetablePaginationMixin from Vuetable-2 and add to the `mixins` section of our Vue component. So, you'll get the following computed properties and functions from this mixin:
- isOnFirstPage
- isOnLastPage
- notEnoughPages
- totalPage
- isCurrentPage
- loadPage
- windowSize
- windowStart
- etc.

> For the full list, please see the [documentation here](https://ratiw.github.io/vuetable-2/#/VuetablePaginationMixin).

It even contains the code for binding pagination's information from Vuetable, so we can just swap it out with VuetablePagination and it'll just work.

If you compare the template of [VuetablePagination](https://github.com/ratiw/vuetable-2/blob/master/src/components/VuetablePagination.vue), you'll see that it is very similar. The template in VuetablePagination looks actually a bit more complex because it was implemented to be more nuetral to different CSS framework.

But since we are implement a pagination component specific to Bootstrap CSS framework, the code you see above will be suffice.

## Replacing the Pagination Component

Let's look at how we replace our pagination component in the "template" version of the code first.

Here's part of the template of [`MyVuetable.vue`](https://github.com/ratiw/vuetable-2-tutorial/blob/lesson-16/src/components/MyVuetable.vue#L34-L40) in lesson 16.
```vue
<template>
  //...
    <div class="vuetable-pagination ui basic segment grid">
      //...
      <vuetable-pagination ref="pagination"
        @vuetable-pagination:change-page="onChangePage"
      ></vuetable-pagination>
    </div>
  //...
</template>
<script>
//..
import VuetablePaginationBootstrap from './VuetablePaginationBootstrap'

export default {
  components: {
    Vuetable,
    VuetablePagination,
    VuetablePaginationInfo,
  },
  //...
}
</script>
```

We just change the lines that reference VuetablePagination to VuetablePaginationBootstrap.
```vue
<template>
  //...
    <div class="vuetable-pagination">
      //...
      <vuetable-pagination-bootstrap ref="pagination"
        @vuetable-pagination:change-page="onChangePage"
      ></vuetable-pagination-bootstrap>
    </div>
  //...
</template>
<script>
//..
import VuetablePaginationBootstrap from './VuetablePaginationBootstrap'

export default {
  components: {
    Vuetable,
    VuetablePaginationBootstrap,
    VuetablePaginationInfo,
  },
  //...
}
</script>
```

And that's it! The event binding stays the same because we use the mixin. Only one problem is that our pagination component is not on the right of the table. Well, that's an easy fix. Just add `class="pull-right"` like so.
```html
  <vuetable-pagination-bootstrap ref="pagination"
    class="pull-right"
    @vuetable-pagination:change-page="onChangePage"
  ></vuetable-pagination-bootstrap>
```

Now, let's see how this is done in the render function version of our code in the [last lesson](https://github.com/ratiw/vuetable-2-tutorial/blob/lesson-18/src/components/MyVuetable.vue#L72-L111).
```vue
<script>
// import VuetablePagination from 'vuetable-2/src/components/VuetablePagination'
import VuetablePaginationBootstrap from './VuetablePaginationBootstrap'
//..

export default {
  components: {
    Vuetable,
    // VuetablePagination <--- commented out
    VuetablePaginationInfo,
    VuetablePaginationBootstrap,
  },
  //...
    renderPagination(h) {
      return h(
        'div',
        { class: {'vuetable-pagination': true} },
        [
          h('vuetable-pagination-info', { ref: 'paginationInfo', props: { css: this.css.paginationInfo } }),
          h('vuetable-pagination-bootstrap', {
            ref: 'pagination',
            class: { 'pull-right': true },
            props: {},
            on: {
              'vuetable-pagination:change-page': this.onChangePage
            }
          })
        ]
      )
    },
    //...
}
</script>
```

We also remove the `css` prop because it does not needed in our own pagination component. So, the `props` object become empty and you can remove it as well, if you like.

Compare it to the previous one we have in the last lesson, you'll clearly see that it only requires tiny changes on a few line of code.

Now try running the project, it should still work the same but with our own Bootstrap styled pagination component.

[Source code for this lesson](https://github.com/ratiw/vuetable-2-tutorial/tree/lesson-18)

You can also look at this [codepen project](https://codepen.io/ratiw/project/editor/DzmJnA/).
