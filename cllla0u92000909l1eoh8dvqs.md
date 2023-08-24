---
title: "Creating and Deploying our first Node.JS Server"
datePublished: Mon Aug 21 2023 19:35:00 GMT+0000 (Coordinated Universal Time)
cuid: cllla0u92000909l1eoh8dvqs
slug: creating-and-deploying-our-first-nodejs-server
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692646463014/92e61005-545f-4c36-acb1-332b530927c7.jpeg
tags: web-development, nodejs, backend, full-stack-development

---

Originally published at: [https://www.crookshanksacademy.com/post/creating-and-deploying-our-first-node-js-server](https://www.crookshanksacademy.com/post/creating-and-deploying-our-first-node-js-server)

In this article, we will be creating our first web server. First of all, make sure that you have Node.JS installed in your system. You can do this by running the following in your command line prompt -

```bash
node --version
```

In this article, we'll create an HTTP server listening on port 1337, which sends Hello, World! to the browser. Note that, instead of using port 1337, you can use any port number of your choice which is currently not in use by any other service.

We will be using the http module of Node.js to create this server. The http module is a Node.js *core module*. So what is a Node.JS core module? A core module is a module included in Node.js's source, that does not require installing additional resources.

First of all, let us load the module. We can start by creating a JavaScript file by the name index.js. Then we can add the following code to load the module -

```javascript
const http = require('http');
```

Now we can start creating the server. The http module provides the functionality to create an HTTP server using the createServer method.

```javascript
http.createServer((request, response) => { 
       //code for server goes here
});
```

As we can see that it takes two variables which are request and response. The request is the data that is received from the server. The response is the data that is sent to the server. You can name the variables anything you want but let us keep it request and response only.

Next, we can tell the browser that everything is okay by using the 200 Status Code. Now what are Status Codes? HTTP status codes are three-digit responses from the server to the browser-side request. This is just a short definition. We will be covering Status Code probably in a different article. For now, let us focus on the task at hand. We can also tell the browser what kind of data it is. Since our data will be plain text let us inform the browser that.

```javascript
http.createServer((request, response) => { 
       //code for server goes here
     response.writeHead(200, {
         'Content-Type' :
         'text/plain'
     });
});
```

Next, let us write the announced text to the body of the page.

```javascript
http.createServer((request, response) => { 
       //code for server goes here
     response.writeHead(200, {
         'Content-Type' :
         'text/plain'
     });

    response.write('Hello World');
});
```

Finally, we can tell the server that everything has been sent and end the response cycle.

```javascript
http.createServer((request, response) => { 
       //code for server goes here
     response.writeHead(200, {
         'Content-Type' :
         'text/plain'
     });

    response.write('Hello World');

    response.end();
});
```

Next, we just need to specify the port. This can be done by adding a function at the end of the code.

```javascript
http.createServer((request, response) => { 
       //code for server goes here
     response.writeHead(200, {
         'Content-Type' :
         'text/plain'
     });

    response.write('Hello World');

    response.end();
}).listen(1337);
```

Now that we have done that, we will be able to listen to requests from port 1337. Now we can run the file by the following command:

```javascript
node index.js
```

And now we can go to our browser and type in `localhost:1337` and we will see Hello World being displayed there.

Congratulations! We created and deployed our first Node.js server on the browser.