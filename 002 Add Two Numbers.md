# 2. Add Two Numbers

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Example 1:
![alt](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)
~~~
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
~~~

## Example 2:
~~~
Input: l1 = [0], l2 = [0]
Output: [0]
~~~

## Example 3:
~~~
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
~~~

## Constraints::
- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

# Solution:
~~~PHP
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function addTwoNumbers($l1, $l2) {
        $num1 = $l1->val;
        $num2 = $l2->val;

        $sum = $num1 + $num2;

        $carry = 0;
        if ($sum >= 10) $carry = 1;

        $val = $sum % 10;

        $l = $cur = new ListNode($val);

        $l2end = false;
        
        while($l1=$l1->next) {
            $num1 = $l1->val;

            if ($l2end === false) {
                $l2 = $l2->next;
                $num2 = $l2->val;

                $sum = $num1 + $num2 + $carry;

                if ($sum >= 10) {
                    $carry = 1;
                } else {
                    $carry = 0;
                }

                $val = $sum % 10;

                $next = new ListNode($val);
                $cur->next = $next;
                $cur = $next;
            } else if ($carry == 1) {
                $sum = $num1 + $carry;

                if ($sum >= 10) {
                    $carry = 1;
                } else {
                    $carry = 0;
                }

                $val = $sum % 10;

                $next = new ListNode($val);
                $cur->next = $next;
                $cur = $next;
            } else {
                $cur->next = $l1;
                break;
            }

            if ($l2 === null) $l2end = true;
        }

        if ($l2end === false) {
            while ($l2 = $l2->next) {
                if ($carry ==0) {
                    $cur->next = $l2;
                    break;
                }

                $num2 = $l2->val;

                $sum = $num2 + $carry;

                if ($sum >= 10) {
                    $carry = 1;
                } else {
                    $carry = 0;
                }

                $val = $sum % 10;

                $next = new ListNode($val);
                $cur->next = $next;
                $cur = $next;
            }
        }
        
        if ($carry === 1) $cur->next = new ListNode(1);

        return $l;
    }
}
~~~