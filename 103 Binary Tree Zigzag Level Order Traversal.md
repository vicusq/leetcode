# 103. Binary Tree Zigzag Level Order Traversal
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:

Given binary tree [3,9,20,null,null,15,7],
~~~
    3
   / \
  9  20
    /  \
   15   7
~~~
return its zigzag level order traversal as:
~~~
[
  [3],
  [20,9],
  [15,7]
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
    function zigzagLevelOrder($root) {
        $result = [];

        if ($root === null) return $result;

        $result[] = [$root->val];
        $nodes = [$root];

        return $this->zigzag_level_order($nodes, $result, true);
    }

    function zigzag_level_order($nodes, $result, $pre_direct) {
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

        if ($val_array) {
            if ($pre_direct) $val_array = array_reverse($val_array);
            $result[] = $val_array;
        }
        $nodes = $current_level;
        if ($have_next) {
            $pre_direct = $pre_direct ? false : true;
            return $this->zigzag_level_order($nodes, $result, $pre_direct);
        } else return $result;
    }
}
~~~