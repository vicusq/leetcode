# 219. Contains Duplicate II
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that **nums[i] = nums[j]** and the **absolute** difference between i and j is at most k.
## Example 1:
~~~
Input: nums = [1,2,3,1], k = 3
Output: true
~~~
## Example 2:
~~~
Input: nums = [1,0,1,1], k = 1
Output: true
~~~
## Example 3:
~~~
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Boolean
     */
    function containsNearbyDuplicate($nums, $k) {
        $duplicate = [];
        foreach ($nums as $key => $num) {
            if (isset($duplicate[$num])) {
                $pre_key = $duplicate[$num];
                if ($key - $pre_key <= $k) return true;
            }

            $duplicate[$num] = $key;
        }

        return false;
    }
}
~~~