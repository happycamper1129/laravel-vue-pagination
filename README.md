# Laravel Vue Pagination
A Vue.js pagination component for Laravel paginators that works with Bootstrap.

## Requirements

* [Vue.js](https://vuejs.org/) 2.x
* [Laravel](http://laravel.com/docs/) 5.x
* [Bootstrap](http://getbootstrap.com/) 3.x

## Usage

Register the component:

```
Vue.component('pagination', require('laravel-vue-pagination'));
```

Use the component:

```
<pagination ref="paginator" :data="laravelData"></pagination>
```

```
Vue.component('example-component', {

	data() {
		return {
			// Our data object that holds the Laravel paginator data
			laravelData: {},
		}
	},

	created() {
		// Set up the pagination event listener
		this.$refs.paginator.$on('pagination-change-page', this.getResults);

		// Fetch initial results
		this.getResults();
	},

	methods: {
		// Our method to GET results from a Laravel endpoint
		getResults(page) {
			if (typeof page === 'undefined') {
				page = 1;
			}

			// Using vue-resource as an example
			this.$http.get('example/results')
				.then(response => {
					return response.json();
				}).then(data => {
					this.laravelData = data;
				});
		}
	}

});
```

## API

### Props

| Name | Type | Description |
| --- | --- | --- |
| `data` | Object | An object containing the structure of a [Laravel paginator](https://laravel.com/docs/5.3/pagination) response. See below for default value. |

```
{
	current_page: 1,
	data: [],
	from: 1,
	last_page: 1,
	next_page_url: null,
	per_page: 10,
	prev_page_url: null,
	to: 1,
	total: 0,
}
```

### Events

| Name | Description |
| --- | --- |
| `pagination-change-page` | Triggered when a user changes page. Passes the new `page` index as a parameter. |

## Credits

Laravel Vue Pagination was created by [Gilbert Pellegrom](http://gilbert.pellegrom.me) from
[Dev7studios](http://dev7studios.co). Released under the MIT license.
