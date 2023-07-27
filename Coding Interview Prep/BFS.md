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