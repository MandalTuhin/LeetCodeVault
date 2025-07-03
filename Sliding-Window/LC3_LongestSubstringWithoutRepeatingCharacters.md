# LC3 - Longest Substring Without Repeating Characters.

**Date:** 2025-07-03
**Status:** ✅ Solved  
**Tags:** Two-Pointers, Sliding Window, Hash-table  
**Difficulty:** Medium  

---
##  Problem Summary
Given a string s, find the length of the longest without duplicate characters.

Problem Link: [Problem Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

> **Input:** s = "abcabcbb"   
> **Output:** 3
> **Explanation:** The answer is "abc", with the length  of 3.

> **Input:** nums = "kkkkkk"  
> **Output:** 1
> **Explanation:** The answer is "b", with the length of 1.

> **Input:** nums = "abkmat"  
> **Output:** 5
> **Explanation:** The answer is "bkmat", with the length of 5.

---

## 💡 Intuition

This is a standard sliding window problem. we will have to initialize two pointer and move the pointer according to some conditions. The intuition is that we have to keep one pointer(`L`) on the start of the window (the substring where no characters repeat.) and we will increment the right pointer (`R`). and we want to move left as soon as we find that some index has been found that already exists in the unordered_map.

we will maintain an unordered_map(hash table) named lastOccur, that will keep the record of the last index of the occurance of all unique letters encountered so far by the right pointer.


## 🔍 Approaches
- Initialize an `unordered_map<char, int>` named `lastOccur`.
- intialize `L` to `0`. (this is our left pointer)
- initialize `maxLen` with 0. (this is what we will be using to store the maximum found length of non-duplicate-character substring).
- Iterate through each value in string `s`. we will use a variable `R` to do it(our right pointer).
    - we check if `s[R]`(current character) exits in `lastOccur`.
        - we update `L` to `max(L, lastOccur[s[r]] + 1)`(here we don't want to move `L` back when we find something that we have already passed).
    - we update `lastOccur[s[R]]` to `R`, ie. the latest found index. 
    - we try to update `maxLen` with `max(maxLen, R - L + 1)` (R - L + 1 is the size of the window.)

---
## 🧪 Code Walkthrough \

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> lastOccur;
        int maxLen = 0;
        int L = 0;
        for(int R = 0; R < s.size(); R++){
            if(lastOccur.count(s[R])){
                L = max(lastOccuuuuuuuur[s[R]] + 1, L);
            }
                lastOccur[s[R]] = R;

            maxLen = max(maxLen, R - L + 1);
            
        }

        return maxLen;
    }
};


```
---
## 🧠 Lessons Learned
- Writing approches and ideas and dry running code is actually a good way to solve problems and understand code.

- No question is actually out of reach. I just have to be a little bit patient and leverage the facts that are given in the question. 
