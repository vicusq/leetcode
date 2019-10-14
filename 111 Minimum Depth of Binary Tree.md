# 111. Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

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
return its minimum depth = 2.
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
    function minDepth($root) {
        if ($root !== null) {
            $depth = 1;
            $nodes = [$root];
            return $this->reach_next($nodes, $depth);
        }

        return 0;
    }

    function reach_next($nodes, $depth) {
        $have_next = false;
        $current_level = [];
        foreach ($nodes as $node) {
            $node0 = $node->left;
            $node1 = $node->right;

            if ($node0 === null && $node1 === null) return $depth;
            if ($have_next === false) $have_next = true;

            if ($node0 !== null) {
                $current_level[] = $node0;
            }
            if ($node1 !== null) {
                $current_level[] = $node1;
            }
        }

        $nodes = $current_level;
        if ($have_next) {
            return $this->reach_next($nodes, ++ $depth);
        }

        return $depth;
    }
}
~~~