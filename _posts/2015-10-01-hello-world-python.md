---
layout: post
title: "Hello world, Python"
subtitle: "How to setup a run task on VS Code for Python"
date: 2015-10-01
author: Jelena Barinova
tags:
  - Python
  - VSCode
  - Visual Studio Code
  - IDE
  - Mac OS
  - dev environment
id: 20005
categories:
  - Coding
---

Today I started exploring Python. For those who know me - Yes, Python! Bear with me - I've got my solid reasons for that (will share it one day).

In this short blog post I just want to share how I setup my IDE - [Visual Studio Code](https://code.visualstudio.com/) on MacOS to handle my Python adventure.

First, I've installed [Python](https://www.python.org/downloads/).

Then, created `app.py` file with "hello world" code in it and setup VSCode task to run this script: 

1. From a Command pallete (`⇧⌘P`) hit "Configure Task Runner". 
2. In a `task.json` file added this:

<script src="https://gist.github.com/JelenaBarinova/1afd44a8470a511bc5ad.js"></script>

You should change python command path (if not default as mine) as well as `args` according to your setup, I just simply have my whole script in `app.py` file.

Finally, as this is the only task in my VSCode tasks list - it runs on `⇧⌘B`. 

Simple as that!