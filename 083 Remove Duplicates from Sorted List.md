# 83. Remove Duplicates from Sorted List
Given a sorted linked list, delete all duplicates such that each element appear only once.
## Example 1:
~~~
Input: 1->1->2
Output: 1->2
~~~
## Example 2:
~~~
Input: 1->1->2->3->3
Output: 1->2->3
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
     * @return ListNode
     */
    function deleteDuplicates($head) {
        $duplicates = [];

        $duplicates[$head->val] = true;
        $list = $pre = $head;
        while ($list = $list->next) {
            if (isset($duplicates[$list->val])) {
                $pre->next = $list->next;
                $list = $pre;
            } else {
                $duplicates[$list->val] = true;
            }

            $pre = $list;
        }

        return $head;
    }
}
~~~