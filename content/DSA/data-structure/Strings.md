# Strings - Data Structure & Algorithms

## 1. Palindrome Check

**Problem:** Check if a given string is a palindrome.

**Input:** `"ABCDCBA"`  
**Output:** `yes`

**Input:** `"ABC"`  
**Output:** `no`

**Explanation:**  
Use two pointers - one at start and one at end. Compare characters while moving towards center.

**Code:**
```java
class Solution {
    public boolean isPalindrome(String s) {
        int i = 0, j = s.length() - 1;
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

**Code Explanation:**  
Two pointers approach: compare characters from both ends moving towards center. If any mismatch found, return false. Time complexity: O(n).

---

## 2. Check if String is Subsequence

**Problem:** Check if string s2 is a subsequence of string s1.

**Input:** s1 = `"ABCD"`, s2 = `"AD"`  
**Output:** `YES`

**Input:** s1 = `"ABCDE"`, s2 = `"AED"`  
**Output:** `NO`

**Explanation:**  
A subsequence doesn't need to be contiguous. Use two pointers to traverse both strings, matching characters in order.

**Code:**
```java
class Solution {
    public boolean isSubsequence(String s1, String s2) {
        int i = 0, j = 0;
        int n = s1.length(), m = s2.length();
        
        while (i < n && j < m) {
            if (s1.charAt(i) == s2.charAt(j)) {
                j++;
            }
            i++;
        }
        return j == m;
    }
}
```

**Code Explanation:**  
Traverse s1 with pointer i. When character matches s2[j], increment j. If j reaches end of s2, all characters matched. Time complexity: O(n).

---

## 3. Check Anagram

**Problem:** Check if two strings are anagrams (permutations of each other).

**Input:** s1 = `"aabca"`, s2 = `"acaba"`  
**Output:** `YES`

**Explanation:**  
Count frequency of each character. If both strings have same character frequencies, they are anagrams.

**Code:**
```java
class Solution {
    public boolean isAnagram(String s1, String s2) {
        if (s1.length() != s2.length()) {
            return false;
        }
        
        int[] count = new int[256];
        int n = s1.length();
        
        for (int i = 0; i < n; i++) {
            count[s1.charAt(i)]++;
            count[s2.charAt(i)]--;
        }
        
        for (int i = 0; i < 256; i++) {
            if (count[i] != 0) {
                return false;
            }
        }
        return true;
    }
}
```

**Code Explanation:**  
Use frequency array. Increment for s1 characters, decrement for s2. If all counts are zero, strings are anagrams. Time complexity: O(n), Space: O(1).

---

## 4. Leftmost Repeating Character

**Problem:** Find the index of the leftmost character that repeats in the string.

**Input:** `"cabbad"`  
**Output:** `0` (character 'a' at index 0 repeats)

**Explanation:**  
Count character frequencies, then find the first character with frequency > 1.

**Code:**
```java
class Solution {
    // Method 1: Two pass - O(n)
    public int leftmostRepeating(String s) {
        int[] count = new int[256];
        int n = s.length();
        
        for (int i = 0; i < n; i++) {
            count[s.charAt(i)]++;
        }
        
        for (int i = 0; i < n; i++) {
            if (count[s.charAt(i)] > 1) {
                return i;
            }
        }
        return -1;
    }
    
    // Method 2: Single pass - O(n)
    public int leftmostRepeatingOptimized(String s) {
        int[] firstIndex = new int[256];
        Arrays.fill(firstIndex, -1);
        int res = Integer.MAX_VALUE;
        int n = s.length();
        
        for (int i = 0; i < n; i++) {
            int idx = firstIndex[s.charAt(i)];
            if (idx == -1) {
                firstIndex[s.charAt(i)] = i;
            } else {
                res = Math.min(res, idx);
            }
        }
        return res == Integer.MAX_VALUE ? -1 : res;
    }
}
```

**Code Explanation:**  
**Method 1:** Count frequencies, then find first character with count > 1.  
**Method 2:** Store first occurrence index. When character repeats, update result with minimum index. Time complexity: O(n).

---

## 5. Leftmost Non-Repeating Character

**Problem:** Find the index of the leftmost character that doesn't repeat.

**Input:** `"geeksforgeeks"`  
**Output:** `5` (character 'f')

**Explanation:**  
Count frequencies, then find the first character with frequency = 1.

**Code:**
```java
class Solution {
    public int leftmostNonRepeating(String s) {
        int[] count = new int[256];
        int n = s.length();
        
        for (int i = 0; i < n; i++) {
            count[s.charAt(i)]++;
        }
        
        for (int i = 0; i < n; i++) {
            if (count[s.charAt(i)] == 1) {
                return i;
            }
        }
        return -1;
    }
}
```

**Code Explanation:**  
First pass counts character frequencies. Second pass finds first character with count = 1. Time complexity: O(n), Space: O(1).

---

## 6. Check if Strings are Rotations

**Problem:** Check if s2 can be obtained by rotating s1.

**Input:** s1 = `"abcd"`, s2 = `"cdab"`  
**Output:** `yes`

**Explanation:**  
Concatenate s1 with itself. If s2 is substring of (s1 + s1), then s2 is a rotation of s1.

**Code:**
```java
class Solution {
    public boolean areRotations(String s1, String s2) {
        if (s1.length() != s2.length()) {
            return false;
        }
        
        String concatenated = s1 + s1;
        return concatenated.contains(s2);
    }
}
```

**Code Explanation:**  
When s1 is concatenated with itself, all possible rotations appear as substrings. Check if s2 exists in concatenated string. Time complexity: O(n).

---

## 7. Anagram Search (Pattern Matching)

**Problem:** Check if any permutation of pattern exists in the text.

**Input:** text = `"geeksforgeeks"`, pattern = `"frog"`  
**Output:** `yes`

**Explanation:**  
Use sliding window with character frequency comparison. Compare frequency arrays for each window.

**Code:**
```java
class Solution {
    public boolean searchAnagram(String text, String pattern) {
        int n = text.length(), m = pattern.length();
        if (m > n) return false;
        
        int[] countText = new int[256];
        int[] countPattern = new int[256];
        
        for (int i = 0; i < m; i++) {
            countText[text.charAt(i)]++;
            countPattern[pattern.charAt(i)]++;
        }
        
        for (int i = m; i < n; i++) {
            if (Arrays.equals(countText, countPattern)) {
                return true;
            }
            countText[text.charAt(i - m)]--;
            countText[text.charAt(i)]++;
        }
        
        return Arrays.equals(countText, countPattern);
    }
}
```

**Code Explanation:**  
Maintain frequency arrays for pattern and current window. Slide window through text, updating frequencies. Compare arrays at each position. Time complexity: O(n).

---

## 8. Longest Substring with Distinct Characters

**Problem:** Find length of longest substring with all distinct characters.

**Input:** `"abac"`  
**Output:** `3` (substring "bac")

**Explanation:**  
Use sliding window with a hash map to track last occurrence of each character.

**Code:**
```java
class Solution {
    public int longestDistinctSubstring(String s) {
        int n = s.length();
        int[] lastIndex = new int[256];
        Arrays.fill(lastIndex, -1);
        
        int maxLen = 0;
        int start = 0;
        
        for (int end = 0; end < n; end++) {
            start = Math.max(start, lastIndex[s.charAt(end)] + 1);
            maxLen = Math.max(maxLen, end - start + 1);
            lastIndex[s.charAt(end)] = end;
        }
        
        return maxLen;
    }
}
```

**Code Explanation:**  
Track last occurrence of each character. When duplicate found, move start pointer to position after previous occurrence. Update max length. Time complexity: O(n).

---

## 9. Lexicographic Rank of String

**Problem:** Find the lexicographic rank of a string among all its permutations.

**Input:** `"string"`  
**Output:** Rank of the string

**Explanation:**  
For each position, count how many characters are smaller and calculate permutations possible with remaining characters.

**Code:**
```java
class Solution {
    private int factorial(int n) {
        int result = 1;
        for (int i = 2; i <= n; i++) {
            result *= i;
        }
        return result;
    }
    
    public int lexicographicRank(String s) {
        int n = s.length();
        int rank = 1;
        int mul = factorial(n);
        
        int[] count = new int[256];
        for (int i = 0; i < n; i++) {
            count[s.charAt(i)]++;
        }
        
        for (int i = 1; i < 256; i++) {
            count[i] += count[i - 1];
        }
        
        for (int i = 0; i < n - 1; i++) {
            mul /= (n - i);
            rank += count[s.charAt(i) - 1] * mul;
            for (int j = s.charAt(i); j < 256; j++) {
                count[j]--;
            }
        }
        
        return rank;
    }
}
```

**Code Explanation:**  
Use cumulative frequency array. For each position, count smaller characters and multiply by factorial of remaining positions. Time complexity: O(n).

---

## 10. Naive Pattern Search

**Problem:** Find all occurrences of pattern in text.

**Input:** text = `"ABCDABC"`, pattern = `"ABC"`  
**Output:** `0 4` (indices where pattern starts)

**Explanation:**  
Check every position in text if pattern matches starting from that position.

**Code:**
```java
class Solution {
    public void naivePatternSearch(String text, String pattern) {
        int n = text.length(), m = pattern.length();
        
        for (int i = 0; i <= n - m; i++) {
            int j;
            for (j = 0; j < m; j++) {
                if (pattern.charAt(j) != text.charAt(i + j)) {
                    break;
                }
            }
            if (j == m) {
                System.out.print(i + " ");
            }
        }
    }
}
```

**Code Explanation:**  
For each position in text, compare pattern character by character. If all match, print index. Time complexity: O((n-m+1) * m).

---

## 11. KMP Algorithm (Pattern Matching)

**Problem:** Efficiently find all occurrences of pattern in text using KMP algorithm.

**Input:** text = `"ababcababaad"`, pattern = `"ababa"`  
**Output:** `5` (index where pattern starts)

**Explanation:**  
Build LPS (Longest Proper Prefix which is also Suffix) array for pattern. Use it to avoid redundant comparisons.

**Code:**
```java
class Solution {
    private int[] computeLPS(String pattern) {
        int m = pattern.length();
        int[] lps = new int[m];
        int len = 0;
        int i = 1;
        
        while (i < m) {
            if (pattern.charAt(i) == pattern.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        return lps;
    }
    
    public void KMPSearch(String text, String pattern) {
        int n = text.length();
        int m = pattern.length();
        int[] lps = computeLPS(pattern);
        
        int i = 0, j = 0;
        while (i < n) {
            if (pattern.charAt(j) == text.charAt(i)) {
                i++;
                j++;
            }
            
            if (j == m) {
                System.out.print((i - j) + " ");
                j = lps[j - 1];
            } else if (i < n && pattern.charAt(j) != text.charAt(i)) {
                if (j != 0) {
                    j = lps[j - 1];
                } else {
                    i++;
                }
            }
        }
    }
}
```

**Code Explanation:**  
LPS array stores length of longest proper prefix which is also suffix. When mismatch occurs, use LPS to skip redundant comparisons. Time complexity: O(n + m).

---

## 12. Rabin-Karp Algorithm (Pattern Matching)

**Problem:** Find pattern in text using rolling hash technique.

**Input:** text = `"GEEKSFORGEEKS"`, pattern = `"EKS"`  
**Output:** `2 10` (indices)

**Explanation:**  
Compute hash of pattern and compare with hash of each text window. Only compare characters when hashes match.

**Code:**
```java
class Solution {
    private final int d = 256;
    private final int q = 101;
    
    public void rabinKarp(String text, String pattern) {
        int n = text.length(), m = pattern.length();
        int h = 1;
        
        for (int i = 1; i < m; i++) {
            h = (h * d) % q;
        }
        
        int p = 0, t = 0;
        for (int i = 0; i < m; i++) {
            p = (p * d + pattern.charAt(i)) % q;
            t = (t * d + text.charAt(i)) % q;
        }
        
        for (int i = 0; i <= n - m; i++) {
            if (p == t) {
                boolean match = true;
                for (int j = 0; j < m; j++) {
                    if (text.charAt(i + j) != pattern.charAt(j)) {
                        match = false;
                        break;
                    }
                }
                if (match) {
                    System.out.print(i + " ");
                }
            }
            
            if (i < n - m) {
                t = ((d * (t - text.charAt(i) * h)) + text.charAt(i + m)) % q;
                if (t < 0) t += q;
            }
        }
    }
}
```

**Code Explanation:**  
Use rolling hash to compute hash values efficiently. When hash matches, verify by comparing actual characters. Time complexity: O(n + m) average case.

---

## 13. Longest Proper Prefix Suffix (LPS Array)

**Problem:** For each prefix of string, find length of longest proper prefix which is also a suffix.

**Input:** `"aaabaaaac"`  
**Output:** `[0, 1, 2, 0, 1, 2, 3, 3, 0]`

**Explanation:**  
Build LPS array used in KMP algorithm. For each position, find longest matching prefix-suffix.

**Code:**
```java
class Solution {
    public int[] computeLPS(String s) {
        int n = s.length();
        int[] lps = new int[n];
        int len = 0;
        int i = 1;
        
        lps[0] = 0;
        
        while (i < n) {
            if (s.charAt(i) == s.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        
        return lps;
    }
}
```

**Code Explanation:**  
Use dynamic programming approach. When characters match, increment length. When mismatch, use previous LPS value to avoid recomputation. Time complexity: O(n).

---
