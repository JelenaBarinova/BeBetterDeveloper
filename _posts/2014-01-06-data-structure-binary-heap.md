---
layout: post
title: "Data Structure: Binary Heap"
date: 2014-01-06
tags:
  - Binary Heap
  - Dynamic Array
id: 254
categories:
  - Data Structure
---

Today I will implement very efficient data structure – [binary heap](http://en.wikipedia.org/wiki/Binary_heap). Binary heap – is an array-based [complete binary tree](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees) (_binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible_) which satisfies one of the following ordering properties:

*   min-heap – the value of each node is not smaller than value of its parent with smallest element at the root;
*   max-heap – the value of each node is not bigger than value of its parent with biggest element at the root
Binary heap is a foundation for an abstract data type - [priority queue](http://en.wikipedia.org/wiki/Priority_queue), wich I will cover in next post.

Due to the nature of binary heap (complete binary tree) it can be very efficiently implemented using [dynamic array](https://en.wikipedia.org/wiki/Dynamic_array). Items in the array are usually stored starting from index 1, thus allowing very easy navigation through binary heap:

*   for the item with index k its parent index is **k &gt;&gt; 1**
*   for the item with index k children indexes are **k &lt;&lt; 1** and **k &lt;&lt; 1 + 1**

Usually binary heaps have following functions:

*   insert() – to add new item
*   delete() – to remove min or max item (depending on the ordering)
*   length() – to get the number of items in binary heap

To add new item:

*   add the item to the bottom level of the binary heap (as the last possible item)
*   compare added item with its parent
*   if they are in correct order – break
*   else – exchange items and repeat with the parent
![](http://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/Heap_add_step1.svg/300px-Heap_add_step1.svg.png)![](http://upload.wikimedia.org/wikipedia/commons/thumb/1/16/Heap_add_step2.svg/300px-Heap_add_step2.svg.png)![](http://upload.wikimedia.org/wikipedia/commons/thumb/5/51/Heap_add_step3.svg/300px-Heap_add_step3.svg.png)

To delete maximum item (for max-heap) or minimum item (for min-heap):

*   replace the root of the binary heap with the last item on the bottom level
*   compare new root with the biggest (for max-heap) or  smallest (for min-heap) of children
*   if they are in correct order – break
*   else – exchange items and repeat with the selected child
![](http://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Heap_delete_step0.svg/300px-Heap_delete_step0.svg.png)![](http://upload.wikimedia.org/wikipedia/commons/thumb/e/ee/Heap_remove_step1.svg/300px-Heap_remove_step1.svg.png)![](http://upload.wikimedia.org/wikipedia/commons/thumb/2/22/Heap_remove_step2.svg/300px-Heap_remove_step2.svg.png)

Bellow you can find possible implementation of the binary heap ([tests](https://github.com/sergejusb/algorithms/blob/master/data-structures/binaryHeap_tests.js)):

<script type="text/javascript" src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/binaryHeap.js?
footer=minimal"></script>

**Complexity**:

*   insert - O(logn)
*   delete - O(logn)