requirejs-tpl
=============

This is an AMD loader for [UnderscoreJS micro-templates](http://underscorejs.org/#template) which can be used as a drop-in replacement to [ZeeAgency/requirejs-tpl](http://github.com/ZeeAgency/requirejs-tpl)


## Overview

- Uses the ``_.template()`` engine maintained by the UnderscoreJS team.

- Uses the official ``text`` loader plugin maintained by the RequireJS team.

- You don't have to specify the template file extension (``.html is assumed``, but this is configurable).


Notes:

- Both libraries can be removed at build-time using ``r.js``.

- The extension ``.html`` is assmumed, and this makes loading templates similar to loading JavaScript files with RequireJS (all extensions are assumned).

## Installation

Download UnderscoreJS and RequireJS-text:

- [UndescoreJS](http://underscorejs.org)

- [RequireJS-text](http://requirejs.org/docs/download.html#text)

Typically, you would place them in a ``scripts/libs`` folder then create a ``scripts/main.js`` file to alias them and to shim UndescoreJS:

```
require.config({
  paths: {
    underscore: 'libs/underscore',
    text: 'libs/text'
    tpl: 'libs/tpl'
  },
  shim: {
    'underscore': {
      exports: '_'
    }
  }
});
```

## Usage

Specify the plugin using ``tpl!`` followed by the template file:

```
require(['backbone', 'tpl!template'], function (Backbone, template) {
  return Backbone.View.extend({
    initialize: function(){
      this.render();
    },
    render: function(){
      this.$el.html(template({message: 'hello'}));
  });
});
```

## Customization

You can specify the template file extension in your main.js:

```
require.config({

  // some paths and shims

  tpl: {
    extension: '.tpl' // default = '.html'
  }
});
```

## Optimization

This plugin is compatible with [r.js](http://requirejs.org/docs/optimization.html).

Optimization brings three benefits to a project:

- The templates are bundled within your code and not dynamically loaded which reduces the number of HTTP requests.

- The templates are pre-compiled before being bundled which reduces the work the client has to do.

- You can use the compiled, non-minimized version of the templates to step over the code in a debugger.


The most important build options are:

- ``stubModules: ['underscore', 'text', 'tpl']``


The list of modules to stub out in the optimized file, i.e. the code is replaced with ``define('module',{});`` by ``r.js``

- ``removeCombined: true``

Removes from the output folder the files combined into a build.

## Example

Copy the ``example`` and ``example-build`` folders to your web server (``text`` is not compatible with the ``file://`` protocol and opening ``index.hml`` directly from your browser will not work).

Alternatively, you can use Connect and NodeJS to spin a web server:

- Install ``connect`` using ``npm`` and launch the server with NodeJS:

```
  $ npm install -g connect
  $ node server.js
```

Go to http://localhost:9000/example. Your browser should load:

- index.html

- require.js

- main.js

- tpl.js

- underscore.js

- text.js

- message.html

Go to http://localhost:9000/example-build. Your browser should load:

- index.html

- require.js

- main.js







