## LeetCode #35

```
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        // base case
        if (target <= nums[0]) {
            return 0;
        }
        if (target == nums[nums.size()-1]) {
            return nums.size() - 1;
        }
        if (target > nums[nums.size()-1]) {
            return nums.size();
        } 
        int left = 0, right = nums.size() - 1;
        while(left <= right) {
            int mid = (right + left) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return left;
    }
};
```