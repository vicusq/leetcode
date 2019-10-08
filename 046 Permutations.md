# 46. Permutations
Given a collection of **distinct** integers, return all possible permutations.
## Example:
~~~
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function permute($nums) {
        $result = [];

        $count = count($nums);

        for ($i = 0; $i < $count; $i ++) {
            if (!$result) {
                foreach ($nums as $key => $num) {
                    $temp = [];
                    $temp['used_keys'] = [$key];
                    $temp['permute'] = [$num];
                    $result[] = $temp;
                }
            } else {
                $current_level = [];
                foreach ($result as $item) {
                    foreach ($nums as $key => $num) {
                        if (!in_array($key, $item['used_keys'])) {
                            $temp = $item;
                            $temp['permute'][] = $num;
                            $temp['used_keys'][] = $key;
                            $current_level[] = $temp;
                        }
                    }
                }

                $result = $current_level;
            }
        }

        return array_column($result, 'permute');
    }
}
~~~