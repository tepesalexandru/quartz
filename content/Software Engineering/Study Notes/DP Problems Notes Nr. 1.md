P1. You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

stair 1 = 1 step => 1 way
stair 2 = 1 step + 1 step or 2 steps => 2 ways
=> num. of steps for stair 1 + 1 step or 2 steps
stair 3 = 1 step + 1 step + 1 step or 1 step + 2 step or 2 step + 1 step => 3 ways
=> num. of steps for stair 2 + 1 step + num of steps for stair 1 + 2 steps

=> Fibonacci sequence with S1 = 1 & S2 = 2 ✅

P2. You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return _the minimum cost to reach the top of the floor_.

**Input:** cost = [10,15,20]
**Output:** 15

**Input:** cost = [1,100,1,1,1,100,1,1,100,1]
**Output:** 6

DP Relation?
min_cost[0] = 0;
min_cost[1] = 0;

min_cost[2] = min(min_cost[0] + cost[0], min_cost[1] + cost[1]);  ✅

P3. You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

**Input:** nums = [1,2,3,1]
**Output:** 4

**Input:** nums = [2,7,9,3,1]
**Output:** 12

DP Relation?
I can either rob a house or decide to skip it.
max_cashout[n] = how much money I have robbed, including house n

max_cashout[0] = nums[0]
max_cashout[1] = nums[1]

max_cashout[2] = max(max_cashout[1], max_cashout[0] + nums[2]);

generic relation => max_cashout[n] = max(max_cashout[n - 1], max_cashout[n - 2] + nums[n])

Iterative solution is the best ✅

P4. You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

The houses are arranged like this: [1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 1, 2, 3, 4, 5]
This means I cannot rob the first house and the last one at the same time.
Therefore, there are two options here, I can rob the interval [1, ..., n - 1] or [0, ..., n - 2]. The answer will be the max payout between those two.

Do I need two arrays or only one?
Let's try with two separate arrays.