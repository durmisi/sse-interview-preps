# Module 02 — Data Structures & Algorithms

**Senior Software Engineer Academy · Module 02 of 12**

> **Learning objective:** Master complexity analysis, internal data structure mechanics, standard algorithmic paradigms, and high-performance C#/.NET collection engineering. Develop the disciplined problem-solving methodology expected in Senior and Staff Software Engineer coding interviews: establishing invariants, identifying bottlenecks, explaining time and auxiliary space trade-offs, and connecting algorithmic solutions to enterprise scalability and production performance.
>
> **Audience:** Experienced C#/.NET engineers preparing for senior technical interviews. Real-world systems experience is assumed; theoretical foundations and runtime memory mechanics are taught with rigorous precision.
>
> **Version note:** Code examples target modern .NET (.NET 8 LTS and .NET 9) with C# 12/13. Features include `PriorityQueue<TElement, TPriority>`, `Span<T>`, `ReadOnlySpan<T>`, `SearchValues<T>` (.NET 8), `FrozenDictionary<TKey, TValue>` (.NET 8), and `Dictionary<TKey, TValue>.GetAlternateLookup` (.NET 9).

## How to use this module

Every section in Part II provides comprehensive senior-level instruction:
1. **Fundamentals & Internal Mechanics:** Mathematical proofs, asymptotic bounds, pointer layouts, and cache-line locality.
2. **C#/.NET Reference Implementation:** Production-grade, zero-allocation algorithms with invariants and bounds checks.
3. **Enterprise Application:** High-volume event deduplication, in-memory caches, rate limiters, DAG task runners, and routing engines.
4. **Trade-offs, Alternatives & Failure Modes:** When a theoretically superior algorithm fails due to constant factors or hardware realities.
5. **What a Senior Engineer Is Expected to Know:** Mid-level vs Senior/Staff reasoning.
6. **Interview Questions with Model Answers:** Real interview questions with structured, senior-level responses.
7. **Practical Exercises:** Deep coding challenges without inline solutions.

## Progress tracker

| Section | Topic | Status |
|---|---|---|
| Section 1 | Complexity Analysis & Algorithmic Thinking | Complete |
| Section 2 | Core Data Structures & .NET Collection Internals | Complete |
| Section 3 | Arrays, Strings & High-Value Array Patterns | Complete |
| Section 4 | Linked Lists, Stacks, Queues & Deques | Complete |
| Section 5 | Hashing, Maps, Sets & Probabilistic Structures | Complete |
| Section 6 | Trees, Heaps, Tries & Skip Lists | Complete |
| Section 7 | Graphs, Traversals & Shortest Paths | Complete |
| Section 8 | Searching & Binary Search on Answer Space | Complete |
| Section 9 | Sorting, Selection & Top-K Patterns | Complete |
| Section 10 | Algorithmic Problem-Solving Paradigms (DP, Greedy, Backtracking) | Complete |
| Section 11 | C#/.NET Algorithmic Fluency & Performance Pitfalls | Complete |
| Section 12 | Senior-Level Coding Interview Methodology | Complete |
| Section 13 | Data Structures & Algorithms in Enterprise Systems | Complete |
| Section 14 | Integrated Assessment & Capstone | Complete |

**Current position:** Full curriculum complete. Ready for self-study, exercises, and interview drills.

## Module boundaries

- **This module owns:** Algorithmic complexity analysis, data structure implementations, pattern templates, coding interview problem-solving technique, in-memory algorithmic tuning, and .NET collection selection.
- **Related topics owned by other modules:**
  - CLR memory layout, GC generations, heap allocation, and JIT compilation → Module 03
  - Object-oriented modeling, encapsulation, and SOLID principles → Module 01
  - Database indexing (B+Tree, Hash), SQL query execution plans, and transactions → Module 05
  - Distributed coordination, distributed caching, and consensus algorithms → Module 07
  - System-level scalability, load balancing, and architectural partitioning → Module 08

---

# Part I — Complete Curriculum

## Section 1 — Complexity Analysis & Algorithmic Thinking
- 1.1 Asymptotic Notation: Big O, Big Omega, Big Theta, strict vs non-strict bounds.
- 1.2 Common Complexity Classes: $O(1)$, $O(\log n)$, $O(n)$, $O(n \log n)$, $O(n^2)$, $O(2^n)$, $O(n!)$; growth table across $n=10$ to $10^6$.
- 1.3 Systematic Loop Analysis: Independent loops, nested loops, triangular series, multiplicative progress.
- 1.4 Recursion Analysis & Master Theorem: Recurrence relations ($T(n) = aT(n/b) + f(n)$), recursion call trees, call-stack space.
- 1.5 Amortized Analysis: Aggregate method, accounting method, potential method; dynamic array geometric resizing proof.
- 1.6 Space Complexity: Auxiliary space vs total space; in-place operations vs hidden allocations.
- 1.7 Complexity vs Runtime Reality: Constant factors, CPU cache lines (L1/L2/L3), branch prediction, hardware prefetching.

## Section 2 — Core Data Structures & .NET Collection Internals
- 2.1 Arrays & Dynamic Arrays: Memory layout, bounds checks, capacity growth, `T[]` vs `List<T>`.
- 2.2 Slicing Primitives: `Span<T>`, `ReadOnlySpan<T>`, `Memory<T>`, `ref struct` rules.
- 2.3 Hash-Based Collections: `Dictionary<TKey, TValue>` and `HashSet<T>` internal buckets, entries, collision resolution, load factors, resizing.
- 2.4 Modern Specialized Collections: `FrozenDictionary<TKey, TValue>`, `SearchValues<T>`, `PriorityQueue<TElement, TPriority>`.
- 2.5 Ordered Collections: `SortedDictionary<TKey, TValue>` (Red-Black tree) vs `SortedList<TKey, TValue>` (binary-searched array).
- 2.6 Thread-Safe Collections: `ConcurrentDictionary<TKey, TValue>`, `ConcurrentQueue<T>`, `Channel<T>` for asynchronous backpressure.

## Section 3 — Arrays, Strings & High-Value Array Patterns
- 3.1 Two Pointers: Opposing direction (two-sum, palindrome, container with most water), same direction (slow/fast pointer, cycle detection, duplicate removal).
- 3.2 Sliding Window: Fixed window (maximum sum subarray of size K) vs variable window (longest substring without repeating characters, minimum window substring).
- 3.3 Prefix Sums & Running Aggregates: 1D prefix sum, 2D matrix range query, subarray sum equals K with hash map.
- 3.4 Difference Arrays: Range update queries in $O(1)$ time with $O(n)$ prefix reconstruction.
- 3.5 Interval Problems: Merging overlapping intervals, interval insertion, meeting rooms concurrency.
- 3.6 String Internals: UTF-16 code units vs `Rune` vs Grapheme clusters; `StringBuilder` capacity planning; zero-allocation parsing with `ReadOnlySpan<char>`.

## Section 4 — Linked Lists, Stacks, Queues & Deques
- 4.1 Linked List Mechanics: Singly vs doubly linked lists; node reference overhead vs cache locality; dummy sentinel heads/tails.
- 4.2 Core Linked List Operations: In-place reversal, cycle detection (Floyd's Tortoise and Hare), finding cycle start, intersection of two lists.
- 4.3 LRU Cache Architecture: $O(1)$ `Get` and `Put` combining a hash map and a doubly linked list.
- 4.4 Stack Patterns: Balanced delimiters, expression evaluation (Reverse Polish Notation), call stack simulation.
- 4.5 Monotonic Stack: Next Greater Element, Daily Temperatures, Largest Rectangle in Histogram ($O(n)$ single-pass).
- 4.6 Queue & Monotonic Deque: BFS foundations, circular buffers, Sliding Window Maximum in $O(n)$ time.

## Section 5 — Hashing, Maps, Sets & Probabilistic Structures
- 5.1 Hashing Mechanics: Hash code distribution, avalanche effect, bucket arrays, collision resolution (separate chaining vs open addressing).
- 5.2 Correctness Hazards: Mutable keys in dictionaries, broken `IEquatable<T>` / `GetHashCode` contracts, hash collisions and HashDoS attacks.
- 5.3 High-Cardinality Sets & Frequency Maps: Anagram grouping, top-K frequent elements, complement lookups.
- 5.4 Probabilistic Structures: Bloom Filters (hashing functions, false positive probability math, bit arrays); Count-Min Sketch for frequency estimation.

## Section 6 — Trees, Heaps, Tries & Skip Lists
- 6.1 Tree Foundations: Terminology (depth, height, diameter), Binary Tree traversals (Pre-order, In-order, Post-order, Level-order BFS).
- 6.2 Binary Search Trees (BST): BST property, search, insert, delete (in-order successor replacement), degeneration risks.
- 6.3 Balanced Search Trees: AVL trees (height-balanced, rotations) vs Red-Black trees (color invariants, 2-3-4 tree isomorphism); why .NET uses Red-Black.
- 6.4 Binary Heaps & Priority Queues: Array-backed complete binary tree, parent/child index math, `HeapifyUp`, `HeapifyDown`, $O(n)$ `BuildHeap` vs $O(n \log n)$ successive inserts.
- 6.5 Tries (Prefix Trees): TrieNode array vs map, insertion, prefix search, auto-complete, wildcard matching.
- 6.6 Skip Lists: Probabilistic multi-level linked lists, $O(\log n)$ search/insert/delete without complex tree rotations.

## Section 7 — Graphs, Traversals & Shortest Paths
- 7.1 Graph Representations: Adjacency List vs Adjacency Matrix vs Edge List; space/time trade-offs for sparse vs dense graphs.
- 7.2 Graph Traversals: Breadth-First Search (BFS) for shortest path in unweighted graphs; Depth-First Search (DFS) for reachability and pathfinding.
- 7.3 Cycle Detection & Connected Components: Directed graphs (three-color DFS), undirected graphs (visited set / parent tracking), strongly connected components.
- 7.4 Topological Sorting: Kahn's algorithm (indegree queue) vs DFS post-order reversal; detecting circular dependencies in build engines.
- 7.5 Single-Source Shortest Path: Dijkstra's algorithm with min-heap (`PriorityQueue`) for non-negative weights; Bellman-Ford for negative weights and cycle detection.
- 7.6 Disjoint Set Union (DSU / Union-Find): Path compression, union by rank/size, near $O(1)$ amortized inverse Ackermann complexity $lpha(n)$.
- 7.7 Minimum Spanning Tree (MST): Kruskal's algorithm (greedy + DSU) vs Prim's algorithm.

## Section 8 — Searching & Binary Search on Answer Space
- 8.1 Binary Search Mechanics: Exact match, lower bound (first occurrence), upper bound (last occurrence); avoiding integer overflow in midpoint calculation.
- 8.2 Rotated & Transformed Sorted Arrays: Binary search in rotated sorted array; search in 2D sorted matrix.
- 8.3 Binary Search on Answer Space (Monotonic Predicates): Identifying monotonicity ($FFFFTTTT$); capacity allocation, shipping packages within D days, Koko eating bananas.

## Section 9 — Sorting, Selection & Top-K Patterns
- 9.1 Comparison Sorts: Merge Sort (stable, $O(n \log n)$ time, $O(n)$ space), Quick Sort (unstable, in-place, median-of-three pivot, 3-way partitioning for duplicates), Heap Sort.
- 9.2 Non-Comparison Sorts: Counting Sort, Radix Sort, Bucket Sort ($O(n)$ under bounded integer distributions).
- 9.3 Selection Algorithms: Quickselect (expected $O(n)$ time, in-place) for finding the Kth smallest/largest element.
- 9.4 Top-K Elements: Min-heap of size K ($O(n \log K)$ time, $O(K)$ space) vs Quickselect ($O(n)$ average).
- 9.5 .NET Sorting Internals: `Array.Sort<T>` uses IntroSort (QuickSort switching to HeapSort when recursion depth exceeds $2 \log n$, switching to InsertionSort for small arrays).

## Section 10 — Algorithmic Problem-Solving Paradigms
- 10.1 Recursion & Backtracking: State space trees, base cases, choice/constraint/goal, state restoration; combinations, permutations, N-Queens, Sudoku.
- 10.2 Divide and Conquer: Merge Sort, Quick Sort, Fast Exponentiation ($O(\log n)$).
- 10.3 Greedy Algorithms: Greedy choice property, optimal substructure, exchange argument proof; interval scheduling, fractional knapsack.
- 10.4 Dynamic Programming (DP): Overlapping subproblems, optimal substructure, top-down memoization vs bottom-up tabulation.
- 10.5 Core DP Archetypes: 1D sequence (Fibonacci, House Robber), Grid traversal (Unique Paths, Minimum Path Sum), 0/1 Knapsack & Unbounded Knapsack, Longest Common Subsequence (LCS) & Edit Distance, Longest Increasing Subsequence (LIS in $O(n \log n)$).

## Section 11 — C#/.NET Algorithmic Fluency & Performance Pitfalls
- 11.1 LINQ Complexity Pitfalls: Deferred execution, multiple enumeration of `IEnumerable<T>`, hidden $O(n^2)$ scans with repeated `.Contains()`.
- 11.2 Allocation & Boxing: Value type boxing across non-generic interfaces, closure allocations in LINQ lambdas, iterator state machine overhead.
- 11.3 Memory Pooling: `ArrayPool<T>.Shared`, renting, returning, buffer clearing, preventing memory leaks and data exposure.
- 11.4 Integer Overflow & Bounds: `checked` arithmetic, bitwise shifts vs division, unsigned bit tricks.

## Section 12 — Senior-Level Coding Interview Methodology
- 12.1 The 7-Step Interview Framework: Clarify -> Explore Constraints -> Propose Baseline -> Identify Bottleneck -> Optimize -> Code with Invariants -> Validate Edge Cases.
- 12.2 Communication Protocol: Narrating trade-offs aloud, structuring whiteboard explanations, handling hints constructively, responding to changing constraints.
- 12.3 Systematic Edge-Case Checklist: Empty input, single element, duplicates, all identical elements, sorted/reverse sorted, large inputs, negative values, integer bounds.

## Section 13 — Data Structures & Algorithms in Enterprise Systems
- 13.1 High-Throughput In-Memory Caching: LRU eviction, concurrency control, lock striping, read-through patterns.
- 13.2 Rate Limiting Algorithms: Token Bucket, Leaky Bucket, Fixed Window Counter, Sliding Window Log, Sliding Window Counter.
- 13.3 Event Stream Processing & Deduplication: Sliding window deduplication, bounded memory queues, backpressure handling with channels.
- 13.4 Retrieval & Search Engineering: Inverted Index for keyword search, Vector embeddings with cosine similarity for AI semantic search.

## Section 14 — Integrated Assessment & Capstone
- 14.1 Full Worked Capstone 1: Design and implement an in-memory, thread-safe, high-concurrency LRU Cache with $O(1)$ read/write and TTL expiration.
- 14.2 Full Worked Capstone 2: Directed Acyclic Graph (DAG) Task Orchestrator with cycle detection, parallel independent execution, and fail-fast cancellation.
- 14.3 Full Worked Capstone 3: High-Volume Sliding Window Rate Limiter handling 100,000 requests/second with minimal memory footprint.

---

# Part II — Lessons

## Section 1 — Complexity Analysis & Algorithmic Thinking

### 1.1 Asymptotic Notation: Big O, Big Omega, and Big Theta

Asymptotic analysis characterizes how resource consumption (time or memory) scales as the input size $n$ tends toward infinity.

1. **Big O ($O$): Asymptotic Upper Bound**
   $f(n) = O(g(n))$ if there exist positive constants $c$ and $n_0$ such that:
   $$0 \le f(n) \le c \cdot g(n) \quad 	ext{for all } n \ge n_0$$
   *Engineering meaning:* The algorithm will never perform worse than $c \cdot g(n)$ steps for sufficiently large inputs.

2. **Big Omega ($\Omega$): Asymptotic Lower Bound**
   $f(n) = \Omega(g(n))$ if there exist positive constants $c$ and $n_0$ such that:
   $$0 \le c \cdot g(n) \le f(n) \quad 	ext{for all } n \ge n_0$$
   *Engineering meaning:* The algorithm requires at least $c \cdot g(n)$ steps in the best case or under all inputs.

3. **Big Theta ($\Theta$): Asymptotically Tight Bound**
   $f(n) = \Theta(g(n))$ if and only if $f(n) = O(g(n))$ and $f(n) = \Omega(g(n))$.
   *Engineering meaning:* The algorithm grows at the exact same rate as $g(n)$ within constant factor bounds.

**Common Interview Shorthand Corrected:**
Interview candidates often say *"Big O means worst case."* That is mathematically false. Big O is a mathematical bounding operator. You can calculate the Big O of the best case (e.g., QuickSort best case is $O(n \log n)$), the Big O of the average case, or the Big O of the worst case (QuickSort worst case is $O(n^2)$).

---

### 1.2 Common Complexity Classes & Growth Rates

The table below illustrates the concrete number of basic operations required across input sizes from $n=10$ to $n=1,000,000$, assuming $10^9$ operations per second (1 GHz CPU execution baseline):

| Complexity Class | Name | $n = 10$ | $n = 100$ | $n = 1,000$ | $n = 10^6$ (One Million) | Theoretical Runtime ($10^9$ ops/sec) |
|---|---|---|---|---|---|---|
| $O(1)$ | Constant | 1 | 1 | 1 | 1 | $pprox 1 	ext{ ns}$ |
| $O(\log n)$ | Logarithmic | $pprox 3$ | $pprox 7$ | $pprox 10$ | $pprox 20$ | $pprox 20 	ext{ ns}$ |
| $O(n)$ | Linear | 10 | 100 | 1,000 | $1,000,000$ | $pprox 1 	ext{ ms}$ |
| $O(n \log n)$ | Linearithmic | $pprox 33$ | $pprox 664$ | $pprox 9,965$ | $pprox 2 	imes 10^7$ | $pprox 20 	ext{ ms}$ |
| $O(n^2)$ | Quadratic | 100 | 10,000 | $1,000,000$ | $10^{12}$ | $pprox 16.6 	ext{ minutes}$ |
| $O(n^3)$ | Cubic | 1,000 | $1,000,000$ | $10^9$ | $10^{18}$ | $pprox 31.7 	ext{ years}$ |
| $O(2^n)$ | Exponential | 1,024 | $1.26 	imes 10^{30}$ | Incomputable | Incomputable | Heat death of universe |
| $O(n!)$ | Factorial | $3.6 	imes 10^6$ | $9.3 	imes 10^{157}$ | Incomputable | Incomputable | Incomputable |

---

### 1.3 Systematic Loop Analysis

#### Independent vs Dependent Nested Loops
```csharp
// Independent loops: Total work = n * m -> O(n * m)
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < m; j++)
        DoWork();
}

// Dependent Triangular loop:
// j runs: 0, 1, 2, ..., n-1
// Total iterations = (n * (n - 1)) / 2 = O(n^2)
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < i; j++)
        DoWork();
}

// Multiplicative loop:
// i doubles: 1, 2, 4, 8, ... 2^k < n -> k = log2(n) iterations -> O(log n)
for (int i = 1; i < n; i *= 2)
{
    DoWork();
}
```

#### The Two-Pointer Illusion (Nested Loop that is $O(n)$)
Do not classify an algorithm as $O(n^2)$ merely because there is a `while` loop inside a `for` loop!
```csharp
// O(n) total time!
int right = 0;
for (int left = 0; left < n; left++)
{
    while (right < n && Condition(left, right))
    {
        right++; // Notice: 'right' NEVER resets! It only moves forward across all iterations of 'left'.
    }
}
```
*Proof:* `left` increments at most $n$ times. `right` increments at most $n$ times. Total combined loop operations $\le 2n = O(n)$.

---

### 1.4 Master Theorem for Divide-and-Conquer Recurrences

For recurrences of the form:
$$T(n) = aT\left(rac{n}{b}ight) + f(n)$$
where $a \ge 1$ (number of subproblems), $b > 1$ (subproblem division factor), and $f(n) = \Theta(n^c)$:

Compare $c$ to $\log_b a$:
1. **Case 1:** If $c < \log_b a$, then $T(n) = \Theta(n^{\log_b a})$ (Tree leaves dominate).
2. **Case 2:** If $c = \log_b a$, then $T(n) = \Theta(n^c \log n) = \Theta(n^{\log_b a} \log n)$ (Work distributed evenly).
3. **Case 3:** If $c > \log_b a$, then $T(n) = \Theta(f(n))$ (Root node dominates).

*Application to Classic Algorithms:*
- **Binary Search:** $T(n) = 1T(n/2) + O(1) \implies a=1, b=2, c=0 \implies \log_2 1 = 0 = c \implies 	ext{Case 2: } \Theta(\log n)$.
- **Merge Sort:** $T(n) = 2T(n/2) + O(n) \implies a=2, b=2, c=1 \implies \log_2 2 = 1 = c \implies 	ext{Case 2: } \Theta(n \log n)$.

---

### 1.5 Amortized Analysis & Dynamic Array Resizing Proof

An operation has **Amortized Complexity $O(1)$** if any sequence of $k$ operations takes at most $O(k)$ total time, meaning the average cost per operation over the sequence is bounded by a constant, even if individual operations occasionally take $O(n)$ time.

#### Mathematical Proof: `List<T>.Add()` with Geometric Doubling
Suppose array capacity starts at 1 and doubles when full ($1, 2, 4, 8, \dots$).
When inserting $n$ elements:
- Cheap appends: Each of the $n$ items requires 1 write operation $\implies n$ writes.
- Expensive resizes: Occur at powers of 2 ($1, 2, 4, 8, \dots, 2^{\lfloor \log_2 n floor}$).
  The total elements copied during all resizes is:
  $$\sum_{i=0}^{\lfloor \log_2 n floor} 2^i = 2^{\lfloor \log_2 n floor + 1} - 1 < 2n$$
- Total operations for $n$ additions: $	ext{Total Work} = n 	ext{ (appends)} + 2n 	ext{ (copies)} = 3n 	ext{ operations}$.
- Average cost per operation: $rac{3n}{n} = 3 = O(1)$ constant amortized time.

*Why Additive Growth is Catastrophic:* If the array grew by adding 100 slots instead of doubling, resizing would occur $rac{n}{100}$ times. The total copy work would be an arithmetic progression summing to $O(n^2)$, yielding an amortized cost of $O(n)$ per insert!

---

### 1.6 Complexity vs Hardware Cache Reality

Two algorithms with identical $O(n)$ asymptotic complexity can exhibit vastly different runtimes due to CPU hardware architecture:
1. **Cache Lines (64 bytes):** When the CPU reads an address from RAM, it loads a contiguous 64-byte line into L1 cache.
   - Array traversal: Contiguous memory layout guarantees maximum spatial locality. The CPU cache-prefetcher anticipates sequential reads, achieving near-instant cache hits.
   - Linked List traversal: Node allocations are scattered arbitrarily across the managed heap. Every node jump triggers a **CPU Cache Miss**, forcing the core to stall for $pprox 200 	ext{ cycles}$ waiting for main memory!
2. **Result:** Iterating over an array of 1,000,000 integers can be **30x to 50x faster** than iterating over a `LinkedList<int>` of 1,000,000 nodes, despite both having $O(n)$ theoretical complexity.

---

### Section 1 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Explain the difference between worst-case complexity and amortized complexity using `List<T>.Add()` in .NET.**
> **Strong answer:** Worst-case complexity measures the maximum time an individual operation can ever take under the worst possible circumstances. For `List<T>.Add()`, the worst-case time is $O(n)$ because when the underlying array runs out of capacity, it must allocate a new array of double the size and copy all $n$ existing elements. Amortized complexity evaluates the average cost per operation across a long sequence of operations. Because doubling capacity ensures that an expensive $O(n)$ resize is preceded by at least $n/2$ cheap $O(1)$ appends, the total cost of resizing across $n$ appends is strictly bounded by $2n$. Thus, the total work for $n$ operations is $O(n)$, giving an amortized cost of $O(1)$ per append. However, in latency-sensitive paths, that single $O(n)$ spike can cause unacceptable tail latency.

#### Practical Exercises
1. **Exercise 1.1:** Derive the Big $\Theta$ time complexity for $T(n) = 4T(n/2) + n^2$ using the Master Theorem.
2. **Exercise 1.2:** Write a benchmark using BenchmarkDotNet comparing sequential traversal of `int[]` vs `LinkedList<int>` for $10^6$ items, and explain the CPU cache miss counter output.

---

## Section 2 — Core Data Structures & .NET Collection Internals

### 2.1 Arrays and `List<T>` Internals

`List<T>` is not a linked list; it is a dynamic array backed by a contiguous `T[] _items` buffer.
- `_size`: The current count of logical items.
- `_capacity`: The length of the internal `_items` array.
- **Index Access (`list[i]`):** $O(1)$ pointer arithmetic: `address = base_address + i * sizeof(T)`.
- **Insert / RemoveAt:** $O(n)$ because elements after the index must be shifted in memory using `Array.Copy()`.

### 2.2 Slicing Primitives: `Span<T>` and `ReadOnlySpan<T>`

`Span<T>` is a `ref struct` (stack-only type) representing a contiguous region of arbitrary memory (managed array, stack memory via `stackalloc`, or native unmanaged memory).
It consists of an interior pointer (`ref T _reference`) and an integer length (`int _length`).
It enables $O(1)$ zero-allocation slicing without copying buffers:
```csharp
byte[] buffer = new byte[1024];
ReadOnlySpan<byte> header = buffer.AsSpan(0, 32); // Zero heap allocations!
```

---

### 2.3 `Dictionary<TKey, TValue>` Internal Architecture

In .NET Core / modern .NET, `Dictionary<TKey, TValue>` uses a **hybrid chained bucket array with separate entry indexing**:

```text
_buckets: [ 1, -1,  0, -1,  2 ]  (int array of size prime P)
             |      |       |
             v      v       v
_entries: [ { Hash, Next= -1, Key= "K1", Value= V1 },
            { Hash, Next=  0, Key= "K2", Value= V2 },
            { Hash, Next= -1, Key= "K3", Value= V3 } ]
```

1. **Hashing:** `hashCode = comparer.GetHashCode(key) & 0x7FFFFFFF` (positive 31-bit integer).
2. **Bucket Mapping:** `bucketIndex = hashCode % _buckets.Length`.
3. **Collision Chaining:** Each bucket stores the index of the first entry in `_entries`. If a collision occurs, `Entry.next` points to the next entry index, creating an in-place linked list within the flat `_entries` array.
4. **Resizing:** When `_size == _entries.Length`, a new capacity (the next prime number roughly double the size) is allocated, and all entries are re-bucketed.

#### Expected vs Worst-Case Lookup:
- **Expected:** $O(1)$ assuming uniform hash code distribution and constant-time equality comparisons.
- **Worst-Case:** $O(n)$ if all keys collide into the same bucket (HashDoS attack) or `GetHashCode()` returns a constant value.

---

### 2.4 `PriorityQueue<TElement, TPriority>` (.NET 6+)

Modern .NET includes `PriorityQueue<TElement, TPriority>`, implemented as a **4-ary (d-ary with $d=4$) min-heap** stored in a flat array:
- Why 4-ary instead of binary? A 4-ary heap has shallower tree depth ($\log_4 n$ vs $\log_2 n$) and significantly better CPU cache line utilization when scanning children.
- `Enqueue(item, priority)`: $O(\log n)$.
- `Dequeue()`: $O(\log n)$ (extracts lowest priority value).
- `Peek()`: $O(1)$.

---

### 2.5 Ordered Collections: `SortedDictionary` vs `SortedList`

| Feature | `SortedDictionary<TKey, TValue>` | `SortedList<TKey, TValue>` |
|---|---|---|
| **Underlying Structure** | Red-Black Tree (Self-balancing BST) | Two flat sorted arrays (`keys[]` and `values[]`) |
| **Lookup** | $O(\log n)$ tree traversal | $O(\log n)$ via Binary Search (`Array.BinarySearch`) |
| **Insertion / Deletion** | $O(\log n)$ node creation & tree rotation | **$O(n)$** because elements must shift in memory |
| **Memory Footprint** | Higher: 32 bytes overhead per node (left, right, parent, color) | Minimal: Two contiguous primitive arrays |
| **Cache Locality** | Poor (nodes scattered on heap) | Exceptional (sequential array memory) |
| **Optimal Use Case** | Frequent insertions and deletions in random order | Build once, read frequently |

---

### Section 2 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Walk me through what happens internally inside a .NET `Dictionary<TKey, TValue>` when you call `dict.Add(key, value)`.**
> **Strong answer:** First, the dictionary checks if `key` is null (throwing `ArgumentNullException` if it is a reference type). It calls `comparer.GetHashCode(key)` and masks the sign bit to produce a positive 31-bit integer. It calculates the target bucket by taking the hash modulo the length of the `_buckets` array (which is always a prime number). It traverses the collision chain starting at `_buckets[bucketIndex]`, inspecting `_entries` to verify if the key already exists using `comparer.Equals()`; if found, it throws `ArgumentException` (or overwrites if using the indexer). If not found, it checks if resizing is required. If `_size == _entries.Length`, it allocates a new prime capacity, re-hashes all existing entries into new buckets, and inserts the new entry at `_entries[_size]`. It links the entry to the previous bucket head and updates `_buckets[bucketIndex]` to point to the newly added entry index.

#### Practical Exercises
1. **Exercise 2.1:** Implement a custom `LinearProbingHashMap<TKey, TValue>` in C# that resolves collisions via open addressing linear probing rather than chaining, and include tombstone deletion.
2. **Exercise 2.2:** Benchmark `Dictionary<string, int>` vs `FrozenDictionary<string, int>` on a set of 500 fixed route strings, and explain why `FrozenDictionary` achieves faster lookups.

---

## Section 3 — Arrays, Strings & High-Value Array Patterns

### 3.1 Two-Pointer Technique (Opposing & Same-Direction)

#### Pattern 1: Opposing Pointers — Two Sum in Sorted Array
```csharp
public static bool HasPairWithSum(ReadOnlySpan<int> sortedNumbers, int target)
{
    int left = 0;
    int right = sortedNumbers.Length - 1;

    while (left < right)
    {
        int sum = sortedNumbers[left] + sortedNumbers[right];
        if (sum == target) return true;
        if (sum < target) left++;
        else right--;
    }

    return false;
}
```

#### Pattern 2: Same-Direction / Fast-Slow Pointer — In-Place Duplicate Removal
```csharp
public static int RemoveDuplicates(Span<int> nums)
{
    if (nums.Length == 0) return 0;
    int slow = 0;

    for (int fast = 1; fast < nums.Length; fast++)
    {
        if (nums[fast] != nums[slow])
        {
            slow++;
            nums[slow] = nums[fast];
        }
    }

    return slow + 1;
}
```

---

### 3.2 Sliding Window Technique

#### Variable-Length Window: Longest Substring Without Repeating Characters ($O(n)$ Time, $O(k)$ Space)
```csharp
public static int LengthOfLongestSubstring(string s)
{
    ReadOnlySpan<char> span = s.AsSpan();
    Span<int> lastIndex = stackalloc int[256];
    lastIndex.Fill(-1);

    int maxLength = 0;
    int windowStart = 0;

    for (int windowEnd = 0; windowEnd < span.Length; windowEnd++)
    {
        char c = span[windowEnd];
        if (c < 256 && lastIndex[c] >= windowStart)
        {
            windowStart = lastIndex[c] + 1;
        }

        if (c < 256) lastIndex[c] = windowEnd;
        maxLength = Math.Max(maxLength, windowEnd - windowStart + 1);
    }

    return maxLength;
}
```

---

### 3.3 Prefix Sums & Difference Arrays

#### Prefix Sum for $O(1)$ Range Queries
Given an array $A$, the prefix sum array $P$ is defined as $P[i] = \sum_{k=0}^{i-1} A[k]$.
The sum of any range $[L, R]$ is computed in $O(1)$ time as:
$$	ext{Sum}(L, R) = P[R + 1] - P[L]$$

#### Difference Array for $O(1)$ Range Updates
To apply multiple range additions $+V$ to ranges $[L, R]$ across an array of size $n$:
1. Initialize difference array $D$ of size $n + 1$ with zeros.
2. For each query $(L, R, V)$:
   $$D[L] \mathrel{+}= V, \quad D[R + 1] \mathrel{-}= V$$
3. Reconstruct the final array by computing the running prefix sum of $D$ in a single $O(n)$ pass!

---

### Section 3 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How do you solve the 'Subarray Sum Equals K' problem in $O(n)$ time when numbers can be negative?**
> **Strong answer:** If numbers can be negative, a sliding window fails because the window sum is non-monotonic (expanding the window can decrease the sum). Instead, we use a Prefix Sum combined with a Hash Map. We maintain a running prefix sum and a hash map tracking how many times each prefix sum has occurred. At each index $i$ with running sum $S$, we check if $(S - K)$ exists in the map. If it does, any previous prefix sum equal to $(S - K)$ implies that the subarray between that prior index and $i$ sums exactly to $K$. We add the frequency of $(S - K)$ to our total count, and record the current sum $S$ in the map. This runs in $O(n)$ time and $O(n)$ auxiliary space.

#### Practical Exercises
1. **Exercise 3.1:** Implement `MergeIntervals(List<Interval> intervals)` in $O(n \log n)$ time and prove that sorting by start time guarantees all potential overlaps are adjacent.

---

## Section 4 — Linked Lists, Stacks, Queues & Deques

### 4.1 Floyd's Tortoise and Hare (Cycle Detection & Start Node Proof)

To detect a cycle in a linked list using $O(1)$ auxiliary memory:
1. Initialize two pointers: `slow` (moves 1 step) and `fast` (moves 2 steps).
2. If `fast` reaches null, there is no cycle.
3. If `slow == fast`, a cycle exists.

#### Proof of Finding Cycle Start:
Let $L$ be the distance from head to cycle entrance. Let $C$ be the cycle length. Let $X$ be the distance from cycle entrance to meeting point.
- Distance traveled by slow: $d_s = L + X$
- Distance traveled by fast: $d_f = L + X + k \cdot C$ (where $k \ge 1$)
- Because fast travels twice as fast: $2(L + X) = L + X + k \cdot C \implies L + X = k \cdot C \implies L = k \cdot C - X$.

*Algorithm to find entrance:* Move `slow` back to the head. Keep `fast` at the meeting point. Move both 1 step at a time. After $L$ steps, `slow` travels $L$ and `fast` travels $k \cdot C - X$. Both will meet exactly at the cycle entrance!

---

### 4.2 LRU Cache (Least Recently Used) Reference Implementation

An LRU Cache requires $O(1)$ `Get` and $O(1)$ `Put`.
We achieve this by combining:
1. `Dictionary<K, LinkedListNode<CacheItem>>`: Provides $O(1)$ key lookup to the exact linked list node.
2. Doubly Linked List: Allows $O(1)$ removal and insertion of nodes at the head (Most Recently Used) and eviction from the tail (Least Recently Used).

```csharp
public sealed class LruCache<TKey, TValue> where TKey : notnull
{
    private readonly int _capacity;
    private readonly Dictionary<TKey, LinkedListNode<CacheEntry>> _map;
    private readonly LinkedList<CacheEntry> _list;

    private readonly record struct CacheEntry(TKey Key, TValue Value);

    public LruCache(int capacity)
    {
        if (capacity <= 0) throw new ArgumentOutOfRangeException(nameof(capacity));
        _capacity = capacity;
        _map = new Dictionary<TKey, LinkedListNode<CacheEntry>>(capacity);
        _list = new LinkedList<CacheEntry>();
    }

    public bool TryGet(TKey key, out TValue value)
    {
        if (_map.TryGetValue(key, out var node))
        {
            _list.Remove(node);
            _list.AddFirst(node); // Move to head (Most Recently Used)
            value = node.Value.Value;
            return true;
        }

        value = default!;
        return false;
    }

    public void Put(TKey key, TValue value)
    {
        if (_map.TryGetValue(key, out var existingNode))
        {
            _list.Remove(existingNode);
        }
        else if (_map.Count >= _capacity)
        {
            var lru = _list.Last!;
            _list.RemoveLast(); // Evict Least Recently Used from tail
            _map.Remove(lru.Value.Key);
        }

        var newNode = _list.AddFirst(new CacheEntry(key, value));
        _map[key] = newNode;
    }
}
```

---

### 4.3 Monotonic Stack: Largest Rectangle in Histogram ($O(n)$ Time)

A Monotonic Stack maintains elements in monotonically increasing or decreasing order.
When an incoming element violates the monotonicity, elements are popped and processed.

```csharp
public static int LargestRectangleArea(ReadOnlySpan<int> heights)
{
    Stack<int> stack = new(); // Stores indices of increasing heights
    int maxArea = 0;
    int n = heights.Length;

    for (int i = 0; i <= n; i++)
    {
        int currentHeight = (i == n) ? 0 : heights[i];

        while (stack.Count > 0 && currentHeight < heights[stack.Peek()])
        {
            int h = heights[stack.Pop()];
            int width = (stack.Count == 0) ? i : i - stack.Peek() - 1;
            maxArea = Math.Max(maxArea, h * width);
        }

        stack.Push(i);
    }

    return maxArea;
}
```

---

### Section 4 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why is an array-backed stack or queue generally preferred over a linked-list-backed stack or queue in production C#?**
> **Strong answer:** A linked list node incurs heavy memory and GC overhead: in a 64-bit CLR, each `LinkedListNode<T>` requires 24 bytes of node reference overhead (Next, Previous, List pointers) plus 16 bytes of Object Header and MethodTable pointer, totaling 40 bytes of heap overhead per element. Furthermore, node allocations are scattered across heap segments, causing severe CPU cache misses during traversal and adding GC pressure during deallocation. Conversely, an array-backed stack or queue (`Stack<T>`, `Queue<T>`) stores items in a contiguous array buffer, ensuring zero per-item heap allocation, maximum CPU cache line locality, and amortized $O(1)$ performance.

#### Practical Exercises
1. **Exercise 4.1:** Implement a `MinStack` supporting `Push`, `Pop`, `Top`, and `GetMin` all in $O(1)$ time and $O(1)$ auxiliary space overhead per element.
2. **Exercise 4.2:** Solve the 'Sliding Window Maximum' problem using a monotonic double-ended queue (`LinkedList<int>`) in $O(n)$ time.

## Section 5 — Hashing, Maps, Sets & Probabilistic Structures

### 5.1 Hashing Mechanics & Mutable Key Disaster

A hash table maps keys to array bucket indices.
**Critical Invariant:** If `key1.Equals(key2)`, then `key1.GetHashCode()` **must equal** `key2.GetHashCode()`.

#### The Mutable Key Hazard
If an object is used as a key in a `Dictionary<TKey, TValue>` or `HashSet<T>` and a field contributing to its `GetHashCode()` is mutated:
```csharp
var person = new MutablePerson { Name = "Alice", Id = 101 };
var map = new Dictionary<MutablePerson, string>();
map[person] = "Engineer";

person.Name = "Bob"; // MUTATION! HashCode changes!

// DISASTER: map.ContainsKey(person) now returns FALSE!
// The entry is trapped in the bucket calculated from "Alice", but searched in the bucket for "Bob"!
```
*Rule:* Dictionary keys must be strictly immutable (`record` or `readonly struct`).

---

### 5.2 Probabilistic Data Structures: Bloom Filter

A Bloom Filter is a space-efficient probabilistic data structure used to test set membership:
- Returns **"Possibly in set"** (False positives possible).
- Returns **"Definitely not in set"** (Zero false negatives!).

#### Mathematical Foundations
Given a bit array of size $m$, $n$ inserted elements, and $k$ independent hash functions:
- Optimal number of hash functions: $k = rac{m}{n} \ln 2 pprox 0.693 rac{m}{n}$
- False positive probability: $p pprox \left(1 - e^{-kn/m}ight)^k$

#### C# Production Implementation
```csharp
public sealed class BloomFilter<T>
{
    private readonly BitArray _bits;
    private readonly int _hashCount;
    private readonly Func<T, (uint, uint)> _hashFunction;

    public BloomFilter(int expectedElements, double falsePositiveRate, Func<T, (uint, uint)> hashFunction)
    {
        _hashFunction = hashFunction;
        // Optimal m = - (n * ln(p)) / (ln(2)^2)
        int m = (int)Math.Ceiling(-expectedElements * Math.Log(falsePositiveRate) / Math.Pow(Math.Log(2), 2));
        // Optimal k = (m / n) * ln(2)
        _hashCount = (int)Math.Round((double)m / expectedElements * Math.Log(2));
        _bits = new BitArray(m);
    }

    public void Add(T item)
    {
        var (h1, h2) = _hashFunction(item);
        for (int i = 0; i < _hashCount; i++)
        {
            // Kirsch-Mitzenmacher optimization: g_i(x) = h1(x) + i * h2(x)
            int combinedHash = (int)((h1 + (uint)i * h2) % (uint)_bits.Length);
            _bits[Math.Abs(combinedHash)] = true;
        }
    }

    public bool MightContain(T item)
    {
        var (h1, h2) = _hashFunction(item);
        for (int i = 0; i < _hashCount; i++)
        {
            int combinedHash = (int)((h1 + (uint)i * h2) % (uint)_bits.Length);
            if (!_bits[Math.Abs(combinedHash)]) return false; // Definitely not in set!
        }
        return true; // Possibly in set!
    }
}
```

---

### Section 5 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How would you protect a high-throughput microservice from database cache-penetration attacks using a Bloom Filter?**
> **Strong answer:** A cache-penetration attack occurs when malicious clients repeatedly query non-existent keys (e.g., random UUIDs). Because the keys don't exist in the cache, every request bypasses the cache and hits the database, exhausting connection pools. We place an in-memory Bloom Filter in front of the cache containing all valid primary keys. When a request arrives, the Bloom filter is checked. If it returns false ("definitely not in set"), we immediately return a 404 without hitting Redis or the database. Only if the Bloom filter returns true do we proceed to the cache and database.

---

## Section 6 — Trees, Heaps, Tries & Skip Lists

### 6.1 Trie (Prefix Tree) Implementation in C#

A Trie is a tree structure used for fast string prefix searching in $O(L)$ time (where $L$ is string length), independent of the number of words stored $N$.

```csharp
public sealed class Trie
{
    private sealed class TrieNode
    {
        public Dictionary<char, TrieNode> Children { get; } = [];
        public bool IsEndOfWord { get; set; }
    }

    private readonly TrieNode _root = new();

    public void Insert(string word)
    {
        var current = _root;
        foreach (char c in word)
        {
            if (!current.Children.TryGetValue(c, out var next))
            {
                next = new TrieNode();
                current.Children[c] = next;
            }
            current = next;
        }
        current.IsEndOfWord = true;
    }

    public bool Search(string word)
    {
        var node = FindPrefixNode(word);
        return node is not null && node.IsEndOfWord;
    }

    public bool StartsWith(string prefix) => FindPrefixNode(prefix) is not null;

    private TrieNode? FindPrefixNode(string prefix)
    {
        var current = _root;
        foreach (char c in prefix)
        {
            if (!current.Children.TryGetValue(c, out current))
                return null;
        }
        return current;
    }
}
```

---

### 6.2 Binary Search Trees & Self-Balancing Invariants

- **Binary Search Tree Property:** For every node $X$, all keys in the left subtree are $< X.Key$, and all keys in the right subtree are $> X.Key$.
- **BST Deletion:**
  - Case 1 (Leaf): Remove node directly.
  - Case 2 (One Child): Replace node with its single child.
  - Case 3 (Two Children): Find the **In-order Successor** (smallest key in the right subtree), overwrite the target node's value with it, and recursively delete the successor from the right subtree.
- **Why Red-Black Trees in .NET?** AVL trees enforce stricter height balancing ($\le 1$ difference), making them faster for lookups but more expensive on inserts/deletions due to frequent rotations. Red-Black trees tolerate slightly looser height bounds (path to deepest leaf is at most twice the shortest), yielding faster insertion and deletion performance while maintaining $O(\log n)$ bounds.

---

### Section 6 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How does an array-backed Binary Heap maintain the complete binary tree invariant during insertion and deletion?**
> **Strong answer:** A binary heap stores nodes in a flat array where parent-child relationships are calculated via index arithmetic: for zero-indexed array index $i$, Left Child is $2i + 1$, Right Child is $2i + 2$, and Parent is $\lfloor(i - 1) / 2floor$. When inserting an item, it is placed at the end of the array (maintaining the structural shape of a complete binary tree) and `HeapifyUp` (sift-up) is performed by repeatedly swapping with its parent until the heap order property is restored ($O(\log n)$). When extracting the min/max root, the root element is replaced with the last element of the array, the array length is decremented by 1, and `HeapifyDown` (sift-down) is performed by swapping with the smaller/larger child until the heap invariant is restored ($O(\log n)$).

---

## Section 7 — Graphs, Traversals & Shortest Paths

### 7.1 Topological Sort with Kahn's Algorithm & Cycle Detection

Topological sorting produces a linear ordering of vertices in a Directed Acyclic Graph (DAG) such that for every directed edge $U 	o V$, $U$ comes before $V$.

```csharp
public static List<int>? GetTopologicalOrder(int numNodes, List<(int From, int To)> edges)
{
    int[] inDegree = new int[numNodes];
    List<int>[] adj = new List<int>[numNodes];
    for (int i = 0; i < numNodes; i++) adj[i] = [];

    foreach (var (from, to) in edges)
    {
        adj[from].Add(to);
        inDegree[to]++;
    }

    Queue<int> zeroInDegreeQueue = new();
    for (int i = 0; i < numNodes; i++)
    {
        if (inDegree[i] == 0)
            zeroInDegreeQueue.Enqueue(i);
    }

    List<int> order = [];
    while (zeroInDegreeQueue.Count > 0)
    {
        int u = zeroInDegreeQueue.Dequeue();
        order.Add(u);

        foreach (int v in adj[u])
        {
            inDegree[v]--;
            if (inDegree[v] == 0)
                zeroInDegreeQueue.Enqueue(v);
        }
    }

    // If order contains fewer than numNodes, a cycle exists!
    return order.Count == numNodes ? order : null;
}
```

---

### 7.2 Dijkstra's Shortest Path Algorithm

Computes single-source shortest paths on graphs with **non-negative edge weights** in $O((V + E) \log V)$ time using `PriorityQueue<TElement, TPriority>`:

```csharp
public static int[] DijkstraShortestPath(int numNodes, List<(int To, int Weight)>[] adj, int startNode)
{
    int[] dist = new int[numNodes];
    Array.Fill(dist, int.MaxValue);
    dist[startNode] = 0;

    var pq = new PriorityQueue<int, int>();
    pq.Enqueue(startNode, 0);

    while (pq.Count > 0)
    {
        pq.TryDequeue(out int u, out int currentDist);

        if (currentDist > dist[u]) continue; // Stale heap entry; skip

        foreach (var (v, weight) in adj[u])
        {
            if (dist[u] + weight < dist[v])
            {
                dist[v] = dist[u] + weight;
                pq.Enqueue(v, dist[v]);
            }
        }
    }

    return dist;
}
```

---

### 7.3 Disjoint Set Union (DSU / Union-Find) with Path Compression and Rank

```csharp
public sealed class DisjointSetUnion
{
    private readonly int[] _parent;
    private readonly int[] _rank;

    public DisjointSetUnion(int size)
    {
        _parent = new int[size];
        _rank = new int[size];
        for (int i = 0; i < size; i++) _parent[i] = i;
    }

    public int Find(int i)
    {
        // Path Compression
        if (_parent[i] != i)
            _parent[i] = Find(_parent[i]);
        return _parent[i];
    }

    public bool Union(int i, int j)
    {
        int rootI = Find(i);
        int rootJ = Find(j);

        if (rootI == rootJ) return false; // Already in same set (Cycle detected!)

        // Union by Rank
        if (_rank[rootI] < _rank[rootJ]) _parent[rootI] = rootJ;
        else if (_rank[rootI] > _rank[rootJ]) _parent[rootJ] = rootI;
        else
        {
            _parent[rootJ] = rootI;
            _rank[rootI]++;
        }

        return true;
    }
}
```

---

### Section 7 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why does Dijkstra's algorithm fail on graphs with negative edge weights, and what algorithm should be used instead?**
> **Strong answer:** Dijkstra's algorithm operates on a greedy invariant: once a vertex is dequeued from the priority queue, its computed shortest distance is declared finalized and never revisited. If negative edges exist, a path through an unexplored negative edge could reduce the cost to an already-finalized vertex, invalidating the greedy assumption and producing incorrect results. If negative edge cycles exist, path costs can decrease indefinitely. For graphs with negative edge weights, the Bellman-Ford algorithm should be used instead ($O(V \cdot E)$ time). Bellman-Ford relaxes all edges $V-1$ times and can detect negative weight cycles on the $V$-th iteration.

---

## Section 8 — Searching & Binary Search on Answer Space

### 8.1 The Standard Binary Search Template (Lower Bound)

Avoid the classic midpoint integer overflow `(low + high) / 2` by writing `low + (high - low) / 2`:

```csharp
public static int LowerBound(ReadOnlySpan<int> array, int target)
{
    int low = 0;
    int high = array.Length; // Exclusive upper bound

    while (low < high)
    {
        int mid = low + (high - low) / 2;
        if (array[mid] >= target)
            high = mid; // Search left half
        else
            low = mid + 1; // Search right half
    }

    return low; // First index where array[index] >= target
}
```

---

### 8.2 Binary Search on Answer Space (Monotonic Predicates)

When asked to find the **minimum capacity**, **minimum speed**, or **maximum threshold** to satisfy a condition, look for a **Monotonic Feasibility Predicate**:
$$	ext{IsFeasible}(	ext{value}) \implies [False, False, False, True, True, True]$$

#### Classic Example: Capacity to Ship Packages Within D Days ($O(n \log(\sum 	ext{weights}))$)
```csharp
public static int ShipWithinDays(int[] weights, int days)
{
    int low = weights.Max(); // Cannot have capacity smaller than heaviest item
    int high = weights.Sum(); // Maximum possible capacity is shipping everything in 1 day

    while (low < high)
    {
        int mid = low + (high - low) / 2;
        if (CanShipInDays(weights, days, mid))
            high = mid;
        else
            low = mid + 1;
    }

    return low;
}

private static bool CanShipInDays(int[] weights, int maxDays, int capacity)
{
    int daysNeeded = 1;
    int currentLoad = 0;

    foreach (int w in weights)
    {
        if (currentLoad + w > capacity)
        {
            daysNeeded++;
            currentLoad = 0;
        }
        currentLoad += w;
    }

    return daysNeeded <= maxDays;
}
```

---

## Section 9 — Sorting, Selection & Top-K Patterns

### 9.1 Quickselect: $O(n)$ Average-Time Kth Selection

Instead of sorting the entire array in $O(n \log n)$ to find the Kth smallest element, Quickselect partitions the array in-place, recursing into only the half containing index $K$:

```csharp
public static int QuickSelect(Span<int> nums, int k)
{
    int left = 0, right = nums.Length - 1;
    Random rand = new();

    while (left <= right)
    {
        int pivotIndex = left + rand.Next(right - left + 1);
        int finalPivotIndex = Partition(nums, left, right, pivotIndex);

        if (finalPivotIndex == k) return nums[finalPivotIndex];
        if (finalPivotIndex < k) left = finalPivotIndex + 1;
        else right = finalPivotIndex - 1;
    }

    return nums[k];
}

private static int Partition(Span<int> nums, int left, int right, int pivotIndex)
{
    int pivotValue = nums[pivotIndex];
    (nums[pivotIndex], nums[right]) = (nums[right], nums[pivotIndex]);
    int storeIndex = left;

    for (int i = left; i < right; i++)
    {
        if (nums[i] < pivotValue)
        {
            (nums[storeIndex], nums[i]) = (nums[i], nums[storeIndex]);
            storeIndex++;
        }
    }

    (nums[storeIndex], nums[right]) = (nums[right], nums[storeIndex]);
    return storeIndex;
}
```

---

### Section 9 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How does .NET's `Array.Sort<T>` work internally, and why is it not pure QuickSort?**
> **Strong answer:** .NET uses **IntroSort** (Introspective Sort), a hybrid sorting algorithm combining QuickSort, HeapSort, and InsertionSort. It begins with QuickSort using median-of-three pivot selection. However, if the recursion depth exceeds $2 \lfloor\log_2 nfloor$ (indicating degenerate unbalanced partitions toward $O(n^2)$), it automatically switches to HeapSort to guarantee an absolute $O(n \log n)$ worst-case time bound. When partitioned subarrays become small ($\le 16$ elements), it switches to InsertionSort, which outperforms QuickSort on small arrays due to minimal overhead and exceptional CPU cache locality.

#### Practical Exercises
1. **Exercise 9.1:** Implement Top-K Frequent Words using a Min-Heap of size K in $O(n \log K)$ time and explain why streaming inputs favor heaps over Quickselect.

## Section 10 — Algorithmic Problem-Solving Paradigms (DP, Greedy, Backtracking)

### 10.1 Backtracking Template (Permutations / Subsets)

Backtracking explores a state-space tree by making a choice, exploring recursively, and **undoing the choice** (state restoration):

```csharp
public static List<List<int>> GenerateSubsets(int[] nums)
{
    List<List<int>> result = [];
    List<int> currentPath = [];
    Backtrack(0, nums, currentPath, result);
    return result;
}

private static void Backtrack(int startIndex, int[] nums, List<int> currentPath, List<List<int>> result)
{
    result.Add([.. currentPath]); // Record state

    for (int i = startIndex; i < nums.Length; i++)
    {
        currentPath.Add(nums[i]); // Choose
        Backtrack(i + 1, nums, currentPath, result); // Explore
        currentPath.RemoveAt(currentPath.Count - 1); // Unchoose (Backtrack)
    }
}
```

---

### 10.2 Dynamic Programming Archetypes

#### Archetype 1: 0/1 Knapsack (Bounded Resource Optimization)
Given item weights and values, find maximum value fitting capacity $W$:
- State: $dp[w]$ represents maximum value achievable with capacity $w$.
- Transition: Iterate backwards through capacities to reuse previous row values in $O(W)$ auxiliary space:
  $$dp[w] = \max(dp[w], dp[w - 	ext{weight}[i]] + 	ext{value}[i])$$

```csharp
public static int Knapsack(int capacity, int[] weights, int[] values)
{
    int[] dp = new int[capacity + 1];

    for (int i = 0; i < weights.Length; i++)
    {
        for (int w = capacity; w >= weights[i]; w--) // Reverse traversal preserves 0/1 invariant!
        {
            dp[w] = Math.Max(dp[w], dp[w - weights[i]] + values[i]);
        }
    }

    return dp[capacity];
}
```

#### Archetype 2: Longest Increasing Subsequence (LIS) in $O(n \log n)$ Time
Instead of standard $O(n^2)$ DP, maintain a `tails` array where `tails[i]` stores the smallest tail of all increasing subsequences of length $i + 1$. Binary search finds insertion points via patience sorting!

```csharp
public static int LengthOfLIS(ReadOnlySpan<int> nums)
{
    List<int> tails = [];

    foreach (int x in nums)
    {
        int idx = tails.BinarySearch(x);
        if (idx < 0) idx = ~idx; // Bitwise complement returns binary search insertion index

        if (idx == tails.Count) tails.Add(x);
        else tails[idx] = x;
    }

    return tails.Count;
}
```

---

## Section 11 — C#/.NET Algorithmic Fluency & Performance Pitfalls

### 11.1 LINQ Pitfalls: Multiple Enumeration & Hidden $O(n^2)$ Scans

```csharp
// DISASTER 1: Multiple Enumeration of deferred query
IEnumerable<Customer> query = customers.Where(c => ExpensiveValidation(c));
int count = query.Count(); // Evaluates validation across all customers
Customer? first = query.FirstOrDefault(); // Re-evaluates entire query from the start!

// DISASTER 2: Hidden O(n * m) scan
List<int> existingIds = GetExistingIds(); // 100,000 items
foreach (var item in incomingItems) // 100,000 items
{
    if (existingIds.Contains(item.Id)) // List<T>.Contains is O(m) linear scan! Total time: O(n * m) = 10 Billion operations!
    { ... }
}
// FIX: Convert existingIds to HashSet<int> -> O(n + m) time!
```

---

### 11.2 `ArrayPool<T>.Shared` for Zero-Allocation Algorithms

```csharp
public static void ProcessData(ReadOnlySpan<byte> input)
{
    byte[] rented = ArrayPool<byte>.Shared.Rent(input.Length);
    try
    {
        input.CopyTo(rented);
        PerformWork(rented.AsSpan(0, input.Length));
    }
    finally
    {
        ArrayPool<byte>.Shared.Return(rented, clearArray: false); // Return buffer to pool!
    }
}
```

---

## Section 12 — Senior-Level Coding Interview Methodology

### The 7-Step Whiteboard Protocol:
1. **Clarify (3 mins):** Ask about constraints: negative numbers, duplicates, input size $n$, empty inputs, memory limits.
2. **Explore Constraints (2 mins):** Translate $n$ into target complexity ($n \le 10^5 \implies O(n \log n)$ or $O(n)$; $n \le 20 \implies O(2^n)$ backtracking).
3. **Propose Baseline (3 mins):** State the brute-force solution and its complexity immediately. Establish a benchmark.
4. **Identify Bottleneck (3 mins):** Explain *why* the baseline is slow (e.g., "We are repeatedly scanning an unsorted array in $O(n)$").
5. **Optimize & State Invariants (4 mins):** Propose the data structure that eliminates the bottleneck (e.g., "A hash map gives expected $O(1)$ lookups").
6. **Code with Clean Idioms (15 mins):** Write clean, modular C# with guard clauses, meaningful names, and invariant comments.
7. **Validate Edge Cases (5 mins):** Manually trace: $n=0$, $n=1$, duplicates, all identical values, boundary integer extremes.

---

## Section 13 — Data Structures & Algorithms in Enterprise Systems

### 13.1 High-Volume Rate Limiting: Sliding Window Log vs Counter

In API Gateways, rate limiting prevents resource exhaustion:
- **Token Bucket:** Allows burstiness; refills tokens at constant rate.
- **Sliding Window Counter:** Divides time into small discrete sub-windows (e.g., 1-second chunks within a 1-minute window), interpolating request rates across window boundaries. Consumes minimal memory compared to storing raw timestamps while preventing burst exploits at window boundaries.

---

## Section 14 — Integrated Assessment & Capstone

### 14.1 Capstone 1: Directed Acyclic Graph (DAG) Task Orchestrator

```csharp
public sealed class DagTaskScheduler
{
    public sealed record TaskNode(string Id, Func<CancellationToken, Task> Action, IReadOnlyList<string> DependsOn);

    public async Task ExecuteAsync(IEnumerable<TaskNode> tasks, CancellationToken ct)
    {
        var taskList = tasks.ToList();
        var taskMap = taskList.ToDictionary(t => t.Id);

        // Compute in-degrees and adjacency
        var inDegree = taskList.ToDictionary(t => t.Id, t => t.DependsOn.Count);
        var dependents = taskList.ToDictionary(t => t.Id, _ => new List<string>());

        foreach (var task in taskList)
        {
            foreach (var dep in task.DependsOn)
            {
                if (!dependents.TryGetValue(dep, out var list))
                    throw new InvalidOperationException($"Missing dependency: {dep}");
                list.Add(task.Id);
            }
        }

        var completedTasks = new ConcurrentDictionary<string, byte>();
        var readyQueue = new ConcurrentQueue<TaskNode>(taskList.Where(t => inDegree[t.Id] == 0));

        if (readyQueue.IsEmpty && taskList.Count > 0)
            throw new InvalidOperationException("Circular dependency detected in task graph!");

        while (completedTasks.Count < taskList.Count)
        {
            List<Task> batch = [];
            while (readyQueue.TryDequeue(out var node))
            {
                batch.Add(Task.Run(async () =>
                {
                    await node.Action(ct);
                    completedTasks.TryAdd(node.Id, 0);

                    foreach (var depId in dependents[node.Id])
                    {
                        if (Interlocked.Decrement(ref inDegree[depId]) == 0)
                        {
                            readyQueue.Enqueue(taskMap[depId]);
                        }
                    }
                }, ct));
            }

            if (batch.Count == 0 && completedTasks.Count < taskList.Count)
                throw new InvalidOperationException("Deadlock or circular dependency detected during execution.");

            await Task.WhenAll(batch);
        }
    }
}
```

---

# Part III — Interview Readiness

## 1. Pattern Recognition Matrix

| Problem Clue / Signal | Recommended Pattern | Primary Data Structure | Target Complexity |
|---|---|---|---|
| Find pair summing to target in sorted array | Opposing Two Pointers | Flat Array | $O(n)$ time, $O(1)$ space |
| Contiguous subarray meeting condition (e.g. min/max sum, distinct chars) | Sliding Window | Array / Hash Map | $O(n)$ time, $O(k)$ space |
| Range sum queries with no array updates | Prefix Sums | 1D / 2D Array | $O(1)$ query, $O(n)$ precomputation |
| Range addition updates ($+V$ to $[L, R]$) with final values requested | Difference Array | Array | $O(1)$ update, $O(n)$ reconstruction |
| Next greater / smaller element; largest rectangle | Monotonic Stack | Array-backed Stack | $O(n)$ time, $O(n)$ space |
| Sliding window maximum / minimum | Monotonic Deque | Double-Ended Queue | $O(n)$ time, $O(k)$ space |
| Top-K largest/smallest elements in high-volume or streaming data | Min-Heap / Max-Heap | `PriorityQueue<TElement, TPriority>` | $O(n \log K)$ time, $O(K)$ space |
| Find Kth element in unsorted array in-place | Quickselect | In-Place Partitioning | Expected $O(n)$ time, $O(1)$ space |
| Task dependencies, build ordering, prerequisite chains | Topological Sort | Kahn's Queue / Indegree Array | $O(V + E)$ time, $O(V + E)$ space |
| Shortest path on graph with non-negative edge weights | Dijkstra's Algorithm | `PriorityQueue<T, TWeight>` | $O((V + E) \log V)$ time |
| Connected components, dynamic network connectivity, cycle detection | Disjoint Set Union (DSU) | Flat Parent & Rank Arrays | Near $O(1)$ per operation ($lpha(n)$) |
| Find minimum capacity, speed, or threshold satisfying feasibility | Binary Search on Answer | Monotonic Feasibility Function | $O(n \log(	ext{range}))$ time |
| String prefix matching, autocomplete, spell-checking | Trie (Prefix Tree) | Multi-way Node Tree | $O(L)$ search/insert where $L$ is word length |
| Detect membership in massive datasets with bounded memory | Bloom Filter | BitArray + Multiple Hashes | $O(k)$ time, minimal memory |
| Optimize choices with overlapping subproblems and optimal substructure | Dynamic Programming | 1D / 2D Tabulation Array | $O(n \cdot m)$ time and space |

---

## 2. Mid-Level vs Senior-Level Coding Interview Comparison

| Dimension | Mid-Level Candidate | Senior / Staff-Level Candidate |
|---|---|---|
| **Problem Initiation** | Starts writing code immediately; assumes input fits in memory; misses negative numbers. | Clarifies constraints up front (input size $n$, duplicates, memory limits); states brute-force baseline and target complexity. |
| **Complexity Analysis** | Recites memorized Big O tags; claims `List<T>.Add()` is always $O(1)$; confuses worst-case with amortized. | Analyzes loop bounds rigorously; proves amortized $O(1)$ using aggregate geometric series; distinguishes time from auxiliary space. |
| **Data Structure Selection** | Uses `List<T>` for everything, performing nested `.Contains()` lookups; unaware of boxing in non-generic collections. | Selects data structures based on access patterns; explains memory locality, hash collisions, and cache misses. |
| **Edge Cases & Invariants** | Writes code until test passes; adds defensive `if (x != null)` randomly. | Establishes loop invariants and boundary conditions before coding; tests $n=0, 1$, duplicates, and overflow systematically. |
| **Communication** | Works silently or rambles; becomes defensive when given hints. | Narrates architectural trade-offs aloud; treats hints as collaborative signals; explains alternatives and failure modes. |

---

## 3. Rapid-Fire Revision Sheet (50 Senior-Level Truths)

1. Big O describes an asymptotic upper bound; it can be applied to best-case, average-case, or worst-case functions.
2. An algorithm requiring $3n^2 + 50n$ steps is $\Theta(n^2)$; constants and lower-order terms drop asymptotically.
3. `List<T>.Add()` has amortized $O(1)$ complexity, but its worst-case single-operation cost is $O(n)$ due to array resizing.
4. Additive array growth (e.g., adding 100 slots) degrades append performance to amortized $O(n)$ and total time to $O(n^2)$.
5. Accessing `array[i]` takes $O(1)$ time via direct pointer arithmetic: `base + i * sizeof(T)`.
6. Iterating through contiguous arrays is up to 50x faster than linked lists due to CPU 64-byte cache line prefetching.
7. A nested loop is not automatically $O(n^2)$; if the inner pointer monotonically advances without resetting, total time is $O(n)$.
8. `Dictionary<TKey, TValue>` uses an array of buckets and an array of entries with collision chaining via entry indices.
9. Dictionary lookup is expected $O(1)$, but can degrade to $O(n)$ under adversarial hash collisions (HashDoS).
10. Mutating an object's properties while it is stored as a dictionary key corrupts lookup capability permanently.
11. `FrozenDictionary<TKey, TValue>` (.NET 8) optimizes read-only lookups using perfect hashing and direct lookup tables.
12. `PriorityQueue<TElement, TPriority>` in .NET uses a 4-ary (d-ary) array-backed min-heap for superior cache locality.
13. `SortedDictionary` uses a Red-Black tree ($O(\log n)$ insert/search); `SortedList` uses sorted arrays ($O(\log n)$ search, $O(n)$ insert).
14. `Span<T>` is a `ref struct` that enables zero-allocation array slicing without copying heap memory.
15. Floyd's Tortoise and Hare algorithm detects linked list cycles in $O(n)$ time and $O(1)$ auxiliary space.
16. In an LRU Cache, combining a hash map with a doubly linked list provides $O(1)$ `Get` and $O(1)$ `Put`.
17. A Monotonic Stack processes the Next Greater Element and Largest Rectangle in Histogram in $O(n)$ single-pass time.
18. A Monotonic Deque solves the Sliding Window Maximum problem in $O(n)$ total time.
19. A Bloom Filter guarantees zero false negatives; it can return false positives, but never false negatives.
20. The optimal number of hash functions in a Bloom Filter is $k = rac{m}{n} \ln 2$.
21. A Trie enables prefix searching and autocomplete in $O(L)$ time, where $L$ is word length, independent of dictionary size.
22. BST deletion requires finding the In-order Successor (smallest value in the right subtree) when deleting a node with two children.
23. Red-Black trees maintain balance via color invariants and rotations, guaranteeing max height $\le 2 \log_2(n + 1)$.
24. In a binary heap stored in a zero-indexed array, the left child of index $i$ is $2i + 1$, right is $2i + 2$, and parent is $\lfloor(i - 1)/2floor$.
25. Building a heap from an unsorted array takes $O(n)$ time using Floyd's bottom-up `BuildHeap`, not $O(n \log n)$.
26. Skip Lists achieve $O(\log n)$ search, insertion, and deletion probabilistically using multi-tiered linked lists without tree rotations.
27. An Adjacency List consumes $O(V + E)$ space, making it ideal for sparse graphs; an Adjacency Matrix consumes $O(V^2)$ space.
28. Breadth-First Search (BFS) computes the shortest path on unweighted graphs in $O(V + E)$ time using a FIFO queue.
29. Topological sorting is only possible on Directed Acyclic Graphs (DAGs); Kahn's algorithm detects cycles via remaining in-degrees.
30. Dijkstra's algorithm solves single-source shortest paths in $O((V + E) \log V)$ time using a min-heap, but fails with negative weights.
31. The Bellman-Ford algorithm handles negative edge weights in $O(V \cdot E)$ time and detects negative weight cycles.
32. Disjoint Set Union (DSU) with path compression and union by rank achieves near-constant amortized time $lpha(n)$ per operation.
33. Kruskal's Minimum Spanning Tree algorithm sorts edges ($O(E \log E)$) and greedily unions components using DSU.
34. Binary search midpoint calculation must be written as `low + (high - low) / 2` to prevent 32-bit signed integer overflow.
35. Binary Search on Answer Space requires identifying a monotonic feasibility predicate ($FFFFTTTT$).
36. Quickselect finds the Kth smallest element in expected $O(n)$ time in-place without fully sorting the array.
37. Top-K elements can be maintained in $O(n \log K)$ time using a Min-Heap of size $K$.
38. .NET's `Array.Sort<T>` uses IntroSort: QuickSort switching to HeapSort when recursion exceeds $2 \log n$, and InsertionSort for small chunks.
39. Merge Sort is stable and guarantees $O(n \log n)$ time, but requires $O(n)$ auxiliary memory.
40. QuickSort with 3-way partitioning (Dijkstra's Dutch National Flag) solves the duplicate keys performance degradation.
41. Backtracking requires explicit state restoration (undoing the choice) after returning from recursive subproblem exploration.
42. 0/1 Knapsack can be solved in $O(W)$ auxiliary memory by traversing the capacity loop in reverse order.
43. Longest Increasing Subsequence (LIS) can be solved in $O(n \log n)$ time using patience sorting and binary search.
44. LINQ queries use deferred execution; invoking `.Count()` followed by `.FirstOrDefault()` enumerates the underlying query twice.
45. Repeatedly calling `List<T>.Contains()` inside a loop over $n$ items creates a hidden $O(n \cdot m)$ performance disaster.
46. `ArrayPool<T>.Shared` rents buffers to eliminate GC allocation spikes, but buffers must be returned in a `finally` block.
47. In C#, strings are immutable UTF-16 code unit sequences; repeated string concatenation in loops creates quadratic $O(n^2)$ memory copying.
48. Token Bucket rate limiting permits burstiness up to bucket capacity; Leaky Bucket smooths traffic to a constant egress rate.
49. An Inverted Index maps words to posting lists of document IDs, forming the core of full-text search engines.
50. High-concurrency systems favor lock-free data structures (`ConcurrentQueue<T>`) or channels (`Channel<T>`) to prevent lock convoying.

---

## 4. Self-Assessment Rubric

| Dimension | Needs Work (Junior) | Developing (Mid-Level) | Senior-Ready | Strong Senior / Staff-Level |
|---|---|---|---|---|
| **Complexity Analysis** | Confuses $O(n)$ with $O(n^2)$; cannot analyze nested loops; ignores space. | Accurately calculates Big O for standard loops; distinguishes best and worst case. | Analyzes amortized costs using mathematical series; applies Master Theorem; accounts for recursion stacks. | Evaluates complexity against hardware cache lines, branch prediction, and memory bandwidth bottlenecks. |
| **Data Structure Selection** | Relies exclusively on `List<T>`; unaware of hash collision mechanics. | Selects between Lists, Sets, and Dictionaries based on basic lookup requirements. | Explains internal bucket architectures, prime resizing, tree balance invariants, and heap arity. | Implements zero-allocation structures; selects custom specialized collections (`FrozenDictionary`, DSU, Bloom Filters). |
| **Algorithmic Patterns** | Memorizes code templates without understanding invariants. | Implements Two Pointers and standard BFS/DFS on familiar LeetCode problems. | Formulates state invariants; identifies Monotonic Predicates for binary search; derives DP transitions. | Solves complex graph and DP problems under time pressure; proves correctness via exchange arguments. |
| **C#/.NET Fluency** | Causes boxing allocations; triggers LINQ multiple enumeration bugs. | Writes correct idiomatic C# using standard generic collections. | Prevents hidden LINQ $O(n^2)$ traps; leverages `Span<T>` and `ArrayPool<T>`; uses `PriorityQueue<TElement, TPriority>`. | Benchmarks with BenchmarkDotNet; profiles allocation rates; optimizes memory layout for GC efficiency. |
| **Interview Leadership** | Jumps into code silently; gets defensive with hints; ignores edge cases. | Communicates while coding; handles basic edge cases with guidance. | Leads the interview methodically (Clarify $	o$ Baseline $	o$ Bottleneck $	o$ Optimize $	o$ Test); tests edge cases systematically. | Drives collaborative architectural dialogue; justifies trade-offs; adapts gracefully to shifting constraints. |

---

# Part IV — References

1. **Foundational Textbooks:**
   - Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. *Introduction to Algorithms* (CLRS) (4th ed.). MIT Press, 2022.
   - Sedgewick, R., & Wayne, K. *Algorithms* (4th ed.). Addison-Wesley, 2011.
   - Skiena, S. S. *The Algorithm Design Manual* (3rd ed.). Springer, 2020.
2. **Microsoft Learn Official Documentation:**
   - [Collections and Data Structures in .NET](https://learn.microsoft.com/dotnet/standard/collections/)
   - [An Introduction to `Span<T>` and Memory in .NET](https://learn.microsoft.com/dotnet/standard/memory-and-spans/)
   - [`PriorityQueue<TElement, TPriority>` Class](https://learn.microsoft.com/dotnet/api/system.collections.generic.priorityqueue-2)
   - [High-Performance C# Collection Improvements (.NET 8/9)](https://learn.microsoft.com/dotnet/core/whats-new/dotnet-8)
