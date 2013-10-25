# Tint.js
Tint.js is Tint's SDK that allows developers to quickly build dynamic social content. Tint.js handles all of the social aggregation and data delivery / pagination / templating.

## Getting Started

Below, you will learn how to use Tint.js to build a basic custom widget.

### Dependencies

Include the Tint script along with the other JavaScript on your page.

```javascript
<script async type="text/javascript" src="somelongurl/tint.js"></script>
```

Then, to run your code after all of the Tint components are loaded, add the following:
```javascript
<script>
	Tint.ready(function(){
		// View and API components are loaded
	});
</script>
```

### The Model

Tint.js models are extensions of Backbone.js modules. Use them to pull in data from our API. These models are used to create views which can be rendered 

```javascript
var collection = new Tint.PostCollection();
collection.username = 'your_username_here'; // required
collection.fetch(); // calls the API for collection data
```

The model comes with a number of properties that can be modified to change what data is returned

```javascript
var collection = new Tint.PostCollection({
	username: '', // required username of your Tint
	network: 'facebook', // optional network - all, twitter, instagram, etc.
	from : 1382485719887 // optional timestamp indicating when to start pulling in data
});
```

### The View

Views can use custom templates to render the data. Our templating system makes this easy. Just do the following:

1. Define a template using mustache.js syntax, and either put it on the page in a script tag, or host it somewhere with jsonp enabled
2. Associate it with a view using the CSS identifier or the URL to your template
3. Optionally, add a CSS file to style the template and store it as "template_css"

```javascript
<!-- 1. defining a custom template -->
<script class="my_template_name" type="application/x-template">
	<div>
		<h2>{{ title }}</h2>
	</div>
</script>
```

```javascript
<!-- 2. setting up model and view with custom template -->
<script>
	Tint.ready(function(){
		// View and API components are loaded
		// create a new collection of posts
		var collection = new Tint.PostCollection();
		collection.username = 'your_username_here'; // required
		// create a new view, associating them with this collection
		var postHolderView = new Tint.PostHolderView({
			model: collection,
			// optional template for a single post (see http://dev.tintup.com/template/postTemplate_basic?callback=example for an example)
			template: 'http://www.example.com/url/to/your/jsonp/template',
			// optional css file to go with your template
			template_css: 'http://www.example.com/url/to/your/css.css',
			// optional function to be called after all of the posts have rendered
			afterRender: function(){
				console.log('render finished');
			}
		});
		// pull data from server
		collection.fetch();
	});
</script>
```

