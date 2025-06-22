# Intuition

This is an introductory problem that requires the use of a Stack. Its feels straightforward in the first glance, but it has subtle cases to be aware of before we can fully code the solution. 
What we will do is, we will create a stack of characters called `myStack` and we will use this to store our opening parenthesis and once we found a matching closing parenthesis, we will pop it, if the stack is empty after we have travesed the entire string, that means our given string of parenthesis is valid. 

we will split the problem into 3 cases.  and we will use this to test when to return false and when to return true
##  Case 1 : When we encounter a closing parenthesis but the stack is empty:
lets say we have this test case: `"}"`. 

This would be an test case where we are supposed to return false;
so we note that if during traversal of the given input string, if we encounter a closing bracket _and_ the stack is empty. then we need to immediately return `false`. 


## Case 2: When we encounter a closing parenthesis but the top of the stack has mis-matching opening parenthesis.

lets say we have this test case: `"[}"`.

This is another test case where we are  supposed to return false. how can we achieve this?
we will push each opening bracket into the stack during traversal and if we find a closing bracket, we will first check whether the stack is empty or not. (above condition.). and then we will check whether the current closing bracket that we are on matches with the top of the stack or not, if it doesn't match, we will return false immediately.

## Case 3: When we have no closing brackets for opening brackets. 

consider this test case: `"{{{{"`.

This is yet another test case where we are supposed to return false. how can we do it?
This is a condition we can check after we have traversed the entire input string. if the string is non empty, this means that there are opening brackets that had no closing brackets in the input string.

  

# Approach

- Delclare  a stack of character `myStack`.
- Traverse through the string.
	- for each charcter in the string, check if it is a starting parenthesis, ie. among `{, (, [`. if it is , push it in the stack. 
	- if the character is not a opening parenthesis, then it is sure that they are closing parenthesis as the problem constraints gurantee this. 
		- we first check if the stack is empty, if yes, immediately return `false`. (as per case 1 as we discused)
		- if not, then we check for mismatch between current closing parenthesis and top of the stack, if yes, immediately return false. (as we discussed in case 2).

- check if the stack is empty at the end, if yes, return true, if no, return false. (this means that the input string had extra opening brackets and not enough closing parenthesis to match them. as we discussed in case 3.)
 

# Complexity

- Time complexity: $$O(n)$$, we traverse through the input string only once. 

  

- Space complexity: $$O(n)$$, we used a stack that can go to the length of the input string in the worst case.

  

# Code

```cpp []
class Solution {
public:
  bool isValid(string s) {
    stack<char> parentheses;
    for (size_t i = 0; i < s.size(); i++) {
      if (s[i] == '{' || s[i] == '[' || s[i] == '(') {
        parentheses.push(s[i]);
      } else if (s[i] == '}' || s[i] == ')' || s[i] == ']') {
        if (parentheses.empty()) {
          return false;
        } else {
            char top = parentheses.top();
          if (top == '[' && s[i] == ']' || top == '{' && s[i] == '}' || top == '(' && s[i] == ')')
            parentheses.pop();
          else return false;
        }
      }
    }

    if (parentheses.empty())
      return true;
    return false;
  }
};
```

