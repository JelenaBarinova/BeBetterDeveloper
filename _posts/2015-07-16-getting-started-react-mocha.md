---
layout: post
title: "Getting started w/ React & Mocha"
subtitle: "The very first steps towards building React website testable w/ Mocha"
date: 2015-07-16
author: Jelena Barinova
tags:
  - JavaScript
  - Mocha
  - Gulp
  - ES2015
  - React
id: 20002
categories:
  - Coding
---
  
It took me half day to setup [almost] empty environment for React app development with testing done using Mocha. 
I decided to share my findings here so it would remain. 
<img src="{{ site.baseurl }}/img/post_img/vfd-react-mocha.png" alt="React and Mocha logo" class="right" />

## My target
I wanted to create an environment for further React development. The things that I needed to have:

* source structure, that would be suitable for medium-sized project
* build scripts, that would do all needed transformations, run tests, show the output of my app
* Mocha as a test framework of choice 

For build scripts I prefer to use gulp.

## tl;dr
You can find working code [here](https://github.com/JelenaBarinova/VeryFirstDiv). Just download it and run 

~~~
$npm install
~~~

followed by 

~~~
$npm test
~~~

If you are using Visual Studio Code - you can build it using `⇧⌘B` (on Mac).  

## How I did it
I started with these three stages:

1. Prepare the environment
2. Create first React component
3. Add Mocha tests

## Step 1. Prepare the environment
First install [Node.js](https://nodejs.org/) (if you don't have it yet).
In your project directory (_VeryFirstDiv_ in my case) create _package.json_ file, containing these settings:
<script src="https://gist.github.com/JelenaBarinova/31ce415a9beac855c75e.js"></script>

To download and install all needed dependences open a terminal and run: 

~~~
$npm install
~~~

Create _index.html_ file:
<script src="https://gist.github.com/JelenaBarinova/65ee857afca288768cb6.js"></script>

Create _gulpfile.js_ to configure build steps:
<script src="https://gist.github.com/JelenaBarinova/143d0b90f977e60184fa.js"></script>
I'm using [gulp-load-plugins](https://www.npmjs.com/package/gulp-load-plugins) for easy and fast use of different gulp plugins. It enables me to access all the plugins I have listed in package.json file without 'require' each of them separately. 

Run buil command: either using `⇧⌘B` (from Visual Studio Code on Mac) or command line:

~~~
$gulp build
~~~

And you should get Chrome opened with very first version of our app.

<img src="{{ site.baseurl }}/img/post_img/vfd-1.png" alt="First step result" class="right" />
  
## Step 2. Create first React component
Create a _components_ directory and _component.jsx_ file in it:
<script src="https://gist.github.com/JelenaBarinova/8a04f9f62934b4773b5d.js"></script>

Add this componenet to DOM (I did it in _app.jsx_ file in my project root directroy _VeryFirstDiv_)
<script src="https://gist.github.com/JelenaBarinova/2d3096930e0f739ab7e5.js"></script>

Add aditional step 'browserify' in build process to have "require('modules')" in browser. I use [gulp-browserify](https://www.npmjs.com/package/gulp-browserify) module. This is our _gulpfile.js_ with new 'browserify' step added:
<script src="https://gist.github.com/JelenaBarinova/912880187a6b55b83b5d.js"></script>

Run build task and we can see our React component in a browser.

<img src="{{ site.baseurl }}/img/post_img/vfd-2.png" alt="Second step result" class="right" />

## Step 3. Adding first Mocha test
This was the trickiest step for me. I found a couple of good articles on the topic. These are my favourite:

* [Isomorphic Server & Browser Side Rendering with React (in 3 parts)](https://github.com/jesstelford/react-isomorphic-boilerplate)
* [Testing React Web Apps with Mocha (in 2 parts)](http://www.hammerlab.org/2015/02/14/testing-react-web-apps-with-mocha/)
* [Testing React Components](http://www.asbjornenge.com/wwc/testing_react_components.html)

Ok, let's begin.
First, we need to install [Mocha](http://mochajs.org/). There are two ways you can do it (apply same instructions to futher installations as well): you can either install needed module from command line, for example 

~~~
$npm install mocha
~~~

or add it to _package.json_ dependencies list and run 

~~~
$npm install
~~~

I prefer the second option, this way you keep track of all used modules and if needed you can install all dependences from zero. 

Create test directory and a first _empty-test.js_, which just asserts true all the time.
<script src="https://gist.github.com/JelenaBarinova/a5a34db9c6a9cf8ccb38.js"></script>

You can try whether it works just running Mocha from command line from you project root folder: 

~~~
$mocha
~~~

You shoud get this output:

<img src="{{ site.baseurl }}/img/post_img/vfd-3.png" alt="Third step result" class="right" />

Now let's add test running step in our gulp configuration.
For this I used [gulp-shell](https://www.npmjs.com/package/gulp-shell) - a command line interface for gulp.

Now add a new 'test' step in _gulpfile.js_ to run mocha:
<script src="https://gist.github.com/JelenaBarinova/7d65aec1091f2ded3063.js"></script>

Before moving on to testing our React component, we need to take care of couple of things.

__First__ - DOM mocking. You can find very good explanation about how to mock DOM in this [blog post](http://www.asbjornenge.com/wwc/testing_react_components.html).
To follow this example we need to install [jsdom](https://github.com/tmpvar/jsdom) and [mocha-jsdom](https://github.com/rstacruz/mocha-jsdom). 
I've created _dom-mock.js_ file.
<script src="https://gist.github.com/JelenaBarinova/fab84f93dae04ca4123a.js"></script>

__Second__ - create a file named mocha.opts in test directroy, add this line to it: 

~~~
--compilers js:babel/register --recursive
~~~ 

I found this reading this [post](https://github.com/jesstelford/react-testing-mocha-jsdom) and install [babel](https://babeljs.io/).

And finally - the test! I've created _component-test.js_ file in test directory:
<script src="https://gist.github.com/JelenaBarinova/c4fd4c4cdad19b28fe0f.js"></script>

Run build. Hurray! The test is passing:

<img src="{{ site.baseurl }}/img/post_img/vfd-4.png" alt="Fourth step result" class="right" />
  
You can also configure test running in your _package.json_ - to run tests from command line using: 

~~~
$npm test
~~~

After this addition our _package.json_ looks like this:
<script src="https://gist.github.com/JelenaBarinova/085b9e9c727f166df806.js"></script>

## ECMAScript 2015
If you are plannig to use ECMAScript 2015, you might want to consider installing gulp-babel to tranform your ECMAScript 2015 code to ECMAScript 5 for your browser to understand it. Just add 'es2015' task in _gulpfile.js_:
<script src="https://gist.github.com/JelenaBarinova/8fd92aee1786dc774a9d.js"></script>
