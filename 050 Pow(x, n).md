# 50. Pow(x, n)
Implement pow(x, n), which calculates x raised to the power n (x<sup>n</sup>).
## Example 1:
~~~
Input: 2.00000, 10
Output: 1024.00000
~~~
## Example 2:
~~~
Input: 2.10000, 3
Output: 9.26100
~~~
## Example 3:
~~~
Input: 2.00000, -2
Output: 0.25000
~~~
Explanation: 2<sup>-2</sup> = 1/2<sup>2</sup> = 1/4 = 0.25

## Note:
* -100.0 < x < 100.0
* n is a 32-bit signed integer, within the range [−2<sup>31</sup>, 2<sup>31</sup> − 1]

# Solution:
~~~PHP
class Solution {

    /**
     * @param Float $x
     * @param Integer $n
     * @return Float
     */
    function myPow($x, $n) {
        $result = 1;

        if ($n < 0) {
            $x = 1 / $x;
            $n = abs($n);
        }

        for ($i = 0; $i < $n; $i ++) {
            $result = $result * $x;

            $multi = ($i + 1) * 2;
            if ($multi <= $n) {
                $result = $result * $result;
                $i = $multi - 1;
            }
        }

        return number_format($result, 5, '.', '');
    }
}
~~~
