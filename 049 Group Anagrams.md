# 49. Group Anagrams
Given an array of strings, group anagrams together.
## Example:
~~~
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
~~~
## Note:
* All inputs will be in lowercase.
* The order of your output does not matter.

# Solution:
~~~PHP
class Solution {

    /**
     * @param String[] $strs
     * @return String[][]
     */
    function groupAnagrams($strs) {
        $result = [];

        foreach ($strs as $str) {
            $str_splice = str_split($str);
            sort($str_splice);
            $str_sort_key = implode('', $str_splice);
            if (isset($result[$str_sort_key])) {
                $result[$str_sort_key][] = $str;
            } else {
                $result[$str_sort_key] = [];
                $result[$str_sort_key][] = $str;
            }
        }

        return array_values($result);
    }
}
~~~