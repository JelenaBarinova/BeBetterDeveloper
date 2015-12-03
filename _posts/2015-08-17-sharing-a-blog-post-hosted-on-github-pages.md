---
layout: post
title: "Sharing a blog post hosted on GitHub Pages"
subtitle: "What to do when you get errors in FB Open Graph Object Debugger"
date: 2015-08-17
author: Lena Barinova
tags:
  - gh-pages
  - Jekyll
  - open graph meta tags
  - Error parsing input URL
  - fb debugger
  - social sharing
id: 20003
categories:
  - Deployment
---

I am hosting all of my personal blogs on [GitHub Pages](https://pages.github.com/) now (here are some reasons why: ['Static HTML is the new black'](http://bebetterleader.com/coding/why-did-i-go-static.html)). With it comes a challenge when I try to share new posts on social media.

I want to have a nice share dialog with description and image of my blog post. Like so:

<img src="{{ site.baseurl }}/img/post_img/fbog-share-dialog.png" alt="Share dialog" class="right" />

In order to achive this, I had to add some code to my Jekyll templates and implement some workarounds with urls and domain configuration. That's how I did it.

First, I added meta tag generation to a head part of my post html:
<script src="https://gist.github.com/LenaBarinova/c63a40854bcd0569a9a6.js"></script>

I get all the open graph meta tags being generated as FB and other social media systems expect it to:

<script src="https://gist.github.com/LenaBarinova/1ef9ae8a8322e3397051.js"></script>

But once I try to share my blog post or scrape url with [Open Graph Object Debugger](https://developers.facebook.com/tools/debug/og/object/) I get `Error parsing input URL, no data was cached, or no data was scraped.`:

<img src="{{ site.baseurl }}/img/post_img/fbog-error.png" alt="Error parsing input URL, no data was cached, or no data was scraped." class="right" />

After spending some time searching for the reasons why this is happening, I found that, Github sometimes return a 302 (Redirect status code) instead of a 200 (OK) in order to avoid DDoS attacks. Same issue is described in this [blog post](http://www.rovrov.com/blog/2014/11/11/github-pages-302-redirect/).

To fix it, in addition to GitHub's IPs I've added `www` subdomain through `CNAME` pointing to my GitHub address `lenabarinova.github.io` in my domain configuration.

<img src="{{ site.baseurl }}/img/post_img/fbog-domain-config.png" alt="Domain configuration" class="right" />

Now I use url with `www` prefix when I want to share my blog post on social media and it works just fine - I get desirable share dialog:

<img src="{{ site.baseurl }}/img/post_img/fbog-fixed.png" alt="Scraper works" class="right" />

With this workaround I can share my posts using nice summary and image in a share dialog.

----


#### Update 10/17/2015

By the way in my `gh-pages` branch on a GitHub I have `CNAME` configured using subdomain + domain, like this: `www.bebetterdeveloper.com`

<img src="{{ site.baseurl }}/img/post_img/fblog-cname.png" alt="CNAME" class="right" />
