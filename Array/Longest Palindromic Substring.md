https://leetcode.com/problems/longest-palindromic-substring/

Tips:
1. 判断一个字符串是否是回文字符串，比较简便的方法是s == s[::-1]

Original Code:
```ruby
class Solution:        
    def ispalindromic(self, s:str) -> bool:
        if s == s[::-1]:
            return True
        else:
            return False
        
    def longestPalindrome(self, s: str) -> str:
        if s == "" or self.ispalindromic(s):
            return s
        length = 1
        current_string = s[0]
        for i in range(len(s)):
            for j in range(i+1, len(s)):
                if s[i] != s[j - 1]:
                    continue
                elif self.ispalindromic(s[i:j]) and j-i > length:
                    length = j - i
                    current_string = s[i:j]
            if self.ispalindromic(s[i:]) and len(s)-i > length:
                length = len(s) - i
                current_string = s[i:]
        return current_string
```
