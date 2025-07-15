# LC567 - [Permutation in String.](https://leetcode.com/problems/permutation-in-string/)

**Date:** 15/07/2025
**Status:** ✅ Solved
**Tags:** Sliding Window, HashMap
**Difficulty:** Medium.

---

## Problem Summary

Given two strings s1 and s2, return true if s2 contains a

of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

Example 1:

Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").

Example 2:

Input: s1 = "ab", s2 = "eidboaoo"
Output: false

---

## 💡 Intuition

- This is a classical sliding window problem that can be easily solved with two hash maps. there is an optimal way to check for the eqality of hash maps and we are going to implement both the solutions.

- We will declare a hashmap which will store the alphabet frequency of each alphabet in the s1 string. and we will use a fixed sliding window of fixed size and we will move it across the entire s2 and see if there is any window that has all the alphabets of same frequency as in our initial hash set.

## 🔍 Approaches

- There are two approaches to solve this problem, both are actually O(n), but if we look closely than the first approach is actually O(26 \* n) (which actually reduces to O(n)). and the second approach is only O(n), one pass through s2.

### 1. Approach 1 - Using HashMaps and comparision of hashMaps.

1. Initialize a hashmap named `s1Count`, we will use it to store freq of characters present in s1.
2. use a for loop to fill the hashmap.
3. Initialize a hashmap named `window`, we will use it to store freq of characters in the current window.
4. initialize l = 0, r = s1.size();
5. while(r < s2.size()):
6. we check if the current window is the valid permutation, if it is, we return
7. else, we increment r and l; we also ensure that the change is reflected in the window hashMap.

### 2. Appraoch 2 - Using a matches variable and 2 arrays to store the freq of alphabets.

1. Initialize an array named `s1Count`, we will use it to store the frequency of all the elements present in the `s1` string.
2. Initialize an array named `s2Count`, we will use it to store the frequency of all the elements present in the current window of `s2` string.
3. we use a for loop to fill in these arrays we declared and we will iterate from `i = 0` to the size of `i < s1.size()`.
   we will use this loop to fill in the `s1count` as well the characters of the current window. (which will start with i = 0 to i = s1.size() - 1)
4. we then declare a variable named `matches`, we initialize this varibale to zero. this will be our key to making the algorighm faster than the previous one.
5. we use a for loop to iterate from 0 to 26. and we find the no of matching alphabets that match the current window and s1(or that are both present in s1 and the current window).
6. Use a for loop to iterate from `r = s1.size()` to `r < s2.size()`, checking each window:
   - **6.1.** If `matches == 26`, the current window is a permutation of `s1`, so return `true`.
   - **6.2.** Add the current character `s2[r]` to `s2Count` by updating its frequency.
   - **6.3.** If incrementing the frequency of `s2[r]` causes `s2Count[s2[r] - 'a'] == s1Count[s2[r] - 'a']`, increment `matches`.
   - **6.4.** If the previous frequency (`s2Count[s2[r] - 'a'] - 1`) matched `s1Count[s2[r] - 'a']`, but now does not, decrement `matches`.
   - **6.5.** For the left pointer (`l`), subtract the frequency of the character being moved past (`s2[l]`), and update `matches` accordingly:
     - If after decrementing, `s2Count[s2[l] - 'a'] == s1Count[s2[l] - 'a']`, increment `matches`.
     - If before decrementing, `s2Count[s2[l] - 'a'] + 1 == s1Count[s2[l] - 'a']`, decrement `matches`.
   - Increment `l` to slide the window forward.

## 🧪 Code Walkthrough

### 1. Using HashMaps and comparision of hashmaps.

```cpp
class Solution {
public:
    binary checkInclusion(string s1, string s2) {
        if(s1.size() > s2.size()) return false;
        unordered_map<char, int> contains;

        for(char ch : s1){
            contains[ch]++;
        }

        int l = 0; int r = s1.size() - 1;
        unordered_map<char, int> window;

        for(int i = 0; i < s1.size(); i++){
            window[s2[i]]++;
        }

        while(r < s2.size()){
            if(window == contains) return true;
            r++;
            if(r < s2.size())
                window[s2[r]]++;
            window[s2[l]]--;
            if(window[s2[l]] == 0)
                window.erase(s2[l]);
            l++;
        }


        return false;

    }
};

```

### 2. Using freqArray and matches variable;

```cpp
class Solution {
public:
    binary checkInclusion(string s1, string s2) {
        if(s1.size() > s2.size()) return false;
        vector<int> s1Count(26, 0);
        vector<int> s2Count(26, 0);

        //store frequency of characters;
        for(int i = 0; i < s1.size(); i++){
            s1Count[s1[i] - 'a']++;
            s2Count[s2[i] - 'a']++;
        }
        int matches = 0;
        for(int i = 0; i < 26; i++){
            if(s1Count[i] == s2Count[i]) matches++;
        }

        int l = 0;
        for(int r = s1.size(); r < s2.size(); r++){
            if(matches == 26) return true;

            s2Count[s2[r] - 'a']++;
            if(s2Count[s2[r] - 'a'] == s1Count[s2[r] - 'a'])
                matches++;
            else if(s2Count[s2[r] - 'a'] - 1 == s1Count[s2[r] - 'a'])
                matches--;

            s2Count[s2[l] - 'a']--;
            if(s2Count[s2[l] - 'a'] == s1Count[s2[l] - 'a'])
                matches++;
            else if(s2Count[s2[l] - 'a'] + 1 == s1Count[s2[l] - 'a'])
                matches--;

            l++;
        }

        return matches == 26;
    }

};

```

---

## 🧠 Lessons Learned

- Writing approches and ideas and dry running code is actually a good way to solve problems and understand code.

```

```
