# 54. Spiral Matrix
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.
## Example 1:
~~~
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
~~~
## Example 2:
~~~
Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
~~~
# Solution:
~~~PHP
class Solution {

    /**
     * @param Integer[][] $matrix
     * @return Integer[]
     */
    function spiralOrder($matrix) {
        $this->result = [];
        $this->position_been = [];

        $this->matrix = $matrix;

        $this->m = count($matrix);
        if ($this->m < 1) return $matrix;
        if ($this->m == 1) return $matrix[0];

        if (!is_array($matrix[0])) return $matrix;
        $this->n = count($matrix[0]);
        if ($this->n == 1) {
            foreach ($matrix as $item) {
                $this->result[] = $item[0];
            }
            return $this->result;
        }

        $this->x = $this->y = 0;
        $this->result[] = $matrix[$this->x][$this->y];
        $this->position_been['00'] = true;

        return $this->walk('y', '+');
    }

    function walk($direct, $forward) {
        switch ($forward) {
            case '+':
                switch ($direct) {
                    case 'x':
                        for($this->x ++;$this->x < $this->m; $this->x ++) {
                            if (isset($this->position_been[$this->x.$this->y])) {
                                if (isset($this->position_been[($this->x - 1).($this->y - 1)])) return $this->result;
                                $this->x --;
                                return $this->walk('y', '-');
                            }

                            $this->result[] = $this->matrix[$this->x][$this->y];
                            $this->position_been[$this->x.$this->y] = true;
                        }

                        $this->x --;
                        return $this->walk('y', '-');
                        break;
                    case 'y':
                        for($this->y ++;$this->y < $this->n; $this->y ++) {
                            if (isset($this->position_been[$this->x.$this->y])) {
                                if (isset($this->position_been[($this->x + 1).($this->y - 1)])) return $this->result;
                                $this->y --;
                                return $this->walk('x', '+');
                            }

                            $this->result[] = $this->matrix[$this->x][$this->y];
                            $this->position_been[$this->x.$this->y] = true;
                        }

                        $this->y --;
                        return $this->walk('x', '+');
                        break;
                }
                break;
            case '-':
                switch ($direct) {
                    case 'x':
                        for($this->x --;$this->x >= 0; $this->x --) {
                            if (isset($this->position_been[$this->x.$this->y])) {
                                if (isset($this->position_been[($this->x + 1).($this->y + 1)])) return $this->result;
                                $this->x ++;
                                return $this->walk('y', '+');
                            }

                            $this->result[] = $this->matrix[$this->x][$this->y];
                            $this->position_been[$this->x.$this->y] = true;
                        }

                        $this->x ++;
                        return $this->walk('y', '+');
                        break;
                    case 'y':
                        for($this->y --; $this->y >= 0; $this->y --) {
                            if (isset($this->position_been[$this->x.$this->y])) {
                                if (isset($this->position_been[($this->x - 1).($this->y + 1)])) return $this->result;
                                $this->y ++;
                                return $this->walk('x', '-');
                            }

                            $this->result[] = $this->matrix[$this->x][$this->y];
                            $this->position_been[$this->x.$this->y] = true;
                        }

                        $this->y ++;
                        return $this->walk('x', '-');
                        break;
                }
                break;
        }
    }
}
~~~