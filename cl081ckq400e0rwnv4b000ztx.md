## LeetCode #724

```
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        if (nums.empty()) {
            return -1;
        }
        int totalSum = 0;
        for (int i : nums) {
            totalSum += i;
        }

        int leftSum = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (leftSum * 2 + nums[i] == totalSum) {
                return i;
            }
            leftSum += nums[i];
        }
        return -1;
    }
};
```