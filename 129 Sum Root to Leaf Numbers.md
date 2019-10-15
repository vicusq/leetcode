# 129. Sum Root to Leaf Numbers
Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

**Note:** A leaf is a node with no children.
## Example:
~~~
Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
~~~
## Example 2:
~~~
Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
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
     * @return Integer
     */
    function sumNumbers($root) {
        $result = 0;

        $all_number = [];
        $pre_number = '';
        if ($root === null) return $result;

        if ($root->val != 0) $pre_number = $root->val;
        
        if ($root->left === null && $root->right === null) return $root->val;

        $this->sum_numbers($root->left, $pre_number, $all_number);
        $this->sum_numbers($root->right, $pre_number, $all_number);

        foreach ($all_number as $number) {
            $result += intval($number);
        }

        return $result;
    }

    function sum_numbers($node, $pre_number, &$all_number) {
        if ($node === null) {
            return true;
        } else {
            $pre_number .= $node->val;

            if ($node->left === null && $node->right == null) {
                $all_number[] = $pre_number;
                return true;
            }

            $this->sum_numbers($node->left, $pre_number, $all_number);
            $this->sum_numbers($node->right, $pre_number, $all_number);
            return true;
        }
    }
}
~~~