---
layout: post
title: "Creating multilingual website w/ React & Flux"
subtitle: "Basic steps to build multilingual React website using Flux"
date: 2015-11-20
author: Lena Barinova
tags:
  - JavaScript
  - React
  - Gulp
  - ES2015
  - Flux
  - multilingual
id: 20005
categories:
  - Coding
---

My post on [Getting started w/ React & Mocha](http://www.bebetterdeveloper.com/coding/getting-started-react-mocha.html) just made it up to the Top 1 of all my blog posts, reaching 1000 uniqueue views, so I decided to continue these series.
<img src="{{ site.baseurl }}/img/post_img/rfe-1.png" alt="React and Flux logo" class="right" />


## My target

This time I want to create a simple multilingual website. I need to have:

* source structure and process suitable for mid-sized project
* fast update of UI on language change (desirably without page refresh)
* easy testable solution

I'll use ES6 where it is suitable, I automate dev process using Gulp.

## Result

This is how the final result looks like:

<img src="{{ site.baseurl }}/img/post_img/out.gif" alt="Switch language" />

Working code in [GitHub](https://github.com/JelenaBarinova/react-flux-example).
To check the website, follow this [link](http://jelenabarinova.github.io/react-flux-example/).

## tl;dr

Just download the code and run

~~~
$npm install
~~~

If you are using Visual Studio Code - you can build it using `⇧⌘B` (on Mac), otherwise use:

~~~
$gulp build
~~~

To run a server locally I use [http-server](https://www.npmjs.com/package/http-server):

~~~
$http-server -a localhost -p 8000
~~~

For those, who are in a hurry to get started with Flux you can skip all preparation steps and go straight to [Using Flux]({% post_url 2015-11-20-getting-started-react-flux %}#step-4-flux).

## My actions

To create this multilingual website I followed these steps:

1. [Created simple HTML]({% post_url 2015-11-20-getting-started-react-flux %}#step-1-simple-html)
2. [Created React components with hardcoded content]({% post_url 2015-11-20-getting-started-react-flux %}#step-2-react-components)
3. [Moved content to JSON]({% post_url 2015-11-20-getting-started-react-flux %}#step-3-content-from-json)
4. [Used Flux]({% post_url 2015-11-20-getting-started-react-flux %}#step-4-flux)
5. [Made some refactoring and add tetst]({% post_url 2015-11-20-getting-started-react-flux %}#step-5-refactoring-and-tests)

## Step 1. Simple HTML

So I started by creating my website as a simple HTML, using Bootstrap, to have the basic static page structure, which I could split to the React components later. That's how my _index.html_ look like:
<style type="text/css">
  .gist {width:640px !important;}
  .gist-file
  .gist-data {max-height: 600px; max-width: 640px;}
</style>
<script src="https://gist.github.com/JelenaBarinova/82dbb2570f81395bc2f6.js"></script>

## Step 2. React components

First I installed React and ReactDOM.

~~~
$npm install react react-dom --save
~~~

Then I prepared everything that is needed for jsx and ES2015 transformations:

~~~
$npm install babel gulp browserify vinyl-source-stream babelify babel-preset-es2015 babel-preset-react --save-dev
~~~

For Babel to transform React files and ES2015 - created _.babelrc_ file with these settings:
<script src="https://gist.github.com/JelenaBarinova/1303d2f6a01a35ff01e9.js"></script>


Created gulp file with a build task. Here it is:
<script src="https://gist.github.com/JelenaBarinova/7f6e5e6945a89a6f17a6.js"></script>


Now moving to React. In my page I identify three components:

1. Menu
2. Home section
3. About section

I created these three components, adding additional one to wrap these three. In this step I added everything in one file _app.jsx_ (will refactor it in further steps). So my _app.jsx_ file looks like this:
<script src="https://gist.github.com/JelenaBarinova/7244d61616f3427a8673.js"></script>
Note: when using html in React don't forget to rename class to className.

Added a placeholder for my react components instead of all the html tags in my _index.html_ and added refference to react and react-dom libraries as well as to my app.js file, which is being produced for me after running

~~~
$gulp build
~~~

or `⇧⌘B` (in VSCode on Mac).

So my _index.html_ now is this:
<script src="https://gist.github.com/JelenaBarinova/e0a7a419f161aa7d8362.js"></script>

* browse files in GitHub at [this point](https://github.com/JelenaBarinova/react-flux-example/tree/b4f1d2557efaa593f4dd4558fae75ec3db884da5)

## Step 3. Content from JSON

What I decided to do now is to move all the content text to JSON file and load the text I have created helper API. The main idea behind this is that later this loading from JSON could be replaced by calling real API to retrieve needed data.

This is how my data _content.json_ file looks like:
<script src="https://gist.github.com/JelenaBarinova/8e0a8f5e3a09b2794ec5.js"></script>

This is my helper API, which load JSON into array and then returns it filtered by language.
<script src="https://gist.github.com/JelenaBarinova/aa9ed4e4afcaaa8b80ff.js"></script>

So now I update my React components to use text from my API. I decided to call API method from my wrapper component and then pass down needed parts to child components via _props_. This is my app.jsx:
<script src="https://gist.github.com/JelenaBarinova/279de096b29d412f5b70.js"></script>

In addition I appended _gulpfile.js_ with new task to delete previously generated _app.js_ file. This is how gulpfile.js looks like now:
<script src="https://gist.github.com/JelenaBarinova/be4c3e8dbe599fe06996.js"></script>

For this I needed to install del library:

~~~
$npm install del --save-dev
~~~

## Step 4. Flux

So finaly, all preparation tasks are done and we can move forward and add Flux.
First let's start with installation.

~~~
$npm install flux --save
~~~
I follow the flow that is being recommended by Flux:
<img src="https://facebook.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png" alt="Flux flow" class="right" />
Picture is taken from [Flux manual](https://facebook.github.io/flux/docs/overview.html#content).

Let's map this diagram items with my code. So starting from left to right, I've got two actions:

* initApp - I call this in my app entry point to load content using default language 'en' (I say it's an action on the left, very first box in the diagram)
* switchLanguage - I dispatch this action on click in language menu (I say it's an action above the Store on the diagram)

My _actions.js_ file:
<script src="https://gist.github.com/JelenaBarinova/cded3bd3a79e1466029b.js"></script>

Then I have a dispatcher:
<script src="https://gist.github.com/JelenaBarinova/8c7a5114b7f5341077b8.js"></script>

In my store I hold the content and register some callbacks with dispatcher to be invoked on specific actions. My _store.js_ file:
<script src="https://gist.github.com/JelenaBarinova/f1c17fa8bad12f7bc5f7.js"></script>

And last, but not least - view. So here I have two components that are related to this flow:

* Menu component - invokes SWITCH_LANGUAGE action on menu item click and passes selected language (this covers View -> Action -> Dispatcher -> Store loop on the diagram)
* Page component - listens to the store changes and when change is happening - gets updated content (this covers Upper Action -> Dispatcher -> Store -> View loop on the diagram).

This is my updated Menu component:
<script src="https://gist.github.com/JelenaBarinova/51022402974b0f06b70e.js"></script>

And here it is my Page compoenent:
<script src="https://gist.github.com/JelenaBarinova/5cac4ff430e13622c42f.js"></script>

## Step 4. Refactoring and Tests

I won't be giving any detaled instruction here, but what I did - is refactored my code:

* Changed source file structure
* Split react components to different files
* Added minification step to the gulp task
* Now working on tests, and I think, that they deserve a separate blog post.

The final version of this example may be found on [GitHub](https://github.com/JelenaBarinova/react-flux-example).

I just love how it works you can experience this smooth language change [here](http://jelenabarinova.github.io/react-flux-example/).