- Static array: fixed length, indexable, contiguous memory
- Dynamic array: not fixed length, indexable, also stored in contiguous memory

| Operation             | Static Array | Dynamic Array |
|-----------------------|--------------|---------------|
| Access by Index       | O(1)         | O(1)          |
| Insertion at End      | N/A          | O(1) (amortized) |
| Insertion at Start    | N/A          | O(n)          |
| Insertion in Middle   | N/A          | O(n)          |
| Deletion at End       | N/A          | O(1)          |
| Deletion at Start     | N/A          | O(n)          |
| Deletion in Middle    | N/A          | O(n)          |
| Search                | O(n)         | O(n)          |



## Practice Problems:


### Two Sum

##### Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.


```
def twoSum(self, nums: List[int], target: int) -> List[int]:
	mappy={}
	for i in range(len(nums)):
		diff = target - nums[i]
		if diff in mappy:
			return [mappy[diff], i]
		else:
			mappy[nums[i]]=i
```

Runtime: O(n)

Intuition:
- We want to avoid looking at numbers more than once 
- By using a dictionary, we can keep track of each number *and* the other number that, if found, would solve the problem
- For example, if our target is 5 and we are looking at a 2, we can first check if there is a 3 in the dictionary. If there is, we are done and can return the index of that other number (stored as the value). Otherwise, we can put 2 in the dictionary as a key, with its index as the value 

