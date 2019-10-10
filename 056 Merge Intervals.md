# 56. Merge Intervals
Given a collection of intervals, merge all overlapping intervals.
## Example 1:
~~~
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
~~~
## Example 2:
~~~
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
~~~
## Note:
input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[][] $intervals
     * @return Integer[][]
     */
    function merge($intervals) {
        $count = count($intervals);

        if ($count < 2) return $intervals;

        $last_check = $count -1;
        for ($i = 0; $i < $last_check ; $i ++) {
            if (!isset($intervals[$i])) continue;

            $current_interval = $intervals[$i];
            $current_interval_changed = false;

            for ($j = $i + 1; $j <= $count; $j ++) {
                if (!isset($intervals[$j])) continue;

                $next_interval = $intervals[$j];

                if ($next_interval[0] > $current_interval[1] || $next_interval[1] < $current_interval[0]) {
                    continue;
                }

                if ($next_interval[0] <= $current_interval[0] && $next_interval[1] >= $current_interval[0]) {
                    $temp = [];
                    $temp[0] = $next_interval[0];
                    $temp[1] = $next_interval[1] >= $current_interval[1] ? $next_interval[1] : $current_interval[1];

                    $intervals[$i] = $temp;
                    $current_interval = $intervals[$i];
                    unset($intervals[$j]);
                    $current_interval_changed = true;
                    continue;
                }

                if ($next_interval[0] >= $current_interval[0] && $next_interval[0] <= $current_interval[1]) {
                    $temp = [];
                    $temp[0] = $current_interval[0];
                    $temp[1] = $next_interval[1] >= $current_interval[1] ? $next_interval[1] : $current_interval[1];

                    $intervals[$i] = $temp;
                    $current_interval = $intervals[$i];
                    unset($intervals[$j]);
                    $current_interval_changed = true;
                    continue;
                }
            }

            if ($current_interval_changed) $i --;
        }

        return $intervals;
    }
}
~~~