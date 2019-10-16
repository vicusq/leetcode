# 231. Power of Two
Given an integer, write a function to determine if it is a power of two.
## Example 1:
~~~
Input: 1
Output: true 
~~~
Explanation: 2<sup>0</sup> = 1
## Example 2:
~~~
Input: 16
Output: true
~~~
Explanation: 2<sup>4</sup> = 16
## Example 3:
~~~
Input: 218
Output: false
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer $n
     * @return Boolean
     */
    function isPowerOfTwo($n) {
        $result = false;
        
        if ($n === 1) return true;
        
        $power = 1;
        for ($i = 0; ; $i ++) {
            $power *= 2;
            
            if ($power < $n) {
                $check = pow($power, 2);
                if ($check > $n) continue;
                
                $power = $check;
            }
            
            if ($power === $n) {
                $result = true;
                break;
            }
            
            if ($power > $n) break;
        }
        
        return $result;
    }
}
~~~