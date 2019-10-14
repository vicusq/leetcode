# 119. Pascal's Triangle II
Given a non-negative index k where k ≤ 33, return the k<sup>th</sup> index row of the Pascal's triangle.

Note that the row index starts from 0.

![Pascal's Triangle](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.

## Example:
~~~
Input: 3
Output: [1,3,3,1]
~~~
## Follow up:
Could you optimize your algorithm to use only O(k) extra space?

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $rowIndex
     * @return Integer[]
     */
    function getRow($numRows) {
        if ($numRows == 0) return [1];

        if ($numRows == 1) return [1,1];

        $last_row = [1,1];

        return $this->generate_next($last_row, 1, $numRows);
    }

    function generate_next($last_row, $current_level, $end_level) {
        $current_level ++;

        $count = count($last_row);
        $last_2_elem = $count - 1;

        $next_row = [1];
        for ($i = 0; $i < $last_2_elem; $i ++) {
            $next_row[] = $last_row[$i] + $last_row[$i + 1];
        }
        $next_row[] = 1;

        if ($current_level < $end_level) return $this->generate_next($next_row, $current_level, $end_level);

        return $next_row;
    }
}
~~~