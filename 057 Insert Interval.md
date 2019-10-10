# 57. Insert Interval
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.
## Example 1:
~~~
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
~~~
## Example 2:
~~~
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
~~~
## Note:
input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[][] $intervals
     * @param Integer[] $newInterval
     * @return Integer[][]
     */
    function insert($intervals, $newInterval) {
        $result = [];

        $count = count($intervals);

        $i = 0;
        for (; $i < $count; $i ++) {
            $current_interval = $intervals[$i];

            if ($newInterval[0] > $current_interval[1]) {
                $result[] = $current_interval;
                continue;
            }

            if ($newInterval[1] < $current_interval[0]) {
                $result[] = $newInterval;
                $result = array_merge($result, array_slice($intervals, $i));
                return $result;
            }

            if (
                ($newInterval[0] >= $current_interval[0] && $newInterval[0] <= $current_interval[1])
                ||
                ($newInterval[1] <= $current_interval[1] && $newInterval[1] >= $current_interval[0])
            ) {

                $current_interval[0] = $newInterval[0] <= $current_interval[0] ? $newInterval[0] : $current_interval[0];
                $current_interval[1] = $newInterval[1] >= $current_interval[1] ? $newInterval[1] : $current_interval[1];

                $j = $i + 1;
                for (; $j < $count; $j ++) {
                    if ($current_interval[1] < $intervals[$j][0]) {
                        $current_interval[1] = $current_interval[1] >= $intervals[$j -1][1] ? $current_interval[1] : $intervals[$j -1][1];
                        $result[] = $current_interval;
                        $result = array_merge($result, array_slice($intervals, $j));
                        return $result;
                    }
                }

                $current_interval[1] = $current_interval[1] >= $intervals[$j - 1][1] ? $current_interval[1] : $intervals[$j - 1][1];
                $result[] = $current_interval;
                return $result;
            }
        }

        $result[] = $newInterval;

        return $result;
    }
}
~~~