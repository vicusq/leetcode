# 101. Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
~~~
    1
   / \
  2   2
 / \ / \
3  4 4  3
~~~
But the following [1,2,2,null,3,null,3] is not:
~~~
    1
   / \
  2   2
   \   \
   3    3
~~~
## Note:
Bonus points if you could solve it both recursively and iteratively.
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
     * @return Boolean
     */
    function isSymmetric($root) {
        return $this->is_symmetric([$root->left, $root->right]);
    }

    function is_symmetric($nodes) {
        $count = count($nodes);
        $end_i = $count / 2;
        for ($i = 0; $i < $end_i; $i ++) {
            $node0 = $nodes[$i];
            $node1 = $nodes[$count - 1 - $i];

            if ($node0 === null || $node1 === null) {
                if ($node0 !== $node1) return false;
                unset($nodes[$i], $nodes[$count - 1 - $i]);
            }
            
            if ($node0->val !== $node1->val) return false;
        }

        $next_level = [];
        $have_next = false;
        foreach ($nodes as $node) {
            if ($node->left !== null || $node->right !== null) $have_next = true;

            $next_level[] = $node->left;
            $next_level[] = $node->right;
        }

        if ($have_next) {
            return $this->is_symmetric($next_level);
        } else return true;
    }
}
~~~