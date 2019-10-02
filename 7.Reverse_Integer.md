# 7. Reverse Integer   
Given a 32-bit signed integer, reverse digits of an integer.   
## Example 1:
~~~
Input: 123
Output: 321
~~~
## Example 2:
~~~
Input: -123
Output: -321
~~~
## Example 3:
~~~
Input: 120
Output: 21
~~~
## Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1].
For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function reverse($x) {
        $sign = $x < 0 ? -1 : 1;

        if ($sign < 0) $x = abs($x);

        $j = [];
        for($i = 1; $x >= 10; $i ++) {
            $j[] = $x % 10;
            $x = floor($x/10);
        }

        $j[] = $x;

        $length = count($j);
        $result = 0;
        foreach($j as $key => $num) {
            $result += $num * pow(10, $length - 1 - $key);
        }
        
        if ($result > 2147483647) $result = 0;

        return intval($sign * $result);
    }
}
~~~