---
layout: post
title: "Sorting: Bubble Sort"
date: 2013-08-04 18:25:31
tags:
  - Bubble Sort
id: 165
categories:
  - Algorithms
  - Sorting
---

In this post I will implement very basic sorting algorithm – [Bubble Sort](http://en.wikipedia.org/wiki/Bubble_sort). The idea of the algorithm is very trivial:

*   starting from the beginning of the list compare every adjacent pair
*   swap their position if they are not in the right order
*   after each iteration the last element is the biggest in the list
*   after each iteration one less element is needed to be compared
*   continue until there are no more elements left to be compared

We can visualize bubble sort algorithm by sorting following list [5 1 4 2 8]. I’ll use colors to specify <span style="color: #ff0000;">current adjacent pair</span> and <span style="color: #99cc00;">already sorted elements</span>.

Iteration #1 : [5 1 4 2 8<span style="color: #99cc00;">]</span>
[<span style="color: #ff0000;">5 1</span> 4 2 8] → [<span style="color: #ff0000;">1 5</span> 4 2 8<span style="color: #99cc00;">]</span>
[1 <span style="color: #ff0000;">5 4</span> 2 8] → [1 <span style="color: #ff0000;">4 5</span> 2 8<span style="color: #99cc00;">]</span>
[1 4 <span style="color: #ff0000;">5 2</span> 8] → [1 4 <span style="color: #ff0000;">2 5</span> 8<span style="color: #99cc00;">]</span>
[1 4 2 <span style="color: #ff0000;">5 8</span>] → [1 4 2 <span style="color: #ff0000;">5 8</span><span style="color: #99cc00;">]</span>

Iteration #2 : [1 4 2 5 <span style="color: #99cc00;">8</span>]
[<span style="color: #ff0000;">1 4</span> 2 5 <span style="color: #99cc00;">8</span>] → [<span style="color: #ff0000;">1 4</span> 2 5 <span style="color: #99cc00;">8</span>]
[1 <span style="color: #ff0000;">4 2</span> 5 <span style="color: #99cc00;">8</span>] → [1 <span style="color: #ff0000;">2 4</span> 5 <span style="color: #99cc00;">8</span>]
[1 2 <span style="color: #ff0000;">4 5</span> <span style="color: #99cc00;">8</span>] → [1 2 <span style="color: #ff0000;">4 5</span> <span style="color: #99cc00;">8</span>]

Iteration #3 : [1 2 4 <span style="color: #99cc00;">5 8</span>]
[<span style="color: #ff0000;">1 2</span> 4 <span style="color: #99cc00;">5 8</span>] → [<span style="color: #ff0000;">1 2</span> 4 <span style="color: #99cc00;">5 8</span>]
[1 <span style="color: #ff0000;">2 4</span> <span style="color: #99cc00;">5 8</span>] → [1 <span style="color: #ff0000;">2 4</span> <span style="color: #99cc00;">5 8</span>]

Iteration #4 : [1 2 <span style="color: #99cc00;">4 5 8</span>]
[<span style="color: #ff0000;">1 2</span> 4 5 8] → [<span style="color: #ff0000;">1 2</span> 4 5 8]

Iteration #5 : [1 <span style="color: #99cc00;">2 4 5 8</span>]

Implementation of the bubble sort is quit simple:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/bubbleSort.js?footer=minimal">
</script>

As you can see we have two loops: outer and inner. Outer loop is executed for each element (n times) and inner loop is executed for n/2 elements on average. As a result we have O(n<sup>2</sup>/2) or just O(n<sup>2</sup>) complexity.

**Complexity:** O(n<sup>2</sup>).