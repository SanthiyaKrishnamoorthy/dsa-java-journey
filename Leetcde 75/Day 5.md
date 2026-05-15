# 345. Reverse Vowels of a String

## Problem Statement

Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are:
- `a`
- `e`
- `i`
- `o`
- `u`

They can appear in both lowercase and uppercase.

---

## Examples

### Example 1

#### Input
```text
s = "IceCreAm"
```

#### Output
```text
"AceCreIm"
```

#### Explanation
Vowels in the string:
```text
I, e, e, A
```

After reversing:
```text
A, e, e, I
```

Result:
```text
"AceCreIm"
```

---

### Example 2

#### Input
```text
s = "leetcode"
```

#### Output
```text
"leotcede"
```

---

# Approach — Two Pointers

## Idea

We use the **Two Pointer Technique**.

- One pointer starts from the beginning.
- Another pointer starts from the end.
- Move both pointers until vowels are found.
- Swap the vowels.
- Continue until both pointers meet.

---

# Algorithm

1. Convert string into character array.
2. Initialize:
   - `left = 0`
   - `right = n - 1`
3. Move `left` forward until a vowel is found.
4. Move `right` backward until a vowel is found.
5. Swap both vowels.
6. Repeat until `left >= right`.
7. Return the modified string.

---

# Java Solution

```java
class Solution {

    public String reverseVowels(String s) {

        char[] arr = s.toCharArray();

        int left = 0;
        int right = arr.length - 1;

        while (left < right) {

            // Move left pointer to next vowel
            while (left < right && !isVowel(arr[left])) {
                left++;
            }

            // Move right pointer to previous vowel
            while (left < right && !isVowel(arr[right])) {
                right--;
            }

            // Swap vowels
            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }

        return new String(arr);
    }

    // Helper method to check vowels
    private boolean isVowel(char ch) {

        return ch == 'a' || ch == 'e' || ch == 'i' ||
               ch == 'o' || ch == 'u' ||
               ch == 'A' || ch == 'E' || ch == 'I' ||
               ch == 'O' || ch == 'U';
    }
}
```

---

# Dry Run

## Input

```text
s = "IceCreAm"
```

## Step-by-Step

| Left | Right | Characters | Action |
|------|--------|------------|--------|
| 0 | 7 | I , m | Right moves |
| 0 | 6 | I , A | Swap |
| 1 | 5 | c , e | Left moves |
| 2 | 5 | e , e | Swap |
| End | End | Done | |

## Final String

```text
"AceCreIm"
```

---

# Complexity Analysis

## Time Complexity

```text
O(n)
```

Each character is visited at most once.

---

## Space Complexity

```text
O(n)
```

Character array is used because Java strings are immutable.

---

# Key Interview Points

- Efficient use of **Two Pointers**
- In-place swapping using character array
- Handles both uppercase and lowercase vowels
- Linear time complexity

---

# Alternative Optimization

Instead of multiple OR conditions, we can use:

```java
String vowels = "aeiouAEIOU";
```

And check:

```java
vowels.indexOf(ch) != -1
```

But the current approach is slightly faster because it avoids extra method calls.

---

# Related Topics

- Two Pointers
- String Manipulation
- Arrays

---

# LeetCode Link

Problem: Reverse Vowels of a String

```text
https://leetcode.com/problems/reverse-vowels-of-a-string/
```
