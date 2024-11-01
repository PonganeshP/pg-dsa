
###### Leetcode:
https://leetcode.com/problems/longest-consecutive-sequence/
###### Logic
***Naive Approach*** - sorting and find the long consecutive sequence
***Optimal Solution*** - Visualize - find first element(no previous element) - find its sequence - calculate max count


###### Code
```
public int LongestConsecutive(int[] nums) {
	var result = 0;
	var hashSet = new HashSet < int > ();
	foreach(var i in nums) {
		hashSet.Add(i);
	}
	foreach(var num in hashSet) {
		// check if num is the starting
		var a = num - 1;
		if(!hashSet.Contains(a)) {
			// if yes calculate the sequence
			var b = num + 1;
			while(hashSet.Contains(b)) {
				hashSet.Remove(b);
				b++;
			}
			// max(sequenceCount, result)
			var length = b - num;
			result = Math.Max(result, length);
		}
	}
	return result;
}
```

###### Time Complexity
O(n)
###### Space Complexity
O(n)

##### Note
Visualize and infer from the diagram & get the idea how to solve.

