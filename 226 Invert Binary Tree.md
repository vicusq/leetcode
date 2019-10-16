# 226. Invert Binary Tree
Invert a binary tree.
## Example:
Input:
~~~
     4
   /   \
  2     7
 / \   / \
1   3 6   9
~~~
Output:
~~~
     4
   /   \
  7     2
 / \   / \
9   6 3   1
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
     * @return TreeNode
     */
    function invertTree($root) {
        $this->invert_tree($root);
        
        return $root;
    }
    
    function invert_tree($node) {
        if ($node->left === null && $node->right === null) return true;
        
        $left = $node->left;
        $node->left = $node->right;
        $node->right = $left;
        
        $this->invert_tree($node->left);
        $this->invert_tree($node->right);
        return true;
    }
}
~~~