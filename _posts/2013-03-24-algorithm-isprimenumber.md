---
layout: post
title: "Algorithm: isPrimeNumber(n)"
date: 2013-03-24
tags:
  - Prime Number
id: 37
categories:
  - Algorithms
  - Math
---

In this post I will implement basic algorithm to detect whether a given number is a prime. In more academic terms – check a number for primality. According to [Wikipedia](http://en.wikipedia.org/wiki/Prime_number) - _a prime number (or a prime) is a natural number greater than 1 that has no positive divisors other than 1 and itself_.

Naïve implementation will test whether n is a multiple of any number between 2 and n-1\. Slightly more optimized version will minimize the test range up-to √n (i.e. between 2 and √n). In this post I’ll use test range between 2 and ⌊n/2⌋ due to the fact calculation of √n itself is more complex than single right shift operation.

**Complexity:** O(n/2) or just O(n).

<script src="http://gist-it.appspot.com/https://github.com/sergejusb/algorithms/blob/master/math/isPrimeNumber.js?footer=minimal">
</script>