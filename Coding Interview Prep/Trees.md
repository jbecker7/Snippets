## Fundamentals 

- Trees are either
	- Empty
	- Key + child trees
- Examples of trees (file systems, decision trees, etc.)
- Lots of types of trees (Binary trees, Heaps, BSTs, AVL trees, etc.)
-  Why are there so many trees?
	- Dynamic data structure: easy to add a new directory/node
	- Structure conveys information: hierarchy (what is a child of what)
- Different organization -> Different types of trees
	- Root is most important -> heap
	- Organized by some kind of rule -> search trees
- Terminology
	- Parent and Child (obvious)
	- Leaf (a node without children)
	- Interior Node (non-leaves)
	- Level (1 + edges from root node, e.g. root is level 1)
	- Height (maximum depth of subtree node to farthest leaf)
	- Forest (collection of trees)
- Nodes contain:
	- A key
	- A list of children nodes
	- (Optional) A parent


### Binary Search Trees 
##### Time: O(logn) (height of tree)
(Cost of rebalancing?)
- Characteristics:
	- Binary Tree (so each node has a maximum of two children)
	- Left subtrees are less than parent
	- Right subtrees are greater than parent 
- Operations
	- Search: Go left to get smaller and go right to get bigger until we hit target value
	- Insert: Trace down until we find a leaf where the new node can fit
	- Deletion: 
		- No child: just search and remove
		- 1 child: connect grandparent and grandchild
		- 2 children: a bit harder, we need to reposition, look for "smallest value larger than the new node" or "biggest value smaller than the new node"
- What can we do?
	- Store things to look up efficiently


#### Useful Code
We can use this very simple Node class
```python
class Node:
	def __init__(self, key):
		self.key = key
		self.left = None
		self.right = None
```

##### BST Insertion 
```python
# Node here is going to be the root of the tree we are inserting into
def insert(node, key):
	if node is None:
		return Node(key)
	if key < node.key:
		# Then we can recurse on the left subtree
		node.left = insert(node.left, key)
	elif key > node.key:
		# Then we can recurse on the right subtree
	    node.right = insert(node.right, key)
	return node
```

##### BST Search
```python
def search(root, key):
	if root is None or root.key == key:
		return key
	if root.key < key:
		return search(root.right, key)
	elif root.key > key:
		return search(root.left, key)
```
##### BST Height
```python
def height(node):
	if node = None:
		return 0
	return 1 + max(height(node.left), height(node.right))
```

##### Node Count (Not 100% on this one)
```python
def BST_size(node):
	count = -1
    if root is not None:
        if root.left is not None:
            count += BST_size(root.left)
        if root.right is not None:
            count += BST_size(root.right)
    return count
```

### Heap/Priority Queue/Binary Heap

#### Heap
##### Insertion O(logn)
##### Access O(1)

- Definitions
	- Complete binary tree
		- All leaf elements must lean to the left
		- The last leaf might not have a right sibling
	- "In a max heap, for any given node C, if P is a parent of C, then the key of P is greater than or equal to the key of C"
	- "In a min heap, the key of P is less than or equal to the key of C"
	- As in other data structures, the node at the top without parents is called the root node
- HeapSort
	- Can be done using priority queues
		- create an empty priority queue
		- for i from 1 to n:
			- insert (A[i])
		- for i from n down to 1:
			- A[i] <- ExtractMax()
- Useful because
	- Height of heap is guaranteed to be O(log(N)) so operations from root to leaf are bounded  by O(log(N))
	- Since nodes in a root-to-leaf path are sorted, adding/removing a node, we only have to fix the order in the vertical path the node is in (so insertion and deletion are both O(log(N)) too)
- We can find the first free leaf to place our new key at using bubble up:
```python
def bubble_up(node):
	while node.parent and node.parent.key > node.key:
		#Obviously swap is Pseudocode
		swap node and node.parent
		node = node.parent
```

- We can delete_min using bubble down:
```python
def bubble_down(node):
	while node is not a leaf:
		smallest_child = child of node with smallest key
		if smallest_child < node:
			swap node and smallest_child
			node = smallest_child
		else:
			break
```
#### Priority Queue
- A special version of a queue
- However, priority queue has no notion of "start" or "end," instead it has a priority each element is assigned, and we can remove them based on those priorities 
- Thus, we need to have an Insert(p) operation and an Extract() method
	- Insert(p) inserts a new element with priority p
	- Extract() extracts the element with the maximum priority
- Additional operations we could add
	- Remove(it) removes an element based on a given iterator
	- GetMax() returns the maximum priority but doesn't extract
	- ChangePriority(it, p) changes the priority of an element pointed by it to p
- Implementation in Python
	- Could use a list or heapq or queue.priorityqueue
	- We would prefer using a heap 


#### Binary Heap
- A specific type of heap implemented using a binary tree
- Can be implemented using an array, with position in the array corresponding to position in the binary tree


### Tries
- Definitions:
	- A binary tree where the root represents the empty bit sequence and the two children represent letters that could come after to form a word
	- Used to store different words/sequences often
	- Instead of left and right nodes, we have some sort of lookup table
- Really useful for word validation (e.g. walk through this scrabble board and find all the words)



## Tree LC Problems

### Easy:
#### [Binary Tree Inorder Traversal (Easy)](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
#### Recursive Approach
##### Complexity: O(n)

```python
class Solution:
	def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
		res = []
		
		def inorder(root):
			if not root:
				return
			inorder(root.left)
			res.append(root.val)
			inorder(root.right)

		inorder(root)
		return res
		
```

#### [Maximum Depth of a Binary Tree (Easy)](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
###### Complexity:

```python
class Solution:
	def maxDepth(self, root: Optional[TreeNode]) -> int:
		if not root:
			return 0
		else:
			return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```


#### [Subtree of Another Tree (Easy)](https://leetcode.com/problems/subtree-of-another-tree/)
##### Complexity: O(s * t) where s and t are the sizes of the tree inputs

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
        if not t:
            return True
        if not s:
            return False

        if self.sameTree(s, t):
            return True
        return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)

    def sameTree(self, s, t):
        if not s and not t:
            return True
        if s and t and s.val == t.val:
            return self.sameTree(s.left, t.left) and self.sameTree(s.right, t.right)
        return False


```


#### [Balanced Binary Tree (Easy)](https://leetcode.com/problems/balanced-binary-tree/)
##### Complexity

```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            if not root:
                return [True, 0]

            left, right = dfs(root.left), dfs(root.right)
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, 1 + max(left[1], right[1])]

        return dfs(root)[0]

```


### Medium:

#### [Binary Tree Zigzag Level Order Traversal (Medium)](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

##### Complexity: O(n)
(Does space complexity get asked a lot)

```python
class Solution:
	def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
		res = []
		q = deque([root] if root else [])
		while q:
			level = []
			for i in range(len(q)):
				node = q.popleft()
				level.append(node.val)
				if node.left:
					q.append(node.left)
				if node.right:
					q.append(node.right)
			level = reversed(level) if len(res) % 2 == 1 else level
			res.append(level)
		return res
```


#### [Construct Binary Tree from Preorder and Inorder Traversal (Medium)](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

##### Complexity: 

Some helpful facts:
- First value in preorder traversal is *always* going to be the root
	-Sublist can be considered recursively 
```python
class Solution:
	def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
		if not preorder or not inorder:
			return None
		
		root = TreeNode(preorder[0])
		mid = inorder.index(preorder[0])
		root.left = self.buildTree(preorder[1:mid + 1], inorder[:mid])
		root.right = self.buildTree(preorder[mid + 1:], inorder[mid + 1:])
```


#### [Kth Smallest Element in a BST (Medium)](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
##### Complexity:

(Iterative Solution)
```python
class Solution:
	def kthSmallest(self, root: Treenode, k: int) -> int:
		n = 0
		stack = []
		cur = root

		while cur and stack:
			while cur:
				stack.append(cur)
				cur = cur.left
			
			cur = stack.pop()
			n += 1
			if n == k:
				return cur.val
			cur = cur.right
		
```


#### [Populating Next Right Pointers in Each Node (Medium)](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

##### Complexity: O(n) for time and memory

- We are essentially using BFS
- Current node, connect next nodes
- then switch next to be current and have its children as next
```python
class Solution:
	def connect(self, node: 'Optional[Node]') -> 'Optional[Node]':
		cur, nxt = node, node.left if node else None

		while cur and nxt:
			cur.left.next = cur.right
			if cur.next:
				cur.right.next = cur.next.left

			cur = cur.next
			if not cur:
				cur = nxt
				next = cur.left
		
		return node
```


#### [Inorder Successor in BST (Medium)](https://leetcode.com/problems/inorder-successor-in-bst/description/)
##### Complexity:

```python
class Solution:
	def inorderSuccessor(self, root: TreeNode, p: TreeNode) -> Optional[TreeNode]
		successor = None

		while root:
			if p.val >= root.val:
				root = root.right
			else:
				successor = root
				root = root.left
		return successor
```

