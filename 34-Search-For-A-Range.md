# Code

```
class Solution {
public:
    int findLower(vector<int>& nums, int start, int end, int target) {
        if (start > end) {
            return -1;
        }

        int mid = (start + end) / 2;
        if (nums[mid] == target) {
            int lower = min(mid, findLower(nums, start, mid - 1, target));
            return lower == -1 ? mid : lower;
        } else if (nums[mid] > target) {
            return findLower(nums, start, mid - 1, target);
        } else {
            return findLower(nums, mid + 1, end, target);
        }
    }

    int findUpper(vector<int>& nums, int start, int end, int target) {
        if (start > end) {
            return -1;
        }

        int mid = (start + end) / 2;
        if (nums[mid] == target) {
            return max(mid, findUpper(nums, mid + 1, end, target));
        } else if (nums[mid] > target) {
            return findUpper(nums, start, mid - 1, target);
        } else {
            return findUpper(nums, mid + 1, end, target);
        }
    }

    vector<int> searchRange(vector<int>& nums, int target) {
        int lower = findLower(nums, 0, nums.size() - 1, target);
        if (lower < 0) {
            return vector<int>({-1, -1});
        }
        int upper = findUpper(nums, lower, nums.size() - 1, target);
        return vector<int>({lower, upper});
    }
};
```

# Difficulty
Medium

# Analyze
Recursive. The most important thing is make it clear, don't mix the search lower and upper at the same time.
