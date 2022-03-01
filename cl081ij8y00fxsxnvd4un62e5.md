## LeetCode #56

```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.size() == 1) {
            return intervals;
        }
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> result;
        result.push_back(intervals[0]);
        int j = 0;
        for (int i = 1; i < intervals.size(); i++) {
            int l = intervals[i][0];
            int r = intervals[i][1];
            if (l > result[j][1]) {
                result.push_back(intervals[i]);
                j++;
                continue;
            }
            if (l < result[j][0]) {
                result[j][0] = l;
            }
            if (r > result[j][1]) {
                result[j][1] = r;
            }
        }
        return result;
    }
};
```