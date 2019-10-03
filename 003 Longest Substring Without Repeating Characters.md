# 3. Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.
## Example 1:
~~~
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
~~~
## Example 2:
~~~
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
~~~
## Example 3:
~~~
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLongestSubstring($s) {
        if (strlen($s) > 0) {
            $result_length = 1;
        } else return 0;

        $str_array = str_split($s);

        $length = count($str_array);
        $temp = [];
        for($i = 0; $i < $length; $i++) {
            if (array_key_exists($str_array[$i], $temp)) {
                $now = count($temp);
                $result_length = $now > $result_length ? $now : $result_length;
                $i = $temp[$str_array[$i]];
                $temp = [];
                continue;
            };

            $temp[$str_array[$i]] = $i;
        }

        $temp_length = count($temp);

        return $temp_length > $result_length ? $temp_length : $result_length;
    }
}
~~~