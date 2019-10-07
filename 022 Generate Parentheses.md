# 22. Generate Parentheses
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
~~~
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $n
     * @return String[]
     */
    function generateParenthesis($n) {
        $result = [];

        $parenthesis = [
            '(' => 0,
            ')' => 1,
        ];

        $str_len = $n * 2;

        $combination_enumerate = [];

        for($i = 0; $i < $str_len ; $i++) {
            $current_level = [];
            if (!$combination_enumerate) {
                foreach ($parenthesis as $symbol => $value) {
                    if ($symbol == ')') break;

                    $temp_str = $symbol;
                    $current_level[] = $temp_str;
                }
            } else {
                foreach ($combination_enumerate as $elem) {
                    foreach ($parenthesis as $symbol => $value) {
                        $temp_str = $elem . $symbol;
                        $current_level[] = $temp_str;
                    }
                }
            }

            $combination_enumerate = $current_level;
        }

        foreach ($combination_enumerate as $elem) {
            $buffer = [];
            for ($i = 0; $i < $str_len; $i ++) {
                $symbol = substr($elem, $i, 1);
                if ($last_elem = array_pop($buffer)) {
                    if ($parenthesis[$last_elem] == 0 && $parenthesis[$symbol] == 1) continue;
                    $buffer[] = $last_elem;
                }
                $buffer[] = $symbol;
            }

            if (empty($buffer)) $result[] = $elem;
        }

        return $result;
    }
}
~~~