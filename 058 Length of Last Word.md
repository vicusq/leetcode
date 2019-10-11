# 58. Length of Last Word
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

**Note:** A word is defined as a character sequence consists of non-space characters only.
## Example:
~~~
Input: "Hello World"
Output: 5
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLastWord($s) {
        $s = trim($s);

        $str_len = strlen($s);
        if ($str_len < 1) return 0;

        $space_last_pos = strrpos($s, ' ');
        if ($space_last_pos === false) return $str_len;

        $last_word = substr($s, $space_last_pos + 1);
        return strlen($last_word);
    }
}
~~~