# 6. ZigZag Conversion
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
~~~
P   A   H   N
A P L S I I G
Y   I   R
~~~
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:
~~~
string convert(string s, int numRows);
~~~
## Example 1:
~~~
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
~~~
## Example 2:
~~~
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param String $s
     * @param Integer $numRows
     * @return String
     */
    function convert($s, $numRows) {
        if ($numRows == 1) return $s;
        
        $s_len = strlen($s);
        $result_s = '';
        $s_array = [];

        $x = $y = 0;
        for ($i = 0; $i < $s_len; $i++) {
            $s_1 = substr($s, $i, 1);

            $x_num = $x % ($numRows - 1);
            if ($x_num) {
                if ($y == ($numRows - 1 - $x_num)) {
                    $s_array[$x][$y] = $s_1;
                } else {
                    $i --;
                    $s_array[$x][$y] = '';
                }
            } else {
                $s_array[$x][$y] = $s_1;
            }

            $y++;
            if ($y == $numRows) {
                $x ++;
                $y = 0;
            }
        }

        for ($y = 0; $y < $numRows; $y++) {
            for($x = 0; array_key_exists($x, $s_array); $x ++) {
                if (array_key_exists($y, $s_array[$x])) {
                    $result_s .= $s_array[$x][$y];
                } else break;
            }
        }

        return $result_s;
    }
}
~~~