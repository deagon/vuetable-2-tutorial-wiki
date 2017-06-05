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

This pagination window shifts when the user changes page, but the number of pagination links displayed stayed the same and the current page is displayed at the center almost all the time. It also provides navigation links to jump to the first and last page of the list.

The pagination window size is calculated using 