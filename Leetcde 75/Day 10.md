# 283. Move Zeroes

## Problem Statement

Given an integer array `nums`, move all `0`s to the end while maintaining the relative order of the non-zero elements.

You must do this **in-place** without making a copy of the array.

---

## Example 1

### Input
```text
nums = [0,1,0,3,12]
```

### Output
```text
[1,3,12,0,0]
```

---

## Example 2

### Input
```text
nums = [0]
```

### Output
```text
[0]
```

---

# Intuition

We need to:
- Keep all non-zero elements in the same order
- Move all zeroes to the end
- Do everything in-place

A brute force approach would involve shifting elements multiple times, which is inefficient.

Instead, we use the **Two Pointer Technique**.

---

# Optimal Approach — Two Pointers

We maintain:
- `i` → traverses the array
- `index` → stores the position where the next non-zero element should be placed

Whenever we encounter a non-zero element:
1. Swap it with `nums[index]`
2. Increment `index`

This automatically pushes zeroes toward the end.

---

# Dry Run

## Input
```text
nums = [0,1,0,3,12]
```

| i | nums[i] | index | Action | Array |
|---|---|---|---|---|
|0|0|0|Skip|[0,1,0,3,12]|
|1|1|0|Swap nums[1] and nums[0]|[1,0,0,3,12]|
|2|0|1|Skip|[1,0,0,3,12]|
|3|3|1|Swap nums[3] and nums[1]|[1,3,0,0,12]|
|4|12|2|Swap nums[4] and nums[2]|[1,3,12,0,0]|

---

# Java Solution

```java
class Solution {

    public void moveZeroes(int[] nums) {

        int index = 0;

        for(int i = 0; i < nums.length; i++) {

            if(nums[i] != 0) {

                int temp = nums[i];
                nums[i] = nums[index];
                nums[index] = temp;

                index++;
            }
        }
    }
}
```

---

# Step-by-Step Explanation

## Step 1
Initialize:
```java
int index = 0;
```

`index` represents the position where the next non-zero element should go.

---

## Step 2
Traverse the array:
```java
for(int i = 0; i < nums.length; i++)
```

---

## Step 3
Check for non-zero elements:
```java
if(nums[i] != 0)
```

---

## Step 4
Swap current element with `index`:
```java
int temp = nums[i];
nums[i] = nums[index];
nums[index] = temp;
```

---

## Step 5
Move `index` forward:
```java
index++;
```

---

# Time Complexity

```text
O(n)
```

- We traverse the array only once.

---

# Space Complexity

```text
O(1)
```

- No extra space is used.

---

# Why This Approach is Optimal?

- In-place solution
- Maintains relative order
- Minimal operations
- Single traversal
- Constant extra space

This satisfies the follow-up requirement efficiently.

---

# Alternative Approach (Extra Array)

We can create another array:
1. Store all non-zero elements first
2. Fill remaining positions with zeroes

But:
- Requires extra space
- Not in-place

Hence, the two-pointer approach is preferred.

---

# Key Takeaways

- Classic Two Pointer problem
- Stable ordering maintained
- Efficient in-place swapping
- Important interview pattern

---
