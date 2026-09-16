# 24BDA70191-EXP-3.1.2-CC-GROUP-A
class Solution {
public:
    bool canCross(vector<int>& stones) {
        int n = stones.size();
        
        // Map stone position to set of possible last jump sizes (k) that reached this stone
        unordered_map<int, unordered_set<int>> dp;
        for (int stone : stones) {
            dp[stone] = unordered_set<int>();
        }
        
        // The frog starts at stone 0 with a jump size of 0
        dp[stones[0]].insert(0);
        
        for (int i = 0; i < n; ++i) {
            int currentStone = stones[i];
            
            for (int k : dp[currentStone]) {
                // Try next jump steps: k - 1, k, k + 1
                for (int step = k - 1; step <= k + 1; ++step) {
                    if (step > 0 && dp.count(currentStone + step)) {
                        dp[currentStone + step].insert(step);
                    }
                }
            }
        }
        
        // Return true if the last stone has any incoming jump sizes recorded
        return !dp[stones.back()].empty();
    }
};
