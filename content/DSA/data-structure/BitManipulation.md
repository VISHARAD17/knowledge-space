---
title: Bit Manipulation
---

## 1. Check if Kth Bit is Set

**Problem:** Check if the kth bit (1-indexed) of a number is set or not.

**Input:** n = 5 (binary: 101), k = 1  
**Output:** `yes`

**Input:** n = 5, k = 2  
**Output:** `no`

**Explanation:**  
Left shift 1 by (k-1) positions to create a mask with only the kth bit set. Perform AND operation with n to check if that bit is set.

**Code:**
```java
class Solution {
    public boolean checkKthBitSetOrNot(int n, int k) {
        int mask = (1 << (k - 1));
        return (n & mask) != 0;
    }
}
```

**Code Explanation:**  
Create a mask by shifting 1 left by (k-1) positions. AND operation with n will be non-zero only if kth bit is set. Time complexity: O(1).

---

## 2. Count Set Bits

**Problem:** Count the number of set bits (1s) in the binary representation of a number.

**Input:** n = 5 (binary: 101)  
**Output:** `2`

**Explanation:**  
Use Brian Kernighan's algorithm: n & (n-1) removes the rightmost set bit. Count iterations until n becomes 0.

**Code:**
```java
class Solution {
    // Method 1: Brian Kernighan's Algorithm - O(number of set bits)
    public int countSetBits(int n) {
        int res = 0;
        while (n > 0) {
            n = n & (n - 1);
            res++;
        }
        return res;
    }

    // Method 2: Lookup Table - O(1)
    public int countSetBitsOptimized(int n) {
        int[] table = new int[256];
        table[0] = 0;
        
        for (int i = 1; i < 256; i++) {
            table[i] = table[i & (i - 1)] + 1;
        }

        return table[n & 255] + 
               table[(n >> 8) & 255] + 
               table[(n >> 16) & 255] + 
               table[(n >> 24) & 255];
    }
}
```

**Code Explanation:**  
**Method 1:** Each iteration removes one set bit using n & (n-1). Count iterations.  
**Method 2:** Precompute set bits for 0-255. Split 32-bit number into 4 bytes, lookup each, and sum. Time complexity: O(1) with preprocessing.

---

## 3. Check if Power of Two

**Problem:** Check if a given number is a power of 2.

**Input:** n = 8  
**Output:** `yes`

**Input:** n = 6  
**Output:** `no`

**Explanation:**  
A power of 2 has exactly one set bit in binary representation (e.g., 8 = 1000, 16 = 10000). Use n & (n-1) == 0 to check.

**Code:**
```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n == 0) return false;
        return (n & (n - 1)) == 0;
    }
}
```

**Code Explanation:**  
For powers of 2, n & (n-1) equals 0 because subtracting 1 flips all bits after the single set bit. Example: 8 (1000) & 7 (0111) = 0. Time complexity: O(1).

---

## 4. Find One Odd Occurring Number

**Problem:** In an array where all numbers occur even times except one, find the number that occurs odd times.

**Input:** `[4, 3, 4, 4, 4, 5, 5]`  
**Output:** `3`

**Explanation:**  
XOR all elements. Since x ^ x = 0, all even occurrences cancel out, leaving only the odd occurring number.

**Code:**
```java
class Solution {
    public int findOddOccurring(int[] nums) {
        int result = 0;
        for (int num : nums) {
            result ^= num;
        }
        return result;
    }
}
```

**Code Explanation:**  
XOR has properties: x ^ x = 0 and x ^ 0 = x. All pairs cancel out, leaving the odd occurring element. Time complexity: O(n), Space: O(1).

---

## 5. Find Two Odd Occurring Numbers

**Problem:** In an array where all numbers occur even times except two, find both numbers that occur odd times.

**Input:** `[3, 4, 3, 4, 5, 4, 4, 6, 7, 7]`  
**Output:** `5 6`

**Explanation:**  
XOR all elements to get x = a ^ b (where a and b are the two odd numbers). Find a set bit in x to divide numbers into two groups, then XOR each group separately.

**Code:**
```java
class Solution {
    public int[] findTwoOddOccurring(int[] nums) {
        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }

        // Find rightmost set bit
        int rightmostSetBit = xor & ~(xor - 1);

        int res1 = 0, res2 = 0;
        for (int num : nums) {
            if ((num & rightmostSetBit) == 0) {
                res1 ^= num;
            } else {
                res2 ^= num;
            }
        }

        return new int[]{res1, res2};
    }
}
```

**Code Explanation:**  
First XOR gives a ^ b. Find any set bit in this result (difference between a and b). Partition array based on this bit - one group contains a, other contains b. XOR each group to get the two numbers. Time complexity: O(n).

---

## 6. Generate Power Set

**Problem:** Generate all subsets (power set) of a given string.

**Input:** `"abc"`  
**Output:** `["", "a", "b", "c", "ab", "ac", "bc", "abc"]`

**Explanation:**  
For n elements, there are 2^n subsets. Use numbers 0 to 2^n-1, where each bit position represents inclusion/exclusion of an element.

**Code:**
```java
class Solution {
    public List<String> powerSet(String s) {
        int n = s.length();
        int powerSetSize = (1 << n); // 2^n
        List<String> result = new ArrayList<>();

        for (int i = 0; i < powerSetSize; i++) {
            StringBuilder subset = new StringBuilder();
            for (int j = 0; j < n; j++) {
                if ((i & (1 << j)) != 0) {
                    subset.append(s.charAt(j));
                }
            }
            result.add(subset.toString());
        }

        return result;
    }
}
```

**Code Explanation:**  
Iterate from 0 to 2^n-1. For each number, check which bits are set - if jth bit is set, include jth character in subset. This generates all possible combinations. Time complexity: O(n * 2^n).

---

## Bit Manipulation Basics

### Common Operations

**Set a bit:**
```java
n = n | (1 << k);  // Set kth bit
```

**Clear a bit:**
```java
n = n & ~(1 << k);  // Clear kth bit
```

**Toggle a bit:**
```java
n = n ^ (1 << k);  // Toggle kth bit
```

**Check if bit is set:**
```java
boolean isSet = (n & (1 << k)) != 0;
```

**Get rightmost set bit:**
```java
int rightmost = n & -n;
// or
int rightmost = n & ~(n - 1);
```

**Remove rightmost set bit:**
```java
n = n & (n - 1);
```

### Important Properties

- `x ^ x = 0` (XOR of same numbers is 0)
- `x ^ 0 = x` (XOR with 0 gives the number itself)
- `x & (x - 1)` removes the rightmost set bit
- `x & -x` isolates the rightmost set bit
- `~x` flips all bits (bitwise NOT)
- Powers of 2 have exactly one set bit

### Common Use Cases

1. **XOR for finding unique elements** - Pairs cancel out
2. **Bit masking** - Represent subsets, states
3. **Fast operations** - Multiply/divide by powers of 2 using shifts
4. **Space optimization** - Store multiple boolean flags in one integer
5. **Subset generation** - Use binary representation for combinations

---
