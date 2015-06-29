title: "Sorting: Shell Sort"
date: 2013-08-28 22:09:55
tags: 
  - Shell Sort
id: 215
categories:
  - Algorithms
  - Sorting
---

In this post I will implement more advanced sorting algorithm – [Shell Sort](https://en.wikipedia.org/wiki/Shellsort). Shell sort is also known as n-gap insertion sort. Instead of comparing only adjacent pair, shell sort makes several passes and uses various gaps between adjacent elements (ending with the gap of 1 or classical insertion sort). The idea of the algorithm is as follows:

*   calculate gaps by using one of the existing sequences, eg.: Shell’s (⌊n/2<sup>k</sup>⌋), Pratt’s (2<sup>p</sup>3<sup>q</sup>) or in our case – Knuth’s ((3<sup>k</sup> - 1) / 2) as being one of the most popular and due to sequence generation easiness
*   starting from the beginning of the list compare value with every n·gap elements on the left (if any)
*   swap their positions if they are not in the right order
*   continue until element on the left is smaller than current element
*   repeat with the smaller gap

We can visualize shell sort algorithm by sorting following list [3 5 4 7 2 1] using gaps 4 and 1\. I’ll use colors to specify <span style="color: #ff0000;">current adjacent pair</span>.

Iteration #1, **gap 4** : [3 5 4 7 2 1]
[<span style="color: #ff0000;">3</span> 5 4 7 <span style="color: #ff0000;">2</span> 1] → [<span style="color: #ff0000;">2</span> 5 4 7 <span style="color: #ff0000;">3</span> 1]

Iteration #2, **gap 4** : [2 5 4 7 3 1]
[2 <span style="color: #ff0000;">5</span> 4 7 3 <span style="color: #ff0000;">1</span>] → [2 <span style="color: #ff0000;">1</span> 4 7 3 <span style="color: #ff0000;">5</span>]

Iteration #3, **gap 1** : [2 1 4 7 3 5]
[<span style="color: #ff0000;">2 1</span> 4 7 3 5] → [<span style="color: #ff0000;">1 2</span> 4 7 3 5]

Iteration #4, **gap 1** : [1 2 4 7 3 5]
[1 <span style="color: #ff0000;">2 4</span> 7 3 5] → [1 <span style="color: #ff0000;">2 4</span> 7 3 5]

Iteration #5, **gap 1** : [1 2 4 7 3 5]
[1 2 <span style="color: #ff0000;">4 7</span> 3 5] → [1 2 <span style="color: #ff0000;">4 7</span> 3 5]

Iteration #6, **gap 1** : [1 2 4 7 3 5]
[1 2 4 <span style="color: #ff0000;">7 3</span> 5] → [1 2 4 <span style="color: #ff0000;">3 7</span> 5]
[1 2 <span style="color: #ff0000;">4 3</span> 7 5] → [1 2 <span style="color: #ff0000;">3 4</span> 7 5]
[1 <span style="color: #ff0000;">2 3</span> 4 7 5] → [1 <span style="color: #ff0000;">2 3</span> 4 7 5]

Iteration #7, **gap 1** : [1 2 3 4 7 5]
[1 2 3 4 <span style="color: #ff0000;">7 5</span>] → [1 2 3 4 <span style="color: #ff0000;">5 7</span>]
[1 2 3 <span style="color: #ff0000;">4 5</span> 7] → [1 2 3 <span style="color: #ff0000;">4 5</span> 7]

Implementation of the shell sort is heavily based on the insertion sort:

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/sorting/shellSort.js?footer=minimal">
</script>

**Complexity:** O(n<sup>3/2</sup>) using Knuth's sequence.