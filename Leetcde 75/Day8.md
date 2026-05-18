# 334. Increasing Triplet Subsequence

- **Difficulty:** Medium  
- **Topics:** Greedy, Array  
- **LeetCode Link:** https://leetcode.com/problems/increasing-triplet-subsequence/

---

# Problem Statement

Given an integer array `nums`, return `true` if there exists a triple of indices `(i, j, k)` such that:

```text
i < j < k
```

and

```text
nums[i] < nums[j] < nums[k]
```

Otherwise, return `false`.

---

# Examples

## Example 1

```text
Input: nums = [1,2,3,4,5]
Output: true
```

### Explanation
Any triplet where `i < j < k` is valid.

---

## Example 2

```text
Input: nums = [5,4,3,2,1]
Output: false
```

### Explanation
No increasing triplet exists.

---

## Example 3

```text
Input: nums = [2,1,5,0,4,6]
Output: true
```

### Explanation
One valid triplet is:

```text
1 < 4 < 6
```

---

# Constraints

```text
1 <= nums.length <= 5 * 10^5
-2^31 <= nums[i] <= 2^31 - 1
```

---

# Intuition

We only need to determine whether an increasing subsequence of length `3` exists.

Instead of checking every triplet, we maintain:

- `first` → smallest element seen so far
- `second` → smallest possible second element

If we later find a number greater than both, then:

```text
first < second < current
```

which means an increasing triplet exists.

---

# Approach

Traverse the array once:

1. If current number is smaller than or equal to `first`,
   update `first`.

2. Else if current number is smaller than or equal to `second`,
   update `second`.

3. Else,
   current number is greater than both `first` and `second`,
   so return `true`.

If no such triplet is found, return `false`.

---

# Dry Run

## Input

```text
nums = [2,1,5,0,4,6]
```

| num | first | second | Action |
|-----|--------|---------|--------|
| 2 | 2 | INF | update first |
| 1 | 1 | INF | update first |
| 5 | 1 | 5 | update second |
| 0 | 0 | 5 | update first |
| 4 | 0 | 4 | update second |
| 6 | 0 | 4 | triplet found |

Return:

```text
true
```

---

# Java Solution

```java
class Solution {

    public boolean increasingTriplet(int[] nums) {

        int first = Integer.MAX_VALUE;
        int second = Integer.MAX_VALUE;

        for (int num : nums) {

            // Update smallest element
            if (num <= first) {
                first = num;
            }

            // Update second smallest element
            else if (num <= second) {
                second = num;
            }

            // Found a number greater than both
            else {
                return true;
            }
        }

        return false;
    }
}
```

---

# Complexity Analysis

## Time Complexity

```text
O(n)
```

We traverse the array only once.

---

## Space Complexity

```text
O(1)
```

Only two variables are used.

---

# Why This Works

We greedily maintain:

- smallest possible first element
- smallest possible second element

This maximizes the chance of finding a third larger element later.

Whenever we encounter:

```text
num > second
```

we already know:

```text
first < second < num
```

Hence, an increasing triplet exists.

---

# Edge Cases

## Case 1

```text
nums = [5,4,3,2,1]
```

Output:

```text
false
```

---

## Case 2

```text
nums = [1,2,3,4,5]
```

Output:

```text
true
```

---

## Case 3

```text
nums = [2,1,5,0,4,6]
```

Output:

```text
true
```

Valid triplet:

```text
0 < 4 < 6
```

---

# Key Takeaway

This is a classic greedy problem where maintaining:

- smallest first value
- smallest second value

helps detect an increasing subsequence of length `3` in optimal time.
