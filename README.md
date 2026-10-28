# cc2-expri-3.1.2

class Solution {
public:
bool canCross(vector<int>& stones) {
int n = stones.size();

    if (stones[1] != 1) {
        return false;
    }

    unordered_map<int, unordered_set<int>> dp;

    for (int stone : stones) {
        dp[stone] = unordered_set<int>();
    }

    dp[0].insert(0);

    for (int stone : stones) {
        for (int jump : dp[stone]) {
            for (int nextJump = jump - 1;
                 nextJump <= jump + 1;
                 nextJump++) {

                if (nextJump <= 0) {
                    continue;
                }

                int nextStone = stone + nextJump;

                if (dp.find(nextStone) != dp.end()) {
                    dp[nextStone].insert(nextJump);
                }
            }
        }
    }

    return !dp[stones[n - 1]].empty();
}


};
