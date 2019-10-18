# 169. Majority Element
Given an array of size n, find the majority element. The majority element is the element that appears **more than** ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.
## Example 1:
~~~
Input: [3,2,3]
Output: 3
~~~
## Example 2:
~~~
Input: [2,2,1,1,1,2,2]
Output: 2
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function majorityElement($nums) {
        $count = count($nums);
        $majority = floor($count / 2);

        $elem = [];

        foreach ($nums as $num) {
            if (isset($elem[$num])) {
                $elem[$num] ++;
            } else {
                $elem[$num] = 1;
            }

            if ($elem[$num] > $majority) return $num;
        }

        return false;
    }
}
~~~