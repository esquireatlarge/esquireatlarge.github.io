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

Before we look at how the algorithm functions, let's take a moment to understand what its complexity means.  The complexity of an algorithm is measured using "Big O" notation, which is different from a certain robot that shoots out from under the ground.  It's a common error to think of complexity as a measure of time, when in reality it is a measure of *scale*.  Even a slow algorithm like bubble sort will perform extremely fast with a small input size, however if the input size is increased, bubble sort starts to take exponentially longer to finish (hence why it's a squared algorithm).

So how does Quick Sort work?  With the fewest words, you choose an element in your array to be your pivot, and then you move all items smaller than the pivot to the left, and all items greater than it to the right.  Repeat with smaller subarrays until the entire array is sorted.  

Now let's see what the code looks like:

{% highlight cpp linenos %}
void quick(int* array, int start, int end)
{
    if(!array)
        return;

    //Print out the array at each recursion.
    for(int i = 0; i < 10; i++)
        std::cout << array[i] << " ";
    std::cout << std::endl;

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

At first glance this might seem pretty heavy, doc.  Let's break it down:

Here is the function signature.
{% highlight cpp %}
void quick(int* array, int start, int end)
{% endhighlight %}
Quick sort is an in situ algorithm, meaning it does not allocate extra space, and thus does not return anything.  The array is sorted as the algorithm progresses, so the parameter "array" is both an input and an output.  The "start" and "end" parameters are only inputs, and they are used to determine which range of the total array to sort.

Here's a safety check as well as some debug output.
{% highlight cpp %}
    if(!array)
        return;

    //Print out the array at each recursion.
    for(int i = 0; i < 10; i++)
        std::cout << array[i] << " ";
    std::cout << std::endl;
{% endhighlight %}
It is good practice to check for any possible edge cases when writing code.  It is possible that the input array could point to NULL, so we should check against that.  The next few lines are just to print what the array looks like at each iteration.


Here's where the meat begins, choosing the pivot value.
{% highlight cpp %}
int pivot = array[(start + end) / 2];
{% endhighlight %}
The pivot value is the number used to determine whether two elements should be swapped.  The goal of quick sort is to move elements larger than this pivot to the right, and elements smaller to the left.  The term "pivot" can be confusing, because it can be interpreted as the physical location in the array which never changes position.  **This is incorrect**, the pivot is just a number, not an array index.


Now the biggest chunk, the loop.

{% highlight cpp %}
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
{% endhighlight %}
Since the goal is to traverse the sub-array, we create two integers which start at the beginning and end of the sub-array, respectively.  Once the start index passes the end index, the loop stops.  
The start index is incremented until it points to an element which is greater than the pivot.  The end index is decremented until it points to an element which is smaller than the pivot.  If these two indices haven't run each other over, then a swap is performed and the indices are once again incremented and decremented.


Now the recursive bit:
{% highlight cpp %}
    if(start < e)
        quick(array, start, e);

    if(s < end)
        quick(array, s, end);
{% endhighlight %}
By the time we reach these lines, the indices have either run each other over, or they've reached the end of the sub-array.  If the end index "e", which marches backwards towards the start, has yet to reach "start", then we can quick sort the sub-array ranging from "start" to "e."
Likewise if the start index "s", which marches forward towards the end of the array "end", has not reached "end", then we can quick sort the sub-array ranging from "s" to "end."  
