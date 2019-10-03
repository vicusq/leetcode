# 9. Palindrome Number
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
## Example 1:
~~~
Input: 121
Output: true
~~~
## Example 2:
~~~
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
~~~
## Example 3:
~~~
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $x
     * @return Boolean
     */
    function isPalindrome($x) {
        if ($x < 0) return false;

        $str_array = str_split($x);
        $str_array = array_reverse($str_array);
        $str = implode('', $str_array);

        return $x === intval($str);
    }
}
~~~