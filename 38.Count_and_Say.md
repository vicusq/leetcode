# 38. Count and Say
The count-and-say sequence is the sequence of integers with the first five terms as following:
~~~
1.     1
2.     11
3.     21
4.     1211
5.     111221
~~~
1 is read off as "one 1" or 11.

11 is read off as "two 1s" or 21.

21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the n^th term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.
## Example 1:
~~~
Input: 1
Output: "1"
~~~
## Example 2:
~~~
Input: 4
Output: "1211"
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $n
     * @return String
     */
    function countAndSay($n) {
        $count_and_say_sequence = [
            1 => '1',
            2 => '11',
            3 => '21',
            4 => '1211',
            5 => '111221',
        ];

        if ($n <= 5) return $count_and_say_sequence[$n];

        for($i=6;$i <= $n; $i++) {
            $pre_count_say = [];
            $pre_count_say['pre'] = '';
            $level = 0;
            $pre_count_say['sequence'] = [];

            $pre_string = $count_and_say_sequence[$i - 1];
            for($j=0; $one = substr($pre_string, $j, 1); $j++) {
                if ($one == $pre_count_say['pre']) {
                    if (!isset($pre_count_say['sequence'][$level])) {
                        $pre_count_say['sequence'][$level] = [$one => 1];
                    }

                    $pre_count_say['sequence'][$level][$one] ++;
                    continue;
                }

                $pre_count_say['pre'] = $one;
                $level++;
                $pre_count_say['sequence'][$level] = [$one => 1];
            }

            $string = '';
            foreach ($pre_count_say['sequence'] as $level => $item) {
                foreach ($item as $one => $count) {
                    $string .= $count . $one;
                }
            }

            $count_and_say_sequence[$i] = $string;
        }

        return $count_and_say_sequence[$n];
    }
}
~~~
