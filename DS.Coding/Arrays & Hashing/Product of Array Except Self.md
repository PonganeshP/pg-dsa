
###### Leetcode:
https://leetcode.com/problems/product-of-array-except-self/
###### Logic
***Naive Approach*** - product of all elements in array and divide by a[i] in another loop
***Optimal Solution*** - without division: front traversal calculate left products and save it in output and right traversal the array and calculate the right products and multiply with the output


###### Code
```
public int[] ProductExceptSelf(int[] nums) {
	var o = new int[nums.Length];
	var pre = 1;
	for(var i = 0; i < nums.Length; i++) {
		o[i] = pre;
		pre = pre * nums[i];
	}
	var post = 1;
	for(var j = nums.Length - 1; j >= 0; j--) {
		o[j] = o[j] * post;
		post = post * nums[j];
	}
	return o;
}
```

###### Time Complexity
O(n)
###### Space Complexity
O(1)

##### Note
Don't rush the codin. Finish the **Pseudocode** first and proceed.
