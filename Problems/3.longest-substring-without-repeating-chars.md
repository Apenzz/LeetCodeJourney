# Problem
[https://leetcode.com/problems/longest-substring-without-repeating-characters/description/](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

# Description
Given a string s, find the length of the longest __substring__ without repeating characters.

# Constraints

- 0 <= s.length <= 5 * 104
- s consists of English letters, digits, symbols and spaces


# Solution
To solve this problem we need to keep track of the longest substring without repeating chars in the string and to do so we use two pointers: _low_ and _high_.

To keep track of the max length substring we store the value in the _curr_max_ variable.
We also initialize a dictionary containing the pairs <char, last_idx_of_char>.

The algorithm iterates over the string:
- If the next char is not in the substring we update the dictonary and increment _high_ by one.
- If the next char _c_ is in the substring we need to remove from the substring all the characters up to and including the first character equal to _c_ but that is easy because we have every index of every character found so far in the dictionary.
We update the pointers according to the above ossservation.



# Code
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        low = high = 0
        curr_max = high - low
        chars = {}
        
        for index, ch in enumerate(s):
            if ch not in s[low:high]:
                chars[ch] = index
                high = index + 1
            else:
                low = chars[ch] + 1
                high = index + 1
                chars[ch] = index
            curr_max = max(curr_max, high-low)
        return curr_max
```

# Complexity
If _n_ is the length of the string then:

- time: O(n)
- space: O(1)