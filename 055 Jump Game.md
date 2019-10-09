# 55. Jump Game
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.
## Example 1:
~~~
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
~~~
## Example 2:
~~~
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function canJump($nums) {
        $count = count($nums);

        for ($i = 0; $i < $count; $i ++) {
            $num = $nums[$i];
            if ($num > 0) continue;

            $key_pre = $i - 1;
            $key_next = $i + 1;

            if ($key_pre < 0 && $key_next < $count) return false;
            if ($key_pre < 0 && $key_next = $count) return true;

            $passed = false;
            $pre = 1;
            for ($j = $key_pre; $j >= 0; $j --) {
                if ($nums[$j] > $pre) {
                    $passed = true;
                    break;
                }

                if ($i == $count - 1 && $nums[$j] == $pre) {
                    $passed = true;
                    break;
                }

                $pre ++;
            }

            if ($passed === false) return false;
        }

        return true;
    }
}
~~~