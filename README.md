# Valid Sudoku
# https://leetcode.com/problems/valid-sudoku

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.
```
Example 1:

Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
Example 2:

Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```
**Note:**

1. A Sudoku board (partially filled) could be valid but is not necessarily solvable.
2. Only the filled cells need to be validated according to the mentioned rules.
3. The given board contain only digits 1-9 and the character '.'.
4. The given board size is always 9x9.


# Implementation :

```java
class Solution {
    private static final int BOARD_SIZE =9;
    private static final int BOX_SIZE = 3;
    
    public boolean isValidSudoku(char[][] board) {
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board.length; j++){
                if(board[i][j] != '.') {
                    if(!isValid(board, i, j, board[i][j]))
                        return false;
                }
            }
        }
        return true;
    }
    
    private boolean isValid(char[][] board, int rowIndex, int columnIndex, char ch) {
	// check if the same row alreday have that same digit
	for (int i = 0; i < BOARD_SIZE; i++) 
	    if (i != columnIndex && board[rowIndex][i] == ch )
	      return false;
		
	// check if the same column alreday have that same digit
	for (int j = 0; j < BOARD_SIZE; j++) 
	    if (j != rowIndex && board[j][columnIndex] == ch )
	      return false;

        // check if the same subgrid(box) alreday have that same digit
	int boxRowOffset = (rowIndex / 3) * BOX_SIZE;
	int boxColumnOffset = (columnIndex / 3) * BOX_SIZE;
		
	for (int i = 0; i < BOX_SIZE; i++) {
	  for (int j = 0; j < BOX_SIZE; j++) {
             if (! ((rowIndex == boxRowOffset + i) && (columnIndex == boxColumnOffset + j )) ) {
                if(board[boxRowOffset + i][boxColumnOffset + j] == ch)
                    return false;
              }    
           }
        }	
     
      return true;
    }
}
```
