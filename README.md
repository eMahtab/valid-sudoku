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
    public boolean isValidSudoku(char[][] board) {
        int rows = board.length;
        int columns = board[0].length;
        
        for(int row = 0; row < rows; row++) {
            for(int column = 0; column < columns; column++) {
                if(board[row][column] != '.') {
                    if(!isValid(board, row, column))
                        return false;
                }
            }
        }
       return true;                
    }
    
    private boolean isValid(char[][] board, int row, int column) {
        // Check the row
        for(int col = 0; col < board[0].length; col++) {
            if(col != column && board[row][col] == board[row][column])
                return false;
        }
        
        // Check the column
        for(int r = 0; r < board.length; r++) {
            if(r != row && board[r][column] == board[row][column])
                return false;
        }
        
        // Check Subgrid
        int subgridStartRow = (row / 3) * 3;
        int subgridStartCol = (column / 3) * 3;
        for(int i = subgridStartRow; i < subgridStartRow + 3; i++) {
            for(int j = subgridStartCol; j < subgridStartCol + 3; j++) {
                if(i == row && j == column)
                    continue;
                else if(board[i][j] == board[row][column])
                        return false;
                
            }
        }
        return true;
    }
}
```
