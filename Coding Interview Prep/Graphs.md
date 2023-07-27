## Objects and Pointers
#### Benefits:
	- Good for edge insertion O(1)
	- Good for vertex insertion O(1)
	- Good for querying O(1)
#### Costs:
	- Okay for deletion O(E)
- Each node is an object
- Each edge is represented by a pointer from one node to another


## Adjacency Matrix
#### Benefits: 
	- Good for adding an edge O(1)
	- Good for removing an edge O(1)
	- Good for querying O(1)
#### Costs:
	- Bad for adding a vertex O(V^2)
	- Bad for removing a vertex O(V^2)
- Matrix where the vertices of the graph are represented on both axes, with a 1 if there is an edge connecting the two vertices


## Adjacency List
#### Benefits: 
	- Good for adding a vertex O(1)
	- Good for adding an edge O(1)
	- Good for removing a vertex O(V^2)
#### Costs:
	- Bad for removing an edge O(E)
	- Bad for querying O(V)
- Collection of unordered lists where each one represents the set of neighbors of a given vertex




## Graph LC Problems

### Number of Islands

This is basically just BFS, could change popleft to pop to make it an iterative DFS

##### Complexity: O(n * m)

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





