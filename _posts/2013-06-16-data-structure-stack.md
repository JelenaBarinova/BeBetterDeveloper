---
layout: post
title: "Data Structure: Stack"
date: 2013-06-16 08:00:09
tags:
  - Linked List
  - Stack
id: 118
categories:
  - Data Structure
---

In this post I will implement very popular abstract data type – [Stack](http://en.wikipedia.org/wiki/Stack_(abstract_data_type)). Stack is a collection where the last element added to the structure must be the first one to be removed (or [LIFO, Last-In First-Out](http://en.wikipedia.org/wiki/LIFO_(computing)), for short). It is widely used in hardware including CPU registers. In software it is used for memory allocation, to track active sub-routines ([call stack](http://en.wikipedia.org/wiki/Call_stack)) or to implement parsers and various higher-level algorithms. Typically stack is implemented using [linked list](http://www.bebetterdeveloper.com/data-structure-linked-list/) or in some cases using dynamic arrays.

Usually stack has following functions:

*   push() – to add new element
*   pop() – to remove first element and return its value
*   peek() – to return value of the first element without removing it
*   isEmpty() - to check whether the stack is empty or not
*   length() - to get the number of items in the stack

Based on the previously [described](http://www.bebetterdeveloper.com/data-structure-linked-list/) linked list, implementation of the stack is rather trivial:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/stack.js?footer=minimal">
</script>