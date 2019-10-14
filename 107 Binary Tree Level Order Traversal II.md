# 107. Binary Tree Level Order Traversal II
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:

Given binary tree [3,9,20,null,null,15,7],
~~~
    3
   / \
  9  20
    /  \
   15   7
~~~
return its bottom-up level order traversal as:
~~~
[
  [15,7],
  [9,20],
  [3]
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
     * @return Integer[][]
     */
    function levelOrderBottom($root) {
        $result = [];

        if ($root === null) return $result;

        $nodes = [$root];

        $this->level_order_bottom($nodes, $result);
        $result[] = [$root->val];
        return $result;
    }

    function level_order_bottom($nodes, &$result) {
        $val_array = [];
        $current_level = [];
        $have_next = false;
        foreach ($nodes as $node) {
            $node0 = $node->left;
            $node1 = $node->right;

            if ($node0 === null && $node1 === null) continue;
            if ($have_next === false) $have_next = true;

            if ($node0 !== null) {
                $val_array[] = $node0->val;
                $current_level[] = $node0;
            }
            if ($node1 !== null) {
                $val_array[] = $node1->val;
                $current_level[] = $node1;
            }
        }
        
        $nodes = $current_level;
        if ($have_next) {
            $this->level_order_bottom($nodes, $result);
            if ($val_array) $result[] = $val_array;
        } else {
            if ($val_array) $result[] = $val_array;
        }
    }
}
~~~