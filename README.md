# Compile Pug templates in an AngularJS module as a Brunch plugin

For each template, wrap around in a shared AngularJS module called
`templates` by default with each template file's path as the template URL.
See [$templateCache](http://docs.angularjs.org/api/ng.$templateCache) for more
information.

For information about Pug (formerly known as Jade), go [here](http://jade-lang.com/).


## Installation

`npm install --save pug-angularjs-templates-brunch`


## Usage

  1. Set `joinTo` attribute for `templates` in `config.coffee`, e.g.

	```coffee
	templates:
	  joinTo:
		'templates.js': /^app/
	```

  2. In your markup, include `templates.js`:

	```html
	<script type="text/javascript" src="/templates.js"></script>
	```

  3. Your app module must require the module your templates were placed in:

	```coffee
	angular.module('MyApp', [
	  ...
	  'templates'
	  ...
	]);
	```

  4. Get a particular template by its path.  Templates can be either .jade or .pug.

	```coffee
	$routeProvider.when('/home', { templateUrl: 'app/home/home.jade' });
	```

  5. Run Brunch (e.g. `brunch build`)


## Options

### module

Specify the module to place the templates in

Default: `templates`

```coffee
plugins:
  pug_angular_templates:
    module: 'MyModule'
```

### path_transform

Specify a transform function for the template path. This callback function will
be invoked with the brunch path to each template file (e.g.
'app/home/home.html') and must return a new path for that template (e.g.
'/partials/home/home.jade'). This new path will be used when inserting into the
template cache. This allows the template files to be served from an arbitrary
location regardless of their source.

Default: no-op (returns input path)

Example: if your template is in app/scripts/somedir/myTemplate.jade buy you'd
prefer to reference the templates as 'somedir/myTemplate.jade', you could use
this path transform:

```coffee
plugins:
  pug_angular_templates:
    path_transform: (path) -> path.replace('app/scripts/', '')
```

### Pug Options

Supports a couple of other Pug options - pretty, doctype, locals

```coffee
plugins:
  pug_angular_templates:
    pretty: true
```


## Credit

Inspiration from the following projects:

- https://github.com/dougmoscrop/angularjs-templates-brunch - direct fork!
- https://github.com/aberman/html2js-brunch
- https://github.com/nathanredblur/html-angularjs-brunch
- https://github.com/kenhkan/angular-templates-brunch/
- https://github.com/jupl/aang-template-brunch
