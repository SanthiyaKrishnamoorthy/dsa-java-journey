# 443. String Compression

## Problem Statement

Given an array of characters `chars`, compress it using the following algorithm:

- Begin with an empty string `s`.
- For each group of consecutive repeating characters in `chars`:
  - If the group's length is `1`, append the character to `s`.
  - Otherwise, append the character followed by the group's length.

The compressed string must be stored inside the input character array `chars`.

Return the new length of the compressed array.

You must use only constant extra space.

---

# Example 1

## Input

```text
chars = ["a","a","b","b","c","c","c"]
```

## Output

```text
6
```

## Explanation

Groups:

```text
aa -> a2
bb -> b2
ccc -> c3
```

Compressed array:

```text
["a","2","b","2","c","3"]
```

---

# Example 2

## Input

```text
chars = ["a"]
```

## Output

```text
1
```

---

# Example 3

## Input

```text
chars = ["a","b","b","b","b","b","b","b","b","b","b","b","b"]
```

## Output

```text
4
```

## Explanation

```text
a + bbbbbbbbbbbb
```

Compressed form:

```text
["a","b","1","2"]
```

---

# Approach

We use the **Two Pointer Technique**.

## Idea

- Traverse the array using pointer `i`
- Count consecutive repeating characters
- Write compressed characters using pointer `index`

For each group:

1. Store the character
2. Count occurrences
3. Write the count if greater than `1`

---

# Dry Run

## Input

```text
["a","a","b","b","c","c","c"]
```

---

## Step 1

Character:

```text
a
```

Count:

```text
2
```

Write:

```text
a2
```

---

## Step 2

Character:

```text
b
```

Count:

```text
2
```

Write:

```text
b2
```

---

## Step 3

Character:

```text
c
```

Count:

```text
3
```

Write:

```text
c3
```

---

## Final Array

```text
["a","2","b","2","c","3"]
```

Return:

```text
6
```

---

# Optimized Java Solution

```java
class Solution {

    public int compress(char[] chars) {

        int index = 0;
        int i = 0;

        while (i < chars.length) {

            char currentChar = chars[i];
            int count = 0;

            // Count consecutive characters
            while (i < chars.length && chars[i] == currentChar) {
                i++;
                count++;
            }

            // Store character
            chars[index++] = currentChar;

            // Store count if greater than 1
            if (count > 1) {

                String cnt = String.valueOf(count);

                for (char c : cnt.toCharArray()) {
                    chars[index++] = c;
                }
            }
        }

        return index;
    }
}
```

---

# Time Complexity

## O(n)

Each character is visited once.

---

# Space Complexity

## O(1)

Only constant extra space is used.

---

# Why Convert Count to String?

Suppose count is:

```text
12
```

It must be stored as:

```text
'1', '2'
```

inside the same character array.

So we convert the number into a string and store each digit separately.

---

# Important Interview Points

## 1. In-place Modification

We directly overwrite values inside the original array.

---

## 2. Two Pointer Technique

- `i` → reads original characters
- `index` → writes compressed characters

---

## 3. Constant Extra Space

No extra array is used.

---

# Edge Cases

## Case 1: Single Character

### Input

```text
["a"]
```

### Output

```text
["a"]
```

Return:

```text
1
```

---

## Case 2: Count Greater Than 9

### Input

```text
["a","a","a","a","a","a","a","a","a","a","a","a"]
```

### Count

```text
12
```

### Compressed

```text
["a","1","2"]
```

---

# Pattern Recognition

This problem is based on:

- Two Pointers
- String Compression
- In-place Array Manipulation

---

# Key Takeaway

Whenever you need to:

- Compress consecutive elements
- Modify arrays in-place
- Track groups of repeating characters

Think about:

```text
Two Pointers + Count Frequency
```
