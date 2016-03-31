# Code

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> existingValues;
        vector<int> result;
        for (int i = 0, size = nums.size(); i < size; i++) {
            int current = nums[i];
            map<int, int>::iterator existingValue = existingValues.find(target - current);
            if (existingValue != existingValues.end()) {
                result.push_back(existingValue->second);
                result.push_back(i);
                break;
            } else {
                existingValues[current] = i;
            }
        }
        return result;
    }
};
```

## Difficulty
Easy
