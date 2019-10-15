# 203. Remove Linked List Elements
Remove all elements from a linked list of integers that have value **val**.
## Example:
~~~
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
~~~
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
     * @param Integer $val
     * @return ListNode
     */
    function removeElements($head, $val) {
        $pre = null;
        $list = $head;
        
        while ($list) {
            if ($list->val == $val) {
                if ($pre === null) {
                    $head = $list->next;
                } else {
                    $pre->next = $list->next;
                }
            } else {
                $pre = $list;
            }
            
            $list = $list->next;
        }
        
        return $head;
    }
}
~~~