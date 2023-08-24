---
title: "Even Node.JS has Hot Restart"
datePublished: Mon Aug 21 2023 19:58:39 GMT+0000 (Coordinated Universal Time)
cuid: clllav96o000l09jp26lo8x1o
slug: even-nodejs-has-hot-restart
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692647898588/65b3bdf2-6c34-4119-b3bd-c2cc0c5292da.jpeg
tags: nodejs

---

If you are a Flutter Developer, you must be aware of Hot Restart. Well... there's an almost similar feature in Node.JS known as nodemon that allows use to Hot Restart our application.

What is Hot Restart? As you build your application, you are going to need to continuously go back and manually run the application from the terminal. That’s not really any fun, and we can and should automate all the things! To have our application automatically reinitialize after we make changes to our JavaScript files, we can install the popular nodemon module to do this for us. Let’s go ahead and add nodemon to our machine.

```bash
npm install nodemon -g
```

Once nodemon is installed, you can now run your applications by typing **nodemon** &lt;filename&gt; instead of **node** &lt;filename&gt;.

What is happening now is that nodemon has put the application in a running state, but it is always monitoring for any changes. If those changes are detected, the application will automatically relaunch and you can watch it in real-time at the terminal. Now we do not need to go re lauch are application everytime we make a change.