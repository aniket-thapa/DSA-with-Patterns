# Sliding Window

When to use:

- Array / String and not on Linked List
- Subarray / Substring problems
- Problems finding max, min, sum, longest, shortest, count, average, at most k, at least k, exactly k of a subarray / substring

## Types of Sliding Window

1. Fixed Length Sliding Window: When the size of the window is fixed
2. Variable Length Sliding Window: When the size of the window is variable and can change based on certain conditions

### Question 1:

[https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1](https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)

**Solution:**

```cpp
class Solution {
public:
    int maxSubarraySum(vector<int>& arr, int k) {
        int low = 0;
        int high = k - 1;
        int sum = 0;
        int res = INT_MIN;
        // Calculate first window sum
        for (int i = low; i <= high; i++) {
            sum += arr[i];
        }
        // Slide the window
        while (high < arr.size()) {
            res = max(res, sum);
            low++;
            high++;
            if (high == arr.size()) {
                break;
            }
            sum = sum - arr[low - 1];
            sum = sum + arr[high];
        }

        return res;
    }
};
```

### Question 2:

[https://leetcode.com/problems/minimum-size-subarray-sum/](https://leetcode.com/problems/minimum-size-subarray-sum/)

**Solution:**

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int left = 0;
        int right = 0;
        int sum = 0;
        int minLength = INT_MAX;
        for (right = 0; right < nums.size(); right++) {
            // Expand window
            sum += nums[right];
            // Shrink window while condition is satisfied
            while (sum >= target) {
                minLength = min(minLength, right - left + 1);
                sum = sum - nums[left];
                left++;
            }
        }
        return (minLength == INT_MAX) ? 0 : minLength;
    }
};
```
