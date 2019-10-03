# 5. Longest Palindromic Substring
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
## Example 1:
~~~
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
~~~
## Example 2:
~~~
Input: "cbbd"
Output: "bb"
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function longestPalindrome($s) {
        $result_str = '';
        $str_len = strlen($s);

        for ($i = 0; $i <= $str_len; $i++) {
            $sub_len = $str_len - $i;
            for ($j = $sub_len; $j >= 1; $j--) {
                $temp_str = substr($s, $i, $j);
                $temp_str_rev = strrev($temp_str);
                if ($temp_str == $temp_str_rev) {
                    $result_str = strlen($temp_str) > strlen($result_str) ? $temp_str : $result_str;
                    break;
                }
            }
        }

        return $result_str;
    }
}
~~~