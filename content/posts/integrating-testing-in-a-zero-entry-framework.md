Title: Test-Driven Development for Novices
Date: 2014-05-10 12:27
Category: Python, Education
Slug: CCBB
Authors: April Wright



## Ch-ch-changes

I've mentioned in passing before that the [CCBB](http://ccbb.biosci.utexas.edu/) is ramping up its [course offerings](http://ccbb.biosci.utexas.edu/training.html). One of the new offerings is the [Big Data in Biology Summer School](http://ccbb.biosci.utexas.edu/summerschool.html). I'm instructing a Python [session](http://ccbb.biosci.utexas.edu/summerschool.html#Python).

I want to try some new things.

## Teaching to the test

We also teach testing in our working group. But it generally comes in quite late, and I've never been super pleased about this. This time around, we're going to start right away with some testing lite. No libraries, just some simple one function, one test programming. 

There's no reason that even a novice programmer can't do test-driven development. If you want your function to return whole numbers to be used in a later computation, anyone can do a simple check that their output is made of integers. If you're looking to return a value between zero and one, that's easy to check, as well. There's no reason to hold off on integrating the logic of unit testing: What _must_ be true about this output for it to be usable? What must be true about my input for my computation to function?

Simple data checking is something that is easy to implement early and often. Self-skepticism about our results is a skill I can either build or scare into students. Actual testing libraries can be covered at the end of the course. Not that anyone is going to use them, anyway.

My plan is that for the first exercises, there are no tests. Then, I'll ask them to add a simple test of something specific (such as, add a line of code that ensures your output is a number, and prints a nasty message if it isn't). On the next assignment, I'll leave it more vague (Decide what must be true about the output of your function and test it). And lastly, the training wheels come off and I tell them to test as appropriate in their script. 

I think I can pull this off. Is anyone else teaching test-driven development for novices?
