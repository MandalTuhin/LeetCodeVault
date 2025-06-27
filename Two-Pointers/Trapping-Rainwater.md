# LC42 - Trapping Rain Water 

**Date:** 2025-06-27
**Status:** ✅ Solved  
**Tags:** Two-Pointers  
**Difficulty:** Difficult  

---
##  Problem Summary
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

![Elevation Map](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

---

## 💡 Intuition
- The height of water above any block is given by the formula `min[maxSoFarRight, maxSoFarLeft] - height[i]`, where i is the block we are talking about.

- We can use two pointer approach here because no matter how much high a piller is present in between the pillers we are currently studying about. we are only concerned about the height of __the max height of piller seen so far__, in both the left and right hand side. this is the nature of water, you can only trap water between two pillers that are on left and right, not on top of a piller if nothing is there to bound the water from both the sides. This is the key intuition to reducing space complexity of the problem

> This intuition is not very intuitive and we can often forget about it, and it is not obvious form the first glance. we can however trace the algorightm by hand and then it will start to feel intuitive. 

## 🔍 Approaches

### 1. Prefix, Suffix Arrays. - O(n) time, O(n) space
- We can store the prefix max arrays for i, from both the left side and right side, we will use these arrays to find the `min(maxLeft, maxRight)` and then we will subtract `height[i]` and then we will find the amount of water present above the current piller.
- Simpler, more Intuitive.

### 2. Two Pointers - O(n) time, O(1) space.
- Upon inspection, we find that we don't need to find the maximum element of both sides, we can focus on what is the minimum value of the the max heights we have seen so far in the `heights` array and we can move the pointers based on whatever is smaller. and then we can perform (maxLeft - height[l]) or (maxRight - height[r]) based on whatever is smaller. why?? because its the property of water, we don't have to know the height of the heighest piller to find the amount of water above the current piller, we just need to find the minimum of two bounding towers. because that is the bottleneck about how much water can be contained over current block. this question is a direct followup from the container with most water problem.

- O(1) space, elegent.

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


