title: "Sorting: Selection Sort"
date: 2013-08-11 17:14:51
tags:
  - Selection Sort
id: 179
categories:
  - Algorithms
  - Sorting
---

In this post I will implement another well know sorting algorithm – [Selection Sort](https://en.wikipedia.org/wiki/Selection_sort). The idea of the algorithm is quite simple:

*   divide input list into two parts: sorted (built up from left to right) and unsorted (remaining items to be sorted)
*   initially sorted part is empty and unsorted part contains input list
*   starting from the beginning of the unsorted part find the smallest element in the list
*   swap its position with the left most element in the unsorted part
*   after each iteration move sorted / unsorted boundary by one element to the right

We can visualize selection sort algorithm by sorting following list [5 1 4 2 8]. I’ll use colors to specify <span style="color: #3366ff;">currently smallest unsorted element</span>, <span style="color: #ff0000;">current unsorted element</span> and <span style="color: #99cc00;">already sorted elements</span>.

Iteration #1 : <span style="color: #99cc00;">[</span>5 1 4 2 8]
<span style="color: #99cc00;">[</span><span style="color: #ff0000;">5</span> 1 4 2 8] → <span style="color: #99cc00;">[</span><span style="color: #3366ff;">5</span> <span style="color: #ff0000;">1</span> 4 2 8] → <span style="color: #99cc00;">[</span>5 <span style="color: #3366ff;">1</span> <span style="color: #ff0000;">4</span> 2 8] → <span style="color: #99cc00;">[</span>5 <span style="color: #3366ff;">1</span> 4 <span style="color: #ff0000;">2</span> 8] → <span style="color: #99cc00;">[</span>5 <span style="color: #3366ff;">1</span> 4 2 <span style="color: #ff0000;">8</span>] → <span style="color: #99cc00;">[</span>**5** <span style="color: #3366ff;">1</span> 4 2 8] → <span style="color: #99cc00;">[</span><span style="color: #3366ff;">1</span> **5** 4 2 8]

Iteration #2 : [<span style="color: #99cc00;">1</span> 5 4 2 8]
[<span style="color: #99cc00;">1</span> <span style="color: #ff0000;">5</span> 4 2 8] → [<span style="color: #99cc00;">1</span> <span style="color: #3366ff;">5</span> <span style="color: #ff0000;">4</span> 2 8] → [<span style="color: #99cc00;">1</span> 5 <span style="color: #3366ff;">4</span> <span style="color: #ff0000;">2</span> 8] → [<span style="color: #99cc00;">1</span> 5 4 <span style="color: #3366ff;">2</span> <span style="color: #ff0000;">8</span>] → [<span style="color: #99cc00;">1</span> **5** 4 <span style="color: #3366ff;">2</span> 8] → [<span style="color: #99cc00;">1</span> <span style="color: #3366ff;">2</span> 4 **5** 8]

Iteration #3 : [<span style="color: #99cc00;">1 2</span> 4 5 8]
[<span style="color: #99cc00;">1 2</span> <span style="color: #ff0000;">4</span> 5 8] → [<span style="color: #99cc00;">1 2</span> <span style="color: #3366ff;">4</span> <span style="color: #ff0000;">5</span> 8] → [<span style="color: #99cc00;">1 2</span> <span style="color: #3366ff;">4</span> 5 <span style="color: #ff0000;">8</span>] → [<span style="color: #99cc00;">1 2</span> <span style="color: #3366ff;">4</span> 5 8]

Iteration #4 : [<span style="color: #99cc00;">1 2 4</span> 5 8]
[<span style="color: #99cc00;">1 2 4</span> <span style="color: #ff0000;">5</span> 8] → [<span style="color: #99cc00;">1 2 4</span> <span style="color: #3366ff;">5</span> <span style="color: #ff0000;">8</span>] → [<span style="color: #99cc00;">1 2 4</span> <span style="color: #3366ff;">5</span> 8]

Iteration #5 : [<span style="color: #99cc00;">1 2 4 5</span> 8]

Implementation of the selection sort is quit simple:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/selectionSort.js?footer=minimal">
</script>

As with bubble sort we have two loops: outer and inner. Outer loop is executed for each element (n times) and inner loop is executed for n/2 elements on average. As a result we have O(n<sup>2</sup>/2) or just O(n<sup>2</sup>) complexity.

**Complexity:** O(n<sup>2</sup>).