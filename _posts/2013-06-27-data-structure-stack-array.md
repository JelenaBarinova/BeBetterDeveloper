---
layout: post
title: "Data Structure: Stack (dynamic array based)"
date: 2013-06-27 13:14:36
tags:
  - Dynamic Array
  - Stack
id: 159
categories:
  - Data Structure
---

Previously I have already [implemented](http://www.bebetterdeveloper.com/data-structure-stack) linked list based abstract data type Stack. As demanded by a friend of mine [Romualdas](https://twitter.com/rstonkus), in this post I will implement dynamic array based Stack. According to Wikipedia, [dynamic array](https://en.wikipedia.org/wiki/Dynamic_array) is a random access, variable-size list data structure that allows elements to be added or removed. It is based on the idea of fixed array that can be extended (usually doubled) when the capacity is reached while storing the logical size or number of items in the array.

Dynamic array based implementation of stack has several advantages over linked list based:

*   there is no need to store reference to the next element so memory usage is smaller
*   memory is allocated / deallocated in chunks so memory pressure is lower

On the other hand, the cost of adding new items is higher for dynamic array based implementation due to array resizing. The good news is – it’s still constant time.

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/data-structures/stack_array.js?footer=minimal">
</script>

As you can see, when pushing we create new double size array if the original one is full. The really interesting part here is function pop: we are halving the size of array only when it’s ¼ full. Why not ½ full? Imagine sequence of actions:

*   create new stack (array capacity – 1, items – 0)
*   push item (array capacity – 1, items – 1)
*   push item (array capacity – 2, items – 2) ← doubled
*   pop item (array capacity – 1, items – 1) ← halved
*   push item (array capacity – 2, items – 2) ← doubled
*   pop item (array capacity – 1, items – 1) ← halved

By triggering shrinking when an array is ¼ full we amortize the cost of working at the boundaries.