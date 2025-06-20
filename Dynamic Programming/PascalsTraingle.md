# Intuition

This Problem is actually straight forword once we understand how to generate the array. we already know that we need to find the elements by summing up elements above the element in the triangle. Its just about how to implement this addition.

  

# Approach

- Declare a 2d array named `triangle`. this is where will store the pascal's traigle and we will return this array.

- Initialize a for loop that loops from `i = 0` to `i < numsRow`.

- declare an array by names `row`. This is the row we are currently working on. so we will make changes here. we will give it a size of `i + 1`. and will intialize each element with 1.

- intialize another for loop that loops from `j = 1` to `j < i`. this is the working loop that will do the summation and will make the traingle. we are looping from `j = 1` because we want `1` in starting. we are looping till `j < i` because we don't want to modify the last element and want to keep it as 1;

- do `row[j] = triangle[i - 1][j - 1] + triangle[i - 1][j];`. This is the main idea behind pascal's triangle. we are summing the values of the previous row, and `j` is helping us to add the things with proper indices.

  

# Complexity

- Time complexity:

$$O((numRows)^2)$$, because we are doing numRows computations numRow times.

  

- Space complexity:

$$O(numRows)$$, since the triangle array is not considered extra space, it's part of the problem requirements.

  

# Code

```cpp[]
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> triangle;

        for (int i = 0; i < numRows; i++) {
            vector<int> row(i + 1, 1);
            for (int j = 1; j < i; j++) {
                row[j] = triangle[i - 1][j - 1] + triangle[i - 1][j];
            }

            triangle.push_back(row);
        }

        return triangle;
    }
};
```
