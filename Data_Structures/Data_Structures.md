# Data Structures
- Linked lists
- Stacks and Queues
- Heaps
- Vectors aka ArrayLists
- Hash Tables
- Trees, Tries
- Graphs

## Binary Heaps
Min-Heap and Max Heap
- Fibonacci heap has excellent amortized operations by using multiple heaps
- Heap can be stored as a single array
    - children are at 2n + 1 and 2n + 2 (for zero index array)
    - parent at (n - 1) / 2

### Min-Heap
- Complete
- Each node smaller than its children
- Root is minimum
- two operations, `insert` and `extract_min`; optionally, replace

### Insert
O(logN) time
1) Insert bottom level, lowest (leftmost position)
2) Swap with parent until fixed (Sift up)

### Extract min
O(logN) time
1) Remove root (the min)
2) Swap last element into root position
3) bubble down until fixed

# Hash Table
A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.
- Load factor: n / k
    - n number of entries occupied in hash table
    - k, number of buckets
As the load factor grows, the table becomes slower 

## Collision resolution
- One method is separate chaining, which is where each bucket is made of another type of storage, e.g. a linked list, self balancing BST, dynamic array.
- Open addressing: When a new entry has to be inserted, the buckets are examined, starting with the hashed-to slot and proceeding in some probe sequence, until an unoccupied slot is found. When searching for an entry, the buckets are scanned in the same sequence, until either the target record is found, or an unused array slot is found, which indicates that there is no such key in the table.   
Generally speaking, open addressing is better used for hash tables with small records that can be stored within the table (internal storage) and fit in a cache line. They are particularly suitable for elements of one word or less. If the table is expected to have a high load factor, the records are large, or the data is variable-sized, chained hash tables often perform as well or better.
    - Disadvantages: more stringent requirements of hash function.
    - Disadvante: Only saves memory for small entries
    - Advantage: Avoids time spent allocation new entries
    - Advantage: Better locality of reference

## Dynamic resizing
When an insert is made such that the number of entries in a hash table exceeds the product of the load factor and the current capacity then the hash table will need to be rehashed.
- All-at-once: copying all entries as the load reaches some threshold
- Incremental resizing: often used by real-time or disk based systems.
- Monotonic keys: 
- Linear Hashing:
- distributed hashing

## Advantages
- The main advantage of hash tables over other table data structures is speed. This advantage is more apparent when the number of entries is large. Hash tables are particularly efficient when the maximum number of entries can be predicted in advance, so that the bucket array can be allocated once with the optimum size and never resized.
- If the set of key-value pairs is fixed and known ahead of time (so insertions and deletions are not allowed), one may reduce the average lookup cost by a careful choice of the hash function, bucket table size, and internal data structures. In particular, one may be able to devise a hash function that is collision-free, or even perfect. In this case the keys need not be stored in the table.

## Drawbacks
- Although operations on a hash table take constant time on average, the cost of a good hash function can be significantly higher than the inner loop of the lookup algorithm for a sequential list or search tree. Thus hash tables are not effective when the number of entries is very small.
- For certain string processing applications, such as spell-checking, hash tables may be less efficient than tries, finite automata, or Judy arrays. Also, if there are not too many possible keys to store—that is, if each key can be represented by a small enough number of bits—then, instead of a hash table, one may use the key directly as the index into an array of values. Note that there are no collisions in this case.
- The entries stored in a hash table can be enumerated efficiently (at constant cost per entry), but only in some pseudo-random order. Therefore, there is no efficient way to locate an entry whose key is nearest to a given key. Listing all n entries in some specific order generally requires a separate sorting step, whose cost is proportional to log(n) per entry. In comparison, ordered search trees have lookup and insertion cost proportional to log(n), but allow finding the nearest key at about the same cost, and ordered enumeration of all entries at constant cost per entry.
- If the keys are not stored (because the hash function is collision-free), there may be no easy way to enumerate the keys that are present in the table at any given moment.
- Although the average cost per operation is constant and fairly small, the cost of a single operation may be quite high. In particular, if the hash table uses dynamic resizing, an insertion or deletion operation may occasionally take time proportional to the number of entries. This may be a serious drawback in real-time or interactive applications.
- Hash tables in general exhibit poor locality of reference—that is, the data to be accessed is distributed seemingly at random in memory. Because hash tables cause access patterns that jump around, this can trigger microprocessor cache misses that cause long delays. Compact data structures such as arrays searched with linear search may be faster, if the table is relatively small and keys are compact. The optimal performance point varies from system to system.
- Hash tables become quite inefficient when there are many collisions. While extremely uneven hash distributions are extremely unlikely to arise by chance, a malicious adversary with knowledge of the hash function may be able to supply information to a hash that creates worst-case behavior by causing excessive collisions, resulting in very poor performance, e.g., a denial of service attack. In critical applications, a data structure with better worst-case guarantees can be used; however, universal hashing—a randomized algorithm that prevents the attacker from predicting which inputs cause worst-case behavior—may be preferable.

## Uses
- Associate array: i.e. dictionary, or string based index
- DB indexing, though B-trees are usually preferred.
- Cache
- Set
- Object
- Unique data representation - string pool
- Transposition table - 

# Trees
## Binary tree
- Each node has up to two children
- Balanced: tree maintains O(n) `insert` and `find`
- Complete: Every level filled, except possibly the last, and then left to right
- Full: Every node zero or two children
- Perfect: Full and Complete. 2^k - 1 nodes where k is levels

## Binary Search Tree
- all left descendents <= root < all right decendents
- nodes = 2^n - 1
- branches = 2^n ?
- depth ~= log(nodes)
- Binary search requires an order relation by which every element (item) can be compared with every other element in the sense of a total preorder.

### Traversal
- In-Order: left, current, right
    - An in-order traversal of a binary search tree will always result in a sorted list of node items (numbers, strings or other comparable items).
    - Recursive or iterative
- Pre-Order: current, left, right
- Post-Order: left, right, current

### Operations
- Search
    - Iteratively or recursively
- Insert
    - Begins as search
    - Recursive or iterative solutions
- Delete
    - Deleting a node with no children: simply remove the node from the tree.
    - Deleting a node with one child: remove the node and replace it with its child.
    - Deleting a node with two children. Do not delete D. Instead, choose either its in-order predecessor node or its in-order successor node as replacement node

### Verification
- if the node is the left child of its parent, then it must be smaller than (or equal to) the parent and it must pass down the value from its parent to its right subtree to make sure none of the nodes in that subtree is greater than the parent
- if the node is the right child of its parent, then it must be larger than the parent and it must pass down the value from its parent to its left subtree to make sure none of the nodes in that subtree is lesser than the parent.
- As pointed out in section Traversal, an in-order traversal of a binary search tree returns the nodes sorted. Thus we only need to keep the last visited node while traversing the tree and check whether its key is smaller (or smaller/equal, if duplicates are to be allowed in the tree) compared to the current key.

### Uses
- In practice, the added overhead in time and space for a tree-based sort (particularly for node allocation) make it inferior to other asymptotically optimal sorts such as heapsort for static list sorting. On the other hand, it is one of the most efficient methods of incremental sorting, adding items to a list over time while keeping the list sorted at all times.
- Binary search trees can serve as priority queues

### Types
There are many types of binary search trees. AVL trees and red-black trees are both forms of self-balancing binary search trees. A splay tree is a binary search tree that automatically moves frequently accessed elements nearer to the root. In a treap (tree heap), each node also holds a (randomly chosen) priority and the parent node has higher priority than its children. Tango trees are trees optimized for fast searches. T-trees are binary search trees optimized to reduce storage space overhead, widely used for in-memory databases

# Tries
- Sometimes called a prefix tree, often used to store words, where each node is a character.
- * or null node represents word termination, sort of memoization.

# Graphs
- Directed (one way edge traversal) or un-directed (two way edge traversal)
- If every pair of verticies have an edge, the graph is 'connected'

## Adjaceny List
- Each node stores a list of connections, either nodes or edges.
- Can be created as an array or hash of lists instead of objects/classes

## Adjaceny Matrix
- NxN boolean matrix where N is number of nodes, and true indicates a connecting edge

## Third way is ???

## Graph search
### DFS
- Depth first: Pick a node and explore branch completely.
- Generally DFS preferred for visiting all nodes.
- Pre-order search with tracking node visits

### BFS
- Breadth First: Pick a branch and explore each neighbor first
- Generally BFS preferred for shortest path aglos.
- Use a queue for tracking nodes to visit
- Bidirectional search: find shortest path, uses two BFS one from each node.