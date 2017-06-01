# Using Twitter's Bootstrap CSS with Vuetable

Vuetable was designed from the beginning to take advantange of CSS framework to render table appearance. So, if your CSS framework of choice is supporting the HTML `table`, it should be easy enough to configure Vuetable to use the CSS specified by those frameworks.

However, `table` is usually not the only element on the page. It usually accompanies by other elements like the pagination, search/filter element, etc. So, in order to successfully apply the CSS of the selected framework to Vuetable, you will need to understand different parts that is going into your web app page.

And we are going to do that in this lesson by applying Twitter's Bootstrap CSS to Vuetable and its related elements.

## index.html
- Replace Semantic UI CSS and JS

## Changes related to Vuetable, VuetablePagination, and VuetablePaginationInfo
- create a new file to store CSS for those components
- field def
- use `css` prop of each component to assign appropriate config object
- buttons and icons in "actions" scoped slot

## Changes outside of Vuetable
- filter-bar
- app CSS
- 