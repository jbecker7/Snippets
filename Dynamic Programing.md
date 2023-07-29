## Fundamentals

1. Figure out parameters
2. Base case
	1. Caching
3. Recursive case


## DP LC Problems


### Medium:

#### [Predict The Winner (Medium)](https://leetcode.com/problems/predict-the-winner/description/)

```python
class Solution:
    def PredictTheWinner(self, nums: List[int]) -> bool:
        visited = defaultdict(int)

        def dp(left, right, turn):
            if left > right:
                return 0
            if (left, right, turn) in visited:
                return visited[(left, right, turn)]

            res = 0 
            # Player 1 tries to maximize their score
            if turn == 1:
                res = max(nums[left] + dp(left + 1, right, 2),
                        nums[right] + dp(left, right - 1, 2))
            # Player 2 tries to minimize player 1's score
            else:
                res = min(dp(left + 1, right, 1), dp(left, right - 1,
                 1))
            visited[(left, right, turn)] = res
            return res

        p1_score = dp(0, len(nums) - 1, 1)
        
        # One-liner to check the win condition, p1 wins ties
        return sum(nums) - p1_score <= p1_score

```
