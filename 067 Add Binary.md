# 67. Add Binary
Given two binary strings, return their sum (also a binary string).

The input strings are both **non-empty** and contains only characters 1 or 0.
## Example 1:
~~~
Input: a = "11", b = "1"
Output: "100"
~~~
## Example 2:
~~~
Input: a = "1010", b = "1011"
Output: "10101"
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param String $a
     * @param String $b
     * @return String
     */
    function addBinary($a, $b) {
        $result = '';

        $count_a = strlen($a);
        $count_b = strlen($b);

        if ($count_a > $count_b) {
            $min = $b;
            $min_len = $count_b;

            $max = $a;
            $max_len = $count_a;
        } else {
            $max = $b;
            $max_len = $count_b;

            $min = $a;
            $min_len = $count_a;
        }

        $added = 0;
        $i = -1;
        for (; $i + $min_len >= 0; $i --) {
            $max_i = substr($max, $i, 1);
            $min_i = substr($min, $i, 1);
            switch ($added) {
                case 0:
                    if ($max_i && $min_i) {
                        $result = '0' . $result;
                        $added = 1;
                    } else if ($max_i || $min_i) {
                        $result = '1' . $result;
                    } else {
                        $result = '0' . $result;
                    }
                    break;
                case 1:
                    if ($max_i && $min_i) {
                        $result = '1' . $result;
                    } else if ($max_i || $min_i) {
                        $result = '0' . $result;
                    } else {
                        $result = '1' . $result;
                        $added = 0;
                    }
                    break;
            }
        }

        if ($added == 1) {
            for (; $i + $max_len >= 0; $i--) {
                $max_i = substr($max, $i, 1);
                if ($max_i) {
                    $result = '0' . $result;
                    $added = 1;
                } else {
                    $result = '1' . $result;
                    $added = 0;
                    $i--;
                    break;
                }
            }
        }

        if ($i + $max_len >= 0) {
            $result = substr($max, 0, $max_len + $i + 1) . $result;
        }

        if ($added == 1) $result = '1' . $result;

        return $result;
    }
}
~~~