# What is a Filter?

## Overview

Angular offers us the powerful concept of filters. They allow us to easily manipulate data, such as changing a date from a unix timestamp to a human readable format or simply change the text to uppercase. Let's take a look at what they can offer us.

## Objectives

- Show an Angular filter
- Use a filter on an ng-repeat
- Use a filter on an input's expressed value

## Filtering our datasets

Filters are simple functions that we can use to manipulate (or filter) data in Angular.

We've touched on the `ng-repeat` directive for repeating a list of data - wouldn't it be neat if we could filter on that data too? This comes in useful when we a large dataset and would like to quickly search through it to find the relevant data.

We can do this using the pipe operator (`|`) after the ng-repeat. The syntax for this is `| filterName: value`. We can use different filters (by changing the `filterName` part) and change what the filter criteria is by changing the `value` part.

The filter that we'd use to filter an ng-repeat by a value is simply named `filter`! We can pass a variable to this filter and it will search the whole dataset for us.

```html
<input ng-model="ctrl.search" />

<ul>
	<li ng-repeat="data in ctrl.data | filter: ctrl.search">
	</li>
</ul>
```

This will filter our dataset by the value of the input data - providing us with a really simple yet powerful search filter! As we type in the input, `ctrl.search` gets updated. Angular notices that we're using `ctrl.search` as a filter and filters the repeat by the value. This means that if we type in "bob", only results containing "bob" will be displayed!

## Display values

There are a few other filters that Angular provides us with, that we don't necessarily use for `ng-repeat`s.

Another powerful filter is `date`. This can take a unix timestamp and returns it nicely formatted for us. We use this with the same syntax as above, passing through a string as the value. The string will change how the date is displayed. Check out the docs to see all the ways we can display a date - there's loads!

```html
<abbr>
	{{ ctrl.date | date:'medium' }} <!-- Dec 25, 2016 2:23:56 PM -->
</abbr>
```

## Filtering in Controllers

We can also filter in our controllers, using the `$filter` service. This is the preferred method for filtering on big sets of data as it helps increase performance.

The syntax to use `$filter` is close to what we used above:

```js
$filter('filterName')(data, 'value');
```

This will then return the filtered data.

If we were to use this instead of the filter in an `ng-repeat`, it would look like the following:

```js
function SomeController($filter) {
	this.list = [{
		name: 'Bob'
	}, {
		name: 'Tom'
	}];

	this.search = 'B';

	this.filteredList = $filter('filter')(this.list, this.search);
}
```

We would then use `filteredList` like normal in our `ng-repeat`:

```html
<ul>
	<li ng-repeat="item in ctrl.filteredList">
		{{ item.name }}
	</li>
</ul>
```

## Resources

- [Built-in Angular filters](https://docs.angularjs.org/api/ng/filter)
- [Date filter docs](https://docs.angularjs.org/api/ng/filter/date)
