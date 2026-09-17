# 🗺️ Ultimate JavaScript-to-Python DSA Mastery Course

A comprehensive, pattern-based curriculum designed specifically for developers transitioning from JavaScript to Python.

---

## 🔄 Phase 0: The JS-to-Python Fast Track (Week 1)
*Goal: Bridge your JavaScript expertise into Python without wasting time on basic programming logic.*

### 🛠️ Syntax & Memory Mechanics
Python uses **whitespace indentation** instead of curly braces `{}` to define code blocks. Variables do not require keywords (`let`/`const`), and statements do not require semicolons.

### 🔄 The Rosetta Stone Chart

| Feature | JavaScript | Python |
| :--- | :--- | :--- |
| **Variable Declaration** | `let x = 10;` <br> `const y = 20;` | `x = 10` <br> `y = 20` |
| **Console Output** | `console.log("Hello");` | `print("Hello")` |
| **Block Boundaries** | Curly Braces `{ ... }` | Indentation (4 spaces / 1 tab) |
| **Arrays vs. Lists** | `let arr = [1, 2, 3];` <br> `arr.push(4);` | `arr = [1, 2, 3]` <br> `arr.append(4)` |
| **Objects vs. Dicts** | `let obj = { "key": "val" };` <br> `obj.key` or `obj["key"]` | `data = { "key": "val" }` <br> `data["key"]` *(Throws error if key missing)* |
| **Conditional Logic** | `if (x === y) { ... } else if` | `if x == y:` <br> `elif x > y:` |

### 🔍 Linear Search Comparison
Finding an element in a sequence sequentially ($O(n)$ time complexity).

#### JavaScript Implementation
```javascript
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) return i;
    }
    return -1;
}
```

#### Python Implementation
```python
def linear_search(arr, target):
    # Native way: if target in arr: return arr.index(target)
    # Manual loop way matching the JS structural logic:
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```

### 📦 Essential Python Built-ins for DSA
*   `collections.deque` — Doubly-ended queue used to achieve $O(1)$ operations during BFS traversals.
*   `heapq` — Min-heap implementation required to build priority queues for algorithms like Dijkstra's.

#### 📺 Visuals & Reference Video
*   [Python for Beginners - Full Course by Programming with Mosh](https://youtube.com) *(Watch the first 1-2 hours to grasp foundational list and dict mechanics).*

---

## 🪟 Phase 1: Dual Sliding Window & Two Pointers (Weeks 2–3)
*Goal: Learn to optimize array/string tracking loops from $O(n^2)$ down to $O(n)$ linear time.*

### 🛠️ Core Algorithmic Patterns
*   **Two Pointers:** Manipulating indices moving toward each other from boundaries or traveling at different speeds.
*   **Fixed Sliding Window:** Maintaining a boundary sequence of static length $K$ by dropping the oldest element while adding the newest.
*   **Variable Sliding Window:** Expanding a trailing right pointer to intake data, then conditionally shrinking an explicit left pointer when boundaries break rules.

### 💻 Code Blueprint: Variable Sliding Window
Finding the maximum length of a subarray matching specific conditions.

#### JavaScript Implementation
```javascript
function maxWindow(arr, limit) {
    let left = 0, currentSum = 0, maxLen = 0;
    for (let right = 0; right < arr.length; right++) {
        currentSum += arr[right];
        while (currentSum > limit) {
            currentSum -= arr[left];
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

#### Python Implementation
```python
def max_window(arr, limit):
    left = 0
    current_sum = 0
    max_len = 0
    
    for right in range(len(arr)):
        current_sum += arr[right]
        # Shrink the window from the left if constraints are broken
        while current_sum > limit:
            current_sum -= arr[left]
            left += 1
        max_len = max(max_len, right - left + 1)
        
    return max_len
```

#### 📺 Visuals & Reference Video
*   [Sliding Window Technique Playlist by NeetCode](https://youtube.com)

#### 🧠 Practice Problems (LeetCode)
*   *LeetCode 167* - Two Sum II (Two Pointers)
*   *LeetCode 643* - Maximum Average Subarray I (Fixed Window)
*   *LeetCode 3* - Longest Substring Without Repeating Characters (Variable Window)

---

## 🌲 Phase 2: Hierarchical Trees & Structural Traversals (Weeks 4–5)
*Goal: Navigate non-linear parent-child memory structures using recursive and iterative strategies.*

### 🛠️ Core Algorithmic Patterns
*   **Depth-First Search (DFS):** Moving deeply into child nodes before processing sibling paths.
    *   *Pre-order:* Root ➡️ Left ➡️ Right
    *   *In-order:* Left ➡️ Root ➡️ Right *(Yields sorted output on Binary Search Trees)*
    *   *Post-order:* Left ➡️ Right ➡️ Root
*   **Breadth-First Search (BFS):** Traversing a hierarchical layer completely before moving to lower layers. Employs a First-In, First-Out (FIFO) queue.

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### 💻 Code Blueprint: Tree Traversals (DFS vs. BFS)

#### Python DFS (In-order Recursion)
```python
def inorder_dfs(root):
    if not root:
        return []
    # Left subtree + Current Node + Right subtree
    return inorder_dfs(root.left) + [root.val] + inorder_dfs(root.right)
```

#### Python BFS (Iterative Level Order)
```python
from collections import deque

def level_order_bfs(root):
    if not root:
        return []
    result = []
    queue = deque([root]) # Efficient FIFO queue
    
    while queue:
        level_size = len(queue)
        current_level = []
        for _ in range(level_size):
            node = queue.popleft() # O(1) removal operation
            current_level.append(node.val)
            if node.left:  queue.append(node.left)
            if node.right: queue.append(node.right)
        result.append(current_level)
    return result
```

#### 📺 Visuals & Reference Video
*   [Binary Tree Algorithms for Technical Interviews by freeCodeCamp](https://youtube.com)

#### 🧠 Practice Problems (LeetCode)
*   *LeetCode 94* - Binary Tree Inorder Traversal (DFS Mechanics)
*   *LeetCode 102* - Binary Tree Level Order Traversal (BFS Layers)
*   *LeetCode 104* - Maximum Depth of Binary Tree (Recursive Tree Properties)

---

## 🕸️ Phase 3: Graph Theory & Network Navigation (Weeks 6–8)
*Goal: Model cyclic interconnected frameworks, navigate grids, and resolve complex dependencies.*

### 🛠️ Core Algorithmic Patterns
*   **Graph Traversals (BFS/DFS with Cycles):** Standard search strategies extended by tracking nodes in a `visited = set()` structure to eliminate endless recursive looping.
*   **Implicit Grid Matrix Transforms:** Treating multi-dimensional lists as geographical coordinates where directional changes act as structural edges.
*   **Dijkstra's Shortest Path Algorithm:** Computing optimal minimal weight routing on graphs using a Min-Heap (`heapq`).
*   **Topological Sorting:** Linearly sorting nodes based on preceding dependencies (Kahn's algorithm).

### 💻 Code Blueprint: Graph Cyclic DFS (Adjacency List)
```python
def has_path_dfs(graph, start, destination, visited=None):
    if visited is None:
        visited = set()
    if start == destination:
        return True
    if start in visited:
        return False
        
    visited.add(start) # Log node to avoid looping back in cycles
    
    for neighbor in graph[start]:
        if has_path_dfs(graph, neighbor, destination, visited):
            return True
            
    return False
```

#### 📺 Visuals & Reference Video
*   [Graph Algorithms Course by William Fiset](https://youtube.com)

#### 🧠 Practice Problems (LeetCode)
*   *LeetCode 1971* - Find if Path Exists in Graph (Standard Network Verification)
*   *LeetCode 200* - Number of Islands (2D Implicit Matrix DFS)
*   *LeetCode 743* - Network Delay Time (Dijkstra's Algorithm Implementation)
*   *LeetCode 207* - Course Schedule (Topological Sort / Cycle Check)

---

## 🚀 Phase 4: Advanced Core Algorithmic Paradigms (Weeks 9–12)
*Goal: Solve high-level structural optimization, combinations, and computational state cache allocation problems.*

### 🛠️ Core Algorithmic Patterns
*   **Binary Search on Search Spaces:** Applying sorted range division tactics to arrive at non-apparent optimal threshold answers.
*   **Backtracking:** Brute-force optimization algorithms that build solution variations step-by-step and roll back state changes if the paths fail.
*   **Dynamic Programming (DP):**
    *   *Top-Down Memoization:* Caching calculation steps within dictionaries or hash maps to eliminate overlapping subproblems.
    *   *Bottom-Up Tabulation:* Solving dependencies sequentially inside linear multidimensional array structures.

### 💻 Code Blueprint: Backtracking Framework
```python
def permute(nums):
    result = []
    
    def backtrack(current_path, used_set):
        if len(current_path) == len(nums):
            result.append(list(current_path)) # Create a deep copy clone
            return
            
        for num in nums:
            if num not in used_set:
                # 1. Take Action / Modify State
                current_path.append(num)
                used_set.add(num)
                
                # 2. Recursively Move Forward
                backtrack(current_path, used_set)
                
                # 3. Rollback State (Undo Action)
                current_path.pop()
                used_set.remove(num)
                

