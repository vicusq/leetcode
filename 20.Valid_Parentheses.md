# 20. Valid Parentheses
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

## Example 1:
~~~
Input: "()"
Output: true
~~~
## Example 2:
~~~
Input: "()[]{}"
Output: true
~~~
## Example 3:
~~~
Input: "(]"
Output: false
~~~
## Example 4:
~~~
Input: "([)]"
Output: false
~~~
## Example 5:
~~~
Input: "{[]}"
Output: true
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isValid($s) {
        $characters_pair_array = [
            '(' => ')',
            '{' => '}',
            '[' => ']',
        ];
        
        if ($s = trim($s)) {
            $str_split_array = str_split($s);
            $length = count($str_split_array);

            $buffer = [];
            for($i = 0; $i < $length; $i++) {
                $now_elem = $str_split_array[$i];
                if ($last_elem = array_pop($buffer)) {
                    if ($characters_pair_array[$last_elem] == $now_elem) continue;
                    $buffer[] = $last_elem;
                };

                $buffer[] = $now_elem;
            }

            return empty($buffer);
        }
        
        return true;
    }
}
~~~

