# 112. Path Sum
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.
## Example:
Given the below binary tree and sum = 22,
~~~
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
~~~
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
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
     * @return Boolean
     */
    function hasPathSum($root, $sum) {
        if ($root === null) return false;

        $current_sum = 0;
        $current_sum += $root->val;

        if ($current_sum == $sum && $root->left === null && $root->right == null) return true;

        return $this->has_path_sum($root->left, $sum, $current_sum) || $this->has_path_sum($root->right, $sum, $current_sum);
    }

    function has_path_sum($node, $sum, $current_sum) {
        if ($node === null) return false;

        $current_sum = $current_sum + $node->val;
        
        if ($node->left === null && $node->right == null && $current_sum == $sum) return true;
        
        return $this->has_path_sum($node->left, $sum, $current_sum) || $this->has_path_sum($node->right, $sum, $current_sum);
    }
}
~~~