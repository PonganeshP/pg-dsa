###### Leetcode: https://leetcode.com/problems/contains-duplicate/
###### Logic
Basic usage of hashset/map (contains - else add)

###### Code
```
public class Solution {
	public bool ContainsDuplicate(int[] nums) {
		var hashSet = new HashSet < int > ();
		foreach(int num in nums) {
			if(hashSet.Contains(num)) return true;
			else {
				hashSet.Add(num);
			}
		}
		return false;
	}
}
```

###### Time Complexity
Average case: O(n)
Worst case: O(n^2) - ref [[HashMap.Theory]]
###### Space Complexity
O(n)

##### Note
