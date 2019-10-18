# 168. Excel Sheet Column Title
Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
~~~
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
~~~
## Example 1:
~~~
Input: 1
Output: "A"
~~~
## Example 2:
~~~
Input: 28
Output: "AB"
~~~
## Example 3:
~~~
Input: 701
Output: "ZY"
~~~

# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $n
     * @return String
     */
    function convertToTitle($n) {
        $result = '';

        $this->letters = [
            1 => 'A',
            2 => 'B',
            3 => 'C',
            4 => 'D',
            5 => 'E',
            6 => 'F',
            7 => 'G',
            8 => 'H',
            9 => 'I',
            10 => 'J',
            11 => 'K',
            12 => 'L',
            13 => 'M',
            14 => 'N',
            15 => 'O',
            16 => 'P',
            17 => 'Q',
            18 => 'R',
            19 => 'S',
            20 => 'T',
            21 => 'U',
            22 => 'V',
            23 => 'W',
            24 => 'X',
            25 => 'Y',
            26 => 'Z',
        ];

        $this->convert_to_title($n, $result);

        return $result;
    }

    function convert_to_title($n, &$result) {
        if ($n > 26) {
            $floor = floor($n / 26);
            $num = $n % 26;

            if ($num == 0) {
                $num = 26;
                $floor -= 1;
            }

            $this->convert_to_title($floor, $result);
        } else {
            $num = $n;
        }

        $result .= $this->letters[$num];
    }
}
~~~