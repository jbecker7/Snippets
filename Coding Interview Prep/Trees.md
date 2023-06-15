## Background 

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
### Breadth-First Search
#### Time: O(V+E)
#### Space: 
- Implemented using a queue since the idea is to deal with things in the order we encounter them
```python
'''
We assume that the graph is a dictionary where a key is a node and each value
is an array with the node's neighbors.
'''
visited = []
queue = []

def bfs(visited, graph, node):
  visited.append(node)
  queue.append(node)

  while queue:         
    m = queue.pop(0) 
    print (m, end = " ") 

    for neighbor in graph[m]:
      if neighbor not in visited:
        visited.append(neighbor)
        queue.append(neighbor)
```


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
        for neighbour in graph[node]:
            dfs(visited, graph, neighbour)
```

- Types of traversals
	- Inorder (DFS: left, self, right)
	- Post order (DFS: left, right, self)
	- Preorder (DFS: self, left, right)


## Binary Search Trees 
#### Time: O(logn) (height of tree)
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
		self. right = None
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

- [ ]  print_values // prints the values in the tree, from min to max
- [ ]  delete_tree
- [ ]  is_in_tree // returns true if given value exists in the tree
- [ ]  get_min // returns the minimum value stored in the tree
- [ ]  get_max // returns the maximum value stored in the tree
- [ ]  is_binary_search_tree
- [ ]  delete_value
- [ ]  get_successor // returns next-highest value in tree after given value, -1 if none