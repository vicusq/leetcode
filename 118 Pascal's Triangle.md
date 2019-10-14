# 118. Pascal's Triangle
Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

![Pascal's Triangle](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.

## Example:
~~~
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $numRows
     * @return Integer[][]
     */
    function generate($numRows) {
        if ($numRows == 0) return [];

        if ($numRows == 1) return [[1]];
        if ($numRows == 2) return [[1], [1,1]];

        $result = [[1], [1,1]];
        
        $this->generate_next($result, 2, $numRows);

        return $result;
    }

    function generate_next(&$result, $current_level, $end_level) {
        $current_level ++;
        
        $end_row = end($result);
        $count = count($end_row);
        $last_2_elem = $count - 1;

        $next_row = [1];
        for ($i = 0; $i < $last_2_elem; $i ++) {
            $next_row[] = $end_row[$i] + $end_row[$i + 1];
        }
        $next_row[] = 1;

        $result[] = $next_row;
        
        if ($current_level < $end_level) $this->generate_next($result, $current_level, $end_level);
    }
}
~~~