---
layout: post
title: "Primitives"
date: 2015-10-19
tags: primitives c c++
description: A quick discussion about C++ primitives
---

You may have heard the word "primitive" before in context of computing, but what is a primitive?
A primitive is a built-in type that can be used on its own or as part of a larger, more complex user-defined object (a class).

So what is an example of a primitive? 
Well, an `int` is a primitive, as is a double, float, char, bool.
Here is a list of primitives for C++:

```cpp
int
float
double
char
bool
wchar_t
void
```

What's important to note is that everything in a computer is bytes - everything.  This means that each primitive is just a different interpretation of a series of bytes.  As an example let's take a look at this C++ code:
{% highlight cpp %}
std::cout << sizeof(int) * CHAR_BIT << std::endl;
{% endhighlight %}

This code will output how many bits comprise the primitive `int`.  In this case the output is 32.
But how did we arrive at this number?  Let's break the code down:
The two keywords to note here are `sizeof` and `CHAR_BIT`; cout and endl are just used for writing to the console.
The sizeof operator is a keyword that when used on a datatype will return the byte size of that object.  In the case of an integer this bit of code:
`sizeof(int)` 
Will return the number 4.  An integer is made up of 4 bytes, and we can see that a byte is 8 bits, so the integer must be 32 bits!  :D

This is all looking good, but what if we are working on a system where a byte **is not** 8 bits?  The best way to be sure is to use the numeric limit `CHAR_BIT`, which provides the number of bits in a byte.  


Let's look at the size of a float:
```cpp
std::cout << sizeof(float) * CHAR_BIT << std::endl;
```
This code again says 32 bits.  So does that mean a float is the same as an integer?  In memory they do share the same size, however a float is interpreted differently so as to provide a fractional value.  Floats are calculated using the [IEEE 754](https://en.wikipedia.org/wiki/IEEE_floating_point) standard.
