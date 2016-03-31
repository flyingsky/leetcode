## Code

```C++
class Solution {
public:
  int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
      int sum = 0;
      int total = 0;
      int index = 0;
      for (int i = 0, size = gas.size(); i < size; i++) {
          sum += gas[i] - cost[i];
          total += gas[i] - cost[i];
          if (sum < 0) {
              index = i + 1;
              sum = 0;
          }
      }
      return total < 0 ? -1 : index;
  }
};

```

## Difficulty
Medium

## Analyze

1. If `gas[0] - cost[0] < 0`, we have to move to next station;
2. Else we can start from station 0 to station 1. If `gas[0]-cost[0] + gas[1]-cost[1] >= 0` after station 1, we can arrive station 2. But if it's less than 0, we cannot arrive station 2. The question is which station we should start again in this case, station 1 or station 2?
3. Because we always start from the station `i` where `gas[i]-cost[i] >= 0`, now at station `j` we find `sum(gas[i, j] - cost[i, j]) < 0`, any station k between `i` and `j` we have `sum(gas[i, k] - cost[i, k]) >= 0`, so choose any station k between i and j, we still get `sum(gas[k, j] - cost[k, j]) < 0`. In another word, we have to choose next station `j+1` as new start station. This is the major logic in our `for-loop`.
4. We need calculate the total value `sum(gas[0, n-1] - cost[0, n-1])` to make sure it's value not less than 0. If less than 0, we cannot find solution.
