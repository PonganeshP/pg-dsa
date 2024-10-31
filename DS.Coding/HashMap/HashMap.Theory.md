# HashMap in C#

In C#, the equivalent of HashMap is called `Dictionary<TKey, TValue>`. It's a generic collection that stores key-value pairs and provides fast lookups based on the key.

## Characteristics of Dictionary<TKey, TValue>

1. Keys must be unique
2. Values can be duplicate
3. Allows null values (if the value type is nullable)
4. Provides fast lookups, insertions, and deletions (O(1) average case)

## Better Alternative: HashSet<T>

While Dictionary is great for key-value pairs, if you only need to store unique elements without associated values, HashSet<T> is a better choice.

# HashSet<T> in C#

HashSet<T> is an unordered collection of unique elements. It's similar to Dictionary<TKey, TValue>, but it only stores keys without associated values.

## Characteristics of HashSet<T>

1. All elements are unique
2. Unordered collection
3. Provides fast lookups, insertions, and deletions (O(1) average case)
4. Efficient for set operations like union, intersection, and difference

## HashSet<T> Example with Different Operations

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create a new HashSet
        HashSet<int> numbers = new HashSet<int>();

        // Add elements (O(1) average case)
        numbers.Add(1);
        numbers.Add(2);
        numbers.Add(3);
        numbers.Add(2); // Duplicate, won't be added

        // Check if an element exists (O(1) average case)
        bool contains4 = numbers.Contains(4); // false
        bool contains2 = numbers.Contains(2); // true

        // Remove an element (O(1) average case)
        numbers.Remove(2);

        // Count elements (O(1))
        int count = numbers.Count; // 2

        // Iterate through elements (O(n))
        foreach (int num in numbers)
        {
            Console.WriteLine(num);
        }

        // Create another HashSet for set operations
        HashSet<int> otherNumbers = new HashSet<int> { 3, 4, 5 };

        // Union (O(n), where n is the size of the smaller set)
        numbers.UnionWith(otherNumbers);

        // Intersection (O(n), where n is the size of the smaller set)
        numbers.IntersectWith(otherNumbers);

        // Difference (O(n), where n is the size of this set)
        numbers.ExceptWith(otherNumbers);

        // Check if it's a subset (O(n), where n is the size of this set)
        bool isSubset = numbers.IsSubsetOf(otherNumbers);

        // Clear all elements (O(n))
        numbers.Clear();
    }
}
```

## Time and Space Complexity

| Operation       | Average Case | Worst Case |
|-----------------|--------------|------------|
| Add             | O(1)         | O(n)       |
| Remove          | O(1)         | O(n)       |
| Contains        | O(1)         | O(n)       |
| Count           | O(1)         | O(1)       |
| Clear           | O(n)         | O(n)       |
| Union           | O(n)         | O(n)       |
| Intersection    | O(n)         | O(n)       |
| Difference      | O(n)         | O(n)       |
| IsSubsetOf      | O(n)         | O(n)       |

Space Complexity: O(n), where n is the number of elements in the HashSet.

Note: The worst-case time complexity for Add, Remove, and Contains operations is O(n) due to potential hash collisions and rehashing. However, these are rare in practice, and the average case is O(1).