# LC128 Longest Consecutive Sequence 

**Date:** 2025-06-27
**Status:** ✅ Solved  
**Tags:** Arrays  
**Difficulty:** Medium

---
##  Problem Summary

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

#### Example 1:

> **Input:** nums = [100,4,200,1,3,2]   
> **Output:** 4    
> **Explanation:** The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4. 

Example 2:

Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9

Example 3:

Input: nums = [1,0,1,2]
Output: 3



---

## 💡 Intuition


## 🔍 Approaches

### 1. Prefix, Suffix Arrays. - O(n) time, O(n) space
-

-

### 2. Two Pointers - O(n) time, O(1) space.
-

-

---
## 🧪 Code Walkthrough \
### 1. Prefix, Suffix Arrays.

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        vector<int> maxLeftHeight(n), maxRightHeight(n);
        int n = height.size();

        maxLeftHeight[0] = height[0];
        // entering max values going from left to right.
        for(int i = 1; i < n; i++){
            maxLeftHeight[n] = max(height[i], maxLeftHeight[i - 1]); 
        }

        maxRightHeight[n - 1] = height[n - 1];
        for(int i = n - 2; i >= 0; i--){
            maxRightHeight[i] = max(height[i], maxRightHeight[i + 1]);
        }

        int res = 0;
        for(int i = 0; i < nums.size(); i++){
            res += min(maxLeftHeight[i], maxRightHeight[i]) - height[i];
        }

        return res;
    }
};
```

### 2. Two Pointers

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int l = 0, r = height.size() - 1;
        int maxLeft = height[l], maxRight = height[r];

        int res = 0;
        while(l < r){
            if(maxLeft < maxRight){
                l++;
                maxLeft = max(maxLeft, height[i]);
                res += maxLeft - height[i];
            } else {
                r--;
                maxRight = max(maxRight, height[i]);
                res += max(maxRight, height[i]);
            }
        }

        return res;
    }
};
```
---
## 🧠 Lessons Learned
- Writing approches and ideas and dry running code is actually a good way to solve problems and understand code.

- No question is actually out of reach. I just have to be a little bit patient and leverage the facts that are given in the question. This question leverages and optimizes the fact that water can only be stored when it is bounded by left and right pillers, which is key to optimizing this question from O(n) space to O(1) space.


