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

### Question 3:

[https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1](https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1)

**Solution:**

```cpp
class Solution {
public:
    int longestKSubstr(string &s, int k) {
        unordered_map<char, int> freq;
        int left = 0;
        int maxLen = -1;
        for (int right = 0; right < s.size(); right++) {
            freq[s[right]]++;
            // Shrink window if distinct characters exceed k
            while (freq.size() > k) {
                freq[s[left]]--;
                if (freq[s[left]] == 0) {
                    freq.erase(s[left]);
                }
                left++;
            }
            // Update answer when exactly k distinct characters exist
            if (freq.size() == k) {
                maxLen = max(maxLen, right - left + 1);
            }
        }
        return maxLen;
    }
};
```

### Question 4:

[https://leetcode.com/problems/fruit-into-baskets](https://leetcode.com/problems/fruit-into-baskets)

**Solution:**

```cpp
// Similar to previous question.
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        unordered_map<int, int> freq;
        int left = 0;
        int maxLen = 0;
        for (int right = 0; right < fruits.size(); right++) {
            freq[fruits[right]]++;
            // Shrink window if distinct characters exceed 2
            while (freq.size() > 2) {
                freq[fruits[left]]--;
                if (freq[fruits[left]] == 0) {
                    freq.erase(fruits[left]);
                }
                left++;
            }
            // Update answer when exactly 2 distinct characters exist
            maxLen = max(maxLen, right - left + 1);
        }
        return maxLen;
    }
};
```

### Question 5:

[https://leetcode.com/problems/longest-substring-without-repeating-characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)

**Solution:**

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> freq;
        int left = 0;
        int maxLen = 0;
        for (int right = 0; right < s.size(); right++) {
            freq[s[right]]++;
            int k = right - left + 1;
            while (freq.size() < k) {
                freq[s[left]]--;
                if (freq[s[left]] == 0) {
                    freq.erase(s[left]);
                }
                left++;
                k = right - left + 1;
            }
            maxLen = max(maxLen, right - left + 1);
        }
        return maxLen;
    }
};
```

### Question 6:

[https://leetcode.com/problems/longest-repeating-character-replacement](https://leetcode.com/problems/longest-repeating-character-replacement)

**Solution:**

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        unordered_map<char, int> freq;
        int left = 0;
        int maxFreq = 0;
        int maxLen = 0;
        for (int right = 0; right < s.size(); right++) {
            freq[s[right]]++;
            maxFreq = max(maxFreq, freq[s[right]]);

            while ((right - left + 1) - maxFreq > k) {
                freq[s[left]]--;
                left++;
            }
            maxLen = max(maxLen, right - left + 1);
        }
        return maxLen;
    }
};
```

### Question 7:

[https://leetcode.com/problems/minimum-window-substring](https://leetcode.com/problems/minimum-window-substring)

**Solution:**

```cpp
class Solution {
public:
    bool fun(vector<int>& have, vector<int>& need) {
        for (int i = 0; i < 256; i++) {
            if (have[i] < need[i])
                return false;
        }
        return true;
    }
    string minWindow(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<int> have(256, 0);
        vector<int> need(256, 0);
        int i;
        if (n < m)
            return "";
        for (i = 0; i < m; i++)
            need[t[i]]++;

        int low = 0, high = 0;
        int res = INT_MAX;
        int start = -1;
        for (high = 0; high < n; high++) {
            have[s[high]]++;

            while (fun(have, need)) // jab tk sahi hai
            {
                int len = high - low + 1;
                if (res > len) {
                    res = len;
                    start = low;
                }
                have[s[low]]--;
                low++;
            }
        }
        if (res == INT_MAX)
            return "";
        return s.substr(start, res);
    }
};
```
