# 113. Path Sum II
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

**Note:** A leaf is a node with no children.

## Example:

Given the below binary tree and sum = 22,
~~~
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
~~~
return:
~~~
[
   [5,4,11,2],
   [5,8,4,5]
]
~~~
# Solution:
~~~PHP
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @param Integer $sum
     * @return Integer[][]
     */
    function pathSum($root, $sum) {
        $result = [];

        if ($root === null) return $result;

        $current_sum = 0;
        $current_sum += $root->val;

        $path = [];
        $path[] = $root->val;

        if ($current_sum == $sum && $root->left === null && $root->right == null) return [[$root->val]];

        $this->path_sum($root->left, $sum, $current_sum, $path, $result);
        $this->path_sum($root->right, $sum, $current_sum, $path, $result);

        return $result;
    }

    function path_sum($node, $sum, $current_sum, $path, &$result) {
        if ($node === null) return false;

        $current_sum = $current_sum + $node->val;
        $path[] = $node->val;

        if ($node->left === null && $node->right == null) {
            if ($current_sum == $sum) {
                $result[] = $path;
                return true;
            } else return false;
        }

        $this->path_sum($node->left, $sum, $current_sum, $path, $result);
        $this->path_sum($node->right, $sum, $current_sum, $path, $result);
        return false;
    }
}
~~~