
###### Leetcode:
https://leetcode.com/problems/top-k-frequent-elements/
###### Logic
***Naive Approach*** - Hashmap and sort it and pick top k
***Optimal Solution*** - Hashmap and Priority Queue(based on k limit eliminate less priority(frequency) element) ref: [[Min vs Max Heap]]


###### Code
```
public int[] TopKFrequent(int[] nums, int k) {
	var dict = new Dictionary < int,
		int > ();
	foreach(var num in nums)
	if(!dict.TryAdd(num, 1)) dict[num]++;
	// Step 2: O(n log k) - Maintaining heap of size k
	var pq = new PriorityQueue < int,
		int > (); // min heap
	foreach(var pair in dict) {
		pq.Enqueue(pair.Key, pair.Value);
		if(pq.Count > k) pq.Dequeue(); // Remove smallest frequency
	}
	// Step 3: O(k log k) - Extracting k elements
	var res = new int[k];
	for(int i = k - 1; i >= 0; i--) res[i] = pq.Dequeue();
	return res;
}
}
```

###### Time Complexity
naive O(n log n) 
O(n log k) which is better than naive
###### Space Complexity
O(n)

##### Note

