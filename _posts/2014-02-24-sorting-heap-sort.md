---
layout: post
title: "Sorting: Heap Sort"
date: 2014-02-24 08:00:26
tags:
  - Binary Heap
  - Heap Sort
id: 276
categories:
  - Algorithms
  - Sorting
---

I have already [demonstrated](http://www.bebetterdeveloper.com/data-structure-max-priority-queue/) one of the binary heap usage scenarios – priority queue. Today I want to show another binary heap usage example – heap sort. The algorithm consist of two steps:

*   on the given set of numbers ensure max-heap invariant (_the value of each node is not bigger than value of its parent with biggest element at the root_)
*   while heap is not empty remove first (max) item from the max-heap

The first part is almost identical to the way we [ensured](https://github.com/sergejusb/algorithms/blob/master/data-structures/binaryHeap.js#L20) binary heap invariant during delete operation. In order to make second step space efficient, we need do following things:

*   swap first (max) item with the last one in the max-heap
*   decrease size of the max-heap by 1
*   ensure max-heap invariant starting from the first item

Let's sort items [3 4 1 3 5 1 2]. As always I'll use collors to specify <span style="color: #99cc00;">parent</span>, <span style="color: #0000ff;">child</span> or items to be <span style="color: #ff0000;">swapped</span>:

Step #1

The binary tree constructed from the given items does not conform max-heap invariant:

<pre>     3
   4   1
  3 5 1 2</pre>

To ensure max-heap invariant for the given set we need to take each node in the tree (except leafs) and recursively ensure it is bigger than any of the child nodes. As a reminder, our binary heap stores items starting from index 1, so we need to temporarily add null item at the begining: [null 3 4 1 3 5 1 2]

[null 3 4 <span style="color: #99cc00;">1</span> | 3 5 <span style="color: #0000ff;">1 2</span>]
[null 3 4 <span style="color: #99cc00;">2</span> | 3 5 <span style="color: #0000ff;">1 1</span>]

[null 3 <span style="color: #99cc00;">4</span> 2 | <span style="color: #0000ff;">3 5</span> 1 1]
[null 3 <span style="color: #99cc00;">5</span> 2 | <span style="color: #0000ff;">3 4</span> 1 1]

[null <span style="color: #99cc00;">3</span> <span style="color: #0000ff;">5 2</span> | 3 4 1 1]
[null <span style="color: #99cc00;">5</span> <span style="color: #0000ff;">3 2</span> | 3 4 1 1]
[null 5 <span style="color: #99cc00;">3</span> 2 | <span style="color: #0000ff;">3 4</span> 1 1]
[null 5 <span style="color: #99cc00;">4</span> 2 | <span style="color: #0000ff;">3 3</span> 1 1]

At this point we have binary max-heap:

<pre>     5
   4   2
  3 3 1 1</pre>
Step #2

Swap first (max) item with the last one and ensure max-heap invariant:

[null <span style="color: #ff0000;">5</span> 4 2 3 3 1 <span style="color: #ff0000;">1</span>|]
[null <span style="color: #ff0000;">1</span> 4 2 3 3 1 | <span style="color: #ff0000;">5</span>]
[null <span style="color: #99cc00;">1</span> <span style="color: #0000ff;">4 2</span> 3 3 1 | 5]
[null <span style="color: #99cc00;">4</span> <span style="color: #0000ff;">1 2</span> 3 3 1 | 5]
[null 4 <span style="color: #99cc00;">1</span> 2 <span style="color: #0000ff;">3 3</span> 1 | 5]
[null 4 <span style="color: #99cc00;">3</span> 2 <span style="color: #0000ff;">3 1</span> 1 | 5]

[null <span style="color: #ff0000;">4</span> 3 2 3 1 <span style="color: #ff0000;">1</span> | 5]
[null <span style="color: #ff0000;">1</span> 3 2 3 1 | <span style="color: #ff0000;">4</span> 5]
[null <span style="color: #99cc00;">1</span> <span style="color: #0000ff;">3 2</span> 3 1 | 4 5]
[null <span style="color: #99cc00;">3</span> <span style="color: #0000ff;">1 2</span> 3 1 | 4 5]
[null 3 <span style="color: #99cc00;">1</span> 2 <span style="color: #0000ff;">3 1</span> | 4 5]
[null 3 <span style="color: #99cc00;">3</span> 2 <span style="color: #0000ff;">1 1</span> | 4 5]

[null <span style="color: #ff0000;">3</span> 3 2 1 <span style="color: #ff0000;">1</span> | 4 5]
[null <span style="color: #ff0000;">1</span> 3 2 1 | <span style="color: #ff0000;">3</span> 4 5]
[null <span style="color: #99cc00;">1</span> <span style="color: #0000ff;">3 2</span> 1 | 3 4 5]
[null <span style="color: #99cc00;">3</span> <span style="color: #0000ff;">1 2</span> 1 | 3 4 5]
[null 3 <span style="color: #99cc00;">1</span> 2 <span style="color: #0000ff;">1</span> | 3 4 5]

[null <span style="color: #ff0000;">3</span> 1 2 <span style="color: #ff0000;">1</span> | 3 4 5]
[null <span style="color: #ff0000;">1</span> 1 2 | <span style="color: #ff0000;">3</span> 3 4 5]
[null <span style="color: #99cc00;">1</span> <span style="color: #0000ff;">1 2</span> | 3 3 4 5]
[null <span style="color: #99cc00;">2</span> <span style="color: #0000ff;">1 1</span> | 3 3 4 5]

[null <span style="color: #ff0000;">2</span> 1 <span style="color: #ff0000;">1</span> | 3 3 4 5]
[null <span style="color: #ff0000;">1</span> 1 | <span style="color: #ff0000;">2</span> 3 3 4 5]
[null <span style="color: #99cc00;">1</span> <span style="color: #0000ff;">1</span> | 2 3 3 4 5]

[null <span style="color: #ff0000;">1</span> <span style="color: #ff0000;">1</span> | 2 3 3 4 5]
[null <span style="color: #ff0000;">1</span> | <span style="color: #ff0000;">1</span> 2 3 3 4 5]

[null <span style="color: #ff0000;">1</span> | 1 2 3 3 4 5]
[null | <span style="color: #ff0000;">1</span> 1 2 3 3 4 5]

Finally we remove leading null item and we have sorted items! Implementation ([tests](https://github.com/sergejusb/algorithms/blob/master/sorting/sort_tests.js)) of the heap sort is heavily based on the binary heap implementation:

<script type="text/javascript" src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/heapSort.js?
footer=minimal"></script>

**Complexity**: O(n·logn)