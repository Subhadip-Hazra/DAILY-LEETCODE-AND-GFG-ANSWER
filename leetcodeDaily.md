# Leetcode 08-May answer

[506. Relative Ranks](https://leetcode.com/problems/relative-ranks/description/?envType=daily-question&envId=2024-05-08)

# Intuition
To assign ranks to the scores, we can first find the maximum score to determine the highest rank. Then, we can iterate through the scores, assigning ranks based on their position relative to the maximum score.

# Approach
1. Find the maximum score in the given array.
2. Initialize an array to store the positions of the scores.
3. Iterate through the scores and store their positions in the array.
4. Iterate through the array of positions in reverse order to assign ranks.
5. Return the array of ranks.

# Complexity
- Time complexity: $$O(n + m)$$, where \(n\) is the number of scores and \(m\) is the maximum score.
- Space complexity: $$O(m)$$, where \(m\) is the maximum score.

# Code
```java
class Solution {
    // Function to find the maximum score
    private int maximum(int[] score, int n) {
        int max = -1;
        for (int i = 0; i < n; i++) {
            if (max < score[i]) {
                max = score[i];
            }
        }
        return max;
    }

    public String[] findRelativeRanks(int[] score) {
        int n = score.length;
        // Find the maximum score
        int top = maximum(score, n);
        // Array to store positions of scores
        int[] array = new int[top + 1];
        // Result array to store ranks
        String[] res = new String[n];

        // Store positions of scores
        for (int i = 0; i < n; i++) {
            array[score[i]] = i + 1;
        }

        int pos = 1;
        // Assign ranks
        for (int i = top; i >= 0; i--) {
            if (array[i] != 0) {
                if (pos == 1) 
                    res[array[i] - 1] = "Gold Medal";
                else if (pos == 2) 
                    res[array[i] - 1] = "Silver Medal";
                else if (pos == 3) 
                    res[array[i] - 1] = "Bronze Medal";
                else 
                    res[array[i] - 1] = String.valueOf(pos);
                pos++;
            }
        }
        return res;
    }
}
```

# Dry Run
Let's dry run the code with an example:

Input: `score = [10, 3, 8, 9, 4]`

1. Find the maximum score: `top = 10`.
2. Initialize array `[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]`.
3. Store positions of scores: 
   - `array[10] = 1`
   - `array[3] = 2`
   - `array[8] = 3`
   - `array[9] = 4`
   - `array[4] = 5`
4. Iterate through the array in reverse order:
   - For `i = 10`, assign "Gold Medal" to position `array[10] - 1 = 0`.
   - For `i = 9`, assign "Silver Medal" to position `array[9] - 1 = 3`.
   - For `i = 8`, assign "Bronze Medal" to position `array[8] - 1 = 2`.
   - For `i = 4`, assign "4" to position `array[4] - 1 = 4`.
   - For `i = 3`, assign "5" to position `array[3] - 1 = 1`.
5. Return `["Gold Medal", "5", "Bronze Medal", "Silver Medal", "4"]`.

For more this type of content follw me on
[Github](https://github.com/subhadip-hazra)
[Linkedin](https://www.linkedin.com/in/subhadiphazra/)
