---
layout: post
title: "Testing React components using Shallow Rendering"
subtitle: "Instructions on how to setup your tests without using DOM"
date: 2015-11-24
author: Jelena Barinova
tags:
  - JavaScript
  - Mocha
  - Gulp
  - ES2015
  - React
  - Shallow rendering
id: 20005
categories:
  - Coding
---

This is a continuation of [Getting started w/ React & Mocha](http://www.bebetterdeveloper.com/coding/getting-started-react-mocha.html) blog post. Here I'll shortly describe one more alternative how to test a React component.
<img src="{{ site.baseurl }}/img/post_img/react-logo.png" alt="React logo" class="right" />

## Set-up

Code for this example can be found on [GitHub](https://github.com/JelenaBarinova/react-mocha-example/tree/shallow-rendering). After downloading the code, run

~~~
$npm install
~~~

followed by

~~~
$npm test
~~~

or this gulp command:

~~~
$gulp build
~~~

If you are using Visual Studio Code - you can build it using `⇧⌘B` (on Mac).

## Testing

So I have this react component, named _VeryFirstDiv_:
<script src="https://gist.github.com/JelenaBarinova/04649597e425254ad5ae.js"></script>

In my previous post to test it I was creating fake DOM using JSDOM library and then rendering my testable component into this fake DOM (Read more about it [here](http://www.bebetterdeveloper.com/coding/getting-started-react-mocha.html#step-3-adding-first-mocha-test)).

This time I'll only use [React TestUtils add-on](https://www.npmjs.com/package/react-addons-test-utils) and rather new feature of it - [Shallow Rendering](https://facebook.github.io/react/docs/test-utils.html#shallow-rendering).

>Shallow rendering is an experimental feature that lets you render a component "one level deep" and assert facts about what its render method returns, without worrying about the behavior of child components, which are not instantiated or rendered. This does not require a DOM.

In my test I create an instance of Shallow Renderer:

~~~javascript
let renderer = ReactTestUtils.createRenderer();
~~~

Then, render my _VeryFirstDiv_ component using this _renderer_

~~~javascript
renderer.render(<VeryFirstDiv />);
~~~

and get the output:

~~~javascript
myDiv = renderer.getRenderOutput();
~~~

At this point you can check anything you fancy. I'll for example want to test whether it is of a type 'div' and does it have a class named "veryFirstDiv"
Here's my test:
<script src="https://gist.github.com/JelenaBarinova/ee83bdfc9330b14ee6d2.js"></script>

For a comparison, I've created same test as in using DOM version:
<script src="https://gist.github.com/JelenaBarinova/44b3a2a997865777a0b2.js"></script>

## Summary

Testing using Shallow Rendering is faster. You can even notice it on this small example: my test using fake DOM runs for _~50ms_, while using Shallow Rendering test takes only _10ms_. I believe the gain is even more significant on big projects. And as a pleasant side effect it doesn't require additional libraries.

Happy Testing!