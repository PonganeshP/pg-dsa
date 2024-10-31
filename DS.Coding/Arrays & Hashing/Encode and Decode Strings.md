
###### Leetcode:
paid. so use neetcode: https://neetcode.io/problems/string-encode-and-decode
###### Logic
***Naive Approach*** - use a delimiter but might end up splitting up strings with the delimiter character
***Optimal Solution*** - use the length of string and suffix it in front of the string along with a non numerical delimiter


###### Code
```
public class Solution {
	public string Encode(IList < string > strs) {
		var result = "";
		foreach(var str in strs) {
			var modifiedStr = $ "{str.Length}#{str}";
			result += modifiedStr;
		}
		return result;
	}
	public List < string > Decode(string s) {
		var result = new List < string > ();
		var index = 0;
		while(s.Length > 0) {
			var lengthToIterate = "";
			while(Char.IsDigit(s.ElementAt(index))) {
				lengthToIterate += s.ElementAt(index);
				index++;
			}
			index = 0;
			if(lengthToIterate.Length > 0) {
				result.Add(s.Substring(lengthToIterate.Length + 1, int.Parse(lengthToIterate))); // 1 for additional non numerical delimiter
			}
			s = s.Substring(int.Parse(lengthToIterate) + 1 + lengthToIterate.Length);
		}
		return result;
	}
}
```

###### Time Complexity
O(n)
###### Space Complexity
O(m)

##### Note
Can improve performance by using [[String Builder]]

