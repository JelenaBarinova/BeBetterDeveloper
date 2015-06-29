---
layout: post
title: "Data Structure: Queue"
date: 2013-06-20
tags:
  - Linked List 
  - Queue
id: 126
categories:
  - Data Structure
---

In this post I will implement another very popular abstract data type – [Queue](http://en.wikipedia.org/wiki/Queue_(abstract_data_type)). Queue is a collection where the first element added to the structure must be the first one to be removed (or [FIFO, First-In First-Out](https://en.wikipedia.org/wiki/FIFO), for short). It is widely used in hardware and software for buffering and [prioritization](http://en.wikipedia.org/wiki/Priority_queue). Typically queue is implemented using (doubly) [linked list](http://www.bebetterdeveloper.com/data-structure-linked-list/) or in some cases using dynamic arrays.

Usually linked lists have following functions:

*   enqueue() – to add new element
*   dequeue() – to remove last element and return its value
*   peak() – to return value of the last element without removing it
*   isEmpty() - to check whether the queue is empty or not
*   length() – to get the number of items in the queue

Based on the previously [described](http://www.bebetterdeveloper.com/data-structure-linked-list/) linked list, implementation of the queue is rather trivial:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/queue.js?footer=minimal">
</script>