# 605. Can Place Flowers

## Problem Statement

You have a long flowerbed in which some plots are planted and some are empty.  
However, flowers cannot be planted in adjacent plots.

Given:
- An integer array `flowerbed` containing `0`s and `1`s
  - `0` → empty plot
  - `1` → already planted
- An integer `n`

Return `true` if `n` new flowers can be planted without violating the no-adjacent-flowers rule, otherwise return `false`.

---

## Examples

### Example 1

```text
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true
```

### Example 2

```text
Input: flowerbed = [1,0,0,0,1], n = 2
Output: false
```

---

## Approach

We use a **Greedy Algorithm**.

For every position:
1. Check if the current plot is empty.
2. Check whether:
   - Left plot is empty (or does not exist)
   - Right plot is empty (or does not exist)
3. If both are empty:
   - Plant a flower
   - Increment count

If count becomes greater than or equal to `n`, return `true`.

---

## Java Solution

```java
class Solution {

    public boolean canPlaceFlowers(int[] flowerbed, int n) {

        int count = 0;

        for (int i = 0; i < flowerbed.length; i++) {

            // Current plot must be empty
            if (flowerbed[i] == 0) {

                // Check left side
                boolean leftEmpty =
                        (i == 0) || (flowerbed[i - 1] == 0);

                // Check right side
                boolean rightEmpty =
                        (i == flowerbed.length - 1) ||
                        (flowerbed[i + 1] == 0);

                // Plant flower if both sides are empty
                if (leftEmpty && rightEmpty) {

                    flowerbed[i] = 1;
                    count++;
                }
            }

            // If enough flowers are planted
            if (count >= n) {
                return true;
            }
        }

        return count >= n;
    }
}
```

---

## Dry Run

### Input

```text
flowerbed = [1,0,0,0,1]
n = 1
```

### Traversal

| Index | Value | Can Plant? | Flowerbed State |
|------|------|------|------|
| 0 | 1 | No | [1,0,0,0,1] |
| 1 | 0 | No | [1,0,0,0,1] |
| 2 | 0 | Yes | [1,0,1,0,1] |

Count = 1

Return `true`

---

## Time Complexity

```text
O(n)
```

We traverse the array once.

---

## Space Complexity

```text
O(1)
```

No extra space is used.

---

## Key Learning

- Greedy approach
- Boundary condition handling
- Array traversal
- In-place modification

---

# LeetCode

Problem Link: https://leetcode.com/problems/can-place-flowers/