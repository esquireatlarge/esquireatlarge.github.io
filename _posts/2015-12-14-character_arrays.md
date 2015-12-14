---
layout: post
title: "Character Arrays and Strings"
date: 2015-12-14
---

Before we look at character arrays, let's first define what an array is.  An array is a sequential list of memory locations ("blocks").  If you declare an array like so:

`int arr[5]`

You will claim five memory "blocks" one after the other; these five blocks are to be interpreted as integers.  Of course someone else could look at where that array is in memory and interpret it completely different, but that's beside the point.
In spite of the seemingly boundless memory that we are now afforded, it is important to understand how that memory is used.  Using less memory is always preferable.

For the array declared above, we are reserving 20 bytes.  An integer is 4 bytes, and we are telling the system that we will have five of them in a row.  Should a less diligent developer exceed that fifth position, they will encounter a *segmentation fault*.


As you might be able to guess, a character array is just as follows:

{% highlight cpp %}
char arr[5]
{% endhighlight %}

Now we are reserving 5 bytes, with each character (in C/C++) being a _single byte_, no fancy Unicode.  Imagine a code snippet like so:

{% highlight c linenos %}
char arr[5];
arr[0] = 'h';
arr[1] = 'e';
arr[2] = 'l';
arr[3] = 'l';
arr[4] = 'o';
{% endhighlight %}

We've made a C-string haven't we?  Yay!  If we printed that, we should get "hello", right?  

Nope.  What you've got there is just a series of single-byte blocks one after the other.  *You* know that they spell "hello," but that doesn't mean the system knows that.  How would the system even know when to stop reading?
The cherry on top which will give us a C-string is the _null terminator_.  The null terminator denotes the end of a C-style string, and looks like:

`\0`

That's a single character, by the way, not two.  This character (which you'll notice is a zero value, similar to how 'a' is 97) tells the system not to read any further.  One might question why this is necessary when we already specified the size of our array to be five, why keep reading after that?
It's true that you know the size of this array, but in practical applications one might not know this size, and even if you did a user's input might not always fill up the buffer.  To that end, the null terminator serves as a _sentinel value_ that lets us know when there is no more data to read.

Let's revise our earlier example:

{% highlight cpp linenos %}
char arr[6];
arr[0] = 'h';
arr[1] = 'e';
arr[2] = 'l';
arr[3] = 'l';
arr[4] = 'o';
arr[5] = '\0';

printf("%s", arr);

{% endhighlight %}

You should see the word "hello" printed now. 

For further reading, you can take a gander at this `ere [FAQ](http://c-faq.com/aryptr/aryptr2.html).



[//]: # (http://stackoverflow.com/questions/4823468/comments-in-markdown)
[//]: # (http://daringfireball.net/projects/markdown/syntax#code)
[//]: # (http://jekyllrb.com/docs/posts/)
