# 238. Product of Array Except Self

## Problem Statement

Given an integer array `nums`, return an array `answer` such that:

```math
answer[i] = product of all elements of nums except nums[i]
```

Constraints:
- Solve in `O(n)` time complexity
- Do not use division
- Follow-up: Solve with `O(1)` extra space (excluding output array)

---

# Example 1

## Input

```text
nums = [1,2,3,4]
```

## Output

```text
[24,12,8,6]
```

---

# Example 2

## Input

```text
nums = [-1,1,0,-3,3]
```

## Output

```text
[0,0,9,0,0]
```

---

# Intuition

For every index `i`, we need:

```math
answer[i] =
(product of elements before i)
×
(product of elements after i)
```

Instead of using division:

- Compute prefix products
- Compute suffix products
- Multiply them together

---

# Approach

## Step 1: Store Prefix Products

For every index:

```math
answer[i] =
nums[0] × nums[1] × ... × nums[i-1]
```

Example:

```text
nums = [1,2,3,4]

Prefix products:
[1,1,2,6]
```

Explanation:
- `1` → no elements on left
- `1` → product of `[1]`
- `2` → product of `[1,2]`
- `6` → product of `[1,2,3]`

---

## Step 2: Compute Suffix Products

Traverse from right to left using a variable:

```java
suffix = 1
```

At each index:
- Multiply current answer with suffix
- Update suffix

---

# Dry Run

## Input

```text
nums = [1,2,3,4]
```

---

## Prefix Pass

```text
answer = [1,1,2,6]
```

---

## Suffix Pass

| i | suffix | Updated answer[i] |
|---|---|---|
| 3 | 1 | 6 |
| 2 | 4 | 8 |
| 1 | 12 | 12 |
| 0 | 24 | 24 |

Final Output:

```text
[24,12,8,6]
```

---

# Java Solution

```java
class Solution {

    public int[] productExceptSelf(int[] nums) {

        int n = nums.length;

        int[] answer = new int[n];

        // Step 1: Prefix products
        answer[0] = 1;

        for (int i = 1; i < n; i++) {
            answer[i] = answer[i - 1] * nums[i - 1];
        }

        // Step 2: Suffix products
        int suffix = 1;

        for (int i = n - 1; i >= 0; i--) {

            answer[i] = answer[i] * suffix;

            suffix *= nums[i];
        }

        return answer;
    }
}
```

---

# Complexity Analysis

## Time Complexity

```math
O(n)
```

- One pass for prefix
- One pass for suffix

---

## Space Complexity

```math
O(1)
```

Ignoring the output array.

---

# Why This Works

At every index:

```math
answer[i]
=
(left product)
×
(right product)
```

The prefix pass stores left products.

The suffix traversal dynamically provides right products.

Multiplying both gives the final answer.

---

# Key Interview Points

## Why not division?

Division fails when:
- Array contains zero
- Problem explicitly forbids division

---

## Why O(1) extra space?

We reuse:
- output array for prefix products
- one variable for suffix products

No extra prefix/suffix arrays are needed.

---

# Edge Cases

## Contains Zero

Input:

```text
[1,2,0,4]
```

Output:

```text
[0,0,8,0]
```

---

## Multiple Zeros

Input:

```text
[0,1,2,0]
```

Output:

```text
[0,0,0,0]
```

---

# Final Takeaway

This problem is a classic optimization problem involving:

- Prefix products
- Suffix products
- Space optimization

The optimal solution:
- Avoids division
- Runs in linear time
- Uses constant extra space
