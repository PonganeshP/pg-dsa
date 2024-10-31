
###### Leetcode:
https://leetcode.com/problems/group-anagrams/description/

###### Logic
***naive***: sort and and group by index (O(nlogn) x k)
***optimal***: convert each string to alpha[26] and keep it as key of a map & if similiar alpha is available group under the value 

###### Code
```
public static IList < IList < string >> GroupAnagrams(string[] strs) {
	var result = new List < IList < string >> ();
	var hashMap = new Dictionary < string,
		List < string >> ();
	foreach(var str in strs) {
		var alphaString = _convertToAlphaString(str);
		if(alphaString != null) {
			if(hashMap.ContainsKey(alphaString)) {
				hashMap[alphaString].Add(str);
			} else {
				hashMap.Add(alphaString, new List < string > () {
					str
				});
			}
		}
	}
	foreach(var k in hashMap.Keys) {
		result.Add(hashMap[k]);
	}
	return result;
}
private static string _convertToAlphaString(string str) {
	var alphaArray = new int[26];
	var resultString = "";
	foreach(var c in str) {
		alphaArray[c - 'a']++;
	}
	foreach(var c in alphaArray) {
		resultString = resultString + "-" + c.ToString();
	}
	return resultString;
}
```

###### Time Complexity
O(nk)
###### Space Complexity
O(n)


##### Note

