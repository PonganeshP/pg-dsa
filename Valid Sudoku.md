
###### Leetcode:
https://leetcode.com/problems/valid-sudoku/
###### Logic
***Naive Approach*** - use 3 hashmap/set to track (row, column, box)
***Optimal Solution*** - use 3 int[] to track numbers by bit index
use bit mask `1<<value` where `value` range `0-8 -> 1 to 9 num`
use `& operator and > 0` to verify if exists or not. if not add to tracker by |=


###### Code
```
public bool IsValidSudoku(char[][] board) {
	int[] rowSet = new int[9];
	var columnSet = new int[9];
	var boxSet = new int[9];
	for(var i = 0; i < board.Length; i++) {
		for(var j = 0; j < board[i].Length; j++) {
			if(board[i][j] == '.') {
				continue;
			}
			var val = board[i][j] - '1';
			if((rowSet[i] & 1 << val) > 0 || (columnSet[j] & 1 << val) > 0 || (boxSet[(i / 3) * 3 + (j / 3)] & 1 << val) > 0) {
				return false;
			}
			rowSet[i] |= 1 << val;
			columnSet[j] |= 1 << val;
			boxSet[(i / 3) * 3 + (j / 3)] |= 1 << val;
		}
	}
	return true;
}
```

###### Time Complexity
O(1)
###### Space Complexity
O(1)
##### Note
`boxSet[(i / 3) * 3 + (j / 3)] |` - To calculate box number
`1 << val where val = 'c'-'1'` - Bit mask
`(rowSet[i] & 1 << val) > 0` - To verify if number is present or not.
`rowSet[i] |= 1 << val;` - OR operator to add the number to tracker
