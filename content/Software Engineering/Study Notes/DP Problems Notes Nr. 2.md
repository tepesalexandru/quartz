P1. A farmer has a **rectangular grid** of land with `m` rows and `n` columns that can be divided into unit cells. Each cell is either **fertile** (represented by a `1`) or **barren** (represented by a `0`). All cells outside the grid are considered barren.

A **pyramidal plot** of land can be defined as a set of cells with the following criteria:

1.  The number of cells in the set has to be **greater than** `1` and all cells must be **fertile**.
2.  The **apex** of a pyramid is the **topmost** cell of the pyramid. The **height** of a pyramid is the number of rows it covers. Let `(r, c)` be the apex of the pyramid, and its height be `h`. Then, the plot comprises of cells `(i, j)` where `r <= i <= r + h - 1` **and** `c - (i - r) <= j <= c + (i - r)`.

An **inverse pyramidal plot** of land can be defined as a set of cells with similar criteria:

1.  The number of cells in the set has to be **greater than** `1` and all cells must be **fertile**.
2.  The **apex** of an inverse pyramid is the **bottommost** cell of the inverse pyramid. The **height** of an inverse pyramid is the number of rows it covers. Let `(r, c)` be the apex of the pyramid, and its height be `h`. Then, the plot comprises of cells `(i, j)` where `r - h + 1 <= i <= r` **and** `c - (r - i) <= j <= c + (r - i)`.

Given a **0-indexed** `m x n` binary matrix `grid` representing the farmland, return _the **total number** of pyramidal and inverse pyramidal plots that can be found in_ `grid`.

**Input:** grid = [0,1,1,0],[1,1,1,1]
**Output:** 2

**Input:** grid = [1,1,1],[1,1,1]
**Output:** 2

Hint 1: How can DP help with this problem?
Hint 2: dp[r][c] = max_height of a pyramid having this position as apex.
Hint 3: How will the values at dp[r+1][c-1] and dp[r+1][c+1] help in determining the value at dp[r][c]?

dp[r][c] = dp[r + 1][c - 1] + dp[r + 1][c + 1] + 1 ✅

Hint 4: For the cell (r, c), is there a relation between the number of pyramids for which it serves as the apex and dp[r][c]? How does it help in calculating the answer?

dp[r][c] = num of piramids with this apex - 1 ✅