---
title: Hashing
---

## 1. Count Distinct Elements

**Problem:** Count the number of distinct elements in an array.

**Input:** `[15, 12, 13, 12, 13, 13, 18]`  
**Output:** `4`

**Explanation:**  
Use a HashSet to store unique elements. The size of the set gives the count of distinct elements.

**Code:**
```java
import java.util.*;

class Solution {
    public int countDistinct(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        return set.size();
    }
}
```

**Code Explanation:**  
HashSet automatically handles duplicates. Add all elements and return set size. Time complexity: O(n), Space: O(n).

---

## 2. Frequency of Array Elements

**Problem:** Print the frequency of each element in an array.

**Input:** `[50, 50, 10, 40, 10]`  
**Output:**  
```
50: 2
10: 2
40: 1
```

**Explanation:**  
Use HashMap to count occurrences of each element.

**Code:**
```java
import java.util.*;

class Solution {
    public void printFrequencies(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

**Code Explanation:**  
HashMap stores element as key and frequency as value. Use `getOrDefault` to handle new elements. Time complexity: O(n).

---

## 3. Union of Two Arrays

**Problem:** Count elements in the union of two unsorted arrays.

**Input:** arr1 = `[15, 20, 5, 15]`, arr2 = `[15, 15, 15, 20, 10]`  
**Output:** `4` (elements: 5, 10, 15, 20)

**Explanation:**  
Add all elements from both arrays to a HashSet. Set size gives union count.

**Code:**
```java
import java.util.*;

class Solution {
    public int countUnion(int[] arr1, int[] arr2) {
        Set<Integer> set = new HashSet<>();
        
        for (int num : arr1) {
            set.add(num);
        }
        for (int num : arr2) {
            set.add(num);
        }
        
        return set.size();
    }
}
```

**Code Explanation:**  
HashSet automatically removes duplicates across both arrays. Time complexity: O(n + m), Space: O(n + m).

---

## 4. Intersection of Two Arrays

**Problem:** Print intersection of two unsorted arrays in the order they appear in first array.

**Input:** arr1 = `[10, 15, 20, 25, 30, 50]`, arr2 = `[30, 5, 15, 80]`  
**Output:** `15 30`

**Explanation:**  
Store second array elements in HashSet. Traverse first array and print elements present in set.

**Code:**
```java
import java.util.*;

class Solution {
    public void printIntersection(int[] arr1, int[] arr2) {
        Set<Integer> set = new HashSet<>();
        
        for (int num : arr2) {
            set.add(num);
        }
        
        for (int num : arr1) {
            if (set.contains(num)) {
                System.out.print(num + " ");
            }
        }
    }
}
```

**Code Explanation:**  
Store arr2 in set for O(1) lookup. Traverse arr1 and check membership. Time complexity: O(n + m).

---

## 5. Pair with Given Sum

**Problem:** Check if there exists a pair with given sum in an unsorted array.

**Input:** `[3, 2, 8, 15, -8]`, sum = 17  
**Output:** `true` (pair: 2, 15)

**Explanation:**  
For each element x, check if (sum - x) exists in the hash set.

**Code:**
```java
import java.util.*;

class Solution {
    public boolean hasPairWithSum(int[] nums, int sum) {
        Set<Integer> set = new HashSet<>();
        
        for (int num : nums) {
            if (set.contains(sum - num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}
```

**Code Explanation:**  
For each element, check if complement exists in set. Add current element to set for future lookups. Time complexity: O(n), Space: O(n).

---

## 6. Subarray with Zero Sum

**Problem:** Check if array contains a subarray with sum equal to zero.

**Input:** `[-3, 4, -3, -1, 1]`  
**Output:** `true`

**Explanation:**  
Use prefix sum. If prefix sum repeats or becomes zero, subarray with zero sum exists.

**Code:**
```java
import java.util.*;

class Solution {
    public boolean hasZeroSumSubarray(int[] arr) {
        Set<Integer> set = new HashSet<>();
        int prefixSum = 0;
        
        for (int num : arr) {
            prefixSum += num;
            
            if (prefixSum == 0 || set.contains(prefixSum)) {
                return true;
            }
            set.add(prefixSum);
        }
        return false;
    }
}
```

**Code Explanation:**  
If prefix sum repeats, elements between two occurrences sum to zero. Time complexity: O(n), Space: O(n).

---

## 7. Subarray with Given Sum

**Problem:** Check if subarray with given sum exists.

**Input:** `[5, 8, 6, 13, 3, -1]`, sum = 22  
**Output:** `true`

**Explanation:**  
Use prefix sum. If (prefixSum - sum) exists in map, subarray with given sum exists.

**Code:**
```java
import java.util.*;

class Solution {
    public boolean hasSubarrayWithSum(int[] arr, int sum) {
        Set<Integer> set = new HashSet<>();
        int prefixSum = 0;
        
        for (int num : arr) {
            prefixSum += num;
            
            if (prefixSum == sum || set.contains(prefixSum - sum)) {
                return true;
            }
            set.add(prefixSum);
        }
        return false;
    }
}
```

**Code Explanation:**  
If (prefixSum - sum) exists, subarray from that index to current has sum equal to target. Time complexity: O(n).

---

## 8. Longest Subarray with Given Sum

**Problem:** Find length of longest subarray with given sum.

**Input:** `[5, 8, -4, -4, 9, -2, 2]`, sum = 0  
**Output:** `5`

**Explanation:**  
Store first occurrence of each prefix sum. When prefix sum repeats, calculate length.

**Code:**
```java
import java.util.*;

class Solution {
    public int longestSubarrayWithSum(int[] arr, int sum) {
        Map<Integer, Integer> map = new HashMap<>();
        int prefixSum = 0;
        int maxLen = 0;
        
        for (int i = 0; i < arr.length; i++) {
            prefixSum += arr[i];
            
            if (prefixSum == sum) {
                maxLen = Math.max(maxLen, i + 1);
            }
            
            if (map.containsKey(prefixSum - sum)) {
                maxLen = Math.max(maxLen, i - map.get(prefixSum - sum));
            }
            
            if (!map.containsKey(prefixSum)) {
                map.put(prefixSum, i);
            }
        }
        return maxLen;
    }
}
```

**Code Explanation:**  
Store first occurrence index of each prefix sum. Calculate length when target prefix sum found. Time complexity: O(n).

---

## 9. Longest Subarray with Equal 0s and 1s

**Problem:** Find length of longest subarray with equal number of 0s and 1s.

**Input:** `[1, 0, 1, 1, 1, 0, 0]`  
**Output:** `6`

**Explanation:**  
Treat 0 as -1 and 1 as +1. Problem becomes finding longest subarray with sum 0.

**Code:**
```java
import java.util.*;

class Solution {
    public int longestSubarrayEqualZerosOnes(int[] arr) {
        Map<Integer, Integer> map = new HashMap<>();
        int prefixSum = 0;
        int maxLen = 0;
        
        for (int i = 0; i < arr.length; i++) {
            prefixSum += (arr[i] == 1) ? 1 : -1;
            
            if (prefixSum == 0) {
                maxLen = Math.max(maxLen, i + 1);
            }
            
            if (map.containsKey(prefixSum)) {
                maxLen = Math.max(maxLen, i - map.get(prefixSum));
            } else {
                map.put(prefixSum, i);
            }
        }
        return maxLen;
    }
}
```

**Code Explanation:**  
Convert to +1/-1 array. Use prefix sum technique to find longest zero-sum subarray. Time complexity: O(n).

---

## 10. Longest Common Span with Same Sum

**Problem:** Find longest common span in two binary arrays with same sum.

**Input:** arr1 = `[0, 1, 0, 0, 0, 0]`, arr2 = `[1, 0, 1, 0, 0, 1]`  
**Output:** `4`

**Explanation:**  
Create difference array (arr1[i] - arr2[i]). Find longest subarray with sum 0 in difference array.

**Code:**
```java
import java.util.*;

class Solution {
    public int longestCommonSpan(int[] arr1, int[] arr2) {
        int n = arr1.length;
        Map<Integer, Integer> map = new HashMap<>();
        int prefixSum = 0;
        int maxLen = 0;
        
        for (int i = 0; i < n; i++) {
            int diff = arr1[i] - arr2[i];
            prefixSum += diff;
            
            if (prefixSum == 0) {
                maxLen = Math.max(maxLen, i + 1);
            }
            
            if (map.containsKey(prefixSum)) {
                maxLen = Math.max(maxLen, i - map.get(prefixSum));
            } else {
                map.put(prefixSum, i);
            }
        }
        return maxLen;
    }
}
```

**Code Explanation:**  
Difference array has sum 0 where both arrays have equal sums. Use prefix sum technique. Time complexity: O(n).

---

## 11. Elements Occurring More Than n/k Times

**Problem:** Print elements that occur more than n/k times in the array.

**Input:** `[10, 10, 10, 10, 20, 20, 30]`, k = 2  
**Output:** `10`

**Explanation:**  
Count frequencies using HashMap. Print elements with frequency > n/k.

**Code:**
```java
import java.util.*;

class Solution {
    public void printFrequentElements(int[] arr, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for (int num : arr) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        int threshold = arr.length / k;
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() > threshold) {
                System.out.print(entry.getKey() + " ");
            }
        }
    }
}
```

**Code Explanation:**  
Count frequencies, then filter elements exceeding threshold. Time complexity: O(n), Space: O(n).

---

## Hashing Basics

### HashMap Operations

```java
Map<Integer, Integer> map = new HashMap<>();

// Insert/Update
map.put(key, value);
map.putIfAbsent(key, value);

// Get
int value = map.get(key);
int value = map.getOrDefault(key, defaultValue);

// Check existence
boolean exists = map.containsKey(key);
boolean exists = map.containsValue(value);

// Remove
map.remove(key);

// Size
int size = map.size();

// Iterate
for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
    int key = entry.getKey();
    int value = entry.getValue();
}
```

### HashSet Operations

```java
Set<Integer> set = new HashSet<>();

// Add
set.add(element);

// Check
boolean exists = set.contains(element);

// Remove
set.remove(element);

// Size
int size = set.size();
```

### Time Complexity

| Operation | Average | Worst Case |
|-----------|---------|------------|
| Insert | O(1) | O(n) |
| Search | O(1) | O(n) |
| Delete | O(1) | O(n) |

---
