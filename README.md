# AppJS

![AppJS](https://github.com/milani/appjs/raw/master/appjs.png "AppJS") AppJS is an SDK to develop desktop applications using node. Or at least
it is going to be!

The goal is to facilitate native app development using
tools every developer is familiar with nowadays: HTML/CSS/JS

_Attention:_ You should not use AppJS before we bump version to 
v0.1.0, it is under heavy development.

# How to install

AppJS uses CEF shared library. You need to have CEF library in your
library path. You need to change path to libcef in bindings.gyp to
be able to compile and use appjs.

_libcef.so included in the repo is only tested under Ubuntu 11.10_

# How to use

There is an example in repo that shows all features implemented.

Here is a simple one:

	var appjs = require('appjs');

	var window;

	// Initialize appjs.
    var app = appjs.init();

    // Called when page load finishes.
    app.on("ready",function(){
	  console.log("Event Ready called");

	  // Runs a script in browser context.
	  window.runInBrowser(function(){
	    var body = document.body;
	    body.style.color="#f60";
	  });

	  // Show created window ( see below )
	  window.show();
	});

	// Called when webview needs to load 
	// a resource of type appjs://
	app.on("route",function(req,callback){
	  // req.url and req.method are available
	  if(req.url == "appjs://app/") {
	  	callback("text/html",
	    	"<html>\
	    		<head><title>Hello world</title></head>\
	    		<body>Hello World</body>\
	    	</html>");
	  }
	});

	// Creates a new window. Its invisible until window.show() get called.
    window = app.createWindow("appjs://app/",{autoResize:false});

You should see something like:

![Hello World](https://github.com/milani/appjs/raw/master/example/output.png "Hello World")

## Thanks to

* Brandon Benvie: He helps me with CEF.
* Ali Farhadi: He helps me with AppJS.

# License

Copyright (c) 2012 Morteza Milani and other AppJS contributors

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.