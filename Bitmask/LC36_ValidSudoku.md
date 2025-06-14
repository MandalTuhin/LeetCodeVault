# LC36 - Valid Sudoku

**Date:** 2025-06-13  
**Status:** ✅ Solved  
**Tags:** Bitmask, HashSet, Grid  
**Difficulty:** Medium  
**Spaced Repetition:** 🔁 1 week

---
##  Problem Summary
Check if a 9x9 board is a valid Sudoku.

---

## 💡 Intuition
- Each number must appear only once in row/col/box
- Use 3 sets or bitmasks to track this

---

## 🔍 Approaches

### 1. HashSet
- Track (row, col, box) as strings in set
- Simple, readable

### 2. Bitmask
- Use 9 integers per row/col/box
- Set/check bits using `1 << digit`

---
## 🧪 Code Walkthrough \
### 1. HashSet Approach
```cpp
class Solution {
public:
  binary validSudoku(vector<vector<int>> board) {
    unordered_map<int, unordered_set<int>> rows, cols;
    map<pair<int, int>, unordered_set<int>> squares;
    for (int r = 0; r < 9; r++) {
      for (int c = 0; c < 9; c++) {
        if (board[r][c] == '.')
          continue;

        pair<int, int> squaresIndex = {r / 3, c / 3};

        if (rows[r].count(board[r][c]) || cols[c].count(board[r][c]) ||
            squares[squaresIndex].count(board[r][c])) {
          return false;
        }

        rows[r].insert(board[r][c]);
        cols[c].insert(board[r][c]);
        squares[squaresIndex].insert(board[r][c]);
      }
    }
    return true;
  }
};
```

### 2. Bitmask Approach

```cpp
int rows[9] = {0}, cols[9] = {0}, boxes[9] = {0};

for (int i = 0; i < 9; i++) {
    for (int j = 0; j < 9; j++) {
        if (board[i][j] == '.') continue;
        int num = board[i][j] - '1';
        int mask = 1 << num;

        if (rows[i] & mask || cols[j] & mask || boxes[(i/3)*3 + j/3] & mask)
            return false;

        rows[i] |= mask;
        cols[j] |= mask;
        boxes[(i/3)*3 + j/3] |= mask;
    }
}
```
---
## 🧠 Lessons Learned
- Bitmasks help reduce space
- Speaking while coding revealed a bug in my box indexing
- `(mask >> digit) & 1` checks if digit is used

---

## 🔁 Next Review: 2025-06-20
