# 53. Maximum Subarray
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
## Example:
~~~
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
~~~
## Follow up:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function maxSubArray($nums) {
        $result = null;

        $count = count($nums);

        for ($i = 0; $i < $count; $i ++) {
            $temp = $nums[$i];

            if ($result === null || $temp > $result) $result = $temp;

            for ($j = $i + 1; $j < $count; $j ++) {
                $temp += $nums[$j];
                if ($temp > $result) $result = $temp;
            }
        }

        return $result;
    }
}
~~~