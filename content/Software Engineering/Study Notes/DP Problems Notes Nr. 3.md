P1. You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Input:** nums = [2,3,1,1,4]
**Output:** true

What's the farthest I can reach by these jump lengths?

[1, 2, 3, 0, 0,  1, 1]
[1, 1, 1, 0, 0, 1, 1]

can_be_reached[i] = the i-th step can be reached or not

DP Relation?
can_be_reached[0] = true;
can_be_reached[1] = jumpLength[0] >= 1
can_be_reached[2] = jumpLength[0] >= 2 OR (jumpLength[1] >= 1 && can_be_reached[1])

can_be_reached[1] will always be true if jumpLength[0] >= 2, therefore it is not needed
=> can_be_reached[2] = jumpLength[0] >= 2 OR jumpLength[1] >= 1

can_be_reached[3] = jumpLength[0] >= 3 OR jumpLength[1] >= 2 OR jumpLength[]