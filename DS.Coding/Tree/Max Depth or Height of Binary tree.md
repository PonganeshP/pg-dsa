Use [[Recursion]]

**Condition:** 
1. `node null -> 0`
2. `node.left && node.right both null -> 1`
**Logic:**
`Max depth of a tree = max(depth of root's children) + 1`