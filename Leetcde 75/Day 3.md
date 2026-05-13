# 1431. Kids With the Greatest Number of Candies

> LeetCode Easy Problem  
> Topic: Arrays

---

# Problem Statement

There are `n` kids with candies.

You are given:

- An integer array `candies`
- An integer `extraCandies`

Where:

```text
candies[i] = number of candies the ith kid has
```

Return a boolean array `result` of length `n`, where:

- `result[i] = true` if giving all `extraCandies` to the `ith` kid makes them have the greatest number of candies among all kids.
- Otherwise, `false`.

> Multiple kids can have the greatest number of candies.

---

# Example 1

## Input

```text
candies = [2,3,5,1,3]
extraCandies = 3
```

## Output

```text
[true,true,true,false,true]
```

## Explanation

| Kid | Current Candies | After Giving Extra Candies | Greatest? |
|------|------------------|----------------------------|------------|
| 1 | 2 | 5 | true |
| 2 | 3 | 6 | true |
| 3 | 5 | 8 | true |
| 4 | 1 | 4 | false |
| 5 | 3 | 6 | true |

---

# Example 2

## Input

```text
candies = [4,2,1,1,2]
extraCandies = 1
```

## Output

```text
[true,false,false,false,false]
```

---

# Example 3

## Input

```text
candies = [12,1,12]
extraCandies = 10
```

## Output

```text
[true,false,true]
```

---

# Constraints

```text
2 <= candies.length <= 100
1 <= candies[i] <= 100
1 <= extraCandies <= 50
```

---

# Intuition

We need to determine whether each kid can reach the maximum candy count after receiving all extra candies.

### Key Observation

If:

```text
candies[i] + extraCandies >= maximum candies
```

Then that kid can have the greatest number of candies.

So:

1. Find the current maximum candy count.
2. Check every kid against it.

---

# Approach

## Step 1: Find Maximum Candies

Traverse the array and store the maximum value.

```java
int max = 0;

for (int candy : candies) {
    max = Math.max(max, candy);
}
```

---

## Step 2: Check Each Kid

For every kid:

```java
if (candy + extraCandies >= max)
```

- Add `true` if condition satisfies
- Otherwise add `false`

---

# Dry Run

## Input

```text
candies = [2,3,5,1,3]
extraCandies = 3
```

## Step 1: Find Maximum

```text
max = 5
```

## Step 2: Check Each Kid

| Kid | Candies | Candies + Extra | >= 5 ? | Result |
|------|----------|-----------------|---------|---------|
| 1 | 2 | 5 | Yes | true |
| 2 | 3 | 6 | Yes | true |
| 3 | 5 | 8 | Yes | true |
| 4 | 1 | 4 | No | false |
| 5 | 3 | 6 | Yes | true |

## Final Answer

```text
[true,true,true,false,true]
```

---

# Java Solution

```java
class Solution {

    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {

        List<Boolean> result = new ArrayList<>();

        int max = 0;

        // Find maximum candy count
        for (int candy : candies) {
            max = Math.max(max, candy);
        }

        // Check every kid
        for (int candy : candies) {

            if (candy + extraCandies >= max) {
                result.add(true);
            } else {
                result.add(false);
            }
        }

        return result;
    }
}
```

---

# Time Complexity

## Finding Maximum Element

```text
O(n)
```

## Traversing Again

```text
O(n)
```

## Total

```text
O(n)
```

---

# Space Complexity

```text
O(n)
```

Because we store the result array/list.

---

# Concepts Used

- Arrays
- Traversal
- Maximum Element
- Conditional Checking
- ArrayList

---

# Key Learning

This problem teaches an important pattern:

## Precompute + Reuse

Instead of recalculating the maximum every time:

1. Compute it once
2. Reuse it efficiently

This reduces unnecessary operations and improves performance.

---

# Optimized Thinking Pattern

Whenever you see problems involving:

- Greatest
- Smallest
- Maximum
- Minimum

Think:

```text
Can I precompute the max/min once?
```

That mindset is very important for coding interviews and DSA optimization.

---

# Final Takeaway

This is a simple but foundational array problem that strengthens:

- Traversal logic
- Comparison logic
- Problem decomposition
- Efficient thinking

A perfect beginner-friendly interview question.