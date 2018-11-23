# Practical Node.js
```
http://file.allitebooks.com/20151129/Practical%20Nodejs.pdf
https://github.com/azat-co/practicalnode


$ node -v
$ npm -v

$ node

> 1+1
> "Hello"+" "+"World"
> a=1;b=2;a+b
> 17+29/2*7
> f = function(x) {return x*2}
> f(b)


$ node program.js

run inline JavaScript/Node.js—for example, $ node -e "console.log(new Date());".
```
```

```

# Node.js Core Modules核心模組
```
Unlike other programming technologies, Node.js doesn’t come with a heavy standard library. The core modules of
node.js are a bare minimum, and the rest can be cherry-picked via the NPM registry. The main core modules, classes,
methods, and events include the following:
•	 http (http://nodejs.org/api/http.html#http_http)
•	 util (http://nodejs.org/api/util.html)
•	 querystring (http://nodejs.org/api/querystring.html)
•	 url (http://nodejs.org/api/url.html)
•	 fs (http://nodejs.org/api/fs.html)
```

### http (http://nodejs.org/api/http.html)
```
http is the main module responsible for the Node.js HTTP server. The main methods are as follows:
•	 http.createServer(): returns a new web server object
•	 http.listen(): begins accepting connections on the specified port and hostname
•	 http.createClient(): is a client and makes requests to other servers
•	 http.ServerRequest(): passes incoming requests to request handlers
•	 data: emitted when a part of the message body is received
•	 end: emitted exactly once for each request
•	 request.method(): the request method as a string
•	 request.url(): request URL string
•	 http.ServerResponse(): creates this object internally by an HTTP server — not by the user
                     — and is used as an output of request handlers
•	 response.writeHead(): sends a response header to the request
•	 response.write(): sends a response body
•	 response.end(): sends and ends a response body
```
### util (http://nodejs.org/api/util.html)
```
The util module provides utilities for debugging. One method is as follows:
•	 util.inspect(): returns a string representation of an object, which is useful for debugging
        querystring (http://nodejs.org/api/querystring.html)
      The querystring module provides utilities for dealing with query strings. Some of the methods include the following:
•	 querystring.stringify(): serializes an object to a query string
•	 querystring.parse(): deserializes a query string to an object
```
###url (http://nodejs.org/api/url.html)
```
The url module has utilities for URL resolution and parsing. One method is as follows:
•	 parse(): takes a URL string and returns an object
```
### fs (http://nodejs.org/api/fs.html)
```
fs handles file system operations such as reading to and writing from files. 
There are synchronous and asynchronous methods in the library. Some of the methods include the following:
•	 fs.readFile(): reads files asynchronously
•	 fs.writeFile(): writes data to files asynchronously
```
```
There is no need to install or download core modules. To include them in your application, all you need is to use
the following syntax:
var http = require('http');
```
# noncore modules非核心模組
```
A list of noncore modules is found at the following locations:
•	 npmjs.org (https://npmjs.org): for the NPM registry
•	 GitHub hosted list (https://github.com/joyent/node/wiki/Modules): for Node.js modules maintained by Joyent
•	 nodetoolbox.com (http://nodetoolbox.com/): for a registry based on stats
•	 Nipster (http://eirikb.github.com/nipster/): for NPM search tools for Node.js
•	 Node tracking (http://nodejsmodules.org): for a registry based on GitHub stats
```
```
If you want to know how to code your own modules, take a look at the article “Your First Node.js Module3.”

Handy Node.js Utilities
Although the core of the Node.js platform was, intentionally, kept small, it has some essential utilities, including
the following:
•	 Crypto(http://nodejs.org/api/crypto.html): has randomizer, MD5, HMAC-SHA1, and other algorithms
•	 Path(http://nodejs.org/api/path.html): handles system paths
•	 String decoder(http://nodejs.org/api/string_decoder.html): decodes to and from buffer and string types
The method we use throughout is path.join and it concatenates the path using an appropriate folder
separator (/ or \\).
3
http://cnnr.me/blog/2012/05/27/your-first-node-dot-js-module/

### Reading to and Writing from the File System in Node.js
```
Reading from files is done via the core fs module (http://nodejs.org/api/fs.html). There are two sets of reading
methods: async and sync. In most cases, developers should use async methods, such as fs.readFile:

var fs = require('fs');
var path = require('path');
fs.readFile(path.join(__dirname, '/data/customers.csv'), {encoding: 'utf-8'}, function (err, data) {
 if (err) throw err;
 console.log(data);
});

To write to the file, execute the following:
var fs = require('fs');
fs.writeFile('message.txt', 'Hello World!', function (err) {
 if (err) throw err;
 console.log('Writing is done.');
});

```

### Streaming Data in Node.js
```
Streaming data is a phrase that means an application processes the data while it’s still receiving it. 
This feature is useful for extra large datasets such as video or database migrations.
Here’s a basic example of using streams that output the binary file content back:
var fs = require('fs');
fs.createReadStream('./data/customers.csv').pipe(process.stdout);

By default, Node.js uses buffers for streams. For more immersive instruction, take a look at stream-adventure
(http://npmjs.org/stream-adventure) and Stream Handbook (https://github.com/substack/stream-handbook).
```
