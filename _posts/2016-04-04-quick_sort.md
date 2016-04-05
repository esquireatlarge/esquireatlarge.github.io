---
layout: post
title: "Quick Sort"
date: 2016-04-04
tags: quick sort cpp c 
description: A description of the common sorting algorithm
visible: 1
---

Let's discuss sorting algorithms.  Sorting algorithms come in a wide variety of flavors - Wikipedia has a nice [overview](https://en.wikipedia.org/wiki/Sorting_algorithm).  Conceptually, bubble sort is probably the easiest algorithm, since you just iterate across an array multiple times and swap elements two at a time.  Unfortunately this algorithm is not the fastest, it's a _O(n^2)_ algorithm.  Larger scale applications demand faster sorting algorithms.

Enter quick sort, an _O(nlogn)_ algorithm (typical of divide and conquer algorithms).  This algorithm is very commonplace, in fact it comprises one of the stages of the [standard library sort](https://en.wikipedia.org/wiki/Sort_(C%2B%2B)).  This algorithm is typically the "go to" algorithm in an interview when being asked for a faster sort.  Conceptually the algorithm can be confusing at first, but it's actually less code than it's equal-complexity (in the average case) brother, merge sort.

Before we look at how the algorithm functions, let's take a moment to understand what it's complexity means.  The complexity of an algorithm is measured using "Big O" notation, which is different from a certain robot that shoots out from under the ground.  It's a common error to think of complexity as a measure of time, when in reality it is a measure of *scale*.  Even a slow algorithm like bubble sort will perform extremely fast with a small input size, however if the input size is increased, bubble sort starts to take exponentially longer to finish (hence why it's a squared algorithm).

Now let's look at what the code looks like:
{% highlight cpp linenos %}
void quick(int* array, int start, int end)
{
    if(!array)
        return;

    //Print out the array at each recursion.
    for(int i = 0; i < 10; i++)
        std::cout << array[i] << " ";
    std::cout << std::endl;

    //The pivot does not necessarily have to be the middle element of the array.
    //One can even make "end" be the pivot if they wish.
    int pivot = array[(start + end) / 2];

    int s = start;
    int e = end;
    while(s <= e)
    {
        while(array[s] < pivot)
            s++;

        while(array[e] > pivot)
            e--;

        if(s <= e)
        {
            //Perform a swap.  The goal is to bring any values
            //smaller than the pivot to the left, and any values greater than the pivot
            //to the right.
            int temp = array[s];
            array[s] = array[e];
            array[e] = temp;

            s++;
            e--;
        }
    }

    if(start < e)
        quick(array, start, e);

    if(s < end)
        quick(array, s, end);
}
{% endhighlight %}
