title: "Sorting: Insertion Sort"
date: 2013-08-18 20:00:36
tags:
  - Insertion Sort
id: 209
categories:
  - Algorithms
  - Sorting
---

In this post I will implement another basic sorting algorithm – [Insertion Sort](https://en.wikipedia.org/wiki/Insertion_sort). The idea of the algorithm is as follows:

*   starting from the beginning of the list compare value with the elements on the left (if any)
*   swap their position if they are not in the right order
*   continue until element on the left is smaller than current element
*   after each iteration elements on the left from the current element are sorted

We can visualize insertion sort algorithm by sorting following list [5 1 4 2 8]. I’ll use colors to specify <span style="color: #ff0000;">current adjacent pair</span> and <span style="color: #99cc00;">already sorted elements</span>.

Iteration #1 : <span style="color: #ff0000;">[5</span> 1 4 2 8]

Iteration #2 : [<span style="color: #99cc00;">5</span> 1 4 2 8]
[<span style="color: #ff0000;">5 1</span> 4 2 8] → [<span style="color: #ff0000;">1 5</span> 4 2 8]

Iteration #3 : [<span style="color: #99cc00;">1 5</span> 4 2 8]
[1 <span style="color: #ff0000;">5 4</span> 2 8] → [1 <span style="color: #ff0000;">4 5</span> 2 8]
[<span style="color: #ff0000;">1 4</span> 5 2 8] → [<span style="color: #ff0000;">1 4</span> <span style="color: #99cc00;">5</span> 2 8]

Iteration #4 : [<span style="color: #99cc00;">1 4 5</span> 2 8]
[1 4 <span style="color: #ff0000;">5 2</span> 8] → [1 4 <span style="color: #ff0000;">2 5</span> 8]
[1 <span style="color: #ff0000;">4 2</span> <span style="color: #99cc00;">5</span> 8] → [1 <span style="color: #ff0000;">2 4</span> <span style="color: #99cc00;">5</span> 8]
[<span style="color: #ff0000;">1 2</span> <span style="color: #99cc00;">4 5</span> 8] → [<span style="color: #ff0000;">1 2</span> <span style="color: #99cc00;">4 5</span> 8]

Iteration #5 : [<span style="color: #99cc00;">1 2 4 5</span> 8]
[1 2 4 <span style="color: #ff0000;">5 8</span>] → [1 2 4 <span style="color: #ff0000;">5 8</span>]

Implementation of the insertion sort is very simple:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/insertionSort.js?footer=minimal">
</script>

Similarly to bubble and selection sorts we have two loops: outer and inner, so the average complexity is similar as well – O(n<sup>2</sup>). For best-case scenario (already sorted elements) insertion sort has better complexity – O(n).

**Complexity:** O(n<sup>2</sup>).