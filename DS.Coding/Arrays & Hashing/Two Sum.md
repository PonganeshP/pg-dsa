
###### Leetcode:
https://leetcode.com/problems/two-sum/description/
###### Logic
***Naive Approach*** - Using two for loops one for storing hashmap values with key and index value, another for looping through array.
***Optimal Solution*** - Use hashmap to solve in a single for loop. Calculate `target - a[i]`. If present in the hashmap then get index from there and return.


###### Code
```
public class Solution {
	public int[] TwoSum(int[] nums, int target) {
		Dictionary < int, int > dict = new();
		dict[nums[0]] = 0;
		for(int i = 1; i < nums.Length; i++) {
			if(dict.ContainsKey(target - nums[i])) {
				return new int[2] {
					i,
					dict[target - nums[i]]
				};
			} else {
				dict.TryAdd(nums[i], i);
			}
		}
		return new int[] {};
	}
}
```

###### Time Complexity
O(n)
###### Space Complexity
O(n)

##### Note

