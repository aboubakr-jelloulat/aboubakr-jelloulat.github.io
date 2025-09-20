---
title: "Boyer–Moore Majority Vote Algorithm"
date: 2025-09-19 00:00:00 +0000
categories: [Programming, Algorithms]
tags: [boyer-moore, majority-vote, algorithm, leetcode]
toc: true
---

## Introduction

>The Boyer–Moore Majority Vote Algorithm is an elegant and efficient solution for finding the majority element in an array. Developed by Robert S. Boyer and J Strother Moore in 1981, this algorithm solves the majority element problem in linear time with constant space complexity, making it particularly valuable in scenarios where memory usage is critical.

_The algorithm works on a simple principle: if an element appears more than n/2 times in an array of size n, it can be found by maintaining a candidate and a counter, eliminating pairs of different elements until only the majority element remains._

## The Problem It Solves

The majority element problem asks us to find an element that appears more than ⌊n/2⌋ times in an array of size n. This is a classic problem in computer science and is featured as [LeetCode Problem 169: Majority Element](https://leetcode.com/problems/majority-element/).

For example, in the array `[3, 2, 3]`, the element `3` appears twice out of three elements, making it the majority element. Similarly, in `[2, 2, 1, 1, 1, 2, 2]`, the element `2` appears four times out of seven elements.

The challenge lies in finding an efficient solution. ~~While a brute force approach or sorting would work, they either require O(n²) time complexity or O(n log n) time complexity respectively~~. Using a ~~hash map achieves O(n) time but requires O(n) additional space in the worst case.~~

>The Boyer–Moore algorithm achieves the optimal solution: **O(n) time complexity with O(1) space complexity**. This efficiency makes it particularly important for:



## Visual Explanation

![Boyer-Moore Majority Vote Algorithm Visualization](/assets/img/Boyer-Moore_MJRTY.svg)

### Step-by-Step Algorithm Walkthrough

Let's trace through the algorithm step by step using the visualization. The algorithm processes the array from left to right, maintaining a candidate and count:

Key Rules:

When count = 0, set new candidate
When current element = candidate, increment count
When current element ≠ candidate, decrement count


Array: 🔵 🔵 🟥 🔵 🟥 ⭐ ⭐ 🟥 🟥 🟥 🔵 🟥 🟥 ⭐ 🟥 🟥
Initial state: candidate = ?, count = 0

Step 1: Element = 🔵

    Count is 0 → Set candidate = 🔵, count = 1

Step 2: Element = 🔵

    Matches candidate 🔵 → count = 2

Step 3: Element = 🟥

    Differs from candidate 🔵 → count = 1

Step 4: Element = 🔵

Matches candidate 🔵 → count = 2

Step 5: Element = 🟥

    Differs from candidate 🔵 → count = 1

Step 6: Element = ⭐

    Differs from candidate 🔵 → count = 0

Step 7: Element = ⭐

    Count is 0 → Set candidate = ⭐, count = 1

Step 8: Element = 🟥

    Differs from candidate ⭐ → count = 0

Step 9: Element = 🟥

    Count is 0 → Set candidate = 🟥, count = 1

Step 10: Element = 🟥

    Matches candidate 🟥 → count = 2

Step 11: Element = 🔵

    Differs from candidate 🟥 → count = 1

Step 12: Element = 🟥

    Matches candidate 🟥 → count = 2

Step 13: Element = 🟥

    Matches candidate 🟥 → count = 3

Step 14: Element = ⭐

    Differs from candidate 🟥 → count = 2

Step 15: Element = 🟥

    Matches candidate 🟥 → count = 3

Step 16: Element = 🟥

    Matches candidate 🟥 → count = 4


Final Result :

Candidate = 🟥 (red square)

### Why It Works
The algorithm works on the principle that if an element appears more than n/2 times, it will "survive" all the cancellations with other elements. Each time we see a different element, we cancel it out with our current candidate. The true majority element will have enough occurrences to remain as the final candidate.
Verification
Count occurrences in the array:

🔵 (blue): 4 times
🟥 (red): 9 times
⭐ (yellow): 3 times

Total elements: 16
Majority threshold: 16/2 = 8
🟥 appears 9 times > 8, so it's the majority element 



## Implementation in C++

>Here's the complete C++ implementation of the Boyer–Moore Majority Vote Algorithm:

![Implementation in C++ ](/assets/img/Boyer-Moore-Algo.png)



## Real-World Example: Political Election System

>The Boyer-Moore algorithm isn't just for numbers - it works perfectly for finding majority winners in political elections! Instead of counting every vote for each party (~~which requires extra memory~~), this algorithm efficiently determines if any party has more than 50% of votes. Let's see how it handles a election between Socialist, Conservative, and Liberal parties.

![Implementation in C++ ](/assets/img/votes_example.png)

## Conclusion

>_The Boyer–Moore Majority Vote Algorithm is a powerful tool for finding majority elements with optimal time and space complexity. Its applications extend beyond competitive programming into real-world scenarios such as voting systems, streaming data analysis ... The algorithm's ability to process data in a single pass with constant memory usage makes it particularly valuable for systems with memory constraints or real time processing requirements._