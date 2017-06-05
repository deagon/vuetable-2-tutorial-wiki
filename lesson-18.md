# Using Twitter's Bootstrap CSS with Vuetable

Vuetable was designed from the beginning to take advantange of CSS framework to render table appearance. So, if your CSS framework of choice is supporting the HTML `table`, it should be easy enough to configure Vuetable to use the CSS specified by those frameworks.

However, `table` is usually not the only element on the page. It usually accompanies by other elements like the pagination, search/filter element, etc. So, in order to successfully apply the CSS of the selected framework to Vuetable, you will need to understand different parts that is going into your web app page.

And we are going to do that in this lesson by applying Twitter's Bootstrap 3 CSS to Vuetable and its related elements.

## First thing first

When you pick a CSS framework of your choice, make sure that you've been working with it for a while and know enough to comfortably using it. If not, take time to learn it first. Do not jump right in; otherwise, you'll be more confused and ended up feel more frustrating than you should be.

### If you're ready, we can proceed on. 

The concept in this lesson should give you enough knowledge to apply it to other CSS framework as well.

## index.html

In our tutorial project, this is where the CSS framework was pulled in. So, it's the first place we should look into as well.

Since the code in this file is quite sort, we'll put it in here.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>vuetable-2-tutorial</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.7/semantic.min.css" media="screen" title="no title" charset="utf-8">
  </head>
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->

     <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.1.0/jquery.min.js" charset="utf-8"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.7/semantic.min.js" charset="utf-8"></script>
  </body>
</html>
```

As you can see, we are using [CDNJS](https://cdnjs.com) to pull in jQuery and Semantic UI files from the cloud. 

> Semantic UI is dependent on jQuery and that's why we have to include it as well.  
> You should check the dependency requirement in your CSS framework as well.

In order to use Twitter's Bootstrap 3, we will modify the code to this.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>vuetable-2-tutorial</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap-theme.min.css">
  </head>
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->

    <script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
  </body>
</html>
```

And since Twitter's Bootstrap does not require jQuery by default, we can left it out.

> If you include your CSS library locally, you'll just have to change the `href` accordingly.

## Dissecting Your App Page

As we progress through our tutorial lessons, you should have noticed that Vuetable component is only part of the picture here. 

We have also build our own component that utilizes Vuetable and its related components inside. So, it is not only Vuetable that you want to apply the CSS from the CSS framework. Other components like pagination, filter bar will also need to be styled as well. But please remember they are separate components. We have to style it one by one!

So, we will first look at how we can style Vuetable using Bootstrap 3. Then, we will also style VuetablePagination, FilterBar.

## Styling Vuetable

Most of the styling for Vuetable can be done via [`css`](https://ratiw.github.io/vuetable-2/#/CSS-Styling) prop. Since we want to reuse it in other parts of the project or other projects, it is best to just create a new file to store. And here is how the styling object would look like with Bootstrap 3.

```javascript
export default {
  tableClass: 'table table-striped table-bordered',
  ascendingIcon: 'glyphicon glyphicon-chevron-up',
  descendingIcon: 'glyphicon glyphicon-chevron-down',
  handleIcon: 'glyphicon glyphicon-menu-hamburger'
}
```

## Rending Icon

Different CSS framework uses different markup to render the icon. Here is the same icon markup in Bootstrap and Semantic UI, respectively.
```html
<!-- Bootstrap3 -->
<span class="glyphicon glyphicon-menu-hamburger"></span>

<!-- Semantic UI -->
<i class="grey sidebar icon"></i>
```

Luckily, Bootstrap also allow using `<i>` tag as well as `<span>` tag. But in other CSS framework, this might be completely different. 

This is why Vuetable uses `renderIcon` function to render icon in its template, which by default uses Semantic UI syntax. Whereever in Vuetable template that would render icon, it would call this `renderIcon` function. And you can override this by providing your own render icon function inside the `css` object. 

```javascript
export default {
  tableClass: 'table table-striped table-bordered',
  ascendingIcon: 'glyphicon glyphicon-chevron-up',
  descendingIcon: 'glyphicon glyphicon-chevron-down',
  handleIcon: 'glyphicon glyphicon-menu-hamburger',
  renderIcon: function(classes, options) {
    return `<span class="${classes.join(' ')}"></span>`
  }
}
```

Right now there are only two places in the Vuetable template where `renderIcon` will be called.
- ascending and descending sort icon in table header, and
- `__handle` special field
 
What about those other icons in the "Action" column?

Well, in our tutorial they are in a template slot and is not part of Vuetable template. But you will have to put the correct tag in there by yourself.

If you're putting other icon as part of your column title, you'll just have to specify correct tag in the `title` option of the column definition.

## Styling VuetablePagination

Even though, VuetablePagination is provided for convenience, it is generic enough that you could use in your project with a bit of styling you'll have to adapt to achieve the coherent look. And you can do so via its [`css`](https://ratiw.github.io/vuetable-2/#/CSS-Styling?id=pagination) prop as well.

```javascript
export default {
  wrapperClass: "pagination pull-right",
  activeClass: "btn-primary",
  disabledClass: "disabled",
  pageClass: "btn btn-border",
  linkClass: "btn btn-border",
  icons: {
    first: "",
    prev: "",
    next: "",
    last: ""
  }
}
```

We can even combine this into one file, like so.
```javascript
export default {
  table: {
    tableClass: 'table table-striped table-bordered',
    ascendingIcon: 'glyphicon glyphicon-chevron-up',
    descendingIcon: 'glyphicon glyphicon-chevron-down',
    handleIcon: 'glyphicon glyphicon-menu-hamburger',
    renderIcon: function(classes, options) {
      return `<span class="${classes.join(' ')}"></span>`
    }
  },
  pagination: {
    wrapperClass: "pagination pull-right",
    activeClass: "btn-primary",
    disabledClass: "disabled",
    pageClass: "btn btn-border",
    linkClass: "btn btn-border",
    icons: {
      first: "",
      prev: "",
      next: "",
      last: ""
    }
  }
}
````

So to use that, we just import the file and use it where it should
```vue
<template>
  <vuetable ref="vuetable"
    //...
    :css="css.table"
  ></vuetable>
  <vuetable-pagination ref="pagination" 
    //...
    :css="css.pagination"
  ></vuetable-pagination>
</template>
<script>
import CssConfig from './VuetableCssConfig.js'

new Vue({
  el: '#app',
  data: {
    //...
    css: CssConfig,
  }
})
</script>
```
