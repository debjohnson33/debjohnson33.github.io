---
layout: post
title:      "Time Complexities"
date:       2020-10-22 09:58:48 +0000
---

A big challenge for me was the part in the week 3 self assessment that asked for an identification of the time complexity for each of the functions listed. I had thought I understood the topic, but was surprised that a few of them were not as intuitive as I thought. Compounding the stress was that this was 1 of 3 parts to the assessment, so time was literally a factor.

So I’m going to go through the process that should be used to figure out time complexities.

First, the innermost operation of the function should be established. An if statement, as an example would be a Constant or O(1) operation. Since we drop constants from our final equation, this really does not affect it much. Working our way out, if the next operation is a loop of some kind that iterates over an array or some other sequence up to ‘n’, then the time complexity goes up to Linear or O(n) since it is visiting each n. If the next operation outside of that first loop is another loop that iterates over an array up to ‘n’ again, then the time complexity is increased up to Quadratic or O(n^2) (n squared). This is because in calculating time complexity, you multiply the n’s, i.e. n * n = n^2. Any further operations in the function could add to this complexity if they come out to Linear. One of the trickier ones to figure out for me is the Logarithmic or O(log n). When looking at a loop that is iterating, if the ‘n’ is being decreased in size each time the loop runs, it is probably Logarithmic. The execution time is increasing, but at a decreasing rate. The other tricky one is the Exponential or O(c^n). An example of this is a function that guesses an n-character long password or the recursive calculation of the fibonacci sequence.

Function example:

```
var bubbleSort = function(array) {
 for (var i = 0; i < array.length; i++) { <--- 2nd for loop iterates to n so O(n)
   for (var j = i + 1; j < array.length; j++) { <--- for loop iterates to n so O(n) (Linear)
     if (array[i] >= array[j]) {   <---Start here if statement/what’s inside is O(1) (Constant)
       var temp = array[i];
       array[i] = array[j];
       array[j] = temp;
     }
   }
 }
 return array;              n * n = n^2 plus the 1
};                            Drop the 1 and you have n^2 (n squared) or Quadratic
```
Fibonacci (Exponential) example:

```
const fibonacci = (n) => {
  if (n <= 1) {
    return n;
  }

  return fibonacci(n-1) + fibonacci(n-2);
}; This is called as many times as needed until base case is met
```

Resources:
https://activelamp.com/blog/development/javascript-introduction-to-time-complexity/

https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course/
