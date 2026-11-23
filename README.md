
# Why Your Binary Search Solution Fails: 5 Common Mistakes and How to Fix Them

Binary Search is one of the most important searching techniques in programming. It can reduce the search time from O(n) to O(log n), making it extremely useful when working with large, sorted datasets.

However, even though the concept sounds simple, many programmers [struggle when implementing](https://fence-space.com/) it.

Sometimes the solution works for normal inputs but fails on edge cases. In other situations, the program enters an infinite loop or returns an incorrect index.

The problem is usually not the algorithm itself but small implementation mistakes.

In this guide, we will explore five common Binary Search mistakes, understand why they happen, and learn how to avoid them.

## 1. Understanding How Binary Search Works

Binary Search works by repeatedly dividing a sorted search space into two halves.

Instead of checking every element individually, we examine the middle element and decide which half could contain the target.

Let's consider an example:

```python
nums = [2, 4, 7, 10, 14, 18, 21]
target = 14
```

We begin with two pointers:

- `left = 0`
- `right = len(nums) - 1`

Then calculate the middle index:

```python
mid = (left + right) // 2
```

If the middle element equals the target, we return its index.

If the middle element is smaller than the target, we search the right half.

If it is greater than the target, we search the left half.

We continue until the target is found or the search space becomes empty.

## 2. Mistake One: Forgetting to Update the Search Boundaries

One of the most common mistakes is updating the pointers incorrectly.

Consider this code:

```python
def binary_search(nums, target):
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid

        elif nums[mid] < target:
            left = mid

        else:
            right = mid

    return -1
```

At first glance, this implementation looks correct.

However, it can enter an infinite loop.

Why?

Imagine that `left` and `right` differ by one. The calculated middle index may equal `left`.

If the target is larger than the middle element, assigning `left = mid` does not change the pointer.

The loop can continue forever.

### Correct Solution

```python
left = mid + 1
```

And for the other direction:

```python
right = mid - 1
```

Always make sure that the search space becomes smaller after each unsuccessful comparison.

## 3. Mistake Two: Using the Wrong Loop Condition

Another common problem is choosing the wrong loop condition.

Consider:

```python
while left < right:
```

This condition can be correct in some Binary Search implementations, but it behaves differently from:

```python
while left <= right:
```

When using `left <= right`, the algorithm continues while at least one candidate index remains.

When using `left < right`, the algorithm stops when both pointers meet.

Neither condition is universally wrong. The important thing is to make sure the pointer updates and final checks match the chosen implementation.

For a standard Binary Search that returns an exact matching index, the following version is straightforward:

```python
while left <= right:
    mid = (left + right) // 2
```

## 4. Mistake Three: Forgetting That Binary Search Requires Sorted Data

Binary Search depends on the ordering of elements.

Consider:

```python
nums = [10, 3, 18, 2, 14, 7]
target = 14
```

Applying standard Binary Search directly to this array can produce incorrect results.

Why?

Because comparing the middle element does not tell us which half contains the target when the elements are unordered.

### Correct Approach

Sort the array first if the problem allows it:

```python
nums = sorted([10, 3, 18, 2, 14, 7])
```

Now the array becomes:

```python
[2, 3, 7, 10, 14, 18]
```

Binary Search can now work correctly.

However, be careful: sorting changes the original indices. If the problem asks for original positions, you must preserve that information or use another approach.

## 5. Mistake Four: Calculating the Middle Index Incorrectly

A common implementation is:

```python
mid = (left + right) // 2
```

This works in Python because its integers can grow beyond fixed-width limits.

However, in languages such as Java and C++, adding two very large integer indices can potentially cause integer overflow.

A safer general expression is:

```python
mid = left + (right - left) // 2
```

This avoids unnecessarily adding two potentially large values.

It is a useful habit when writing Binary Search in languages with fixed-width integer types.

## 6. Mistake Five: Ignoring Edge Cases

A Binary Search solution should not only work for normal inputs.

It should also handle unusual situations correctly.

Consider these examples:

**Empty Array**

```python
nums = []
target = 5
```

Expected result:

```text
-1
```

**Single Element**

```python
nums = [8]
target = 8
```

Expected result:

```text
0
```

**Target Smaller Than Every Element**

```python
nums = [3, 5, 7, 9]
target = 1
```

Expected result:

```text
-1
```

**Target Larger Than Every Element**

```python
nums = [3, 5, 7, 9]
target = 12
```

Expected result:

```text
-1
```

Testing these cases helps identify pointer and boundary mistakes before submitting your solution.

## 7. A Complete and Correct Binary Search Implementation

Now let's combine everything into one implementation.

```python
def binary_search(nums, target):

    left = 0
    right = len(nums) - 1

    while left <= right:

        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid

        elif nums[mid] < target:
            left = mid + 1

        else:
            right = mid - 1

    return -1


nums = [2, 4, 7, 10, 14, 18, 21]

print(binary_search(nums, 14))
print(binary_search(nums, 5))
```

Output:

```text
4
-1
```

This implementation handles empty arrays, missing targets, and normal search operations correctly, assuming the input is sorted.

## 8. Understanding Time and Space Complexity

Binary Search is efficient because it eliminates approximately half of the remaining search space after each comparison.

**Time Complexity: O(log n)**

For an array containing 1,024 elements, Binary Search needs at most 11 iterations to identify a matching element or establish that it is absent.

**Space Complexity: O(1)**

The iterative implementation uses only a few variables and does not require additional data structures proportional to the input size.

This makes it efficient for searching large sorted arrays.

## 9. When Should You Use Binary Search?

Binary Search is useful in several situations:

- Searching for an element in a sorted array.
- Finding the first or last occurrence of a value.
- Finding the insertion position of an element.
- Searching for a minimum or maximum feasible answer.
- Solving problems involving a monotonic condition.
- Working with sorted ranges and boundaries.

One important extension is Binary Search on Answer, where we search over possible answers instead of directly searching through an array.

This technique appears in many challenging competitive programming problems.

## 10. Practice These LeetCode Problems

If you want to improve your Binary Search skills, try these problems:

1. [704. Binary Search](https://leetcode.com/problems/binary-search/)
2. [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)
3. [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
4. [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
5. [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

Try solving these problems without immediately looking at the solutions.

Pay attention to how the search boundaries change in each problem.

## Final Thoughts

Binary Search is not difficult because of its basic idea. The real challenge is implementing it correctly.

A small mistake in pointer updates, loop conditions, or boundary handling can completely change the result.

The best way to improve is to understand why each line of code exists rather than simply memorizing a template.

Practice different variations, test edge cases, and compare your implementations.

Once you understand the logic behind Binary Search, you will be better prepared to solve more advanced searching and optimization problems.

**What is the most confusing part of Binary Search for you: pointer updates, loop conditions, or finding boundaries? Share your experience in the comments.**
