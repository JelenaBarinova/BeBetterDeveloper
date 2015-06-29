---
layout: post
title: "Sorting: Quick Sort"
date: 2013-10-13 20:16:55
tags:
  - Quick Sort
id: 241
categories:
  - Algorithms
  - Sorting
---

In this, [last](http://www.bebetterdeveloper.com/category/algorithms/sorting/) in the series, post I will implement probably on of the best known sorting algorithm - [Quick Sort](http://en.wikipedia.org/wiki/Quicksort). The idea of the in-place algorithm is as follows:

*   randomize initial list
*   select first element as partition value
*   scan i from left to right so long as current element is less than partition value
*   scan j from right to left so long as current element is more than partition value
*   exchange i-indexed element with j-indexed element
*   repeat until i and j cross
*   exchange first element with j-indexed element
*   split list into two sub-lists bounded by j-indexed partition
*   recursively repeat until list contains one or zero elements

After each iteration when first element is exchanged with j-indexed element following invariant should be valid: elements to left are smaller or equal than partition value and elements to the right are bigger or equal. We can visualize quick sort algorithm by sorting following list [3 5 4 7 2 1]. I’ll use colors to specify <span style="color: #0000ff;">partition value</span>, <span style="color: #99cc00;">current i-indexed element</span> and <span style="color: #ff0000;">current j-indexed element</span>.

Iteration #1
[<span style="color: #0000ff;">3</span> 5 4 7 2 1] → [<span style="color: #0000ff;">3</span> <span style="color: #99cc00;">5</span> 4 7 2 1] → [<span style="color: #0000ff;">3</span> <span style="color: #99cc00;">5</span> 4 7 2 <span style="color: #ff0000;">1</span>] → [<span style="color: #0000ff;">3</span> <span style="color: #99cc00;">**1**</span> 4 7 2 <span style="color: #ff0000;">**5**</span>]
[<span style="color: #0000ff;">3</span> 1 <span style="color: #99cc00;">4</span> 7 2 <span style="color: #ff0000;">5</span>] → [<span style="color: #0000ff;">3</span> 1 <span style="color: #99cc00;">4</span> 7 <span style="color: #ff0000;">2</span> 5] → [<span style="color: #3366ff;">3</span> 1 **<span style="color: #99cc00;">2</span>** 7 <span style="color: #ff0000;">**4**</span> 5]
[<span style="color: #3366ff;">3</span> 1 2 <span style="color: #99cc00;">7</span> <span style="color: #ff0000;">4</span> 5] → [<span style="color: #3366ff;">3</span> 1 2 <span style="color: #ff0000;">7 </span>4 5] → [<span style="color: #3366ff;">3</span> 1 <span style="color: #ff0000;">2</span> <span style="color: #99cc00;">7</span> 4 5] → [**2** 1 **<span style="color: #0000ff;">3</span>** 7 4 5]

Iteration #2
[ [<span style="color: #0000ff;">2</span> 1] 3 [7 4 5] ] → [ [<span style="color: #0000ff;">2</span> <span style="color: #99cc00;">1</span>] 3 [7 4 5] ] → [ [<span style="color: #0000ff;">2</span> <span style="color: #ff0000;">1</span>] 3 [7 4 5] ] → [ [**1** **<span style="color: #0000ff;">2</span>**] 3 [7 4 5] ]

Iteration #3
[ [<span style="color: #0000ff;">1</span>] [2] 3 [7 4 5] ] → [<span style="color: #0000ff;">1</span> [2] 3 [4 7 5] ]

Iteration #4
[1 [<span style="color: #0000ff;">2</span>] 3 [7 4 5] ] → [1 <span style="color: #0000ff;">2</span> 3 [7 4 5] ]

Iteration #5
[1 2 3 [<span style="color: #0000ff;">7</span> 4 5] ] → [1 2 3 [<span style="color: #0000ff;">7</span> <span style="color: #99cc00;">4</span> 5] ] → [1 2 3 [<span style="color: #0000ff;">7</span> 4 <span style="color: #99cc00;">5</span>] ] → [ 1 2 3 [<span style="color: #0000ff;">7</span> 4 <span style="color: #ff0000;">5</span>] ] → [1 2 3 [**5** 4 **<span style="color: #0000ff;">7</span>**] ]

Iteration #6
[1 2 3 [<span style="color: #0000ff;">5</span> 4] 7] → [1 2 3 [<span style="color: #0000ff;">5</span> <span style="color: #99cc00;">4</span>] 7] → [1 2 3 [<span style="color: #0000ff;">5</span> <span style="color: #ff0000;">4</span>] 7]  → [1 2 3 [**4** **<span style="color: #0000ff;">5</span>**] 7]

Iteration #7
[1 2 3 [<span style="color: #0000ff;">4</span>] [5] 7] → [1 2 3 <span style="color: #0000ff;">4</span> [5] 7]

Iteration #8
[1 2 3 4 [<span style="color: #0000ff;">5</span>] 7] → [1 2 3 4 <span style="color: #0000ff;">5</span> 7]

For the sake of easiness I'll skip list randomization step. Implementation of the quick sort heavily rely on sort and partition functions:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/quickSort.js?footer=minimal">
</script>

**Complexity:** O(n·logn).