### Fundamentals

This is a very basic recursive DFS. 

- We first check the edge cases (there is no tree or we are already at the target). 
- We see if we can find the target in the left subtree  
	- The only way it can return anything is if it finds the target.
	- If it returns none, we can move on to the right subtree.
- Once we get to the right subtree, we do the same thing
	- If it finds target, it returns it
	- Otherwise we return None, which means it was not in the right subtree either (and thus does not exist)

#### Example Implementation:

```python
def dfs(root, target):
	if root is None:
		return None
	if root.val == target:
		return root 

	left = dfs(root.left, target)
	if left is not None:
		return left

	return dfs(root.right, target)
```

When it comes to doing it outside of just trees:
1. Need a set to avoid repeats
2. Need to check boundaries
3. DFS should take two coordinates
4. We need to check all the directions




### Depth-First Search 
#### Time: O(V+E)
#### Space: 
- Implemented using a stack since the idea is to look at the most recently encountered nodes first
```python
#Assuming the same input as my BFS above
visited = set() 

def dfs(visited, graph, node): 
    if node not in visited:
        print (node)
        visited.add(node)
        for neighbor in graph[node]:
            dfs(visited, graph, neighbor)
```

- Types of traversals
	- Inorder (DFS: left, self, right)
	- Post order (DFS: left, right, self)
	- Preorder (DFS: self, left, right)


## DFS LC Problems 

### Easy:

#### [Find All The Lonely Nodes (Easy)](https://leetcode.com/problems/find-all-the-lonely-nodes/description/)
A recursive solution like this is a lot more elegant.

```python
class Solution:
	def getLonelyNodes(self, root: Optional[TreeNode]) -> List[int]:
		self.lonelyarray = []

		def dfs(node):
			if node.left and not node.right:
				self.lonelyarray.append(node.left.val)
			if node.right and not node.left:
				self.lonelyarray.append(node.right.val)

			if node.left:
				dfs(node.left)
			if node.right:
				dfs(node.right)

		dfs(root)
		return self.lonelyarray
```


#### [Island Perimeter (Easy)](https://leetcode.com/problems/island-perimeter/)

```python
class Solution:
	def islandPerimeter(self, grid: List[List[int]]) -> int:
		visit = set()
		def dfs(i, j):
			if i >= len(grid) or j >= len(grid[0]) or \
				i < 0 or j < 0 or grid[i][j] == 0:
				return 1
				
			if (i, j) in visit:
				return 0
			
			visit.add((i,j))
			perim = dfs(i, j + 1)
			perim += dfs(i+1, j)
			perim += dfs(i, j-1)
			perim +=dfs(i-1, j)
			return perim 
"""
The part below is literally just to get us started--find one land--because we are guaranteed that all the land is connected.
"""

		for i in range(len(grid)):
			for j in range(len(grid[0])):
				if grid[i][j]:
					return dfs(i,j)
```


#### [Maximum Depth of a Binary Tree (Easy)](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

```python
class Solution:
	def maxDepth(self, root: Optional[TreeNode]) -> int:
		if not root:
			return 0 
		else:
			return 1+max(self.maxDepth(root.left),
			 self.maxDepth(root.right))
```


### Medium:


#### [Detect Cycles in 2D Grid (Medium)](https://leetcode.com/problems/detect-cycles-in-2d-grid/description/)

```python
class Solution:
    def containsCycle(self, grid: List[List[str]]) -> bool:
        visited = set()

        def dfs(i, j, pi, pj):
            if i < 0 or i >= len(grid) or j < 0 or \
            j >= len(grid[0]) or grid[i][j] != grid[pi][pj]:
            return False
            
            if (i, j) in visited:
                return True
            
            visited.add((i, j))
            for ni, nj in [(i+1, j), (i-1, j), (i, j+1), (i, j-1)]:
                if (ni, nj) != (pi, pj) and dfs(ni, nj, i, j):
                    return True
            
            return False

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if (i, j) not in visited and dfs(i, j, i, j):
                    return True
                
        return False

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
		currentislands = 0
		
		def dfs(r, c):
			currentislands += 1
			visit.add((0, 0))
			queue.append((0, 0))
			directions = [[1, 0], [0, 1], [-1, 0], [0, -1]]
			for x, y in directions:
				r, c = row + x, col + y
				if (r in range(rows) and
					c in range(cols) and
					grid[r][c] == "1" and
					(r,c) not in visit):
						visit.add((r,c))
						dfs(r,c)

			for r in range(rows):
				for c in range(cols):
					if grid[r][c] == "1" and (r, c) not in visit:
						currentislands = 0
						dfs(r, c)
					if currentislands > maxislands:
						maxislands = currentislands

			return maxislands
```



#### [All Paths From Source to Target (Medium)](https://leetcode.com/problems/all-paths-from-source-to-target/)

```python
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        end = len(graph) - 1

        def dfs(node, path, output):
            if node == end:
                output.append(path)

            for nx in graph[node]:
                dfs(nx, path+[nx], output)

        output = []
        dfs(0,[0],output)
        return output

```
