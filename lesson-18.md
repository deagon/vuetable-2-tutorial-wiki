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


## Changes related to Vuetable and its bundled components (VuetablePagination and VuetablePaginationInfo)
- create a new file to store CSS for those components
- field def
- use `css` prop of each component to assign appropriate config object
- buttons and icons in "actions" scoped slot

## Changes outside of Vuetable
- filter-bar
- app CSS
- 