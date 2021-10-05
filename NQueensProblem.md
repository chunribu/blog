[🏠HOME](README.md)

# N-Queens Problem
---

The eight queens puzzle is the problem of placing eight chess queens on an 8×8 chessboard so that no two queens threaten each other. Thus, a solution requires that no two queens share the same row, column, or diagonal. The eight queens puzzle is an example of the more general n queens problem of placing n non-attacking queens on an n×n chessboard, for which solutions exist for all natural numbers n with the exception of n=2 and n=3.

## Solutions
**Backtracking Algorithm**
fferent columns, starting from the leftmost column. When we place a queen in a column, we check for clashes with already placed queens. In the current column, if we find a row for which there is no clash, we mark this row and column as part of the solution. If we do not find such a row due to clashes then we backtrack and return false.

```
1) Start in the leftmost column;
2) If all queens are placed, return true;
3) Try all rows in the current column.  Do following for every tried row:
    a) If the queen can be placed safely in this row then mark this [row, column] as part of the solution and recursively check if placing queen here leads to a solution.
    b) If placing queen in [row, column] leads to a solution then return true.
    c) If placing queen doesn't lead to a solution then umark this [row, column] (Backtrack) and go to step (a) to try other rows.
4) If all rows have been tried and nothing worked, return false to trigger backtracking.
```
**Implement in Python**
```python
class NQueens:
    def __init__(self, queens_count):
        self.queens_count = queens_count
        self.solutions = []
    def is_safe(self, positions, row, col):
        if positions == []: return True
        for y, x in enumerate(positions):
            if x==row: return False
            if y==col: return False
            if abs(x-row) == abs(y-col): return False
        return True
    def recursive(self, positions, col):
        if col == self.queens_count: 
            self.solutions.append(positions)
            return True
        for row in range(self.queens_count):
            if self.is_safe(positions, row, col):
                self.recursive(positions+[row], col+1)
        return False
    def solve(self):
        self.recursive([], 0)
        return len(self.solutions)
    def show(self):
        n = self.queens_count
        for idx, s in enumerate(self.solutions):
            chessboard = [['·']*n for i in range(n)]
            for c, r in enumerate(s):
                chessboard[r][c] = 'Q'
            print(f'Solution NO. {idx+1}:')
            for i in chessboard:
                print(' '.join(i))
if __name__ == '__main__':
    nq = NQueens(8)
    nq.solve()
    nq.show()
```
