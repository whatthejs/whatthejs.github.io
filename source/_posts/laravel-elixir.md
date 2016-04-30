---
title: Easy Frontend Tooling with Laravel Elixir - Without Laravel!
category: Tooling
---

Frontend tooling has gotten really complicated and it's no longer an aspect of your project you can ignore. You really don't need me to convince you right? Every project demands a level of my attention on things that shouldn't matter. I just want to build apps! More importantly, so does your team, and they want to do it quickly.

So, what is Laravel Elixir and how will it get me to building apps faster? First, Laravel itself, as some of you might know, is a PHP MVC framework. It has a lot of great features but Laravel also comes with Elixir, which the [documentation](https://laravel.com/docs/5.2/elixir#introduction) explains:

> Laravel Elixir provides a clean, fluent API for defining basic Gulp tasks for your Laravel application. Elixir supports several common CSS and JavaScript pre-processors, and even testing tools. Using method chaining, Elixir allows you to fluently define your asset pipeline.


For example, if you need to compile `sass` you don't have to install any additional plugins - Elixir ships with the most common. This is your `gulpfile.js` file:

``` javascript
var elixir = require('laravel-elixir');

elixir(function(mix) {
  mix.sass('app.sass');
});
```

Just this little bit of code comes packed with features you normally would have to prepare separately. When you run `gulp` in the terminal, Elixir will automatically build your css file with sourcemaps, when not running in production. It knows where your source files are and it knows where to save them to after compile.

The reason it can do so much is because it assumes you've installed a full Laravel application. Because you've installed Laravel, it knows that you save your source files in specific folders; it knows where your public folder is so it can save the output without you having to specify it. It passes these configuration options to Elixir. However, these configuration options can be changed.

This is why it's so simple to use Elixir in your own non-Laravel projects. Either use Laravel's folder conventions or change the configuration options, and you'll be using Elixir in your own projects!

## So let's get started!

### Install Laravel Elixir

``` bash
$ npm install laravel-elixir
```

### Set up the folders for saving your source files to:

This creates a `resources/assets/sass` and a `resources/assets/js` folder at the root of your project.
``` bash
$ mkdir -p resources/assets/{sass,js}
```

### Make sure you have a public folder:

``` bash
$ mkdir public
```

### Prepare your gulp file:

Besides compiling Sass, Elixir ships with *many* other tasks including one for compiling Javascript with Browserify. So, let's create a file for compiling both Sass and Javascript:

``` javascript
var elixir = require('laravel-elixir');

elixir(function(mix) {
  mix.sass('app.sass');
  mix.browserify('main.js');
});
```

Look how wonderfully clean that is! What if you don't like the default choice for file locations? Well with Elixir, configuring paths is straight-forward.

Let's say I wanted to have all my source files (sass, jsx, etc) in a different folder, one called `src` (instead of `resources/assets`)? I also wanted those files to be compiled to a folder called `build` (instead of `public`)? Easy!

``` javascript
var elixir = require('laravel-elixir');

elixir.config.assetsPath = 'src';
elixir.config.publicPath = 'build';

elixir(function(mix) {
  mix.sass('app.sass');
  mix.browserify('main.js');
});
```

And there you have it. Elixir ships with many other tasks like `browsersync`, `coffeescript`, file versioning/cache busting, copying files and folders, and more. Note, that when you need to ship your assets to production, just run gulp with the production flag - which minifies/uglifies your assets: `gulp --production`. Sweet! Head over to Elixir's [documentation](https://laravel.com/docs/5.2/elixir#introduction) to get a ton more detail.
