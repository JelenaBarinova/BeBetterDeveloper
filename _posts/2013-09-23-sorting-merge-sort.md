---
layout: post
title: "Sorting: Merge Sort"
date: 2013-09-23 22:03:20
tags:
  - Merge Sort
id: 233
categories:
  - Algorithms
  - Sorting
---

In this post I will implement well known [divide and conquer](http://en.wikipedia.org/wiki/Divide_and_conquer_algorithm) sorting algorithm – [Merge Sort](http://en.wikipedia.org/wiki/Merge_sort). The idea of the algorithm is as follows:

*   recursively divide unsorted list into two sub-lists
*   continue until each sub-list contains 1 element
*   recursively merge them back in the right order

We can visualize merge sort algorithm by sorting following list [3 5 4 7 2 1]. I’ll use colors to specify <span style="color: #0000ff;">current split list</span> and <span style="color: #ff0000;">current merge elements</span>.

Split Iteration #1
<span style="color: #0000ff;">[3 5 4 7 2 1]</span> → <span style="color: #0000ff;">[3 5 4]</span> <span style="color: #0000ff;">[7 2 1]
</span><span style="color: #0000ff;">[3 5 4]</span> [7 2 1] → <span style="color: #0000ff;">[3]</span> <span style="color: #0000ff;">[5 4]</span> [7 2 1]
<span style="color: #0000ff;">[3]</span> [5 4] [7 2 1] → <span style="color: #0000ff;">[3]</span> [5 4] [7 2 1]

Merge Iteration #1
[<span style="color: #ff0000;">3</span>] [5 4] [7 2 1] → [<span style="color: #ff0000;">3</span>] [5 4] [7 2 1]

Split Iteration #2
[3] <span style="color: #0000ff;">[5 4]</span> [7 2 1] → [3] <span style="color: #0000ff;">[5]</span> <span style="color: #0000ff;">[4]</span> [7 2 1]

Merge Interation #2
[3] [<span style="color: #ff0000;">5</span>] [<span style="color: #ff0000;">4</span>] [7 2 1] → [3] [<span style="color: #ff0000;">4</span> ...
[3] [<span style="color: #ff0000;">5</span>] [4] [7 2 1] → [3] [4 <span style="color: #ff0000;">5</span>] [7 2 1]

Merge Iteration #3
[<span style="color: #ff0000;">3</span>] [<span style="color: #ff0000;">4</span> 5] [7 2 1] → [<span style="color: #ff0000;">3 </span>...
[3] [<span style="color: #ff0000;">4</span> 5] [7 2 1] → [3 <span style="color: #ff0000;">4</span> ...
[3] [4 <span style="color: #ff0000;">5</span>] [7 2 1] → [3 4 <span style="color: #ff0000;">5</span>] [7 2 1]

Split Iteration #3
[3 4 5] <span style="color: #0000ff;">[7 2 1]</span> → [3 4 5] <span style="color: #0000ff;">[7]</span> <span style="color: #0000ff;">[2 1]
</span>[3 4 5] <span style="color: #0000ff;">[7]</span> [2 1] → [3 4 5] <span style="color: #0000ff;">[7]</span> [2 1]

Merge Iteration #4
[3 4 5] [<span style="color: #ff0000;">7</span>] [2 1] → [3 4 5] [<span style="color: #ff0000;">7</span>] [2 1]

Split Iteration #4
[3 4 5] [7] <span style="color: #0000ff;">[2 1]</span> → [3 4 5] [7] <span style="color: #0000ff;">[2] [1]</span>

Merge Iteration #5
[3 4 5] [7] [<span style="color: #ff0000;">2</span>] [<span style="color: #ff0000;">1</span>] → [3 4 5] [7] [<span style="color: #ff0000;">1 </span>...
[3 4 5] [7] [<span style="color: #ff0000;">2</span>] [1] → [3 4 5] [7] [1 <span style="color: #ff0000;">2</span>]

Merge Iteration #6
[3 4 5] [<span style="color: #ff0000;">7</span>] [<span style="color: #ff0000;">1</span> 2] → [3 4 5] [<span style="color: #ff0000;">1</span> ...
[3 4 5] [<span style="color: #ff0000;">7</span>] [1 <span style="color: #ff0000;">2</span>] → [3 4 5] [1 <span style="color: #ff0000;">2</span> ...
[3 4 5] [<span style="color: #ff0000;">7</span>] [1 2] → [3 4 5] [1 2 <span style="color: #ff0000;">7</span>]

Merge Iteration #7
[<span style="color: #ff0000;">3</span> 4 5] [<span style="color: #ff0000;">1</span> 2 7] → [<span style="color: #ff0000;">1</span> ...]
[<span style="color: #ff0000;">3</span> 4 5] [1 <span style="color: #ff0000;">2</span> 7] → [1 <span style="color: #ff0000;">2</span> ...]
[<span style="color: #ff0000;">3</span> 4 5] [1 2 <span style="color: #ff0000;">7</span>] → [1 2 <span style="color: #ff0000;">3</span> ...]
[3 <span style="color: #ff0000;">4</span> 5] [1 2 <span style="color: #ff0000;">7</span>] → [1 2 3 <span style="color: #ff0000;">4</span> ...]
[3 4 <span style="color: #ff0000;">5</span>] [1 2 <span style="color: #ff0000;">7</span>] → [1 2 3 4 <span style="color: #ff0000;">5</span> ...]
[3 4 5] [1 2 <span style="color: #ff0000;">7</span>] → [1 2 3 4 5 <span style="color: #ff0000;">7</span>]

Implementation of the merge sort heavily rely on sort and merge functions:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/mergeSort.js?footer=minimal">
</script>

**Complexity:** O(n·logn).