# 88. Merge Sorted Array
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
## Note:
* The number of elements initialized in nums1 and nums2 are m and n respectively.
* You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
## Example:
~~~
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer $m
     * @param Integer[] $nums2
     * @param Integer $n
     * @return NULL
     */
    function merge(&$nums1, $m, $nums2, $n) {
        if ($m === 0 ) {
            $nums1 = $nums2;
            return;
        }

        $i = $j = $start = 0;

        for(; $i < $n; $i ++) {
            $num2 = $nums2[$i];
            $placed = false;

            for (; $j < $m; $j ++) {
                $num1 = $nums1[$j];

                if ($num1 > $num2) {
                    $start = $j + 1;
                    $nums1[$j] = $num2;
                    $m++;
                    $placed = true;
                    for (; $j < $m - 1; $j++) {
                        $temp = $nums1[$j + 1];
                        $nums1[$j + 1] = $num1;
                        $num1 = $temp;
                    }

                    $j = $start;
                    break;
                }
            }

            if ($placed === false) {
                $nums1[$j] = $num2;
                $j ++;
            }
        }
    }
}
~~~