- set `fields` prop
- set `api-mode` to `false`
- set `data` prop
- set `data-total` prop
- set `data-manager` prop

## What is Data mode?


> __Note__    
> What we discuss in this lesson is the way to supply offline (or pre-loaded) data to Vuetable.   
> This means that you still have to provided other props that Vuetable needs in order to work as expected.
> For example, you still have to provide fields definition in the `fields` prop.

## Using Data mode

You can use `data` prop to set the data for Vuetable-2.

`data` prop can accept either 
- an "Array" of data, _or_ 
- an object containing the data and pagination information.

### Using Array in `data` prop

If you just want to use Vuetable to display the data you already have, you can set those data array to the `data` prop. Vuetable will use the data provided to render HTML table. VuetablePagination and VuetablePaginationInfo will not work in this scenerio since no pagination information is available.

To do that, you will have to
- provide fields definition in the `fields` prop
- enable Data mode by setting `:api-mode="false"`
- pass your data array in the `data` prop, or call `setData` method to pass your data in.

### Using Object in `data` prop

If you not only want to use offline (or pre-loaded) data with Vuetable but also VuetablePagination and/or VuetablePaginationInfo to still work as in the API mode, you have to provide data object containing both data and pagination info to the `data` prop.

To do that, you will have to
- provide fields definition in the `fields` prop
- enable Data mode by setting `:api-mode="false"`
- pass your data object in the `data` prop, or call `setData` method to pass your data object in. This will be the initial data that will be rendered when Vuetable is loaded.
- provide the total number of data rows in `data-total` prop, so that the pagination component can perform correctly.
- set the data manager function to handle the data that will be sent to Vuetable for rendering.

