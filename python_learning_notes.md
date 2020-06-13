## Array
- create array in one line
  
```python
grid = [[0,0,0,0], [0,0,0,0]]

n = len(grid) # 2
m = len(grid[0]) # 4

explored = [0] * m
# [0, 0, 0, 0]

explored = [[0] * m ]
# [[0, 0, 0, 0]]

explored = [[0] * m for i in range(n)]
# [[0,0,0,0], [0,0,0,0]]

''' Don't do this'''
explored = [[0]] * m
# [[0], [0], [0], [0]] but all 0 reference to same object

explored = [[0] * m] * n
# [[0,0,0,0], [0,0,0,0]]
```
`[0] * m` returns a reference to a list of m zeros, but not a list. <br/>
`*n` then creates a list of n items that all reference to the same list.

## Collection
  
  - `defaultdict`
```python
import collections

# Init a dict with zero as defulat value
dic = collection.defaultdict(0)

# Init a dict with []
dic = collection.defaultdict[]

```

## Heapq
- heapq is a min-heap (priority queue) 
- Complexity
  - heapify: 
  - heappush:  
  - heappop:  

```python
import heapq

# Min Heap
min_heap = [1,7,3,5]
heapq.heapify(min_heap) # [1, 5, 3, 7]
heapq.heappush(max_heap,4) # [1 ,4, 3, 7, 5]

# Max Heap
max_heap = [i * -1 for i in l]
heapq.heapify(max_heap)

heapq.heappush(max_heap, 4*-1) 
```

```
Colloetcions.counter
```

## Queue
- Complexity
  - popleft: `O(1)`
  - append: `O(1)` 

```python
from collections import deque

queue = [1,2,3]
queue.popleft() #[2,3]
# 1
queue.append(4) #[2,3,4]
```

- `bisect.bisect`
```

```python
import bisect
```