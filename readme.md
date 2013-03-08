# grunt-php [![Build Status](https://secure.travis-ci.org/sindresorhus/grunt-php.png?branch=master)](http://travis-ci.org/sindresorhus/grunt-php)

*requires grunt 0.4 and PHP 5.4.0+*

> Start a [PHP-server](http://php.net/manual/en/features.commandline.webserver.php)

Pretty much a drop-in replacement for [grunt-contrib-connect](https://github.com/gruntjs/grunt-contrib-connect). Useful for eg. running tests on a PHP project. Uses the built-in server in PHP 5.4.0+.


## Getting Started

If you haven't used [grunt][] before, be sure to check out the [Getting Started][] guide, as it explains how to create a [gruntfile][Getting Started] as well as install and use grunt plugins. Once you're familiar with that process, install this plugin with this command:

```shell
npm install grunt-php --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-php');
```

[grunt]: http://gruntjs.com
[Getting Started]: https://github.com/gruntjs/grunt/wiki/Getting-started


## Documentation


### Example usage


#### Start a short-lived PHP-server

Useful for you need to fire up a PHP-server for running unit tests or something.

```javascript
grunt.initConfig({
	php: {
		dist: {
			options: {
				port: 5000,
				base: 'subfolder'
			}
		}
	}
});

grunt.registerTask('default', ['php']);
```

Run this with `grunt php` or `grunt php:dist`.


#### Start a persistent PHP-server and open in browser

```javascript
grunt.initConfig({
	php: {
		test: {
			options: {
				keepalive: true,
				open: true
			}
		}
	}
});

grunt.registerTask('test', ['php', 'mocha']);
```


### Options

#### port

Type: `Integer`  
Default: `8000`

The port on which you want to access the webserver. Task will fail if the port is already in use.

#### hostname

Type: `String`  
Default: `'localhost'`

The hostname the webserver will use.

#### base

Type: `String`  
Default: `'.'`

From which folder the webserver will be served. Defaults to the directory of the Gruntfile.

#### keepalive

Type: `Boolean`  
Default: `false`

Keep the server alive indefinitely. Any task specified after this will not run.

This option can also be enabled ad-hoc by running the task like `grunt php:targetname:keepalive`

#### open

Type: `Boolean`  
Default: `false`

Open the server in the browser when the task is triggered.

#### router

Type: `String`  

Optionally specify the path to a [router script](http://php.net/manual/en/features.commandline.webserver.php#example-380) that is run at the start of each HTTP request. If this script returns `false`, then the requested resource is returned as-is. Otherwise the script's output is returned to the browser.

Example router script:

```php
<?php
// router.php
if (preg_match('/\.(?:png|jpg|jpeg|gif)$/', $_SERVER["REQUEST_URI"])) {
	return false;    // serve the requested resource as-is
} else {
	echo "<p>Thanks for using grunt-php :)</p>";
}
?>
```


## License

MIT License
(c) [Sindre Sorhus](http://sindresorhus.com)
