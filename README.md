# Lab 4: Concept Review

This lab reviews the foundational concepts of algorithms and data structures that we have covered in the first half of the course. 

**Instructions:** To complete this lab, you may work in groups, but you must write your solutions yourself. Choose two of the topics below that you need to review and complete the corresponding problems. Where relevant, you are given the answer and must provide the justification as your solution. Once you have completed the lab, push your changes to your forked repository.

**Topics:** asymptotic analysis, data structures, empirical comparison of algorithms, pseudocode, greedy algorithms. 
Name: Luke Perezs

## Asymptotic Analysis

1. Use the rules from lecture 07 to prove that $T(n) = 5 \log n + 7n$ is $\mathcal{O}(n)$.
Using the rules from lecture, we can drop multiplicative constants meaning that this function becomes logn + n. Since O(n) is the fastest growth for the worst case running time out of both of those, the functions upper bound of running time in the worst case is O(n). 

2. True/False/Possibly: $T(n)$ is $\mathcal{O}(n^2)$?

**Answer**: Yes

**Justification**: Yes, the Big O bound is also O(n^2) since that falls below the current upper bound of O(n). 

3. True/False/Possibly: $T(n)$ is $\Omega(n \log n)$?

**Answer**: No

**Justification**: Omega(nlogn) falls below our upper bound of O(n) meaning that it could be an upper bound but not a lower bound like Omega states. 

4. For any algorithm, we can give a trivial lower bound. What is that lower bound?

**Answer**: $\Omega(1)$

**Justification**: That means the function is just 1 step, which means every function does at least 1 thing. 

5. Is there a corresponding trivial upper bound? Why or why not?

**Answer**: No

**Justification**: We can always say a function will do at least 1 thing but we can never say a function can do at most a certain amount of things because every function has a different point, so we can not set a guaranteed upper bound. 


## Data Structures

1. You are programming a robot to navigate a maze. As the robot moves forward, it records each intersection it passes. When it hits a dead end, it needs to retreat to the most recently visited intersection to try a different path.

**Answer**: Stack

**Justification**: Since you can just remove the last part, which is the most recently visited intersection, to go to a different intersection, thats what a stack does. In linear time, you can pop to remove the end and then push to append to the end. 

2. A server receives a massive influx of data packets from a streaming video application. To prevent the video from skipping or playing out of order on the user's end, the server must process and forward these packets in the exact sequence they were received.

**Answer**: Queue

**Justification**: A queue is useful for this because it has the enqueue and dequeue functions, which always keep the order like is necessary here. Dequeue will just process the packet at the front of the order and Enqueue will add a new packet but only onto the back of the order, meaning it will never end up in a place it shouldn't. 

3. An atmospheric monitoring system reads temperature data from 10,000 sequentially numbered sensors (IDs 0 through 9999). Throughout the day, the system needs to constantly update and read the current temperature of randomly selected sensors based on their ID number to build localized weather maps.

**Answer**: Array

**Justification**: An array is useful for this because it can just peek at any of the 10,000 values in linear time. It will hold every one of those values at a certain index and then if it needs a certain index, it can go straight to that one without having to go through every other one. 

4. You are building a lightweight syntax checker for a code editor. Its sole job is to scan a document and ensure that every opened parenthesis `(`, bracket `[`, and brace `{` is matched with its corresponding closing character in the correct nested order.

**Answer**: Stack

**Justification**: A stack is good for this because if it locates an error, like a parenthesis is wrongly matched with a bracket, then it can go in there and pop from the end which would be the incorrect bracket, and then also push to the end to insert a parenthesis so it is correctly matched. 

## Empirical Comparison of Algorithms

1. A student is benchmarking an algorithm that takes a list as its input. They run it on progressively larger randomly generated lists, doubling the number of elements ($n$) and record the following execution times:

- $n = 1000$: 0.12 seconds
- $n = 2000$: 0.94 seconds
- $n = 4000$: 7.61 seconds
- $n = 8000$: 60.85 seconds

 Based on this empirical data, what is the most likely asymptotic time complexity of the algorithm? **Hint**: Calculate the doubling ratio between each pair of consecutive runs.

 **Answer**: Cubic time complexity, $\mathcal{O}(n^3)$

**Justification**: Based on the corresponding running times, we can see they consistently increase by a multiplicative of 8 and since we know the values double every time, that is a base of 2. So 2^x = 8, and solving for x we can see that it is 2^3 = 8, or cubic. 

 2. Two students write separate algorithms to compute a metric over an array of 10 million integers. Both algorithms perform exactly one mathematical operation per element, meaning both have a theoretical time complexity of $O(N)$. However, during benchmarking, Algorithm A consistently runs 15x faster than Algorithm B. Why might theoretical Big-O analysis fail to predict this massive performance gap? 

**Answer**: Just looking at the Big O bound ignores any constant factors, so both algorithms are O(n) but one might be running on better hardware or any implementation factors. 

 3. Scenario: To measure the running time of algorithms for an empirical comparison, a developer writes the following benchmarking script:

```python
import time

large_array = [i for i in range(1000000)]
start = time.time()
myAlg(large_array)
end = time.time()

print("Time:", end - start)
```

They run this script exactly once for each algorithm on their laptop while streaming a movie in the background. Identify at least three distinct methodological flaws in this benchmarking setup that make the results unreliable.

**Answer**: The movie in the background takes up processing power and therefore it is not a complete, accurate running time because the computer is doing 2 things at once. time.time() is not the best timer, time.perf_counter() should be used for a high resolution timer of elapsed time. They only run the script once for each algorithm but a thorough test should be run multiple times to see the exact benchmark. 

## Pseudocode

1. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
count = 0
for i = 1 to N do
    for j = i to N do
        do_work()
```

Write a closed-form expression for the number of times `do_work()` is called in terms of $N$.
n * n times. One n for each for loop. 

2. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
i = N
while i > 0:
    for j = 1 to i:
        do_work()
    i = floor(i / 2)
```

If $N=16$, how many times is `do_work()` called?

**Answer**: 31

**Justification**: We start at 16 times, then it is halved to 8 times, then 4 times, then 2, then finally 1. So adding all of those up 16 + 8 + 4 + 2 + 1 = 31 times. 

## Greedy Algorithms

You are organizing a film festival but only have access to a single screen. You are given a list of $n$ films, each with a specific `start_time` and `end_time`. You want to screen the maximum number of films possible.

Consider the following three greedy strategies:

- **Shortest First**: Always pick the film with the shortest duration (that doesn't conflict with already chosen films).
- **Earliest Start**: Always pick the film that starts the earliest (that doesn't conflict).
- **Earliest Finish**: Always pick the film that finishes the earliest (that doesn't conflict).

Which of these three strategies guarantees an optimal solution (maximum number of films)? For the two strategies that fail, provide a counter-example (a small set of film times) where the greedy choice results in a sub-optimal schedule.

**Answer**: The earliest finish strategy guarantees an optimal solution.

**Justification**: