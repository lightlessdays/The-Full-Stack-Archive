---
title: "Routing using plain Node.JS"
datePublished: Mon Aug 21 2023 20:37:49 GMT+0000 (Coordinated Universal Time)
cuid: clllc9me8000o0amn6shb97w4
slug: routing-using-plain-nodejs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692821874829/c5ff1a12-aa40-455c-9558-61162e74453d.jpeg
tags: nodejs

---

In the context of Node.js, routing refers to the process of determining how an incoming HTTP request should be handled and which code (usually a function or a set of functions) should be executed to generate the appropriate response. Routing is a fundamental concept in web development and is crucial for building applications with multiple pages, APIs, or endpoints.

Whoa, Whoa!!! That was too much information to take it. Let us break it down. So basically in layman terms routing simply refers to displaying different data for different urls. For example, google.com/images show a different page and google.com/maps show a different one. As simple as that.

Well we will obviously need a package to do routing since we don't want to do anything from scratch. The package we will be using is `url`.

```javascript
const url = require ('url')
```

Now that we have done that, let us build a simple Hello World Server in Node.JS.

```javascript
const http = require('http'); 
const url = require ('url')

http.createServer ((request, response) => { 
    //code for server goes here
  response.writeHead(200, {
      'Content-Type' :
      'text/plain'
  });

 response.write("Hello World");

 response.end();
}).listen(1201);
```

Now we want that instead of Hello World the path after localhost:1201 should be visible. So what do we do? We can replace "Hello World" with `request.url` which returns the path of the page's url.

```javascript
const http = require('http'); 
const url = require ('url')

http.createServer ((request, response) => { 
    //code for server goes here
  response.writeHead(200, {
      'Content-Type' :
      'text/plain'
  });

 response.write(request.url);

 response.end();
}).listen(1201);
```

And now let us run it in the browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692649554818/accb971e-67bf-4b52-a29b-8410be86f570.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692649580412/c1bfca63-ffa1-4c88-a5f0-5880731f847b.png align="center")

Now let us give custom responses using a very simple if else statement. We can alternatively use switch case statement as well.

```javascript
const http = require('http'); 
const url = require ('url')

http.createServer ((request, response) => { 
    //code for server goes here
  

  if(request.url==='/'){
    response.writeHead(200, {
        'Content-Type' :
        'text/plain'
    });
    response.write("This is the homepage.");
  }else if(request.url.length>3 && request.url.charAt(3)==='a'){
    response.writeHead(200, {
        'Content-Type' :
        'text/plain'
    });
    response.write("The third character of the path is alphabet a.");
  }else{
    response.writeHead(404).write("Page Not Found!!!");
  }


 response.end();
}).listen(1201);
```

Now let us look at the above code. Here we take an if statement. If request.url is the homepage, then we display `This is the homepage.`. If request.url has a in the third place, then we display `The third character of the path is alphabet a.`. And finally if we do not find that page, we will display a 404 error Page not Found with a 404 head.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692650070039/f6ebb283-c2e0-4a61-a34f-094ee27d8ff9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692650087217/ae76c884-ebb0-42b1-92ed-b276d86206a2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692650102287/378d3017-240f-4680-b891-70ea9bc9b7f7.png align="center")

Now we know that all of this can get very messy quickly. Hence we have Express.JS to our rescue - but that is for another article.