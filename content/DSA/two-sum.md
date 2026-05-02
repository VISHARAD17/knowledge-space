---
title: Two Sum
tags: [array, hashmap, easy]
---

# Two Sum

**Difficulty:** Easy  
**Topic:** Array, Hash Map

---

## Problem

Given an array `nums` and a `target`, return indices of two numbers that add up to target.

## Approach

- Use a hash map to store `value → index`
- For each number, check if `target - num` exists in map

**Time:** O(n) | **Space:** O(n)

## Solution

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
```

## Examples

| Input | Output |
|-------|--------|
| `nums = [2,7,11,15], target = 9` | `[0, 1]` |
| `nums = [3,2,4], target = 6` | `[1, 2]` |

## Edge Cases

- [ ] Empty array
- [ ] No solution exists
- [ ] Duplicate numbers
