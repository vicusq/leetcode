# 100. Same Tree
Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

## Example 1:
~~~
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
~~~
## Example 2:
~~~
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
~~~
## Example 3:
~~~
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
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
     * @param TreeNode $p
     * @param TreeNode $q
     * @return Boolean
     */
    function isSameTree($p, $q) {
        if ($p === null || $q === null) {
            return $p === $q;
        }

        if ($p->val === $q->val) {
            return $this->isSameTree($p->left, $q->left) && $this->isSameTree($p->right, $q->right);
        }

        return false;
    }
}
~~~