# Core Knwl.js

This repo is a fork from Knwl.js. It just intends to give a ready for adding
your plugins repo. It drops the default and experimental plugins from the
original repo, so that you do not pollute your project with plugins you do not
need.

Knwl.js is a Javascript library that parses through text for you name it what (e.g. dates, times, phone numbers, emails, places, and more). 

Parser plugins are what make Knwl.js tick and give it new parsing abilities.  
If you're interested in developing plugins for Knwl.js, ```./plugin_development.md``` is a great place to start.

## Installation

Installation instructions are specific to whether you want to run Knwl.js in the browser, or on the server with Node.js.

###For Node.js

#### Install using ```npm```:

```console
npm install knwl.js
```

1. Load the ```knwl``` module using ```require()``` and create a new Instance.

```javascript
var Knwl = require("./knwl.js");

var knwlInstance = new Knwl('english');
```

You can optionally specify a language in the first parameter. This helps plugins identify and better suit particular languages.

2. Load a parser plugin.

```javascript
knwlInstance.register('your_plugin', require('./your_plugins/your_plugin'));
```

The first parameter is the desired label for the plugin. The second parameter is a ```require()``` call to load the plugin.

###For the Browser

**Note: A packaged version of Knwl.js for the browser with default plugins is available in the ```./dist``` directory.**

These steps require the ```npm``` package.

1. Run ```npm install``` to install dependencies.

2. ```browserify``` may be used to build a Knwl.js project from Node.js for the browser.

Use the following syntax in the terminal:

```console
./node_modules/.bin/browserify script.js knwl.js > output.js
```

The ```script.js``` file is the Node.js file you wish to package for the browser.

## Usage Guide

These steps are the same regardless of whether Knwl.js is running on the server or client.

3. Initiate Knwl.js on a String.

``` javascript
knwlInstance.init("This is a string. This was written on the 2nd of June, of 2015.");
```

This line runs the initial parser functions that
prepare the String for plugins to use. **Plugins
will not function without this method first being called
on the String.**

4. Initiate a plugin to parse the String.

``` javascript
var dates = knwlInstance.get('dates');
```

The first parameter of ```knwl.get()``` is the
name of the parser plugin you're trying to access (make sure you've added the plugin's .js file to the header of the page).
The names of all default parser plugins are provided
towards the end of this document. If you're using
plugins other than the defaults, see their respective
documentation.

Anyways, if the parser plugin is found, ```knwl.get()``` will return
an array of this format:

```javascript
var results = [
{ //result
  //plugin-specific properties
  "preview": "This was written on the 2nd of June of 2015.", //the sentence of rough location of the data from the String
    "found": integer //the position (in words) of the result in the String
}
]
```

For example, here's what is returned from ```knwl.get('dates')``` when called on the previously mentioned String:

```json
[
{
  "year": 2015,
    "month": 6,
    "day": 2,
    "preview": "This was written on the 2nd of June of 2015.",
    "found": 5
}
]
```
