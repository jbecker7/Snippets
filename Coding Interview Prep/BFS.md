## Fundamentals

## BFS LC Problems

## Easy:

```python
class Solution:
	def getTargetCopy(self, original: TreeNode, cloned: TreeNode, target: TreeNode) -> TreeNode:
		if not original:
			return None

		if original is target:
			return cloned

#remember that "or" below will just return the first one that evaluates to True

		return self.getTargetCopy(original.left, cloned.left, target) or 
		self.getTargetCopy(original.right, cloned.right, target)
```


### [Merge Two Binary Trees (Easy)](https://leetcode.com/problems/merge-two-binary-trees/description/)


```python
class Solution:
	def mergeTrees(self, t1, t2):
		if t1 and t2:
			root = TreeNode(t1.val + t2.val)
			root.left = self.mergeTrees(t1.left, t2.left)
			root.right = self.mergeTrees(t1.right, t2.right)
			return root

else:
	return t1 or t2
```




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

```


### [Minimum Knight Moves (Medium)](https://leetcode.com/problems/minimum-knight-moves/)

Slow Brute Force:

```python
class Solution:
	def minKnightMoves(self, x: int, y: int) -> int:
		memo = {(0,0):0}
		queue = collections.deque([(0,0)])
		
		def get_next(loc):
			xx, yy = loc
			for dx, dy in [(2, 1), (1, 2), (-2, 1), (-1, 2), (2, -1),
			 (1, -2), (-1, -2), (-2, -1)]:
				 nx, ny = xx + dx, yy + dy
				 if (nx, ny) in memo: continue 
				 yield (nx, ny)
		
		step = 0
		while (x,y) not in memo:
			step += 1
			for _ in range(len(queue)):
				loc = queue.popleft()
				for next_loc in get_next(loc):
					memo[next_loc] = step
					queue.append(next_loc)

		
		return memo[(x,y)]
```


### [Snakes and Ladders (Medium)](https://leetcode.com/problems/snakes-and-ladders/)

```python
class Solution:
	def snakesAndLadders(self, board: List[List[int]]) -> int:
	n = len(board)
	
	def label_to_position(label):
		r, c = divmod(label-1, n)
		if r % 2 == 0:
			return n-1-r, c
		else:
			return n-1-r, n-1-c
	
	seen = set()
	queue = collections.deque()
	queue.append((1, 0))
	while queue:
		label, step = queue.popleft()
		r, c = label_to_position(label)
		if board[r][c] != -1:
			label = board[r][c]
		if label == n*n:
			return step
		for x in range(1, 7):
			new_label = label + x
			if new_label <= n*n and new_label not in seen:
				seen.add(new_label)
				queue.append((new_label, step+1))
	return -1
```
Yeah so I def do not understand what is going on in the above just yet hahahaha to be revisited


### [Pacific Atlantic Water Flow (Medium)](https://leetcode.com/problems/pacific-atlantic-water-flow/)
```python
class Solution:
	def pacificAtlantic(self, matrix: List[List[int]]) -> List[List[int]]:
		if not matrix:
			return []
		p_land = set()
		a_land = set()
		R, C = len(matrix), len(matrix[0])
		def spread(i, j, land):
			land.add((i, j))
			for x, y in ((i+1, j), (i, j+1), (i-1, j), (i, j-1)):
				if (0<=x<R and 0<=y<C and matrix[x][y] >= matrix[i][j]
				and (x, y) not in land):
					spread(x, y, land)
		for i in range(R):
			spread(i, 0, p_land)
			spread(i, C-1, a_land)
		for j in range(C):
			spread(0, j, p_land)
			spread(R-1, j, a_land)

		return list(p_land & a_land)
```


### [The Maze (Medium)](https://leetcode.com/problems/the-maze/)

```python
class Solution:
		def hasPath(self, maze: List[List[int]], start: List[int],
		 destination: List[int]) -> bool:
			stack = [start]
			n, m = len(maze), len(maze[0])
			dirs = ((0,1), (0,-1),(1,0), (-1,0))
			stopped = set()

			while stack:
				r, c = stack.pop()
				if [r,c] == destination: return True
				for dr, dc in dirs:
					nwR, nwC = r, c
					while 0 <= nwR + dr <= n-1 and 0 <= nwC + dc <= m-1
					 and maze[nwR+dr][nwC+dc] == 0:
						nwR += dr
						nwC += dc
					if (nwR, nwC) in stopped: continue
					else:
						stopped.add((nwR, nwC))
						stack.append(([nwR, nwC]))

			return False
```