---
layout: post
title: "Character Arrays"
date: 2015-10-19
---

Before we look at character arrays, let's first define what an array is.  An array is a sequential list of memory locations ("blocks").  If you declare an array like so:

`int arr[5]`

You will claim five memory "blocks" one after the other; these five blocks are to be interpreted as integers.  Of course someone else could look at where that array is in memory and interpret it completely different, but that's beside the point.
In spite of the seemingly boundless memory that we are now afforded, it is important to understand how that memory is used.  Using less memory is always preferable.

For the array declared above, we are reserving 20 bytes.  An integer is 4 bytes, and we are telling the system that we will have five of them in a row.  Should a less diligent developer exceed that fifth position, they will encounter a segmentation fault.



For further reading, you can take a gander at this `ere [FAQ](http://c-faq.com/aryptr/aryptr2.html).
