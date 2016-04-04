---
layout: post
title: "Quick Sort"
date: 2016-04-04
tags: quick sort cpp c 
description: A description of the common sorting algorithm
visible: 0
---

Let's discuss sorting algorithms.  Sorting algorithms come in a wide variety of flavors - Wikipedia has a nice [overview](https://en.wikipedia.org/wiki/Sorting_algorithm).  Conceptually, bubble sort is probably the easiest algorithm, since you just iterate across an array and swap elements two at a time.  Unfortunately this algorithm is not the fastest, it's a _O(n^2)_ algorithm.  Larger scale applications demand faster sorting algorithms.

Enter quick sort, an _O(nlogn)_ algorithm (typical of divide and conquer algorithms).  
