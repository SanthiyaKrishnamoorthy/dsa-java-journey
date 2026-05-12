# 1071. Greatest Common Divisor of Strings

## Problem Statement

For two strings `s` and `t`, we say `"t divides s"` if and only if:

```text
s = t + t + t + ... + t
```

Given two strings `str1` and `str2`, return the **largest string** `x` such that `x` divides both strings.

---

# Example

## Example 1

```text
Input:
str1 = "ABCABC"
str2 = "ABC"

Output:
"ABC"
```

---

## Example 2

```text
Input:
str1 = "ABABAB"
str2 = "ABAB"

Output:
"AB"
```

---

## Example 3

```text
Input:
str1 = "LEET"
str2 = "CODE"

Output:
""
```

---

# Core Concept

A string divides another string if repeating it multiple times forms the original string.

Example:

```text
"AB" -> "ABABAB"
```

because:

```text
"AB" + "AB" + "AB" = "ABABAB"
```

---

# Approach 1 — Brute Force

## Idea

1. Take every possible prefix from largest to smallest.
2. Check whether it can form both strings completely.
3. Return the first valid prefix.

---

# Brute Force Algorithm

1. Find the smaller length between the two strings.
2. Traverse from `minLength` to `1`.
3. Check:
   - Length divides both strings
   - Prefix can repeatedly form both strings
4. Return the first valid prefix.

---

# Brute Force Code

```java
class Solution {

    public String gcdOfStrings(String str1, String str2) {

        int minLen = Math.min(str1.length(), str2.length());

        for (int i = minLen; i >= 1; i--) {

            if (str1.length() % i == 0 &&
                str2.length() % i == 0) {

                String candidate = str1.substring(0, i);

                if (isDivisible(str1, candidate) &&
                    isDivisible(str2, candidate)) {

                    return candidate;
                }
            }
        }

        return "";
    }

    private boolean isDivisible(String str, String pattern) {

        int repeat = str.length() / pattern.length();

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < repeat; i++) {
            sb.append(pattern);
        }

        return sb.toString().equals(str);
    }
}
```

---

# Time Complexity

```text
O(min(n,m) * (n+m))
```

Where:

- `n = str1.length()`
- `m = str2.length()`

---

# Approach 2 — Optimized (Using GCD Concept)

## Important Observation

If two strings have a common divisor string, then:

```text
str1 + str2 == str2 + str1
```

### Example

```text
"ABCABC" + "ABC"
=
"ABC" + "ABCABC"
```

Both become:

```text
"ABCABCABC"
```

But:

```text
"LEET" + "CODE"
!=
"CODE" + "LEET"
```

So no common divisor exists.

---

# Main Logic

If concatenations are equal:

1. Find GCD of the lengths
2. Return substring from `0` to `gcdLength`

---

# Why GCD Works

Example:

```text
str1 = "ABABAB"   -> length = 6
str2 = "ABAB"     -> length = 4
```

GCD:

```text
gcd(6, 4) = 2
```

First 2 characters:

```text
"AB"
```

This becomes the answer.

---

# Optimized Code

```java
class Solution {

    public String gcdOfStrings(String str1, String str2) {

        // No common repeating pattern
        if (!(str1 + str2).equals(str2 + str1)) {
            return "";
        }

        int gcdLength = gcd(str1.length(), str2.length());

        return str1.substring(0, gcdLength);
    }

    private int gcd(int a, int b) {

        while (b != 0) {

            int temp = b;
            b = a % b;
            a = temp;
        }

        return a;
    }
}
```

---

# Euclidean Algorithm Concept

The GCD function uses:

```text
gcd(a, b) = gcd(b, a % b)
```

until `b == 0`.

Example:

```text
gcd(6,4)

6 % 4 = 2
4 % 2 = 0

Answer = 2
```

---

# Time Complexity

## Concatenation Check

```text
O(n + m)
```

## GCD Calculation

```text
O(log(min(n,m)))
```

## Overall Complexity

```text
O(n + m)
```

---

# Dry Run

## Input

```text
str1 = "ABABAB"
str2 = "ABAB"
```

---

## Step 1

```text
str1 + str2
=
"ABABABABAB"

str2 + str1
=
"ABABABABAB"
```

Equal ✔

---

## Step 2

Lengths:

```text
6 and 4
```

GCD:

```text
gcd(6,4) = 2
```

---

## Step 3

Take first 2 characters:

```text
"AB"
```

Answer:

```text
"AB"
```

---

# Key Interview Insight

The optimized solution is based on this important observation:

> If two strings are made from the same repeating base pattern, concatenating them in different orders produces the same result.

This is the core idea interviewers expect.

---

# Concepts Learned

- String divisibility
- Prefix checking
- String concatenation property
- Euclidean GCD Algorithm
- Optimization using mathematical observation
- Time complexity improvement
- Pattern repetition problems

---

# Related Topics

- Strings
- Mathematics
- Euclidean Algorithm
- GCD
- Pattern Matching

---

# Similar Problems

1. Repeated Substring Pattern
2. Greatest Common Divisor
3. String Compression
4. KMP Pattern Matching
5. Repeated String Match

---