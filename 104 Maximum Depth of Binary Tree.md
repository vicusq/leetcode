# 104. Maximum Depth of Binary Tree
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.
## Example:
Given binary tree [3,9,20,null,null,15,7],
~~~
    3
   / \
  9  20
    /  \
   15   7
~~~
return its depth = 3.
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
     * @return Integer
     */
    function maxDepth($root) {
        if ($root !== null) {
            $depth = 1;
            $nodes = [$root];
            return $this->reach_next($nodes, $depth);
        }

        return 0;
    }

    function reach_next($nodes, $depth) {
        $have_next = false;
        $next_level = [];
        foreach ($nodes as $node) {
            $left = $node->left;
            $right = $node->right;
            
            if ($left === null && $right === null) continue;
            
            if ($have_next === false) $have_next = true;

            if ($left !== null) {
                $next_level[] = $left;
            }
            if ($right !== null) {
                $next_level[] = $right;
            }
        }

        if ($have_next) {
            return $this->reach_next($next_level, ++ $depth);
        } else return $depth;
    }
}
~~~