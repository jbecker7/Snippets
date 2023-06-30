Constant lookup time for a set



'''

Let's say you are planning for a road trip with a car, the goal is to find the shortest time from you to get from point A to point B.

Given

location A

location B

a list of location pairs that tells you which two locations are connected.

  
  

Input: a, d, [[a,b], [a,c], [b,c], [c,d]]

  

"a" , "d" , [["a","b"], ..... ]

  

a - c - d

  

output = 2

  
  

dfs , bfs

  

bfs

  

'''

  

from collections import deque , defaultdict

  
  
  

def preprocess(adj_list):

map_dict = {}

'''

for i in range(len(adj_list)):

if adj_list[i][0] in map_dict:

map_dict[i][0].append(adj_list[i][1])

else:

map_dict[i][0] = []

for a,b in adj_list:

if a in map_dict:

map_dict[a].append(b)

else:

map_dict[a] = [b]

'''

map_dict = defaultdict(list)

for a,b in adj_list:

map_dict[a].append(b)

map_dict[b].append(a)

  

return map_dict

  

L = [["a","b"],["a","c"],["b","c"],["c","d"]]

  

def bfs(map_dict, start, end):

graph = preprocess(map_dict)

  

queue = deque()

visited = set()

  

visited.add(start)

queue.append((start, 0))

  

print("graph", graph)

while len(queue) > 0:

current, distance = queue.popleft()

print(current, distance)

print("current queue", queue)

if current == end:

return distance

  

for neighbor in graph[current]:

print("neighbour", neighbor)

print("visited", visited)

if neighbor not in visited:

print("adding to visited and queue", neighbor)

visited.add(neighbor)

queue.append((neighbor, distance+1))

return -1

  

map_dict = {"a": ["b","c"] }

bfs(L, "a", "d")