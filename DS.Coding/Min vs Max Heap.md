Let me explain the time complexity difference between using max heap and min heap for finding top K frequent elements:

**Method 1: Using Max Heap** (Original Solution)
```csharp
public int[] TopKFrequent(int[] nums, int k) {
    // Step 1: O(n)
    var dict = new Dictionary<int, int>();
    foreach(var num in nums)
        if (!dict.TryAdd(num, 1))
            dict[num]++;

    // Step 2: O(n log n) - Adding all elements to max heap
    var pq = new PriorityQueue<int,int>(Comparer<int>.Create((a,b)=>b-a));
    foreach(var pair in dict)
        pq.Enqueue(pair.Key, pair.Value);

    // Step 3: O(k log n) - Extracting k elements
    var res = new int[k];
    for(int i = 0; i < k; i++)
        res[i] = pq.Dequeue();

    return res;
}
// Total: O(n log n)
```

**Method 2: Using Min Heap** (Optimized Solution)
```csharp
public int[] TopKFrequent(int[] nums, int k) {
    // Step 1: O(n)
    var dict = new Dictionary<int, int>();
    foreach(var num in nums)
        if (!dict.TryAdd(num, 1))
            dict[num]++;

    // Step 2: O(n log k) - Maintaining heap of size k
    var pq = new PriorityQueue<int,int>(); // min heap
    foreach(var pair in dict) {
        pq.Enqueue(pair.Key, pair.Value);
        if(pq.Count > k)
            pq.Dequeue(); // Remove smallest frequency
    }

    // Step 3: O(k log k) - Extracting k elements
    var res = new int[k];
    for(int i = k-1; i >= 0; i--)
        res[i] = pq.Dequeue();

    return res;
}
// Total: O(n log k)
```

**Key Differences:**

1. Max Heap Approach:
- Stores all n elements
- Each insertion is O(log n)
- Total complexity: O(n log n)
- Uses more space: O(n)

2. Min Heap Approach:
- Never stores more than k elements
- Each insertion is O(log k)
- Total complexity: O(n log k)
- Uses less space: O(k)

**Why Min Heap is More Efficient:**
1. Smaller Heap Size:
   - Only keeps k elements
   - All heap operations are cheaper (log k vs log n)

2. Early Filtering:
   - Immediately removes smaller frequencies
   - Only keeps top k frequencies at any time

3. Example Scenario:
```csharp
// For array of size 1 million, finding top 10 elements
n = 1,000,000
k = 10

Max Heap: O(1,000,000 × log(1,000,000)) ≈ O(1,000,000 × 20)
Min Heap: O(1,000,000 × log(10)) ≈ O(1,000,000 × 3.32)
```

**Visual Representation:**
```
Max Heap (stores all elements):
            9
          /   \
         7     6
        / \   / \
       5   4 3   2
      / \
     1   0

Min Heap (stores only k=3 elements):
            3
          /   \
         5     4
```

**When to Use Each:**
1. Use Min Heap (Method 2) when:
   - k is significantly smaller than n
   - Memory is a concern
   - Need better performance

2. Use Max Heap (Method 1) when:
   - k is close to n
   - Need all elements sorted
   - Code simplicity is priority

Remember:
- Both solutions give the same result
- Min heap approach is more efficient for typical cases where k << n
- The difference becomes more significant as n grows larger
- Built-in C# PriorityQueue defaults to min heap behavior

Let me know if you need any clarification or want to see more detailed examples!

# Example
I'll explain how both max heap and min heap process these pairs (number, frequency) where k=3. Let's break it down step by step.

Given pairs: [1,3], [2,1], [3,4], [5,2] where first number is the element and second is its frequency.

**Max Heap Approach:**
```
Step 1: Insert [3,4]  (element 3 with frequency 4)
       4(3)
       
Step 2: Insert [1,3]
       4(3)
      /
    3(1)

Step 3: Insert [5,2]
       4(3)
      /    \
    3(1)   2(5)

Step 4: Insert [2,1]
       4(3)
      /    \
    3(1)   2(5)
   /
1(2)

Final Tree (showing frequencies):
       4
      / \
     3   2
    /
   1

Result extraction (top 3):
1. Dequeue: 3 (frequency 4)
2. Dequeue: 1 (frequency 3)
3. Dequeue: 5 (frequency 2)

Answer: [3,1,5]
```

**Min Heap Approach (k=3):**
```
Step 1: Insert [3,4]
       4(3)

Step 2: Insert [1,3]
       4(3)
      /
    3(1)

Step 3: Insert [5,2]
       4(3)
      /    \
    3(1)   2(5)

Step 4: Insert [2,1]  
// Since frequency(2,1) < min current frequency and heap size = k,
// don't insert it

Final Tree (showing frequencies):
       2
      / \
     3   4
     
Elements stored: (Numbers with frequencies)
2 -> 5 (frequency 2)
3 -> 1 (frequency 3)
4 -> 3 (frequency 4)

Result extraction (reverse order):
1. Dequeue: 5 (frequency 2)
2. Dequeue: 1 (frequency 3)
3. Dequeue: 3 (frequency 4)

Answer: [3,1,5]
```

Let's see the code execution with detailed logging:

```csharp
public int[] TopKFrequent(int[] nums, int k) {
    // Input pairs: [1,3], [2,1], [3,4], [5,2]
    
    // Max Heap Approach
    var maxPQ = new PriorityQueue<int,int>(Comparer<int>.Create((a,b)=>b-a));
    
    // Insert operations:
    maxPQ.Enqueue(3, 4);  // Tree: 4(3)
    maxPQ.Enqueue(1, 3);  // Tree: 4(3)/3(1)
    maxPQ.Enqueue(5, 2);  // Tree: 4(3)/3(1),2(5)
    maxPQ.Enqueue(2, 1);  // Tree: 4(3)/3(1),2(5)/1(2)
    
    // Result: [3,1,5]

    // Min Heap Approach (k=3)
    var minPQ = new PriorityQueue<int,int>();
    
    // Insert operations:
    minPQ.Enqueue(3, 4);  // Tree: 4(3)
    minPQ.Enqueue(1, 3);  // Tree: 3(1)/4(3)
    minPQ.Enqueue(5, 2);  // Tree: 2(5)/3(1),4(3)
    // 2,1 not inserted as its frequency is less than min in heap
    
    // Result: [3,1,5]
}
```

Key Differences:
1. Max Heap:
   - Stores all elements (4 pairs)
   - Orders by highest frequency first
   - Takes more space
   - More heapify operations

2. Min Heap:
   - Stores only k elements (3 pairs)
   - Keeps smallest frequencies at top for easy removal
   - Takes less space
   - Fewer heapify operations

The final result [3,1,5] represents:
- 3 with frequency 4
- 1 with frequency 3
- 5 with frequency 2

Both approaches give the same result, but min heap is more efficient because:
1. It maintains smaller tree size (k vs n)
2. Performs fewer heapify operations
3. Uses less memory
4. Each heapify operation is cheaper (log k vs log n)

Let me know if you need any clarification or want to see more detailed steps!