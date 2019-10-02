# 1. Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

## Example:
~~~
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        foreach ($nums as $key => $num) {
            $target_num = $target - $num;
            $exist_key = array_search($target_num, $nums);
            if ($exist_key !== false && $exist_key !== $key) {
                return [$key, $exist_key];
            }
        }
        
        return [];
    }
}
~~~