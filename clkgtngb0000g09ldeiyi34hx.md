---
title: "What the f*ck is Node.JS and why should I use it?"
datePublished: Mon Jul 24 2023 12:05:54 GMT+0000 (Coordinated Universal Time)
cuid: clkgtngb0000g09ldeiyi34hx
slug: what-the-fck-is-nodejs-and-why-should-i-use-it
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690200314600/2baa9bce-b5a0-480e-b9c8-374b0809eb55.jpeg
tags: web-development, nodejs

---

### 1\. Introduction

"Node.js is an open-source and cross-platform JavaScript runtime environment." This sounds like a cool, straightforward answer. But for a beginner, this definition might raise further questions. So let's break it down and understand what it means.

**1️⃣ Open Source:** Think of Node.js as a big treasure box that's open for everyone to peek inside. Lots of smart people from all over the world gather together to put amazing ideas and secret codes into this box. They share everything, so we all learn and make it even better!

**2️⃣ Cross Platform:** Imagine Node.js is like a friendly ghost that can go anywhere without any problem. It can play happily with any type of computer, whether it's Windows, Mac, or Linux. It's like having a special friend that works on all computers!

**3️⃣ JavaScript Runtime Environment:** Alright, this one's a bit tricky, but don't worry—I've got your back! You know how when you write a super cool recipe, it won't turn into a tasty cake unless you put it in the oven? Well, the oven is like the magic place where your recipe comes to life! Node.js is that magical oven for JavaScript codes. It takes your cool codes and makes them do amazing things outside of just web browsers!

And guess what? Node.js was created by a coding wizard named Ryan Dahl, and it all started in 2008. But hey, we don't need to remember all that! What's important is that Node.js helps us do magical coding and create fantastic things on our computers!

So grab your coding wand (a.k.a. your computer), and let's explore the enchanting world of Node.js together! With Node.js, you can cast coding spells and make your very own awesome web applications!

### 2\. Node.JS versus Browsers

If browsers can run JavaScript code, why do I need Node.JS? Ah, the epic battle between browsers and Node.js! It's like a magical showdown between two powerful wizards—both capable of casting JavaScript spells, but each with unique strengths! Let's uncover their secrets in a way that even Merlin would appreciate! 🧙‍♂️🔮

**1️⃣ Browser Magic:** Imagine browsers as the guardians of a splendid castle called the Document Object Model (DOM). They hold the keys to the kingdom of web pages and can perform all sorts of enchanting operations inside that castle! But, alas, browsers don't know much about the outside world beyond their castle walls.

**2️⃣ Node.js Sorcery:** Now, Node.js is like a cunning trickster who knows the secrets of the entire kingdom! It can interact with the operating system, access files, and do all kinds of fantastic stuff outside of the castle. But, it doesn't have access to the magical DOM castle like the browsers do.

**3️⃣ Window and Global Wizards:** Browsers call their magical global object the "window," where they keep special methods and properties for their castle. On the other hand, Node.js has its special global object called "global," where it stores its secrets!

But wait, there's more! With Node.js, you have the incredible power to choose the version of JavaScript you want to use for your server-side spells. You can wield modern JavaScript features without worrying about any pesky version conflicts! But in the browser, you can't control which version your visitors use to view your magical web app.

So, whether you're in the browser castle, working with the DOM, or outside in the vast realm of Node.js, tinkering with the entire kingdom, remember that both wizards have their unique strengths! Use them wisely, and you'll be a coding wizard capable of crafting extraordinary web experiences for all to behold!

### 3\. Why should you learn Node.JS?

Oh, buckle up, my fellow coding adventurer! Node.js is like a treasure chest filled with amazing gems, and here are just a few dazzling jewels to get you excited:

**1️⃣ One JavaScript to Rule Them All:** Imagine having a superpower that lets you speak the same language with both the front and back of your app! With Node.js, you can work your coding magic using JavaScript for both the client (that's the front-end) and the server (that's the back-end). No need to learn new languages from scratch—you've got JavaScript, your trusty spellbook, to conquer it all!

**2️⃣ Google's Blessing:** Picture this—the heart of Node.js beats with the Chrome V8 engine, which powers Google's in-browser wonders like Gmail! And guess what? Google loves Node.js so much that they invest lots of magic to keep it super fast and powerful. You're riding on a magic carpet powered by the giants of tech!

**3️⃣ The Magical NPM Library:** Behold the treasure trove called NPM—a magical library with over a million packages! Each package is like a spell scroll that contains reusable code. It's like having a whole shelf of powerful potions at your fingertips! Mix and match these packages to create your very own coding concoctions.

Now that we're on the edge of our seats, let's grab our wands (or keyboards) and start our Node.js adventure! We'll summon this incredible power to create our very own "Hello World" program! Get ready to cast your spell, and soon you'll be conjuring web wonders like a true coding wizard!

### 4\. Getting Started with Node.JS

Let's see how you can create your first Node.js application. This section will show you how to run Node.js scripts from the command line.

**1️⃣ Installation**

First, you need to download and install Node.js. There are different ways you can do that. If you are a beginner, I would suggest that you download Node.js from the official website. Here is the link to the official website: [https://nodejs.org/en/download](https://nodejs.org/en/download)

Official packages are available on the website for all major platforms (Windows, macOS, and Linux). Download and install the appropriate package for your system.

**2️⃣ Verifying Installation**

To check the Node.js version, run the command node --version in your terminal. If the installation was successful, you will see the version of Node.js you installed. You should get a response like the screenshot below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690200022912/a2bcc2b7-38a9-4f90-8dc1-d08d994bd2f9.png align="center")

**3️⃣ Creating a Hello World Application**

Let's build a simple `Hello World` app.

Create a new project folder. You can call it `my-project.` Open the project in your code editor. Inside the folder, create an `app.js` file.

Add the following code to `app.js`

```javascript
console.log("Hello World")
```

As you can see, this is JavaScript code.

You can run the script in the command line by running the command `node <fileName>`. In this case, the file name is `app.js`.

Run the following command in your terminal to execute the `Hello world.` program:

```javascript
node app.js
```

You should see the string "Hello world." logged in your terminal like so.

### About the Author

This article was authored by Dhruv Badaya for The Full Stack Archive. He's a full-stack developer with over five years of experience. You can connect with him at [https://dhruvbadaya.com/links](https://dhruvbadaya.com/links).