# 47. Permutations II
Given a collection of numbers that might contain duplicates, return all possible unique permutations.
## Example:
~~~
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function permuteUnique($nums) {
        $result = [];

        $count = count($nums);

        for ($i = 0; $i < $count; $i ++) {
            if (!$result) {
                $duplicate = [];
                foreach ($nums as $key => $num) {
                    if (isset($duplicate[$num])) {
                        continue;
                    } else {
                        $duplicate[$num] = true;
                    }

                    $temp = [];
                    $temp['used_keys'] = [$key];
                    $temp['permute'] = [$num];
                    $result[] = $temp;
                }
            } else {
                $current_level = [];
                foreach ($result as $item) {
                    $duplicate = [];
                    foreach ($nums as $key => $num) {
                        if (!in_array($key, $item['used_keys'])) {
                            if (isset($duplicate[$num])) {
                                continue;
                            } else {
                                $duplicate[$num] = true;
                            }

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
