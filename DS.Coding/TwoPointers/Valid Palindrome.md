
###### Leetcode:
https://leetcode.com/problems/valid-palindrome/description/
###### Logic
***Naive Approach*** 
***Optimal Solution*** - Use two pointers approach


###### Code
```
public class Solution {
	public bool IsPalindrome(string s) {
		s = s.ToLower();
		var i = 0;
		var j = s.Length - 1;
		while(i < j) {
			while(i < j && i < s.Length && !Char.IsLetterOrDigit(s[i])) i++;
			while(i < j && j >= 0 && !Char.IsLetterOrDigit(s[j])) j--;
			if(Char.IsLetterOrDigit(s[j]) && Char.IsLetterOrDigit(s[i]) && s[i] != s[j]) return false;
			i++;
			j--;
		}
		return true;
	}
}
```

###### Time Complexity
O(n/2)
###### Space Complexity
O(1)

##### Note

