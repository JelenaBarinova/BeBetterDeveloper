---
layout: post
title: "Serverless system architecture using AWS, React and Node.js"
subtitle: "Hosting a website, running scheduled computations and sending email notifications - all done using AWS services"
date: 2016-01-22
author: Lena Barinova
tags:
  - JavaScript
  - Node.js
  - React
  - Flux
  - ES2015
  - AWS
  - Lambda
  - DynamoDB
  - API Gateway
  - SNS
  - S3
id: 20006
categories:
  - Coding
  - Architecture
---

This post is about my most recent freetime-killer "DIY project" - [Price tracker](http://price-tracker-website.s3-website-us-west-2.amazonaws.com/), which has a beautiful serverless architecture that I want to share with all of your.

The story behind this app: I want to buy some items (such as skiing goggles, or new luggage set, or shoes), I want to get them for the best price and these items are not urgent for me so I can wait for a price drop. But I don't want to hunt for sales and constantly check online stores for price decrease. I've got better things to do :) 

So I've developed a system, which tracks price changes for my desirable products in online stores (which I trust to buy from) and notifies me over the email when price drops.

## Architecture

There are three major parts of the system:

1. [Website]({% post_url 2016-01-22-serverless-system-architecture-using-aws %}#website) - to view the products and recent prices in different shops 
2. [Watcher]({% post_url 2016-01-22-serverless-system-architecture-using-aws %}#watcher) - a job scheduled to scrape online shops and track price changes every couple of hours
3. [Notifier]({% post_url 2016-01-22-serverless-system-architecture-using-aws %}#notifier) - a job to watch changes to the price and notify me over the email when the price drops

In addition to these parts - there is a database to hold all my products, shops and price changes.

##  Technologies

In autumn 2015 I won a $100 AWS credit as a HackersRank prize in an algorithms coding contest and I decided to make a good use of it. So the platform of a choise to build this system is AWS. In addition to that, lately I am focused on everything JavaScript, thus the language of a choise is JavaScript: both for a frontend - React.js and backend - Node.js. 

Here is the architecture:
<img src="{{ site.baseurl }}/img/post_img/pt-architecture.png" alt="Architecture" class="right" /> 

## Implementation

The sources are in Github at [LenaBarinova/PriceTracker](https://github.com/LenaBarinova/PriceTracker). 
Now shortly about how I implemented each of my three major system components.

#### Website

My Website - is a quite simple Single Page Application done in React using Flux pattern to handle UI changes. Website gets information about the products via a REST API implemented through AWS API Gateway, which calls AWS Lamdba function (written in Node.js) to actually get data from database. I use DynamoDB as a database, storing all of my products as JSON objects. UI is built using Bootstrap and some more advanced css styles to create flipping cards effects for products.

Here's how it looks:

<img src="{{ site.baseurl }}/img/post_img/pt-ui.gif" alt="Price Tracker UI" /> 

Tests for UI are written in Mocha. Website is hosted in Amazon S3. For deployment I use Gulp and many Gulp plugins to transpose, convert from ES6, concatenate and minify my JavaScript files, run tests, bundle all together and upload to S3 bucket.

### Watcher

Watcher is AWS Lambda function implemented in Node.js. It queries a database, gets all the products and runs scrapers for each product to retrieve a new price from online stores. Scraper function is specific for each store, it loads shop's html and gets/parses price fields using jQuery selectors. If there is change in price - product is updated with a new price and persisted to DynamoDB.

Watcher is scheduled to run every 4 hours using AWS CloudWatch Events.

### Notifier

One more AWS Lambda function which listens to events in DynamoDB and if there is a price decrease - it sends email notification using AWS SNS service. 

All AWS Lambda functions are written in JavaScript and tested using Mocha. Deployment is as easy as running "gulp deploy" task - it runs tests, gets all dependant node modules, zips all files together and uploads my JavaScript code to AWS as Lamdba functions. 

## Pros and Cons

Though it's nice not to have a server and run everything on different services, and Lambda is a kind of magic, there are some drawbacks to it. In my case it's perfect for Watcher and Notifier, but not that good for a data retrieval from DynamoDB. The problem is that in order to run Lambda function there is a lot of work done in the background (container creation, environment configuration, etc.) before actually running my function, that takes some time. When the task is a background job - it's totally fine, but with UI - it gives me undesirable lag before loading my products for the first time. I don't worry about it now, because I'm the only user of this system and visit this site once a week or so, but if someday there is more users than me, I'll definitely look into it and refactor this part of the system.

Besides this small issue, everything else works as a charm. And with deployment automation - it is a real pleasure to work on this "project".

Happy Architecting!

_P.S.: If you want to hear more about any part of this system - just leave a comment. And if you by any chance would like to try PriceTracker yourself - let me know, I'd be happy to set up it for you._