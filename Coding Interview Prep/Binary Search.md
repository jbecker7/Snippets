## Runtime: O(log n)
### Works by continuously dividing the size of the list
	- In an iterative approach, this means cutting the size of the list with pointers
	- In a recursive approach, this means calling the function again on smaller and smaller lists

```python
class findTarget:        

#Lol I forgot the built-in absolute value syntax, so I wrote my own
    def av(self, a, b):

        if a < b :

            return b-a

        return a-b 

    def findImpl(self, arr, low, high, target, closest):

        #base case

        if low > high:

            return closest
  
        mid = low+(high-low)//2

        if arr[mid] == target:

            return mid

        elif arr[mid] > target:

            if av(mid, target) < closest:

                closest = mid

            return findImpl(arr, low, mid-1, target, closest)

        else:

            if av(mid, target) < closest:

                closest = mid

            return findImpl(arr, mid+1, high, target, closest)


    # return the index of the target in the array. or return -1.

    def find(self, arr: [Int], target):

        return findImpl(arr, 0, len(arr)-1, target,9999999999999999)

```


### [Search Insert Position (Easy)](https://leetcode.com/problems/search-insert-position/)

```python
class Solution:

def searchInsert(self, nums: List[int], target: int) -> int:
	left, right = 0, len(nums) - 1
	while left <= right:
		middle = (left+right)//2
	
		if nums[middle] == target:
			return middle

		elif nums[middle] > target:
			right = middle - 1

		else:
			left = middle + 1
	
	return left

"""
`left` points to the first element in the search range that is greater than the target (or points to the end of the list if the target is greater than all elements). As such, inserting the target at the `left` index ensures that the list remains sorted.
"""
```


### [Valid Perfect Square (Easy)](https://leetcode.com/problems/valid-perfect-square/)

```python
class Solution:
    def mysqrt(self, num: int) -> int:
        if num == 0 or num == 1:
            return num

        left, right = 1, num
        while left <= right:
            mid = left + (right - left) // 2
            square = mid * mid

            if square == num:
                return mid
            elif square < num:
                left = mid + 1
            else:
                right = mid - 1

        # When the loop ends, 'right' will be smaller than 'left',
        # and 'right' * 'right' will be the largest square smaller than 'num'.
        return right

    def isPerfectSquare(self, num: int) -> bool:
        sqrt_num = self.mysqrt(num)
        return sqrt_num * sqrt_num == num

```

### [Koko Eating Bananas (Medium)](https://leetcode.com/problems/koko-eating-bananas/)



### [Heaters (Medium)](https://leetcode.com/problems/heaters/)


