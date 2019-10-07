# 4. Median of Two Sorted Arrays
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.
## Example 1:
~~~
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
~~~
## Example 2:
~~~
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Float
     */
    function findMedianSortedArrays($nums1, $nums2) {
        $count_1 = count($nums1);
        $count_2 = count($nums2);

        $count = $count_1 + $count_2;
        $middle = floor($count / 2);
        $keys = [];
        if (intval($middle * 2) == $count) {
            $keys[] = $middle;
            $keys[] = $middle + 1;
        } else {
            $keys[] = $middle + 1;
        }

        $final_nums = [];
        for ($i = 0; $i < $count_2; $i ++) {
            $num2 = $nums2[$i];
            $placed = false;
            $num1 = current($nums1);
            if ($num2 < $num1) {
                $final_nums[] = $num2;
                $placed = true;
                continue;
            }

            if (is_numeric($num1)) $final_nums[] = $num1;
            while ($num1 = next($nums1)) {
                if ($num2 < $num1) {
                    $final_nums[] = $num2;
                    $placed = true;
                    break;
                }

                $final_nums[] = $num1;
            }

            if ($placed === false) {
                $final_nums = array_merge($final_nums, array_slice($nums2, $i));
                break;
            };
        }

        $nums1_key = key($nums1);
        if ($nums1_key !== null) $final_nums = array_merge($final_nums, array_slice($nums1, $nums1_key));

        $median = 0;
        $keys_count = count($keys);
        foreach ($keys as $key) {
            $median += $final_nums[$key - 1];
        }

        return $median / $keys_count;
    }
}
~~~