
###### Leetcode:
https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/
###### Logic
***Naive Approach*** - Use hashmap to store index and target-a[i] is found? return index
***Optimal Solution*** - Without visiting the same element, follow the below pseudocode
**Pseudocode:**
- Initialize a result array of size 2
- Set two pointers: `left` at the start and `right` at the end of the array
- While `left` is less than `right`:
    - If the sum of numbers at `left` and `right` equals the target:
        - Store the indices (adding 1 to convert to 1-based indexing)
        - Exit the loop
    - If the sum is greater than the target:
        - Move the right pointer left (to reduce the sum)
    - If the sum is less than the target:
        - Move the left pointer right (to increase the sum)
- Return the result array with the two indices


###### Code
```
public static int[] TwoSum(int[] numbers, int target) {
	var res = new int[2];
	var i = 0;
	var j = numbers.Length - 1;
	while(i < j) {
		if(numbers[i] + numbers[j] == target) {
			res[0] = i + 1;
			res[1] = j + 1;
			break;
		} else if(numbers[i] + numbers[j] > target) {
			j--;
		} else {
			i++;
		}
	}
	return res;
}
```

###### Time Complexity
O(n)
###### Space Complexity
O(1)

##### Note

