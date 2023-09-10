
## Fundamentals 

Fixed Sliding Window (gets the sums of all windows of size k)

```python
def fixed_sliding_window(arr: List[int], k: int) -> List[int]:
	curr_subarray = sum(arr[:k])
	result = [curr_subarray]

	#remove the leftmost, add the rightmost
	
	for i in range(1, len(arr)-k+1):
		curr_subarray = curr_subarray - arr[i-1]
		curr_subarray = curr_subarray + arr[i+k-1]

		result.append(curr_subarray)

	return result
```

Dynamic Sliding Window 

This is an example of a problem that requires a dynamic sliding window, in this case we need to find the minimum size that is bigger than x, so we don't know the size of the window.

```python
def dynamic_sliding_window(arr: List[int], x:int) -> int:
	min_length = float('inf')

	start = 0
	end = 0
	current_sum = 0

	while end < len(arr):
		current_sum = current_sum + arr[end]
		end = end + 1

		while start < end and current_sum >= x:
			current_sum = current_sum - arr[start]
			start = start + 1

		min_length = min(min_length, end-start+1)

	return mid_length
```



## Sliding Window LC Problems 

### Easy
#### [Best Time to Buy and Sell Stock (Easy)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```python
class Solution:
	def maxProfit(self, prices: List[int]) -> int:
		l, r = 0, 1
		maxP = 0

		while r < len(prices):
			if prices[l] < prices[r]:
				profit = prices[r] = prices[l]
				maxP = max(maxP, profit)
			else:
				l = r 

			r += 1
		return maxP
```




## Medium

### [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```python
class Solution:
	def lengthOfLongestSubstring(self, s: str) -> int:
		charSet = set()

		l = 0 
		res = 0

		for r in range(len(s)):
			while s[r] in charSet:
				charSet.remove(s[l])
				l += 1
			charSet.add(s[r])
			res = max(res, r - l + 1)
		return res
```


### [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

```python
class Solution:

	def characterReplacement(self, s: str, k: int) -> int:
		count = {}
		res = 0
	
		l = 0
		for r in range(len(s)):
			count[s[r]] = 1 + count.get(s[r], 0)
		#we have too many remaining "needs to be replaced"	
			while (r - l + 1) - max(count.values()) > k:
				count[s[l]] -= 1
				l += 1
			res = max(res, r - l + 1)
		return res
```


### [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

```python
class Solution:
	def findAnagrams(self, s: str, p: str) -> List[int]:
		if len(p) > len(s): return []
		pCount, sCount = {}. {}
		for i in range(len(p)):
			pCount[p[i]] = 1 + pCount.get(p[i], 0)
			sCount[s[i]] = 1 + sCount.get(s[i], 0)

		res = [0] if sCount == pCount else []

		l = 0 
		for r in range(len(p), len(s)):
			sCount[s[r]] = 1 + sCount.get(s[r], 0)
			sCount[s[l]] -= 1

			if sCount[s[l]] == 0:
				sCount.pop(s[l])
			l += 1
			if sCount == pCount:
				res.append(l)
		return res
```

### [Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

```python
class Solution: 
	def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int: 
	l = 0 
	res = 0 
	product = 1 
	
	for r in range(len(nums)): 
		product *= nums[r] 
		
		if product >= k: 
			while product >= k and l <= r: 
				product /= nums[l] 
				l += 1 
				
		res += r - l + 1 
		
	return res

```




## Hard

### [Sliding Window Median](https://leetcode.com/problems/sliding-window-median/)

```python
class Solution:

	def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:

		output = []
		q = collections.deque()
		l = r = 0
	
		while r < len(nums):
			while q and nums[q[-1]] < nums[r]:
				q.pop()
			q.append(r)
	
			if l > q[0]:
				q.popleft()
	
			if (r + 1) >= k:
				output.append(nums[q[0]])
				l += 1
			r += 1
	
		return output 
		
	
```