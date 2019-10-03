# 14. Longest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string " ".
## Example 1:
~~~
Input: ["flower","flow","flight"]
Output: "fl"
~~~
## Example 2:
~~~
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
~~~
## Note:
All given inputs are in lowercase letters a-z.

# Solution:
~~~PHP
class Solution {

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs) {
        $result_str = '';

        $count = count($strs);
        if ($count > 1) {
            $first_str = $strs[0];
            $first_str_len = strlen($first_str);

            for($i=1;$i <= $first_str_len; $i ++) {
                $result_str = substr($first_str, 0, $i);

                for($j = 1; $j < $count; $j++) {
                    $pare_str = substr($strs[$j], 0, $i);
                    if ($result_str != $pare_str) {
                        if ($i > 1) {
                            return substr($first_str, 0, $i -1);
                        } else return '';
                        break;
                    }
                }
            }
        } else if ($count == 1) { return $strs[0];}

        return $result_str;
    }
}
~~~
