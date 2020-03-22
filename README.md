# Overview

is a javascript plugin that makes it easy to create simple, beautiful wysiwyg editors with the help of [wysihtml5](https://github.com/xing/wysihtml5) and [Twitter Bootstrap](http://twitter.github.com/bootstrap/).

## Dependencies

Additionally to the existing dependencies I added handlebars in version 0.2.0. You only need the handlebars.runtime.min.js. The templates are precompiled during build. This adds less than 7kB to your client (~3kB gzipped). Thus it is easier to maintain the code.
<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

Because maintaining code requires maintainable code.

## About us

 - [Waxolunist](https://github.com/Waxolunist) 
 - [schnawel007](https://github.com/schnawel007) 

## Development

Install all development dependencies via
npm install
Additionaly you need grunt, grunt-cli and bower as global packages installed.

Also install the client dependencies via bower install There is a grunt task for building. Just run

    grunt

on the command line and everything should build fine.

## Examples

-   [http://waxolunist.github.io/bootstrap3-wysihtml5-bower/](http://bootstrap-wysiwyg.github.io/bootstrap3-wysiwyg/)

For use with requirejs see the examples in the repo.

### Files to reference

In the folder dist you will the plain unminified javascript files and two kinds of minified files.

**bootstrap3-wysihtml5.min.js**: This file contains the jquery plugin, the templates and the english translations. If you are referencing this file, you have to reference jquery, bootstrap jquery plugin, handlebars runtime and wysihtml.js.

### Usage

#### Editable Div

This is the new style from version 0.3 on and will be supported on all browsers.

```javascript
$('.textarea').html('Some text dynamically set.');
```

#### Textarea

This is the old style usage and does use a sandboxed iframe, which will from version 0.3 on not work in IE.

```html
<textarea id="some-textarea" placeholder="Enter text ..." style="styles to copy to the iframe"></textarea>
<script type="text/javascript">
	$('#some-textarea').wysihtml5();
</script>
```

## Options

An options object can be passed in to `.wysihtml5()` to configure the editor:

```javascript
$('#some-textarea').wysihtml5({someOption: 23, ...})
```

er maintainability of templates.
* *0.1.0* (2013/11/20): 
	* Forked code and made it fit for bower.
	* Add build tasks for grunt.
	* Some bug fixes, to run tests again.

# Thanks for assistance and contributions

* Garito (https://github.com/Garito)
