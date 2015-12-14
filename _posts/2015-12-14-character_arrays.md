---
layout: post
title: "Character Arrays and Strings"
date: 2015-10-19
---

Before we look at character arrays, let's first define what an array is.  An array is a sequential list of memory locations ("blocks").  If you declare an array like so:

`int arr[5]`

You will claim five memory "blocks" one after the other; these five blocks are to be interpreted as integers.  Of course someone else could look at where that array is in memory and interpret it completely different, but that's beside the point.
In spite of the seemingly boundless memory that we are now afforded, it is important to understand how that memory is used.  Using less memory is always preferable.

For the array declared above, we are reserving 20 bytes.  An integer is 4 bytes, and we are telling the system that we will have five of them in a row.  Should a less diligent developer exceed that fifth position, they will encounter a *segmentation fault*.


As you might be able to guess, a character array is just as follows:

`char arr[5]`

Now we are reserving 5 bytes, with each character (in C/C++) being a _single byte_, no fancy Unicode.  Imagine a code snipper like so:

{% highlight c %}
char arr[5];
arr[0] = 'h';
arr[1] = 'e';
arr[2] = 'l';
arr[3] = 'l';
arr[4] = 'o';
{% endhighlight %}

We've made a c-string haven't we?  Yay!  If we printed that, we should get "hello", right?  

Nope.  What you've got there is just a series of single-byte blocks one after the other.  *You* know that they spell "hello," but that doesn't mean the system knows that.  How would the system even know when to stop reading?

For further reading, you can take a gander at this `ere [FAQ](http://c-faq.com/aryptr/aryptr2.html).
