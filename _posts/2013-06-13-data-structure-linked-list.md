---
layout: post
title: "Data Structure: Linked List"
date: 2013-06-13
tags:
  - Linked List
id: 80
categories:
  - Data Structure
---

In this post I will implement one of the most fundamental data structure in computer science – [linked list](https://en.wikipedia.org/wiki/Linked_list). Linked list – is a dynamic sequence of linked nodes where each node composed of a datum and a reference to the next node. Lists, stacks, queues and many other data types can be implemented using linked list. There are several types of linked lists:

*   [singly linked list](https://en.wikipedia.org/wiki/Linked_list#Singly_linked_list)
*   [doubly linked list](https://en.wikipedia.org/wiki/Linked_list#Doubly_linked_list)
*   [circular linked list](https://en.wikipedia.org/wiki/Linked_list#Circular_list)

In this post I will implement the most frequent type – singly linked list. Let’s start with the definition of node:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/node.js?footer=minimal">
</script>

Usually linked list has following functions:

*   isEmpty() – to check whether the list is empty or not
*   length() – to get the number of nodes in the list
*   find() – to find existing node by value
*   addAfter(), addBefore() – to add new node after / before the specified node
*   remove() – to remove existing node
In more advance cases linked list can also have functions:

*   addFirst(), addLast() - to add new node at given position
*   removeFirst(), removeLast() - to remove existing node at given position
*   reverse() – to reverse existing nodes
*   copy() – to create deep copy of the existing list
*   merge() – to merge given list with the current one

Instead of the specific functions addFirst(), addLast(), removeFirst() and removeLast() I will implement more generic addFromStart(), addFromEnd(), removeFromStart() and removeFromEnd(), where one can specify the exact position a node has to be added or removed. Also it's worth mentioning, that my implementation heavily relies on a notion of a [dummy (or sentinel) node](https://en.wikipedia.org/wiki/Linked_list#Sentinel_nodes).

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/linkedList.js?footer=minimal">
</script>