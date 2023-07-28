## Fundamentals

## BFS LC Problems

## Easy:


## Medium:

#### [Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)

```python
class Solution:
	def numIslands(self, grid: List[List[str]]) -> int:
		if not grid:
			return 0

		rows, cols = len(grid), len(grid[0])
		visit = set()
		islands = 0

		def bfs(r, c):
			q = collections.deque()
			visit.add((r, c))
			q.append((r,c))

			while q:
				row, col = q.popleft()
				directions = [[1, 0], [-1, 0], [0, 1], [0, -1]]

				for dr, dc in directions:
					r, c = row + dr, col + dc
					if (r in range(rows) and 
					    (c in range(cols) and
						grid[r][c] == "1" and
						(r, c) not in visit):
						q.append((r, c))
						visit.add((r,c))

		for r in range(rows):
			for c in range(cols):
				if grid[r][c] == "1" and (r, c) not in visit:
					bfs(r, c)
					islands += 1
		return islands
```

#### [Max Island Size (Medium)](https://leetcode.com/problems/max-area-of-island/)

```python
class Solution:
	def maxIslandSize(self, grid: List[List[str]]) -> int:
		if not grid:
			return 0
		rows, cols = len(grid), len(grid[0])
		visit = set()
		maxislands = 0
	def bfs(r, c):
		currentislands = 0
		queue = collections.deque()
		visit.add((0, 0))
		queue.append((0, 0))
		while queue:
			row, col = queue.popleft()
			directions = [[1, 0], [0, 1], [-1, 0], [0, -1]]
			for x, y in directions:
				r, c = row + x, col + y
				if (r in range(rows) and
					c in range(cols) and
					grid[r][c] == "1" and
					(r,c) not in visit):
						queue.append((r,c))
						visit.add((r,c))
						currentislands+=1
			if currentislands > maxislands:
				maxislands = currentislands

		for r in range(rows):
			for c in range(cols):
				if grid[r][c] == "1" and (r, c) not in visit:
					bfs(r, c)
	return maxislands


