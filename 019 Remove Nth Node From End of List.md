# 19. Remove Nth Node From End of List
Given a linked list, remove the n-th node from the end of list and return its head.
## Example:
~~~
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
~~~
## Note:
Given n will always be valid.
## Follow up:
Could you do this in one pass?

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
     * @param Integer $n
     * @return ListNode
     */
    function removeNthFromEnd($head, $n) {
        $node_array = [$head];
        while ($head->next) {
            $node_array[] = $head->next;
            $head = $head->next;
        }
        
        $count = count($node_array);
        switch (true) {
            case $n == $count:
                return $node_array[1];
                break;
            case $n < $count:
                $elem = $count - $n;
                $pre_node = $node_array[$elem - 1];
                $next_node = null;
                if (array_key_exists($elem + 1, $node_array)) $next_node = $node_array[$elem + 1];
                $pre_node->next = $next_node;
                return $node_array[0];
                break;
        }
    }
}
~~~