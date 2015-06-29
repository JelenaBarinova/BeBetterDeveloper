---
layout: post
title: "Data Structure: Max Priority Queue"
date: 2014-02-15
tags:
  - Binary Heap
  - Priority Queue
id: 266
categories:
  - Data Structure
---

Today I will implement another important abstract data type – [priority queue](http://en.wikipedia.org/wiki/Priority_queue). Priority queues are used:

*   in heap sort
*   to track top N elements in a very long sequence
*   to merge K ordered sequences and produce single ordered sequence

Usually priority queues have following functions:

*   insert() – to add new item with a priority
*   deleteMin() or deleteMax() – to remove an item with min/max priority
*   findMin() or findMax() – to get an item with min/max priority
*   length() – to get the number of items in the priority queue

As a foundation I’ll use in the [last post](http://www.bebetterdeveloper.com/data-structure-binary-heap/) described efficient data structure – binary heap (in fact, max-heap). Overall, priority queue can be seen as a generalization of [stack](http://www.bebetterdeveloper.com/data-structure-stack-array/) and [queue](http://www.bebetterdeveloper.com/data-structure-queue/) data structures. Stack can be implemented as a max priority queue where priority of each inserted element is monotonically increasing and queue – where priority of each inserted element is monotonically decreasing. 

The implementation of max priority queue ([tests](https://github.com/sergejusb/algorithms/blob/master/data-structures/maxPriorityQueue_tests.js)) is almost identical to the max-heap implementation:

<script type="text/javascript" src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/maxPriorityQueue.js?
footer=minimal"></script>

**Complexity**:

*   insert - O(logn)
*   deleteMin/deleteMax - O(logn)
*   findMin/findMax - O(1)