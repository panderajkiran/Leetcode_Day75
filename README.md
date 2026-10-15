# Leetcode_Day75
# Day 75: Earliest Finish Time for Land and Water Rides I

**LeetCode Problem:** 3633. Earliest Finish Time for Land and Water Rides I  
**Difficulty:** Easy  
**Topic:** Arrays, Simulation, Nested Loops  
**Language:** Java

## Problem Statement

A theme park has two types of rides: land rides and water rides.

Each ride has:
- A start time, which is the earliest time the ride can be started.
- A duration, which is the time required to complete the ride.

A tourist must experience exactly one land ride and one water ride, in either order.

Find the earliest possible time at which the tourist can finish both rides.

## Approach: Brute Force

I solved this problem by checking every possible combination of land and water rides.

For each pair of rides, I calculate the finishing time in both possible orders.

### Case 1: Land Ride First
1. Calculate when the land ride finishes.
2. Start the water ride at the later of the land ride's finish time and its opening time.
3. Add the water ride's duration to get the final finishing time.

### Case 2: Water Ride First
1. Calculate when the water ride finishes.
2. Start the land ride at the later of the water ride's finish time and its opening time.
3. Add the land ride's duration to get the final finishing time.

Finally, I keep track of the minimum finishing time across all combinations.

## Java Solution

class Solution {
    public int earliestFinishTime(int[] landStartTime,
                                  int[] landDuration,
                                  int[] waterStartTime,
                                  int[] waterDuration) {

        int ans = Integer.MAX_VALUE;

        for (int i = 0; i < landStartTime.length; i++) {
            for (int j = 0; j < waterStartTime.length; j++) {

                int landFinish =
                    landStartTime[i] + landDuration[i];

                int waterFinish =
                    Math.max(landFinish, waterStartTime[j])
                    + waterDuration[j];

                ans = Math.min(ans, waterFinish);

                int waterFirstFinish =
                    waterStartTime[j] + waterDuration[j];

                int landSecondFinish =
                    Math.max(waterFirstFinish, landStartTime[i])
                    + landDuration[i];

                ans = Math.min(ans, landSecondFinish);
            }
        }

        return ans;
    }
}

## Complexity Analysis

- **Time Complexity:** O(L × W), where L is the number of land rides and W is the number of water rides.
- **Space Complexity:** O(1), because only a constant number of extra variables are used.

## What I Learned

- How to compare different possible sequences of activities.
- How Math.max() helps determine when the next ride can begin.
- How Math.min() helps track the earliest finishing time.
- How nested loops can explore every possible pair of choices.

## Takeaway

Today's problem reminded me that sometimes the best result comes from considering different possibilities before making a decision.

In coding, comparing every valid option helps us find the optimal answer. In life, taking a moment to consider our options can help us make better decisions.

**Day 75 complete — 75 days of learning, solving, and growing one problem at a time!**
