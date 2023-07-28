### Fundamentals
#### Objects and Pointers
##### Benefits:
	- Good for edge insertion O(1)
	- Good for vertex insertion O(1)
	- Good for querying O(1)
##### Costs:
	- Okay for deletion O(E)
- Each node is an object
- Each edge is represented by a pointer from one node to another


#### Adjacency Matrix
##### Benefits: 
	- Good for adding an edge O(1)
	- Good for removing an edge O(1)
	- Good for querying O(1)
##### Costs:
	- Bad for adding a vertex O(V^2)
	- Bad for removing a vertex O(V^2)
- Matrix where the vertices of the graph are represented on both axes, with a 1 if there is an edge connecting the two vertices

#### Adjacency List
##### Benefits: 
	- Good for adding a vertex O(1)
	- Good for adding an edge O(1)
	- Good for removing a vertex O(V^2)
##### Costs:
	- Bad for removing an edge O(E)
	- Bad for querying O(V)
- Collection of unordered lists where each one represents the set of neighbors of a given vertex

## Graph LC Problems




