Node.js
=======

Installation
------------

`https://nodejs.org`

```
node --version
node -v
npm -v
```

```javascript
$ node
>var example = "hello!";
>alert(example);
>.exit
```

Docs 
----

[Document](https://nodejs.org/en/docs/): 

Example
-------

`hello.js`
```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

```
node hello
Server running at http://127.0.0.1:3000/
```

Grunt
-----

Gulp
----
  

