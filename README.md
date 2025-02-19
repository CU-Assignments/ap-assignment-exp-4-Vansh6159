# experiment-no.-4-22BCS_IOT-701B
https://leetcode.com/problems/longest-nice-substring/description/
https://leetcode.com/problems/maximum-subarray/description/
Experiment no. 4
# Maximum Subarray Sum & Longest Nice Substring

## Introduction
This Java program implements **Kadane's Algorithm** to find the **maximum sum subarray** in a given integer array. The algorithm efficiently determines the contiguous subarray with the largest sum in **O(n)** time complexity.

Additionally, it includes a function to find the **longest nice substring** from a given string. A string is considered "nice" if, for every letter in the substring, both its uppercase and lowercase forms exist within it.

## Algorithm Explanation
### Kadane's Algorithm
Kadane's Algorithm maintains two variables:
1. `currentSum` - Tracks the running sum of the current subarray.
2. `maxSum` - Stores the maximum subarray sum found so far.

At each step, we decide whether to:
- **Continue the current subarray** by adding the current element.
- **Start a new subarray** with the current element.

This decision is made using:
```java
currentSum = Math.max(nums[i], currentSum + nums[i]);
```
We then update `maxSum` whenever `currentSum` becomes larger:
```java
maxSum = Math.max(maxSum, currentSum);
```

### Longest Nice Substring Algorithm
The function `longestNiceSubstring` finds the longest contiguous substring where every letter has both its uppercase and lowercase present. The algorithm works by recursively splitting the string at characters that do not meet this condition and checking both parts for the longest nice substring.

## Code Implementation
### Kadane's Algorithm (Maximum Subarray Sum)
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];  // Store the maximum sum found
        int currentSum = nums[0];  // Running sum of the subarray

        for (int i = 1; i < nums.length; i++) {
            // Either continue the current subarray or start a new one
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }

    // Main function for testing
    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.maxSubArray(new int[]{-2,1,-3,4,-1,2,1,-5,4})); // Output: 6
        System.out.println(sol.maxSubArray(new int[]{1}));                     // Output: 1
        System.out.println(sol.maxSubArray(new int[]{5,4,-1,7,8}));            // Output: 23
    }
}
```

### Longest Nice Substring
```java
class Solution {
    public String longestNiceSubstring(String s) {
        if (s.length() < 2) return "";

        // Check if the string is nice
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (s.indexOf(Character.toUpperCase(c)) != -1 && s.indexOf(Character.toLowerCase(c)) != -1) {
                continue;
            }

            // If c is an unpaired letter, split at i and check both parts
            String left = longestNiceSubstring(s.substring(0, i));
            String right = longestNiceSubstring(s.substring(i + 1));

            return left.length() >= right.length() ? left : right;
        }

        return s;  // If no unpaired characters are found, the whole string is nice
    }

    // Main function for testing
    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.longestNiceSubstring("YazaAay"));  // Output: "aAa"
        System.out.println(sol.longestNiceSubstring("Bb"));       // Output: "Bb"
        System.out.println(sol.longestNiceSubstring("c"));        // Output: ""
    }
}
```

## Example Test Cases
### Kadane's Algorithm
| Input Array                    | Maximum Subarray Sum |
|--------------------------------|----------------------|
| `{-2,1,-3,4,-1,2,1,-5,4}`      | `6` (subarray: `[4,-1,2,1]`) |
| `{1}`                          | `1`  |
| `{5,4,-1,7,8}`                 | `23` (subarray: `[5,4,-1,7,8]`) |

### Longest Nice Substring
| Input String    | Longest Nice Substring |
|----------------|-----------------------|
| `"YazaAay"`   | `"aAa"`                |
| `"Bb"`        | `"Bb"`                 |
| `"c"`         | `""` (empty string)    |

## Complexity Analysis
- **Kadane's Algorithm**
  - **Time Complexity:** `O(n)`, since we traverse the array once.
  - **Space Complexity:** `O(1)`, as we use only a few extra variables.
- **Longest Nice Substring**
  - **Time Complexity:** `O(n^2)`, since we recursively split the string.
  - **Space Complexity:** `O(n)`, due to recursive calls.

## Applications
- **Kadane’s Algorithm**
  - Used in stock price analysis to find the best period for maximum profit.
  - Helps in analyzing large datasets for pattern recognition.
  - Applied in AI/ML for signal and image processing.
- **Longest Nice Substring**
  - Useful in text processing and formatting.
  - Can be applied in NLP (Natural Language Processing) for structured string analysis.





