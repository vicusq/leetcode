# 206. Reverse Linked List
Reverse a singly linked list.
## Example:
~~~
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
~~~
## Follow up:
A linked list can be reversed either iteratively or recursively. Could you implement both?
# Solution:
~~~PHP
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function reverseList($head) {
        $reverse_head = null;
        $this->reverse_list($head, $head->next, $reverse_head);
        $head->next = null;

        return $reverse_head;
    }

    function reverse_list($list, $next_list, &$reverse_head) {
        if ($list->next === null) {
            $reverse_head = $list;
        } else {
            $next = $list->next;
            $this->reverse_list($next, $next->next, $reverse_head);
            $next_list->next = $list;
        }
    }
}
~~~