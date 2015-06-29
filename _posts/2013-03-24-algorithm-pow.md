---
layout: post
title: "Algorithm: Pow(n, exp)"
date: 2013-03-24
tags:
  - Exponent
  - Pow
id: 49
categories:
  - Algorithms
  - Math
---

In this post I will implement basic algorithm to raise floating point number (also known as base) to integer power (also known as exponent). In academic world this process usually referred as [Exponentiation](http://en.wikipedia.org/wiki/Exponentiation). The most naïve implementation is based on the definition of x<sup>y</sup>, i.e. repetitive y-time multiplication of x.

**Complexity**: O(n).

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/math/pow_naive.js?footer=minimal">
</script>

This implementation can be optimized by using following exponentiation properties:

*   b<sup>m</sup> = b · b<sup>m-1</sup>
*   b<sup>m+n</sup> = b<sup>m</sup> · b<sup>n</sup>
*   b<sup>m·n</sup> = (b<sup>m</sup>)<sup>n</sup>
In other words, given 2<sup>7</sup> we can calculate the result as follows:

2<sup>7</sup> = 2 · 2<sup>6</sup> = 2 · 2<sup>2+4</sup> = 2 · 2<sup>2</sup> · 2<sup>4</sup> = 2 · 2<sup>2</sup> · 2<sup>2·2</sup> = 2 · 2<sup>2</sup> · (2<sup>2</sup>)<sup>2</sup>

As you can see, instead of 7 iterations now we have only 3.

**Complexity:** O(log n).

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/math/pow.js?footer=minimal">
</script>