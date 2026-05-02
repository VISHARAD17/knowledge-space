--- 
title: Arrays 
---

## 1. Check if Array is Sorted

**Problem:** Check if a given array is sorted in non-decreasing order.

**Input:** `[3, 4, 5, 7]`  
**Output:** `true`

**Explanation:**  
Iterate through the array and check if each element is greater than or equal to the previous element. If any element is smaller than its previous element, return false.

**Code:**
```java
class Solution {
    public boolean checkIfArrayIsSorted(int[] nums) {
        int n = nums.length;
        for (int i = 1; i < n; i++) {
            if (nums[i] < nums[i - 1]) return false;
        }
        return true;
    }
}
```

**Code Explanation:**  
Start from index 1 and compare each element with its predecessor. If any element violates the sorted order, return false immediately. Time complexity: O(n).

---

## 2. Second Largest Element

**Problem:** Find the index of the second largest element in an array.

**Input:** `[20, 10, 20, 8, 12]`  
**Output:** `4` (element 12 at index 4)

**Explanation:**  
Track the largest and second largest elements in a single pass. When a new largest is found, the previous largest becomes the second largest.

**Code:**
```java
class Solution {
    public int secondLargestElement(int[] nums) {
        int secondLargestIdx = -1;
        int largestIdx = 0;
        int n = nums.length;

        for (int i = 1; i < n; i++) {
            if (nums[largestIdx] < nums[i]) {
                secondLargestIdx = largestIdx;
                largestIdx = i;
            } else if (nums[i] != nums[largestIdx]) {
                if (secondLargestIdx == -1 || nums[i] > nums[secondLargestIdx]) {
                    secondLargestIdx = i;
                }
            }
        }
        return secondLargestIdx;
    }
}
```

**Code Explanation:**  
Maintain two indices: one for largest and one for second largest. Update them as we traverse. If all elements are same, return -1. Time complexity: O(n).

---

## 3. Reverse Array Elements

**Problem:** Reverse the elements of an array in-place.

**Input:** `[10, 20, 30]`  
**Output:** `[30, 20, 10]`

**Explanation:**  
Use two pointers approach - one at the start and one at the end. Swap elements and move pointers towards center.

**Code:**
```java
class Solution {
    public void reverseArrayElements(int[] nums) {
        int n = nums.length;
        int low = 0, high = n - 1;

        while (low < high) {
            int tmp = nums[low];
            nums[low] = nums[high];
            nums[high] = tmp;
            low++;
            high--;
        }
    }
}
```

**Code Explanation:**  
Two pointers start from both ends and swap elements while moving towards center. Time complexity: O(n), Space complexity: O(1).

---

## 4. Remove Duplicates from Sorted Array

**Problem:** Remove duplicates from a sorted array in-place and return the count of unique elements.

**Input:** `[10, 20, 30, 30, 40, 50, 50]`  
**Output:** `5`, Array becomes `[10, 20, 30, 40, 50, _, _]`

**Explanation:**  
Since array is sorted, duplicates are adjacent. Keep a pointer for the position of unique elements and copy non-duplicate elements.

**Code:**
```java
class Solution {
    public int removeDuplicatesFromSortedArray(int[] nums) {
        int n = nums.length;
        int res = 1;
        for (int i = 1; i < n; i++) {
            if (nums[i - 1] != nums[i]) {
                nums[res] = nums[i];
                res++;
            }
        }
        return res;
    }
}
```

**Code Explanation:**  
Use `res` to track position for next unique element. Compare current with previous; if different, place at `res` position. Time complexity: O(n).

---

## 5. Left Rotate Array by One

**Problem:** Rotate array elements to the left by one position.

**Input:** `[1, 2, 3, 4, 5]`  
**Output:** `[2, 3, 4, 5, 1]`

**Explanation:**  
Store the first element, shift all elements one position left, and place the first element at the end.

**Code:**
```java
class Solution {
    public void leftRotateByOne(int[] nums) {
        int n = nums.length;
        int tmp = nums[0];
        for (int i = 0; i < n - 1; i++) {
            nums[i] = nums[i + 1];
        }
        nums[n - 1] = tmp;
    }
}
```

**Code Explanation:**  
Save first element, shift all elements left by one position, then place saved element at end. Time complexity: O(n).

---

## 6. Left Rotate Array by D Places

**Problem:** Rotate array elements to the left by d positions.

**Input:** `[1, 2, 3, 4, 5]`, d = 2  
**Output:** `[3, 4, 5, 1, 2]`

**Explanation:**  
Store first d elements in temporary array, shift remaining elements left, then copy temporary elements to end.

**Code:**
```java
class Solution {
    public void leftRotateByDPlaces(int[] nums, int d) {
        int n = nums.length;
        d %= n;
        int[] tmp = new int[d];
        
        for (int i = 0; i < d; i++) tmp[i] = nums[i];
        for (int i = d; i < n; i++) nums[i - d] = nums[i];
        for (int i = n - d; i < n; i++) nums[i] = tmp[i - n + d];
    }
}
```

**Code Explanation:**  
First handle case where d > n using modulo. Store first d elements, shift rest left, then append stored elements. Time complexity: O(n).

---

## 7. Move Zeros to End

**Problem:** Move all zeros in array to the end while maintaining order of non-zero elements.

**Input:** `[10, 5, 0, 0, 8, 0, 9, 0]`  
**Output:** `[10, 5, 8, 9, 0, 0, 0, 0]`

**Explanation:**  
Use two pointers - one tracks position for next non-zero element, other traverses array. Swap non-zero elements to front.

**Code:**
```java
class Solution {
    public void moveZerosToEnd(int[] nums) {
        int n = nums.length;
        int curIdx = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] != 0) {
                int tmp = nums[curIdx];
                nums[curIdx] = nums[i];
                nums[i] = tmp;
                curIdx++;
            }
        }
    }
}
```

**Code Explanation:**  
`curIdx` points to position where next non-zero should go. When non-zero found, swap with position at `curIdx`. Time complexity: O(n).

---

## 8. Leaders in Array

**Problem:** Find all leaders in array. An element is a leader if no greater element exists on its right.

**Input:** `[7, 10, 4, 3, 6, 5, 2]`  
**Output:** `[10, 6, 5, 2]`

**Explanation:**  
Traverse from right to left. Last element is always a leader. Update current leader when a larger element is found.

**Code:**
```java
class Solution {
    public void leadersInArray(int[] nums) {
        int n = nums.length;
        int curLeader = nums[n - 1];
        System.out.print(curLeader + " ");
        
        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] > curLeader) {
                System.out.print(nums[i] + " ");
                curLeader = nums[i];
            }
        }
    }
}
```

**Code Explanation:**  
Start from rightmost element (always a leader). Moving left, if element is greater than current leader, it's a new leader. Time complexity: O(n).

---

## 9. Maximum Difference (arr[j] - arr[i] where j > i)

**Problem:** Find maximum value of arr[j] - arr[i] such that j > i.

**Input:** `[2, 3, 10, 6, 4, 8, 1]`  
**Output:** `8` (10 - 2)

**Explanation:**  
Track minimum element seen so far. For each element, calculate difference with minimum and update maximum difference.

**Code:**
```java
class Solution {
    public int maxDiffInOrder(int[] nums) {
        int n = nums.length;
        int maxDiff = Integer.MIN_VALUE;
        int minEleSoFar = nums[0];

        for (int i = 1; i < n; i++) {
            minEleSoFar = Math.min(nums[i], minEleSoFar);
            maxDiff = Math.max(maxDiff, nums[i] - minEleSoFar);
        }
        return maxDiff;
    }
}
```

**Code Explanation:**  
Keep track of minimum element encountered. For each element, compute difference with minimum and update max difference. Time complexity: O(n).

---

## 10. Frequency in Sorted Array

**Problem:** Print frequency of each element in a sorted array.

**Input:** `[10, 10, 10, 25, 30, 30]`  
**Output:**  
```
10 : 3
25 : 1
30 : 2
```

**Explanation:**  
Since array is sorted, identical elements are adjacent. Count consecutive occurrences of each element.

**Code:**
```java
class Solution {
    public void findFreqInSortedArray(int[] nums) {
        int n = nums.length;
        int curFrq = 1;
        
        for (int i = 1; i < n; i++) {
            if (nums[i] == nums[i - 1]) {
                curFrq++;
            } else {
                System.out.println(nums[i - 1] + " : " + curFrq);
                curFrq = 1;
            }
        }
        System.out.println(nums[n - 1] + " : " + curFrq);
    }
}
```

**Code Explanation:**  
Compare each element with previous. If same, increment count; otherwise print previous element's frequency and reset count. Time complexity: O(n).

---

## 11. Stock Buy and Sell

**Problem:** Find maximum profit from buying and selling stocks multiple times (can buy and sell on any day).

**Input:** `[1, 5, 3, 8, 12]`  
**Output:** `13` (buy at 1, sell at 5, buy at 3, sell at 12)

**Explanation:**  
Profit is sum of all increasing segments. Add difference whenever next day price is higher than current day.

**Code:**
```java
class Solution {
    public int buyAndSellStock(int[] nums) {
        int n = nums.length;
        int totalProfit = 0;
        for (int i = 1; i < n; i++) {
            if (nums[i] > nums[i - 1]) {
                totalProfit += (nums[i] - nums[i - 1]);
            }
        }
        return totalProfit;
    }
}
```

**Code Explanation:**  
Sum all positive differences between consecutive days. This captures all upward price movements. Time complexity: O(n).

---

## 12. Trapping Rain Water

**Problem:** Calculate how much water can be trapped between bars after raining.

**Input:** `[3, 0, 1, 2, 5]`  
**Output:** `6`

**Explanation:**  
Water trapped at each position = min(max_left, max_right) - current_height. Precompute max heights on left and right for each position.

**Code:**
```java
class Solution {
    public int trappingRainWater(int[] nums) {
        int n = nums.length;
        int totalWater = 0;
        int[] leftMax = new int[n];
        int[] rightMax = new int[n];
        
        leftMax[0] = nums[0];
        rightMax[n - 1] = nums[n - 1];

        for (int i = 1; i < n; i++) {
            leftMax[i] = Math.max(leftMax[i - 1], nums[i]);
        }
        for (int i = n - 2; i >= 0; i--) {
            rightMax[i] = Math.max(rightMax[i + 1], nums[i]);
        }

        for (int i = 1; i < n - 1; i++) {
            totalWater += Math.min(leftMax[i], rightMax[i]) - nums[i];
        }

        return totalWater;
    }
}
```

**Code Explanation:**  
Precompute maximum heights to left and right of each position. Water at position i is limited by minimum of these maxima minus bar height. Time complexity: O(n).

---

## 13. Maximum Consecutive 1s

**Problem:** Find length of longest sequence of consecutive 1s in binary array.

**Input:** `[1, 0, 1, 1, 1, 1, 0, 1, 1]`  
**Output:** `4`

**Explanation:**  
Track current consecutive count. Reset when 0 is encountered, update maximum length.

**Code:**
```java
class Solution {
    public int maxConsecutiveOnes(int[] nums) {
        int n = nums.length;
        int curLen = 0;
        int maxLen = 0;

        for (int x : nums) {
            if (x == 0) {
                maxLen = Math.max(maxLen, curLen);
                curLen = 0;
            } else {
                curLen++;
            }
        }
        return Math.max(maxLen, curLen);
    }
}
```

**Code Explanation:**  
Maintain current streak length. When 1 is found, increment; when 0 is found, update max and reset. Time complexity: O(n).

---

## 14. Maximum Subarray Sum (Kadane's Algorithm)

**Problem:** Find maximum sum of any contiguous subarray.

**Input:** `[-5, 1, -2, 3, -1, 2, -2]`  
**Output:** `3` (subarray [3, -1, 2])

**Explanation:**  
At each position, decide whether to extend previous subarray or start new one. Track maximum sum ending at each position.

**Code:**
```java
class Solution {
    public int maxSubarraySum(int[] nums) {
        int n = nums.length;
        int maxSum = nums[0];
        int maxEnding = nums[0];
        
        for (int i = 1; i < n; i++) {
            maxEnding = Math.max(nums[i], maxEnding + nums[i]);
            maxSum = Math.max(maxSum, maxEnding);
        }
        return maxSum;
    }
}
```

**Code Explanation:**  
`maxEnding` tracks max sum ending at current position. Either extend previous subarray or start fresh. Update global max. Time complexity: O(n).

---

## 15. Longest Even-Odd Subarray

**Problem:** Find length of longest subarray with alternating even and odd elements.

**Input:** `[5, 10, 20, 6, 3, 8]`  
**Output:** `5` (subarray [10, 20, 6, 3, 8])

**Explanation:**  
Track current alternating sequence length. Reset when pattern breaks.

**Code:**
```java
class Solution {
    public int longestEvenOddSubarray(int[] nums) {
        int n = nums.length;
        int curLen = 1, maxLen = 1;

        for (int i = 1; i < n; i++) {
            if ((nums[i] % 2 == 0 && nums[i - 1] % 2 == 1) || 
                (nums[i] % 2 == 1 && nums[i - 1] % 2 == 0)) {
                curLen++;
                maxLen = Math.max(maxLen, curLen);
            } else {
                curLen = 1;
            }
        }
        return maxLen;
    }
}
```

**Code Explanation:**  
Check if current and previous elements have different parity. If yes, extend sequence; otherwise reset. Time complexity: O(n).

---

## 16. Maximum Circular Subarray Sum

**Problem:** Find maximum sum of subarray in circular array (last element connects to first).

**Input:** `[5, -2, 3, 4]`  
**Output:** `12` (circular subarray [3, 4, 5])

**Explanation:**  
Maximum can be either normal subarray or circular. For circular, find minimum subarray sum and subtract from total.

**Code:**
```java
class Solution {
    private int normalMaxSum(int[] nums) {
        int res = nums[0];
        int maxEnding = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxEnding = Math.max(nums[i], maxEnding + nums[i]);
            res = Math.max(res, maxEnding);
        }
        return res;
    }

    public int maxCircularSumSubarray(int[] nums) {
        int n = nums.length;
        int maxNormal = normalMaxSum(nums);
        
        if (maxNormal < 0) return maxNormal;
        
        int arrSum = 0;
        for (int i = 0; i < n; i++) {
            arrSum += nums[i];
            nums[i] *= -1;
        }
        int maxCircular = arrSum + normalMaxSum(nums);
        return Math.max(maxNormal, maxCircular);
    }
}
```

**Code Explanation:**  
Find normal max sum. Then invert array, find max sum (which gives min of original), subtract from total. Return maximum of both. Time complexity: O(n).

---

## 17. Majority Element

**Problem:** Find element appearing more than n/2 times (Boyer-Moore Voting Algorithm).

**Input:** `[6, 8, 4, 8, 8]`  
**Output:** `8`

**Explanation:**  
Use voting algorithm to find candidate, then verify if it appears more than n/2 times.

**Code:**
```java
class Solution {
    public int majorityElement(int[] nums) {
        int res = 0, count = 1;
        int n = nums.length;
        
        for (int i = 1; i < n; i++) {
            if (nums[res] == nums[i]) {
                count++;
            } else {
                count--;
            }
            if (count == 0) {
                res = i;
                count = 1;
            }
        }

        count = 0;
        for (int i = 0; i < n; i++) {
            if (nums[res] == nums[i]) count++;
        }
        
        if (count > n / 2) return res;
        return -1;
    }
}
```

**Code Explanation:**  
First pass finds candidate using voting (increment for same, decrement for different). Second pass verifies candidate. Time complexity: O(n), Space: O(1).

---

## 18. Minimum Consecutive Flips

**Problem:** Find minimum groups to flip in binary array to make all elements same.

**Input:** `[0, 0, 1, 1, 0, 0, 1, 1, 0, 1]`  
**Output:** Groups to flip (indices)

**Explanation:**  
Always flip the element different from first element. This gives minimum flips.

**Code:**
```java
class Solution {
    public void minFlips(int[] nums) {
        int n = nums.length;
        
        for (int i = 1; i < n; i++) {
            if (nums[i] != nums[i - 1]) {
                if (nums[i] != nums[0]) {
                    System.out.print("From " + i + " to ");
                } else {
                    System.out.println(i - 1);
                }
            }
        }
        if (nums[n - 1] != nums[0]) {
            System.out.println(n - 1);
        }
    }
}
```

**Code Explanation:**  
Identify groups different from first element. These are the groups to flip. Time complexity: O(n).

---

## 19. Maximum Sum of K Consecutive Elements (Sliding Window)

**Problem:** Find maximum sum of k consecutive elements.

**Input:** `[10, 5, -2, 20, 1]`, k = 3  
**Output:** `23` (subarray [5, -2, 20])

**Explanation:**  
Use sliding window - compute sum of first k elements, then slide window by removing first and adding next element.

**Code:**
```java
class Solution {
    public int maxSumOfKConsecutive(int[] nums, int k) {
        int n = nums.length;
        int res = Integer.MIN_VALUE;
        int curSum = 0;
        
        for (int i = 0; i < k; i++) curSum += nums[i];
        res = Math.max(res, curSum);
        
        for (int i = k; i < n; i++) {
            curSum -= nums[i - k];
            curSum += nums[i];
            res = Math.max(res, curSum);
        }
        return res;
    }
}
```

**Code Explanation:**  
Calculate initial window sum. Then slide window: subtract leftmost element, add new rightmost element. Time complexity: O(n).

---

## 20. Subarray with Given Sum

**Problem:** Check if subarray with given sum exists (array has non-negative numbers).

**Input:** `[1, 4, 20, 3, 10, 5]`, sum = 33  
**Output:** `YES`

**Explanation:**  
Use two pointers. Expand window if sum is less, shrink if sum is more.

**Code:**
```java
class Solution {
    public boolean subarrayWithGivenSum(int[] nums, int sum) {
        int n = nums.length;
        int start = 0, end = 0;
        int curSum = 0;
        
        while (end < n) {
            if (curSum < sum) {
                curSum += nums[end];
                end++;
            } else if (curSum > sum) {
                curSum -= nums[start];
                start++;
            } else {
                return true;
            }
        }
        return false;
    }
}
```

**Code Explanation:**  
Two pointers maintain window. Expand right if sum too small, shrink left if too large. Time complexity: O(n).

---

## 21. Prefix Sum

**Problem:** Answer range sum queries efficiently using prefix sum.

**Input:** `[2, 8, 3, 9, 6, 5, 4]`, query: sum from index 1 to 3  
**Output:** `20` (8 + 3 + 9)

**Explanation:**  
Precompute cumulative sums. Range sum = prefix[r] - prefix[l-1].

**Code:**
```java
class Solution {
    public int prefixSum(int[] nums, int l, int r) {
        int n = nums.length;
        int[] prefix = new int[n];
        prefix[0] = nums[0];

        for (int i = 1; i < n; i++) {
            prefix[i] = nums[i] + prefix[i - 1];
        }
        
        int sum = prefix[r];
        if (l != 0) sum -= prefix[l - 1];
        return sum;
    }
}
```

**Code Explanation:**  
Build prefix array where prefix[i] = sum of elements from 0 to i. Range sum computed in O(1). Preprocessing: O(n).

---

## 22. Equilibrium Point

**Problem:** Find if array has equilibrium point (sum of left elements = sum of right elements).

**Input:** `[3, 4, 8, -9, 20, 6]`  
**Output:** `YES` (at index 2)

**Explanation:**  
Track left sum and right sum. At equilibrium point, both are equal.

**Code:**
```java
class Solution {
    public int isEquilibrium(int[] nums) {
        int n = nums.length;
        int leftSum = 0, rightSum = 0;
        
        for (int x : nums) rightSum += x;

        for (int i = 0; i < n; i++) {
            rightSum -= nums[i];
            if (leftSum == rightSum) return i;
            leftSum += nums[i];
        }
        return -1;
    }
}
```

**Code Explanation:**  
Calculate total sum as right sum. Traverse array: subtract current from right, check equality, add to left. Time complexity: O(n).

---

## 23. Maximum Appearing Element in Ranges

**Problem:** Find element appearing in maximum number of given ranges.

**Input:** left = `[1, 2, 4]`, right = `[4, 5, 7]`  
**Output:** `4` (appears in ranges [1,4] and [4,7])

**Explanation:**  
Use difference array technique. Mark start and end+1 of ranges, then compute prefix sum to get frequencies.

**Code:**
```java
class Solution {
    public int maxAppearingElementInRange(int[] left, int[] right) {
        int n = left.length;
        int[] freq = new int[101];

        for (int i = 0; i < n; i++) {
            freq[left[i]]++;
            freq[right[i] + 1]--;
        }

        int res = 0;
        for (int i = 1; i < 101; i++) {
            freq[i] += freq[i - 1];
            if (freq[i] > freq[res]) {
                res = i;
            }
        }
        return res;
    }
}
```

**Code Explanation:**  
Increment at range start, decrement at range end+1. Compute prefix sum to get actual frequencies. Find index with max frequency. Time complexity: O(n + max_value).

---
