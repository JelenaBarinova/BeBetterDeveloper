---
layout: post
title: "Getting started w/ React & Mocha"
subtitle: "The very first steps towards building React website testable w/ Mocha"
date: 2015-07-16
author: Lena Barinova
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

_11/23/2015: I updated this blog post as well as the code to support the newest version of React, ReactDOM, ReactTestUtils, Mocha, JSDOM, Babel. The changed are really minor, but may be frustraiting for some. For those, who are interested in how should this code be written using older version of these libs (React 0.13.3, Mocha 2.0.1, JSDOM 3.1.2, Mocha-JSDOM 1.0.0, Babel 5.1.13) please clone this [commit from GitHub](https://github.com/LenaBarinova/react-mocha-example/tree/9b71d468a1b7af5b6366be71a3e0dee9b45e3f37)._

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
You can find working code [here](https://github.com/LenaBarinova/react-mocha-example). Just download it and run

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
In your project directory (_react-mocha-example_ in my case) through Terminal do:

~~~
$npm init
~~~

and follow the instruction. Then run this command to install libraries to setup the working environment:

~~~
$npm install react react-dom babel babel-preset-es2015 babel-preset-react gulp gulp-load-plugins browserify babelify babel-core vinyl-source-stream gulp-open --save-dev
~~~

Now your _package.json_ should look like this:
<script src="https://gist.github.com/LenaBarinova/31ce415a9beac855c75e.js"></script>

Add _.babelrc_ file to your project root with these settings:
<script src="https://gist.github.com/LenaBarinova/23f8af665b0a8b15c855.js"></script>

Create _gulpfile.js_ to configure build steps:
<script src="https://gist.github.com/LenaBarinova/143d0b90f977e60184fa.js"></script>
I'm using [gulp-load-plugins](https://www.npmjs.com/package/gulp-load-plugins) for easy and fast use of different gulp plugins. It enables me to access all the plugins I have listed in package.json file without 'require' each of them separately.

So now everything is ready to start really writing a code. Create _index.html_ file:
<script src="https://gist.github.com/LenaBarinova/65ee857afca288768cb6.js"></script>

Run build command: either using `⇧⌘B` (from Visual Studio Code on Mac) or command line:

~~~
$gulp build
~~~

And you should get Chrome opened with very first version of our app.

<img src="{{ site.baseurl }}/img/post_img/vfd-1.png" alt="First step result" class="right" />

## Step 2. Create first React component
Create a _components_ directory and _component.jsx_ file in it:
<script src="https://gist.github.com/LenaBarinova/8a04f9f62934b4773b5d.js"></script>

Add this componenet to DOM (I did it in _app.jsx_ file in my project root directroy _react-mocha-example_)
<script src="https://gist.github.com/LenaBarinova/2d3096930e0f739ab7e5.js"></script>

Run build task and we can see our React component in a browser.

<img src="{{ site.baseurl }}/img/post_img/vfd-2.png" alt="Second step result" class="right" />

## Step 3. Adding first Mocha test
This was the trickiest step for me. I found a couple of good articles on the topic. These are my favourite:

* [Isomorphic Server & Browser Side Rendering with React (in 3 parts)](https://github.com/jesstelford/react-isomorphic-boilerplate)
* [Testing React Web Apps with Mocha (in 2 parts)](http://www.hammerlab.org/2015/02/14/testing-react-web-apps-with-mocha/)
* [Testing React Components](http://www.asbjornenge.com/wwc/testing_react_components.html)

Ok, let's begin.
First, we need to install [Mocha](http://mochajs.org/). To do it, run npm install command with --save-dev, this way your _package.json_ file will be kept updated with all the dependances you use:

~~~
$npm install mocha --save-dev
~~~

Create test directory and a first _empty-test.js_, which just asserts true all the time.
<script src="https://gist.github.com/LenaBarinova/a5a34db9c6a9cf8ccb38.js"></script>

You can try whether it works just running Mocha from command line from you project root folder:

~~~
$mocha
~~~

You should get this output:

<img src="{{ site.baseurl }}/img/post_img/vfd-3.png" alt="Third step result" class="right" />

Now let's add test running step in our gulp configuration.
For this I used [gulp-mocha](https://www.npmjs.com/package/gulp-mocha) - a gulp plugin wrapper around Mocha.

Now add a new 'test' step in _gulpfile.js_ to run mocha:
<script src="https://gist.github.com/LenaBarinova/7d65aec1091f2ded3063.js"></script>

Before moving on to testing our React component, we need to take care of a couple of things.

__First__ - DOM mocking. You can find very good explanation about how to mock DOM in this [blog post](http://www.asbjornenge.com/wwc/testing_react_components.html).
To follow this example we need to install [jsdom](https://github.com/tmpvar/jsdom) and [mocha-jsdom](https://github.com/rstacruz/mocha-jsdom).
I've created _dom-mock.js_ file (it's a bit different from what is given in the article, I adopted it to be compatible with the newest JSDOM version).
<script src="https://gist.github.com/LenaBarinova/fab84f93dae04ca4123a.js"></script>

__Second__ - install [React TestUtils add-on](https://www.npmjs.com/package/react-addons-test-utils):

~~~
$npm install react-addons-test-utils --save-dev
~~~

And finally - the test! I've created _component-test.js_ file in test directory:
<script src="https://gist.github.com/LenaBarinova/c4fd4c4cdad19b28fe0f.js"></script>

Run build. Hurray! The test is passing:

<img src="{{ site.baseurl }}/img/post_img/vfd-4.png" alt="Fourth step result" class="right" />

You can also configure your _package.json_ - to run tests from command line using npm. For this add test section in your _package.json_ like this:
<script src="https://gist.github.com/LenaBarinova/085b9e9c727f166df806.js"></script>


Now you can run:

~~~
$npm test
~~~

That's it! You can download the latest code for this example from [GitHub](https://github.com/LenaBarinova/react-mocha-example).

Happy Testing!