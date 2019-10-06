# 36. Valid Sudoku
Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

![Sudoku](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

## Example 1:
~~~
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
~~~

## Example 2:
~~~
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
~~~

## Note:
* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.
* The given board contain only digits 1-9 and the character '.'.
* The given board size is always 9x9.

# Solution:
~~~PHP
class Solution {

    /**
     * @param String[][] $board
     * @return Boolean
     */
    function isValidSudoku($board) {
        for ($i = 0; $i < 9; $i ++) {
            $temp = $temp_c= [];
            for ($j = 0; $j < 9; $j ++) {
                if (isset($temp[$board[$i][$j]])) return false;
                if (is_numeric($board[$i][$j])) $temp[$board[$i][$j]] = true;

                if (isset($temp_c[$board[$j][$i]])) return false;
                if (is_numeric($board[$j][$i])) $temp_c[$board[$j][$i]] = true;
            }
        }

        for ($r = 0; $r < 3; $r ++) {
            for ($c = 0; $c < 3; $c ++) {
                $temp = [];
                for ($i = 0; $i < 3; $i ++) {
                    $i_key = $i + $r * 3;
                    for ($j = 0; $j < 3; $j ++) {
                        $j_key = $j + $c * 3;
                        if (isset($temp[$board[$i_key][$j_key]])) return false;
                        if (is_numeric($board[$i_key][$j_key])) $temp[$board[$i_key][$j_key]] = true;
                    }
                }
            }
        }

        return true;
    }
}
~~~
