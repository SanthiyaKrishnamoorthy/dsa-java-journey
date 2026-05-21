# 392. Is Subsequence

## Problem Statement

Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise.

A subsequence of a string is formed by deleting some characters (can be none) without disturbing the relative order of the remaining characters.

---

## Examples

### Example 1

```text
Input: s = "abc", t = "ahbgdc"
Output: true
```

Explanation:

- 'a' found
- 'b' found after 'a'
- 'c' found after 'b'

So `"abc"` is a subsequence of `"ahbgdc"`.

---

### Example 2

```text
Input: s = "axc", t = "ahbgdc"
Output: false
```

Explanation:

- 'a' found
- 'x' not found

Hence return `false`.

---

# Approach 1: Two Pointers

## Idea

Use two pointers:

- `i` for string `s`
- `j` for string `t`

Traverse `t` completely.

Whenever characters match:
- move pointer `i`

Always move pointer `j`.

At the end:
- if `i == s.length()`
  → all characters were matched in sequence.

---

# Dry Run

## Input

```text
s = "abc"
t = "ahbgdc"
```

| i | j | s[i] | t[j] | Action |
|---|---|------|------|--------|
|0|0|a|a|Match → i++, j++|
|1|1|b|h|j++|
|1|2|b|b|Match|
|2|3|c|g|j++|
|2|4|c|d|j++|
|2|5|c|c|Match|

Now:

```text
i == s.length()
```

So return:

```text
true
```

---

# Java Solution

```java
class Solution {

    public boolean isSubsequence(String s, String t) {

        int i = 0;
        int j = 0;

        while(i < s.length() && j < t.length())
        {
            if(s.charAt(i) == t.charAt(j))
            {
                i++;
            }

            j++;
        }

        return i == s.length();
    }
}
```

---

# Complexity Analysis

## Time Complexity

```text
O(n)
```

Where:

- `n = t.length()`

Because we traverse `t` once.

---

## Space Complexity

```text
O(1)
```

No extra space used.

---

# Edge Cases

## Case 1

```text
s = ""
t = "abc"
```

Output:

```text
true
```

Empty string is always a subsequence.

---

## Case 2

```text
s = "abc"
t = ""
```

Output:

```text
false
```

Cannot find characters in empty string.

---

## Case 3

```text
s = "aaaa"
t = "aa"
```

Output:

```text
false
```

Not enough occurrences.

---

# Follow-Up Question

## Problem

Suppose there are billions of incoming queries:

```text
s1, s2, s3, s4 ...
```

and the same `t` is reused every time.

How can we optimize?

---

# Optimized Approach

Instead of scanning `t` repeatedly:

## Preprocess `t`

Store indices of every character.

Example:

```text
t = "ahbgdc"
```

Store:

```text
a -> [0]
h -> [1]
b -> [2]
g -> [3]
d -> [4]
c -> [5]
```

Use:

```java
HashMap<Character, List<Integer>>
```

---

# Core Idea

For every character in `s`:

- Find the next valid position in `t`
- Use Binary Search

This avoids scanning entire `t`.

---

# Optimized Complexity

## Preprocessing

```text
O(n)
```

## Each Query

```text
O(m log n)
```

Where:

- `m = s.length()`
- `n = t.length()`

Very efficient for large-scale systems.

---

# Optimized Java Code

```java
import java.util.*;

class Solution {

    Map<Character, List<Integer>> map = new HashMap<>();

    public Solution(String t) {

        for(int i = 0; i < t.length(); i++)
        {
            char ch = t.charAt(i);

            map.putIfAbsent(ch, new ArrayList<>());
            map.get(ch).add(i);
        }
    }

    public boolean isSubsequence(String s) {

        int prevIndex = -1;

        for(char ch : s.toCharArray())
        {
            if(!map.containsKey(ch))
                return false;

            List<Integer> list = map.get(ch);

            int nextIndex = upperBound(list, prevIndex);

            if(nextIndex == list.size())
                return false;

            prevIndex = list.get(nextIndex);
        }

        return true;
    }

    private int upperBound(List<Integer> list, int target)
    {
        int low = 0;
        int high = list.size();

        while(low < high)
        {
            int mid = low + (high - low) / 2;

            if(list.get(mid) <= target)
                low = mid + 1;
            else
                high = mid;
        }

        return low;
    }
}
```

---

# Why This Follow-Up Matters

This question tests:

- Two Pointer Technique
- Preprocessing
- Binary Search
- Handling Massive Query Systems
- Time Complexity Optimization

---

# Related Problems

- Longest Common Subsequence
- Find Common Characters
- String Matching Problems
- Two Pointer Pattern
- Binary Search on Arrays

---

# Key Takeaways

## Basic Solution

- Use two pointers
- Traverse both strings

## Optimized Solution

- Preprocess `t`
- Store character positions
- Use Binary Search

---

# Interview Tip

Whenever interviewer says:

```text
"Same input reused many times"
```

Think about:

- Preprocessing
- Caching
- Indexing
- Tradeoff between time and space

This is a very common optimization pattern in interviews.
````
