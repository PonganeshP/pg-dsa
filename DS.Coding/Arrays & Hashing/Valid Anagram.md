
###### Leetcode:
https://leetcode.com/problems/valid-anagram/solutions/
###### Logic
***Naive Approach*** - sort and compare strings
***Optimal Solution*** - use hashmap(add for str1 and remove for str2) finally check the hashmap
or use char array of 26 and calculate alphanumeric and add those in resp array and final check - if any has values then false


###### Code
```
public bool IsAnagram(string s, string t) {
	var hashMap = new Dictionary < char,
		int > ();
	foreach(char c in s) {
		if(hashMap.ContainsKey(c)) hashMap[c]++;
		else hashMap.Add(c, 1);
	}
	foreach(char c in t) {
		if(!hashMap.ContainsKey(c)) {
			return false;
		} else if(hashMap[c] > 0) {
			hashMap[c]--;
			if(hashMap[c] == 0) {
				hashMap.Remove(c);
			}
		}
	}
	if(hashMap.Count == 0) return true;
	return false;
}
```

###### Time Complexity
O(n)
###### Space Complexity
O(n)

##### Note

