---
title: "Using the (Very) Simple API we built to create a Farm Website"
datePublished: Wed Aug 23 2023 23:24:20 GMT+0000 (Coordinated Universal Time)
cuid: cllod3hdl000509jjbpno3h7q
slug: using-the-very-simple-api-we-built-to-create-a-farm-website
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692831943341/d7aa3445-e015-4d08-81d8-2b6702581d79.jpeg
tags: nodejs

---

You must have used Google. When you use Google, the URL of the homepage looks like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692822026830/33e86bc2-693b-42d8-b819-5f88ce36c18a.png align="center")

But when you search for something on Google, let's say 'Dhruv Badaya', then the URL changes to this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692822065675/ea54a746-c2d0-4e17-bd60-106f1f2d9f97.png align="center")

If you notice carefully then the actual URL of the page is google.com/search. The rest of it are just parameters.

![Parts of a URL parameter
](https://ahrefs.com/blog/wp-content/uploads/2022/07/1-url-parameter-parts.png align="center")

As we can see in the above diagram, ? marks the beginning of URL parameters. After '?' and '&' we have a URL parameter followed by = and value. If there is a space in the value it is replaced by + or %20. Similarly, a lot of characters get replaced by different characters - but we do not have to remember all of that because we have JavaScript to our rescue.

So we have a project that we will be beginning this walkthrough from where we left in Building a (Very) Simple API Walkthrough.

So when we click on one of the cards, we are taken to another URL, which is a 404 page. We want to extract parameters from the URL. How do we do that? Well... let us take a URL.

```javascript
http://localhost:1200/product?id=0
```

Now, let us parse it.

```javascript
    console.log(url.parse(request.url,true))
```

And now, let us look at the console:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692829118913/a7bc2e58-083f-499c-ad14-90170178b539.png align="center")

Now we need to values here query and pathname. We can do this using ES6 syntax by using the exact same names as there are in this dictionary.

```javascript
const {query,pathname} = url.parse(request.url,true);
```

This will create two variables: query and pathname - one containing the query and one containing the pathname. As simple as that.

```javascript
    const {query,pathname} = url.parse(request.url,true);


    //OVERVIEW PAGE
  if(pathname==='/' || pathname==='/overview'){ 
    
    const cardsHtml=productData.map(element=>replaceTemplates(card,element)).join('')
    
    const homePage = overview.replace(/{%PRODUCT_CARDS%}/g,cardsHtml);

    response.writeHead(200,{'Content-type':'text/html'}).end(homePage);

    //API PAGE : DO NOT TOUCH
  }else if(pathname==='/api'){
    response.writeHead(200,{'Content-type':'application/json'});
    
    response.end(data);
  }else if(pathname==='/product'){

    response.writeHead(200,{'Content-type':'text/html'});
    const output=replaceTemplates(product,productData[query.id]);

    response.end(output)

  }
  else{
    response.writeHead(404).end("Error 404: Page Not Found");

  }
```

And now when we run this in the browser, we will see the magic.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692831863270/0b449697-e8b1-47e0-aade-807bcd3d5bb0.png align="center")