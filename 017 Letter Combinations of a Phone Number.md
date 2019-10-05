# 17. Letter Combinations of a Phone Number
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![Telephone keypad](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

## Example:
~~~
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
~~~
## Note:
Although the above answer is in lexicographical order, your answer could be in any order you want.

# Solution:
~~~PHP
class Solution {

    /**
     * @param String $digits
     * @return String[]
     */
    function letterCombinations($digits) {
        $digits_letters = [
            2 => ['a', 'b', 'c'],
            3 => ['d', 'e', 'f'],
            4 => ['g', 'h', 'i'],
            5 => ['j', 'k', 'l'],
            6 => ['m', 'n', 'o'],
            7 => ['p', 'q', 'r', 's'],
            8 => ['t', 'u', 'v'],
            9 => ['w', 'x', 'y', 'z'],
        ];

        $result = [];
        $digits_len = strlen($digits);

        if ($digits_len > 0) {
            for($i = 0; $i < $digits_len; $i ++) {
                $digit = substr($digits, $i, 1);

                if (empty($result)) {
                    $result = $digits_letters[$digit];
                } else {
                    $temp = [];
                    foreach ($result as $item) {
                        foreach ($digits_letters[$digit] as $item_1) {
                            $temp[] = $item . $item_1;
                        }
                    }

                    $result = $temp;
                }
            }
        }

        return $result;
    }
}
~~~
