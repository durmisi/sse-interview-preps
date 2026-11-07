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
- 7.6 Disjoint Set Union (DSU / Union-Find): Path compression, union by rank/size, near $O(1)$ amortized inverse Ackermann complexity $\alpha(n)$.
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
   $$0 \le f(n) \le c \cdot g(n) \quad \text{for all } n \ge n_0$$
   *Engineering meaning:* The algorithm will never perform worse than $c \cdot g(n)$ steps for sufficiently large inputs.

2. **Big Omega ($\Omega$): Asymptotic Lower Bound**
   $f(n) = \Omega(g(n))$ if there exist positive constants $c$ and $n_0$ such that:
   $$0 \le c \cdot g(n) \le f(n) \quad \text{for all } n \ge n_0$$
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
| $O(1)$ | Constant | 1 | 1 | 1 | 1 | $\approx 1 \text{ ns}$ |
| $O(\log n)$ | Logarithmic | $\approx 3$ | $\approx 7$ | $\approx 10$ | $\approx 20$ | $\approx 20 \text{ ns}$ |
| $O(n)$ | Linear | 10 | 100 | 1,000 | $1,000,000$ | $\approx 1 \text{ ms}$ |
| $O(n \log n)$ | Linearithmic | $\approx 33$ | $\approx 664$ | $\approx 9,965$ | $\approx 2 \times 10^7$ | $\approx 20 \text{ ms}$ |
| $O(n^2)$ | Quadratic | 100 | 10,000 | $1,000,000$ | $10^{12}$ | $\approx 16.6 \text{ minutes}$ |
| $O(n^3)$ | Cubic | 1,000 | $1,000,000$ | $10^9$ | $10^{18}$ | $\approx 31.7 \text{ years}$ |
| $O(2^n)$ | Exponential | 1,024 | $1.26 \times 10^{30}$ | Incomputable | Incomputable | Heat death of universe |
| $O(n!)$ | Factorial | $3.6 \times 10^6$ | $9.3 \times 10^{157}$ | Incomputable | Incomputable | Incomputable |

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
$$T(n) = aT\left(\frac{n}{b}\right) + f(n)$$
where $a \ge 1$ (number of subproblems), $b > 1$ (subproblem division factor), and $f(n) = \Theta(n^c)$:

Compare $c$ to $\log_b a$:
1. **Case 1:** If $c < \log_b a$, then $T(n) = \Theta(n^{\log_b a})$ (Tree leaves dominate).
2. **Case 2:** If $c = \log_b a$, then $T(n) = \Theta(n^c \log n) = \Theta(n^{\log_b a} \log n)$ (Work distributed evenly).
3. **Case 3:** If $c > \log_b a$, then $T(n) = \Theta(f(n))$ (Root node dominates).

*Application to Classic Algorithms:*
- **Binary Search:** $T(n) = 1T(n/2) + O(1) \implies a=1, b=2, c=0 \implies \log_2 1 = 0 = c \implies \text{Case 2: } \Theta(\log n)$.
- **Merge Sort:** $T(n) = 2T(n/2) + O(n) \implies a=2, b=2, c=1 \implies \log_2 2 = 1 = c \implies \text{Case 2: } \Theta(n \log n)$.

---

### 1.5 Amortized Analysis & Dynamic Array Resizing Proof

An operation has **Amortized Complexity $O(1)$** if any sequence of $k$ operations takes at most $O(k)$ total time, meaning the average cost per operation over the sequence is bounded by a constant, even if individual operations occasionally take $O(n)$ time.

#### Mathematical Proof: `List<T>.Add()` with Geometric Doubling
Suppose array capacity starts at 1 and doubles when full ($1, 2, 4, 8, \dots$).
When inserting $n$ elements:
- Cheap appends: Each of the $n$ items requires 1 write operation $\implies n$ writes.
- Expensive resizes: Occur at powers of 2 ($1, 2, 4, 8, \dots, 2^{\lfloor \log_2 n \rfloor}$).
  The total elements copied during all resizes is:
  $$\sum_{i=0}^{\lfloor \log_2 n \rfloor} 2^i = 2^{\lfloor \log_2 n \rfloor + 1} - 1 < 2n$$
- Total operations for $n$ additions: $\text{Total Work} = n \text{ (appends)} + 2n \text{ (copies)} = 3n \text{ operations}$.
- Average cost per operation: $\frac{3n}{n} = 3 = O(1)$ constant amortized time.

*Why Additive Growth is Catastrophic:* If the array grew by adding 100 slots instead of doubling, resizing would occur $\frac{n}{100}$ times. The total copy work would be an arithmetic progression summing to $O(n^2)$, yielding an amortized cost of $O(n)$ per insert!

---

### 1.6 Complexity vs Hardware Cache Reality

Two algorithms with identical $O(n)$ asymptotic complexity can exhibit vastly different runtimes due to CPU hardware architecture:
1. **Cache Lines (64 bytes):** When the CPU reads an address from RAM, it loads a contiguous 64-byte line into L1 cache.
   - Array traversal: Contiguous memory layout guarantees maximum spatial locality. The CPU cache-prefetcher anticipates sequential reads, achieving near-instant cache hits.
   - Linked List traversal: Node allocations are scattered arbitrarily across the managed heap. Every node jump triggers a **CPU Cache Miss**, forcing the core to stall for $\approx 200 \text{ cycles}$ waiting for main memory!
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

### 2.6 Thread-Safe & Producer-Consumer Collections

#### `ConcurrentDictionary<TKey, TValue>` Internals & Lock Striping
Unlike wrapping a standard `Dictionary<TKey, TValue>` in a single global `lock` (which serializes all threads), `ConcurrentDictionary<TKey, TValue>` partitions its internal bucket table across an array of fine-grained locks (**lock striping**, defaulting to `Environment.ProcessorCount` locks):
- **Reads (`TryGetValue`):** Completely **lock-free**! Readers traverse volatile bucket pointers using acquire/release memory barriers (`Volatile.Read`).
- **Writes (`TryAdd`, `AddOrUpdate`):** Acquire only the lock covering `bucketIndex % _locks.Length`, allowing concurrent mutations on different buckets.
- **Resizing:** Acquires *all* stripe locks sequentially to double the table safely.

**Critical Senior Pitfall — `GetOrAdd(key, valueFactory)` Executes Outside the Lock:**
In `dict.GetOrAdd(key, k => CreateExpensiveResource(k))`, the `valueFactory` delegate is invoked **outside** the bucket lock to prevent user callbacks from causing deadlocks while holding internal dictionary locks. Under race conditions, two threads requesting the same missing key simultaneously will **both execute `valueFactory`**, and only the first to acquire the bucket lock will win the insertion (`TryAddInternal`), while the second thread's created instance is silently discarded!
- *Mitigation:* If the factory has side effects or opens unmanaged connections, wrap the value in `Lazy<T>` (`ConcurrentDictionary<TKey, Lazy<TValue>>` with `LazyThreadSafetyMode.ExecutionAndPublication`).

#### `ConcurrentQueue<T>` vs `System.Threading.Channels.Channel<T>`
- `ConcurrentQueue<T>` is a lock-free FIFO queue built on linked array segments of 32 slots using `Interlocked.CompareExchange` (CAS loops). However, it is purely synchronous: if a consumer thread polls an empty `ConcurrentQueue<T>` in a `while` loop, it burns 100% CPU spinning.
- `Channel<T>` (`System.Threading.Channels`) is the modern async/await producer-consumer primitive in .NET. A `BoundedChannel<T>` enforces **asynchronous backpressure**: when the buffer reaches capacity, `Writer.WriteAsync()` suspends the producer asynchronously without blocking OS threads until a consumer drains slots via `Reader.ReadAllAsync()`.

```csharp
using System.Threading.Channels;

public sealed class BoundedTelemetryIngestionPipeline : IAsyncDisposable
{
    private readonly Channel<TelemetryEvent> _channel;
    private readonly Task _consumerLoop;

    public BoundedTelemetryIngestionPipeline(int maxCapacity = 10_000)
    {
        // Bounded channel applies backpressure when 10,000 events are queued in memory
        _channel = Channel.CreateBounded<TelemetryEvent>(new BoundedChannelOptions(maxCapacity)
        {
            FullMode = BoundedChannelFullMode.Wait,
            SingleWriter = false,
            SingleReader = true
        });

        _consumerLoop = Task.Run(ProcessQueueAsync);
    }

    public ValueTask EnqueueAsync(TelemetryEvent evt, CancellationToken ct) =>
        _channel.Writer.WriteAsync(evt, ct);

    private async Task ProcessQueueAsync()
    {
        await foreach (var evt in _channel.Reader.ReadAllAsync())
        {
            await FlushEventToStorageAsync(evt);
        }
    }

    private static ValueTask FlushEventToStorageAsync(TelemetryEvent evt) => ValueTask.CompletedTask;

    public async ValueTask DisposeAsync()
    {
        _channel.Writer.Complete();
        await _consumerLoop;
    }
}

public readonly record struct TelemetryEvent(Guid Id, long TimestampTicks, string MetricName, double Value);
```

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
$$\text{Sum}(L, R) = P[R + 1] - P[L]$$

#### Difference Array for $O(1)$ Range Updates
To apply multiple range additions $+V$ to ranges $[L, R]$ across an array of size $n$:
1. Initialize difference array $D$ of size $n + 1$ with zeros.
2. For each query $(L, R, V)$:
   $$D[L] \mathrel{+}= V, \quad D[R + 1] \mathrel{-}= V$$
3. Reconstruct the final array by computing the running prefix sum of $D$ in a single $O(n)$ pass!

---

### 3.4 Interval Problems: Merging & Concurrency

#### Pattern 1: Merging Overlapping Intervals ($O(n \log n)$ Time)
**Invariant:** When intervals $[S_i, E_i]$ are sorted monotonically by start time ($S_1 \le S_2 \le \dots \le S_n$), any intervals that can possibly overlap with the current active interval are guaranteed to be contiguous in the sorted sequence. Two adjacent intervals $[S_a, E_a]$ and $[S_b, E_b]$ (with $S_a \le S_b$) overlap if and only if $S_b \le E_a$, in which case they coalesce into $[S_a, \max(E_a, E_b)]$.

#### Pattern 2: Peak Interval Concurrency / Meeting Rooms II ($O(n \log n)$ Time)
To find the minimum number of concurrent resource slots (e.g., meeting rooms, worker threads, or database connections) required to serve all intervals without conflict:
1. Sort intervals by `Start` time ascending.
2. Maintain a **Min-Heap** (`PriorityQueue<Interval, int>`) keyed by `End` time, representing currently active rooms.
3. For each interval, if the earliest-ending active room finishes on or before the new interval starts (`minHeap.Peek() <= current.Start`), dequeue and reuse that room; otherwise allocate a new room.

```csharp
public readonly record struct TimeInterval(int Start, int End);

public static class IntervalAlgorithms
{
    public static List<TimeInterval> MergeIntervals(IReadOnlyList<TimeInterval> intervals)
    {
        if (intervals.Count == 0) return [];

        var sorted = intervals.OrderBy(i => i.Start).ToArray();
        List<TimeInterval> merged = [sorted[0]];

        for (int i = 1; i < sorted.Length; i++)
        {
            var current = sorted[i];
            var last = merged[^1];

            if (current.Start <= last.End)
            {
                // Overlap: extend the end of the last merged interval
                merged[^1] = new TimeInterval(last.Start, Math.Max(last.End, current.End));
            }
            else
            {
                merged.Add(current);
            }
        }

        return merged;
    }

    public static int MinConcurrentRoomsRequired(IReadOnlyList<TimeInterval> intervals)
    {
        if (intervals.Count == 0) return 0;

        var sorted = intervals.OrderBy(i => i.Start).ToArray();
        var activeEndTimes = new PriorityQueue<int, int>();

        foreach (var interval in sorted)
        {
            if (activeEndTimes.TryPeek(out _, out int earliestEnd) && earliestEnd <= interval.Start)
            {
                activeEndTimes.Dequeue(); // Reuse the room that freed up earliest
            }

            activeEndTimes.Enqueue(interval.End, interval.End);
        }

        return activeEndTimes.Count;
    }
}
```

---

### 3.5 String Internals & Zero-Allocation Parsing

#### UTF-16 `char` vs Unicode Scalar `Rune` vs Grapheme Clusters
In .NET, a `string` is a sequentially allocated, immutable array of 16-bit **UTF-16 code units** (`System.Char`). Assuming `1 char == 1 user-perceived character` is a classic enterprise bug:
1. **`char` (16-bit UTF-16 code unit):** Represents code points in the Basic Multilingual Plane (`U+0000` to `U+FFFF`). Characters above `U+FFFF` (such as emojis or rare CJK ideographs) require a **surrogate pair** of two `char` instances (4 bytes total). Calling `str.Substring(0, 1)` on `"🚀"` splits the surrogate pair in half, producing corrupted invalid UTF-16 (`\uD83D`)!
2. **`System.Text.Rune` (Unicode Scalar Value, 32-bit):** Represents a valid Unicode code point (`U+0000` to `U+10FFFF`, excluding lone surrogates). Iterating via `str.EnumerateRunes()` safely processes surrogate pairs as a single `Rune`.
3. **Grapheme Cluster (TextElement):** A single user-perceived visual character may be composed of *multiple* `Rune` scalars joined by Zero-Width Joiners (e.g., `"👨‍👩‍👧‍👦"` is 7 `Rune` scalars and 11 `char` units!). Use `StringInfo.GetTextElementEnumerator(str)` when truncating user-facing display strings.

#### `StringBuilder` Linked-Chunk Internals
`StringBuilder` does **not** maintain a single flat `char[]` like `List<char>`. Internally, it is a **linked list of `StringBuilder` chunks** (`char[] m_ChunkChars`, `StringBuilder? m_ChunkPrevious`). When a chunk fills up, it allocates a new `StringBuilder` node linked to the previous chunk rather than copying the entire existing buffer, avoiding Large Object Heap (LOH, $\ge 85,000$ bytes) allocations until `.ToString()` materializes the final contiguous string. However, if you know the approximate final size, always pre-size via `new StringBuilder(capacity)` to collapse the linked list into a single chunk.

#### Vectorized `SearchValues<char>` (.NET 8) & `GetAlternateLookup<ReadOnlySpan<char>>` (.NET 9)
- **`SearchValues<T>` (.NET 8+):** Precomputes hardware-accelerated SIMD lookup tables (SSE2/AVX2/NEON bitmaps or probabilistic vectorized masks) for character/byte sets. Store `SearchValues<char>` in a `static readonly` field for $O(n)$ SIMD-accelerated `.IndexOfAny()`.
- **`Dictionary<string, TValue>.GetAlternateLookup<ReadOnlySpan<char>>()` (.NET 9+):** Historically, looking up a slice of a string in a `Dictionary<string, T>` required calling `.ToString()` on the `ReadOnlySpan<char>`, allocating a temporary heap string on every lookup. .NET 9 introduces `GetAlternateLookup<ReadOnlySpan<char>>()`, enabling true **zero-allocation dictionary lookups** directly from a `ReadOnlySpan<char>`!

```csharp
using System.Buffers;
using System.Text;

public static class HighPerformanceStringParser
{
    // Precomputed SIMD vectorized character set (.NET 8+)
    private static readonly SearchValues<char> Delimiters = SearchValues.Create(":;, \t");

    public static bool TryLookupHeader(
        Dictionary<string, int> headerRegistry,
        ReadOnlySpan<char> rawLine,
        out int headerCode)
    {
        int delimiterIdx = rawLine.IndexOfAny(Delimiters);
        ReadOnlySpan<char> keySlice = delimiterIdx >= 0 ? rawLine[..delimiterIdx] : rawLine;

        // .NET 9 AlternateLookup: Queries Dictionary<string, int> using ReadOnlySpan<char> with ZERO string allocation!
        var spanLookup = headerRegistry.GetAlternateLookup<ReadOnlySpan<char>>();
        return spanLookup.TryGetValue(keySlice, out headerCode);
    }

    public static int CountUnicodeScalars(string text)
    {
        int count = 0;
        foreach (Rune _ in text.EnumerateRunes())
            count++;
        return count;
    }
}
```

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
- Optimal number of hash functions: $k = \frac{m}{n} \ln 2\approx 0.693 \frac{m}{n}$
- False positive probability: $p\approx \left(1 - e^{-kn/m}\right)^k$

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

### 5.3 Count-Min Sketch (Frequency Estimation in Bounded Space)

While a Bloom Filter answers **set membership** ("Have we seen key $X$?"), a **Count-Min Sketch** answers **frequency estimation** ("Approximately how many times has key $X$ appeared in this massive stream?") using fixed, sub-linear $O(d \cdot w)$ memory instead of an unbounded `Dictionary<TKey, long>`.

#### Mathematical Foundations & Error Bounds
A Count-Min Sketch consists of a 2D integer matrix of depth $d$ (number of pairwise-independent hash functions) and width $w$ (buckets per row):
- Given desired additive error factor $\varepsilon$ and failure probability $\delta$:
  $$w = \left\lceil \frac{e}{\varepsilon} \right\rceil, \quad d = \left\lceil \ln\left(\frac{1}{\delta}\right) \right\rceil$$
- **`Increment(item)`:** For each row $i \in [0, d-1]$, compute column $j = h_i(\text{item}) \bmod w$ and increment `matrix[i, j]++`.
- **`EstimateCount(item)`:** Return $\min_{0 \le i < d} \text{matrix}[i, h_i(\text{item}) \bmod w]$.
- **Invariant:** Because hash collisions can only *increase* bucket counters, the sketch **never underestimates** the true frequency ($\hat{f}(x) \ge f(x)$). Taking the minimum across all $d$ rows selects the row with the fewest collisions, bounding the overestimation error to $\le \varepsilon N$ with probability at least $1 - \delta$.

```csharp
public sealed class CountMinSketch<T>
{
    private readonly long[,] _table;
    private readonly int _depth;
    private readonly int _width;
    private readonly Func<T, (uint H1, uint H2)> _hasher;

    public CountMinSketch(double epsilon, double delta, Func<T, (uint H1, uint H2)> hasher)
    {
        if (epsilon is <= 0 or >= 1) throw new ArgumentOutOfRangeException(nameof(epsilon));
        if (delta is <= 0 or >= 1) throw new ArgumentOutOfRangeException(nameof(delta));

        _width = (int)Math.Ceiling(Math.E / epsilon);
        _depth = (int)Math.Ceiling(Math.Log(1.0 / delta));
        _table = new long[_depth, _width];
        _hasher = hasher;
    }

    public void Increment(T item, long count = 1)
    {
        var (h1, h2) = _hasher(item);
        for (int row = 0; row < _depth; row++)
        {
            int col = (int)((h1 + (uint)row * h2) % (uint)_width);
            _table[row, col] += count;
        }
    }

    public long EstimateFrequency(T item)
    {
        var (h1, h2) = _hasher(item);
        long minEstimate = long.MaxValue;

        for (int row = 0; row < _depth; row++)
        {
            int col = (int)((h1 + (uint)row * h2) % (uint)_width);
            minEstimate = Math.Min(minEstimate, _table[row, col]);
        }

        return minEstimate;
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

### 6.3 Binary Heaps & Floyd's O(n) BuildHeap Proof

#### Array-Backed Complete Binary Tree Layout
A binary min-heap is a complete binary tree stored compactly in a flat array (`T[]`) without node pointers:
- For any node at zero-based index $i$:
  - $\text{Parent}(i) = \lfloor (i - 1) / 2 \rfloor$
  - $\text{LeftChild}(i) = 2i + 1$
  - $\text{RightChild}(i) = 2i + 2$
- All non-leaf (internal) nodes reside in indices $0 \dots \lfloor n/2 \rfloor - 1$; all leaves reside in indices $\lfloor n/2 \rfloor \dots n - 1$.

#### Mathematical Proof: Why Floyd's Bottom-Up `BuildHeap` is $O(n)$, Not $O(n \log n)$
Inserting $n$ elements one by one via `HeapifyUp` costs $O(n \log n)$ because the $n/2$ elements at the bottom of the tree each travel up to $\log_2 n$ levels toward the root.
Floyd's bottom-up `BuildHeap` reverses this: it leaves the bottom half of the array (leaves) untouched and runs `HeapifyDown` (sift-down) starting from index $\lfloor n/2 \rfloor - 1$ down to $0$:
- At height $h$ from the bottom, there are at most $\left\lceil \frac{n}{2^{h+1}} \right\rceil$ nodes, and each node sifts down at most $h$ levels.
- Total work across all heights:
  $$T(n) \le \sum_{h=0}^{\lfloor \log_2 n \rfloor} \frac{n}{2^{h+1}} \cdot h = \frac{n}{2} \sum_{h=0}^{\infty} \frac{h}{2^h}$$
- Since the infinite arithmetico-geometric series $\sum_{h=0}^{\infty} \frac{h}{2^h}$ converges to $2$:
  $$T(n) \le \frac{n}{2} \cdot 2 = n = O(n)$$

```csharp
public static class BinaryMinHeap
{
    // Floyd's O(n) Bottom-Up Heap Construction in-place
    public static void BuildMinHeap(Span<int> array)
    {
        for (int i = (array.Length / 2) - 1; i >= 0; i--)
        {
            SiftDown(array, i, array.Length);
        }
    }

    public static void SiftDown(Span<int> heap, int index, int count)
    {
        while (true)
        {
            int left = 2 * index + 1;
            int right = 2 * index + 2;
            int smallest = index;

            if (left < count && heap[left] < heap[smallest])
                smallest = left;
            if (right < count && heap[right] < heap[smallest])
                smallest = right;

            if (smallest == index)
                break;

            (heap[index], heap[smallest]) = (heap[smallest], heap[index]);
            index = smallest;
        }
    }
}
```

---

### 6.4 Skip Lists (Probabilistic Balanced Indexing)

#### Fundamentals & Enterprise Use Cases
A **Skip List** (invented by William Pugh, 1989) is a probabilistic multi-layered linked list that achieves $O(\log n)$ expected time for search, insertion, and deletion without the complex multi-node rebalancing rotations of AVL or Red-Black trees.
- **Level 0:** A standard sorted linked list containing all $n$ elements.
- **Levels $1 \dots L_{\max}$:** Express lanes where a node at level $k$ is promoted to level $k + 1$ with probability $p = 0.5$ (via a fast PRNG bit flip).
- **Why Redis (`ZSET`) and RocksDB (`MemTable`) Choose Skip Lists Over Balanced BSTs:**
  1. **Lock-Free Concurrency:** Inserting into a Skip List only updates local forward pointers at each level (amenable to `Interlocked.CompareExchange`), whereas a Red-Black tree rotation can propagate all the way to the root, invalidating reader paths across the tree.
  2. **Sequential Range Scans:** Traversing `[minKey, maxKey]` is a trivial linear walk along Level 0 pointers.

```csharp
public sealed class SkipList<TKey, TValue> where TKey : IComparable<TKey>
{
    private const int MaxLevel = 16;
    private sealed class Node(TKey key, TValue value, int level)
    {
        public TKey Key { get; } = key;
        public TValue Value { get; set; } = value;
        public Node?[] Forward { get; } = new Node?[level];
    }

    private readonly Node _head = new(default!, default!, MaxLevel);
    private int _currentMaxLevel = 1;

    public bool TryGetValue(TKey key, out TValue value)
    {
        var current = _head;
        for (int lvl = _currentMaxLevel - 1; lvl >= 0; lvl--)
        {
            while (current.Forward[lvl] is { } next && next.Key.CompareTo(key) < 0)
            {
                current = next;
            }
        }

        current = current.Forward[0];
        if (current is not null && current.Key.CompareTo(key) == 0)
        {
            value = current.Value;
            return true;
        }

        value = default!;
        return false;
    }

    public void Upsert(TKey key, TValue value)
    {
        Span<int> _ = stackalloc int[1]; // Keep method stack-friendly
        var update = new Node[MaxLevel];
        var current = _head;

        for (int lvl = _currentMaxLevel - 1; lvl >= 0; lvl--)
        {
            while (current.Forward[lvl] is { } next && next.Key.CompareTo(key) < 0)
            {
                current = next;
            }
            update[lvl] = current;
        }

        if (current.Forward[0] is { } existing && existing.Key.CompareTo(key) == 0)
        {
            existing.Value = value;
            return;
        }

        int nodeLevel = RollLevel();
        if (nodeLevel > _currentMaxLevel)
        {
            for (int lvl = _currentMaxLevel; lvl < nodeLevel; lvl++)
                update[lvl] = _head;
            _currentMaxLevel = nodeLevel;
        }

        var newNode = new Node(key, value, nodeLevel);
        for (int lvl = 0; lvl < nodeLevel; lvl++)
        {
            newNode.Forward[lvl] = update[lvl].Forward[lvl];
            update[lvl].Forward[lvl] = newNode;
        }
    }

    private static int RollLevel()
    {
        int level = 1;
        while (level < MaxLevel && (Random.Shared.Next() & 1) == 0)
            level++;
        return level;
    }
}
```

---

### Section 6 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How does an array-backed Binary Heap maintain the complete binary tree invariant during insertion and deletion?**
> **Strong answer:** A binary heap stores nodes in a flat array where parent-child relationships are calculated via index arithmetic: for zero-indexed array index $i$, Left Child is $2i + 1$, Right Child is $2i + 2$, and Parent is $\lfloor(i - 1) / 2\rfloor$. When inserting an item, it is placed at the end of the array (maintaining the structural shape of a complete binary tree) and `HeapifyUp` (sift-up) is performed by repeatedly swapping with its parent until the heap order property is restored ($O(\log n)$). When extracting the min/max root, the root element is replaced with the last element of the array, the array length is decremented by 1, and `HeapifyDown` (sift-down) is performed by swapping with the smaller/larger child until the heap invariant is restored ($O(\log n)$).

---

## Section 7 — Graphs, Traversals & Shortest Paths

### 7.1 Topological Sort with Kahn's Algorithm & Cycle Detection

Topological sorting produces a linear ordering of vertices in a Directed Acyclic Graph (DAG) such that for every directed edge $U \to V$, $U$ comes before $V$.

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

### 7.4 Minimum Spanning Tree (Kruskal's & Prim's Algorithms)

Given a connected, undirected, weighted graph $G = (V, E)$, a **Minimum Spanning Tree (MST)** is a subset of $V - 1$ edges that connects all $V$ vertices without cycles and minimizes total edge weight.

| Algorithm | Strategy | Time Complexity | Optimal Graph Density |
|---|---|---|---|
| **Kruskal's Algorithm** | Sort all edges by weight ascending; greedily add edge $(u, v)$ if `dsu.Union(u, v)` succeeds (no cycle). | $O(E \log E)$ or $O(E \log V)$ | **Sparse Graphs** ($E \approx V$) — fast array sort + $O(\alpha(V))$ DSU. |
| **Prim's Algorithm** | Grow a single tree from a start vertex by greedily dequeuing the lightest cross-cut edge from a `PriorityQueue`. | $O(E \log V)$ | **Dense Graphs** ($E \approx V^2$) — avoids sorting all $V^2$ edges upfront. |

```csharp
public readonly record struct WeightedEdge(int U, int V, int Weight) : IComparable<WeightedEdge>
{
    public int CompareTo(WeightedEdge other) => Weight.CompareTo(other.Weight);
}

public static class MinimumSpanningTree
{
    // Kruskal's Algorithm using DisjointSetUnion: O(E log E) time, O(V) auxiliary space
    public static (long TotalWeight, List<WeightedEdge> TreeEdges) KruskalMst(int numVertices, Span<WeightedEdge> edges)
    {
        edges.Sort(); // Sorts in-place by Weight ascending via WeightedEdge.CompareTo
        var dsu = new DisjointSetUnion(numVertices);
        var mstEdges = new List<WeightedEdge>(Math.Max(0, numVertices - 1));
        long totalWeight = 0;

        foreach (ref readonly var edge in edges)
        {
            if (dsu.Union(edge.U, edge.V))
            {
                totalWeight += edge.Weight;
                mstEdges.Add(edge);

                if (mstEdges.Count == numVertices - 1)
                    break; // MST complete!
            }
        }

        if (numVertices > 0 && mstEdges.Count != numVertices - 1)
            throw new InvalidOperationException("Graph is disconnected; no spanning tree exists.");

        return (totalWeight, mstEdges);
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

### 8.2 Binary Search in Rotated Sorted Array

#### The Split-Monotonicity Invariant
When a sorted array of distinct values (e.g., `[0, 1, 2, 4, 5, 6, 7]`) is rotated at an unknown pivot (`[4, 5, 6, 7, 0, 1, 2]`), standard binary search fails because the global array is no longer monotonic.
However, a critical **structural invariant** holds at every midpoint `mid`: **at least one of the two halves (`[low..mid]` or `[mid..high]`) is strictly sorted!**
1. Check if `nums[low] <= nums[mid]`:
   - If true, the **left half `[low..mid]` is contiguous and sorted**. We can test in $O(1)$ if `target` lies within `[nums[low], nums[mid])`. If so, set `high = mid - 1`; otherwise `low = mid + 1`.
   - If false, the pivot lies in the left half, which guarantees the **right half `[mid..high]` is contiguous and sorted**. We test if `target` lies within `(nums[mid], nums[high]]`. If so, set `low = mid + 1`; otherwise `high = mid - 1`.

```csharp
public static int SearchRotatedSortedArray(ReadOnlySpan<int> nums, int target)
{
    int low = 0;
    int high = nums.Length - 1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target)
            return mid;

        // Invariant check: Is the left subarray [low..mid] strictly sorted?
        if (nums[low] <= nums[mid])
        {
            if (target >= nums[low] && target < nums[mid])
                high = mid - 1; // Target is trapped inside the sorted left half
            else
                low = mid + 1;
        }
        else
        {
            // Otherwise, the right subarray [mid..high] is guaranteed to be strictly sorted
            if (target > nums[mid] && target <= nums[high])
                low = mid + 1;  // Target is trapped inside the sorted right half
            else
                high = mid - 1;
        }
    }

    return -1;
}
```

---

### 8.3 Binary Search on Answer Space (Monotonic Predicates)

When asked to find the **minimum capacity**, **minimum speed**, or **maximum threshold** to satisfy a condition, look for a **Monotonic Feasibility Predicate**:
$$\text{IsFeasible}(\text{value}) \implies [False, False, False, True, True, True]$$

#### Classic Example: Capacity to Ship Packages Within D Days ($O(n \log(\sum \text{weights}))$)
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

### Section 8 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: What happens to the time complexity of Binary Search in a Rotated Sorted Array if duplicate elements are allowed (e.g., `[2, 2, 2, 0, 2, 2]`)?**
> **Strong answer:** With distinct elements, comparing `nums[low] <= nums[mid]` deterministically reveals which half is sorted in $O(1)$ time, guaranteeing $O(\log n)$ worst-case complexity. However, when duplicates are permitted, we can encounter `nums[low] == nums[mid] == nums[high]` (for example, `[2, 2, 2, 0, 2]` where `low=0, mid=2, high=4`). In this state, it is impossible to tell in $O(1)$ time whether the minimum pivot lies to the left or right of `mid`. The only safe transition is shrinking the bounds linearly (`low++; high--;`), which degrades the worst-case time complexity from $O(\log n)$ to $O(n)$ when almost all elements are identical.

**Q2: How do you avoid infinite loops when choosing between `while (low <= high)` and `while (low < high)` in binary search?**
> **Strong answer:** The loop condition must match the search interval representation and midpoint rounding. In `while (low < high)` (half-open convergence to a boundary index), `mid = low + (high - low) / 2` rounds *down* toward `low`. Therefore, the branch that updates `low` **must** advance past `mid` (`low = mid + 1`), while the branch that updates `high` sets `high = mid`. If you instead set `low = mid` while rounding `mid` down, a 2-element range (`low = 0, high = 1`) computes `mid = 0` and sets `low = 0`, causing an infinite loop.

#### Practical Exercises
1. **Exercise 8.1:** Implement `FindMinimumInRotatedSortedArray(ReadOnlySpan<int> nums)` in $O(\log n)$ time using `while (low < high)` boundary convergence.
2. **Exercise 8.2:** Given $n$ server nodes and an array of task durations, use Binary Search on Answer Space to compute the minimum time required to complete all tasks if tasks are assigned contiguously to servers.

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

### 9.2 Merge Sort, QuickSort (3-Way Partitioning) & Non-Comparison Sorts (Counting/Radix)

#### Comparison vs Non-Comparison Sorting Matrix
Any comparison-based sorting algorithm requires at least $\Omega(n \log n)$ comparisons in the worst and average cases because a binary decision tree must have at least $n!$ leaves to distinguish all permutations ($\log_2(n!) = \Theta(n \log n)$ by Stirling's approximation). Non-comparison sorts bypass this lower bound by exploiting the internal bit/radix representation of keys.

| Algorithm | Best | Average | Worst | Auxiliary Space | Stable? | Key Engineering Trade-off |
|---|---|---|---|---|---|---|
| **Merge Sort** | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $O(n)$ | **Yes** | Guaranteed $O(n \log n)$ and stable, but requires $O(n)$ buffer allocation. |
| **QuickSort (3-Way)** | $\Theta(n)$ (all equal) | $\Theta(n \log n)$ | $\Theta(n^2)$ | $O(\log n)$ stack | No | Dutch National Flag partitioning prevents $O(n^2)$ degradation on duplicate keys. |
| **HeapSort** | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $O(1)$ | No | Zero extra memory and worst-case safe, but poor CPU cache locality (jumps across array indices $i \to 2i+1$). |
| **Counting / Radix Sort** | $\Theta(d(n + b))$ | $\Theta(d(n + b))$ | $\Theta(d(n + b))$ | $O(n + b)$ | **Yes** | Beats $O(n \log n)$ for fixed-width integers (`int`, `long`, `Guid` bytes), where $d$ is digits and $b$ is base (e.g., $256$). |

#### Dijkstra's 3-Way QuickSort (Dutch National Flag Partitioning)
Standard 2-way Lomuto/Hoare QuickSort degrades to $O(n^2)$ when the input contains many duplicate keys (e.g., sorting 1,000,000 orders by 5 status codes). **3-Way Partitioning** partitions the subarray into three regions in a single pass:
- `[low .. lt - 1]`: Strictly less than `pivot` ($< P$)
- `[lt .. gt]`: Equal to `pivot` ($== P$) — **excluded from recursive calls!**
- `[gt + 1 .. high]`: Strictly greater than `pivot` ($> P$)

```csharp
public static class AdvancedSorts
{
    public static void QuickSort3Way(Span<int> nums)
    {
        if (nums.Length <= 1) return;

        int pivot = nums[nums.Length / 2];
        int lt = 0, i = 0, gt = nums.Length - 1;

        while (i <= gt)
        {
            if (nums[i] < pivot)
            {
                (nums[lt], nums[i]) = (nums[i], nums[lt]);
                lt++;
                i++;
            }
            else if (nums[i] > pivot)
            {
                (nums[i], nums[gt]) = (nums[gt], nums[i]);
                gt--;
            }
            else
            {
                i++;
            }
        }

        // All elements in [lt..gt] equal the pivot and are already in their final sorted positions!
        QuickSort3Way(nums[..lt]);
        QuickSort3Way(nums[(gt + 1)..]);
    }

    // LSD Radix Sort (Base-256, 4 passes for non-negative 32-bit integers): O(n) Time
    public static void RadixSortNonNegative(Span<int> nums)
    {
        if (nums.Length <= 1) return;
        int[] temp = ArrayPool<int>.Shared.Rent(nums.Length);
        Span<int> buffer = temp.AsSpan(0, nums.Length);
        Span<int> count = stackalloc int[256];

        try
        {
            for (int shift = 0; shift < 32; shift += 8)
            {
                count.Clear();
                foreach (int val in nums)
                    count[(val >> shift) & 0xFF]++;

                // Convert frequencies to prefix starting offsets (preserves stability!)
                int sum = 0;
                for (int b = 0; b < 256; b++)
                {
                    int c = count[b];
                    count[b] = sum;
                    sum += c;
                }

                foreach (int val in nums)
                {
                    int bucket = (val >> shift) & 0xFF;
                    buffer[count[bucket]++] = val;
                }

                buffer.CopyTo(nums);
            }
        }
        finally
        {
            ArrayPool<int>.Shared.Return(temp);
        }
    }
}
```

---

### Section 9 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How does .NET's `Array.Sort<T>` work internally, and why is it not pure QuickSort?**
> **Strong answer:** .NET uses **IntroSort** (Introspective Sort), a hybrid sorting algorithm combining QuickSort, HeapSort, and InsertionSort. It begins with QuickSort using median-of-three pivot selection. However, if the recursion depth exceeds $2 \lfloor\log_2 n\rfloor$ (indicating degenerate unbalanced partitions toward $O(n^2)$), it automatically switches to HeapSort to guarantee an absolute $O(n \log n)$ worst-case time bound. When partitioned subarrays become small ($\le 16$ elements), it switches to InsertionSort, which outperforms QuickSort on small arrays due to minimal overhead and exceptional CPU cache locality.

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
  $$dp[w] = \max(dp[w], dp[w - \text{weight}[i]] + \text{value}[i])$$

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

### 10.3 Greedy Algorithms & Exchange Argument

#### Greedy Choice Property & Proving Correctness via Exchange Argument
A **Greedy Algorithm** constructs a global solution by making the locally optimal choice at each step without backtracking or exploring alternative branches. Unlike Dynamic Programming (which evaluates all overlapping subproblems), a greedy strategy is valid *if and only if* the problem exhibits the **Greedy Choice Property** and **Optimal Substructure**.

To prove in a senior interview that a greedy heuristic is globally optimal, use an **Exchange Argument**:
1. Assume there exists an optimal solution $O$ that differs from our greedy solution $G$.
2. Identify the first step $i$ where $O$ chose element $o_i$ while $G$ chose the locally best element $g_i$.
3. Prove that swapping $o_i$ for $g_i$ inside $O$ (yielding $O' = O \setminus \{o_i\} \cup \{g_i\}$) remains feasible and produces a solution at least as good as $O$ ($\text{Value}(O') \ge \text{Value}(O)$).
4. By induction, $O$ can be transformed step-by-step into $G$ without degrading quality, proving $G$ is optimal!

#### Canonical Example: Activity Selection / Maximum Non-Overlapping Intervals ($O(n \log n)$)
- **Wrong Greedy Heuristic:** Pick the shortest interval or earliest-starting interval first (fails when a short interval straddles two valid intervals, or an early interval spans the entire timeline).
- **Correct Greedy Choice:** Sort intervals by **End Time ascending** ($E_1 \le E_2 \le \dots \le E_n$) and always pick the next compatible interval that finishes earliest.
- **Exchange Argument Proof:** Since $g_1$ finishes no later than $o_1$ ($E(g_1) \le E(o_1)$), replacing $o_1$ with $g_1$ in any optimal schedule never conflicts with $o_2$ (since $E(g_1) \le E(o_1) \le S(o_2)$), leaving *more or equal* remaining timeline for subsequent tasks.

```csharp
public static int MaxNonOverlappingActivities(ReadOnlySpan<TimeInterval> intervals)
{
    if (intervals.Length == 0) return 0;

    var sorted = intervals.ToArray();
    Array.Sort(sorted, static (a, b) => a.End.CompareTo(b.End));

    int count = 1;
    int lastEnd = sorted[0].End;

    for (int i = 1; i < sorted.Length; i++)
    {
        if (sorted[i].Start >= lastEnd)
        {
            count++;
            lastEnd = sorted[i].End;
        }
    }

    return count;
}
```

---

### Section 10 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why must the inner capacity loop run backwards (`w = capacity` down to `weights[i]`) in 1D space-optimized 0/1 Knapsack, and what happens if you run it forwards?**
> **Strong answer:** In 0/1 Knapsack, each item $i$ can be selected at most once. The recurrence $dp[i][w] = \max(dp[i-1][w], dp[i-1][w - \text{weight}[i]] + \text{value}[i])$ depends strictly on values from the *previous* row $i - 1$. When we compress the 2D table into a single 1D array `dp[w]`, iterating `w` backwards from `capacity` down to `weights[i]` guarantees that when we read `dp[w - weights[i]]`, that lower index has not yet been updated for item $i$—it still holds the $i - 1$ state. Conversely, if we iterate `w` forwards from `weights[i]` up to `capacity`, `dp[w - weights[i]]` may already include item $i$, allowing the same item to be picked repeatedly! In fact, running the loop forwards solves the **Unbounded Knapsack** problem.

**Q2: How do you decide between Top-Down Memoization and Bottom-Up Tabulation in production C#?**
> **Strong answer:** Bottom-Up Tabulation is strongly preferred in production .NET for two reasons: (1) It avoids deep recursive call frames that can trigger an unrecoverable `StackOverflowException` when $n \ge 10^4$, and (2) It allows space-compression optimizations (such as reducing $O(n \cdot W)$ matrix memory to a single $O(W)$ contiguous array with superior CPU cache locality). Top-Down Memoization is advantageous only when the state space is sparse—meaning only a small fraction of all $(i, j)$ combinations are actually reachable from the initial query—and the recursion depth is strictly bounded.

#### Practical Exercises
1. **Exercise 10.1:** Implement `CoinChangeMinCoins(int[] coins, int amount)` using 1D Bottom-Up DP, and prove via a counterexample why the greedy approach (always picking the largest coin) fails for `coins = [1, 3, 4]` and `amount = 6`.
2. **Exercise 10.2:** Implement `EditDistance(ReadOnlySpan<char> source, ReadOnlySpan<char> target)` (Levenshtein distance) using only $O(\min(n, m))$ auxiliary space via two rolling `stackalloc` or `ArrayPool<int>` rows.

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

### 11.3 Checked Arithmetic & Bitwise Manipulation

#### Silent Integer Overflow vs `checked` Contexts
By default, C# executes integer arithmetic in an `unchecked` context: `int.MaxValue + 1` silently wraps around in two's complement to `int.MinValue` (`-2,147,483,648`). In financial ledger calculations, pagination offset math (`pageIndex * pageSize`), or buffer size computations, silent wrap-around can cause negative array indices or security vulnerabilities.
- Use `checked { ... }` blocks or `checked(a + b)` expressions on untrusted bounds or financial quantities so overflow throws `OverflowException` immediately.

#### Hardware Intrinsics in `System.Numerics.BitOperations` (.NET Core 3.0+)
Modern .NET exposes CPU bit-manipulation instructions (`POPCNT`, `LZCNT`, `TZCNT`) directly via `System.Numerics.BitOperations`:
- **Power-of-Two Check (`x > 0 && (x & (x - 1)) == 0`):** `BitOperations.IsPow2(x)` in $O(1)$.
- **Next Power of Two (for array/hash sizing):** `BitOperations.RoundUpToPowerOf2((uint)n)`.
- **Set Bit Count (Hamming Weight):** `BitOperations.PopCount((ulong)mask)` compiles to a single CPU `popcnt` instruction.
- **Clear Lowest Set Bit (Brian Kernighan's trick):** `x &= (x - 1)` strips the lowest `1` bit in $O(1)$.
- **XOR Self-Inverse Property ($x \oplus x = 0$ and $x \oplus 0 = x$):** Finds the single non-duplicated element in an array in $O(n)$ time and $O(1)$ space.

```csharp
using System.Numerics;

public static class BitwiseAndCheckedPrimitives
{
    public static int SafeCalculateBufferBytes(int itemCount, int bytesPerItem)
    {
        // Throws OverflowException instead of wrapping to a negative size!
        return checked(itemCount * bytesPerItem);
    }

    public static int FindSingleUniqueNumber(ReadOnlySpan<int> nums)
    {
        int xorAccumulator = 0;
        foreach (int n in nums)
            xorAccumulator ^= n;
        return xorAccumulator;
    }

    public static int CountDiffBits(ulong a, ulong b) =>
        BitOperations.PopCount(a ^ b); // Hamming distance in 1 hardware instruction
}
```

---

### Section 11 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: When renting a buffer from `ArrayPool<T>.Shared.Rent(minLength)`, what are the two most common production bugs engineers introduce?**
> **Strong answer:** First, `Rent(minLength)` returns an array that is *at least* `minLength` long (typically rounded up to a power-of-two bucket, e.g., requesting 1,000 bytes returns a 1,024-byte array). Passing `rentedArray.Length` instead of `actualCount` to downstream serializers or network streams writes trailing garbage bytes from previous tenants of that buffer! You must always slice via `rentedArray.AsSpan(0, actualLength)`. Second, if the buffer holds sensitive data (PII, JWT tokens, cryptographic keys) or reference types, failing to set `clearArray: true` on `Return()` either leaks memory references (preventing GC collection of objects still pointed to by the pooled array) or exposes sensitive data to the next caller.

**Q2: Why does passing a capturing lambda to `list.Where(x => x.Id == targetId)` allocate on the managed heap, and how do you prevent unintended closure allocations?**
> **Strong answer:** When a lambda expression captures a local variable or parameter (`targetId`), the C# compiler synthesizes a hidden closure class (`<>c__DisplayClass`) on the managed heap to hold `targetId` and allocates a new delegate instance pointing to that closure object on every call. On hot paths, this creates significant Gen-0 GC pressure. When a lambda does not need state, mark it with the `static` modifier (`static x => x.IsActive`), which forces a compile error if any variable is accidentally captured and allows the compiler to cache a single static delegate instance for the lifetime of the process.

#### Practical Exercises
1. **Exercise 11.1:** Write a zero-allocation tokenizer using `ReadOnlySpan<char>` and `ArrayPool<Range>.Shared` that splits a CSV line without allocating `string[]` or substring instances.
2. **Exercise 11.2:** Use `BitOperations` and a single `ulong` bitmask to represent and evaluate a 64-permission RBAC entitlement check in $O(1)$ time.

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

### Section 12 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: In a 45-minute senior coding interview, what should you do if you do not immediately see the optimal $O(n)$ solution?**
> **Strong answer:** Never sit in silence for 10 minutes hoping for an epiphany. Immediately state the brute-force baseline (e.g., $O(n^2)$ nested scan) and write down its time and space complexity in 60 seconds. Next, articulate the exact bottleneck aloud—such as repeated range minimum queries or redundant suffix comparisons—and systematically test candidate data structures against that bottleneck (Hash Map for $O(1)$ complement lookup, Monotonic Stack for next greater element, Binary Search if the answer space is monotonic, or Heap for dynamic min/max). Interviewers evaluate senior candidates on structured bottleneck elimination and invariant communication, not theatrical instant recall.

**Q2: How do you handle an interviewer interrupting your explanation with "Are you sure that handles negative numbers?"**
> **Strong answer:** Treat every interviewer question as a high-signal collaborative hint rather than a confrontation. Pause coding immediately, construct a minimal 3-element test case containing a negative number (e.g., `[2, -1, 3]` with target `K = 4`), and trace your current invariant against it aloud. Acknowledge specifically which assumption broke (for instance, 'My two-pointer window assumes prefix sums grow monotonically, which fails when `nums[i] < 0`') and pivot cleanly to the appropriate structure (such as a Prefix Sum Hash Map or Monotonic Deque).

#### Practical Exercises
1. **Exercise 12.1:** Record yourself solving a hard array/graph problem aloud in 30 minutes following all 7 steps of the Whiteboard Protocol, verifying that you state the loop invariant before writing the loop body.
2. **Exercise 12.2:** Construct a reusable 5-line C# edge-case test harness template (`[], [42], [5, 5, 5], [int.MinValue, int.MaxValue]`) that you can mentally trace in under 90 seconds at the end of every interview.

---

## Section 13 — Data Structures & Algorithms in Enterprise Systems

### 13.1 High-Volume Rate Limiting: Sliding Window Log vs Counter

In API Gateways, rate limiting prevents resource exhaustion:
- **Token Bucket:** Allows burstiness; refills tokens at constant rate.
- **Sliding Window Counter:** Divides time into small discrete sub-windows (e.g., 1-second chunks within a 1-minute window), interpolating request rates across window boundaries. Consumes minimal memory compared to storing raw timestamps while preventing burst exploits at window boundaries.

---

### 13.2 Token Bucket & Sliding Window Counter Rate Limiters

#### Rate Limiting Algorithm Comparison Matrix
| Algorithm | Memory per Tenant | Burst Behavior | Boundary Edge-Case |
|---|---|---|---|
| **Fixed Window Counter** | $O(1)$ (1 counter + window ID) | Allows $2\times$ burst across window boundary (e.g., 100 reqs at `00:59.9` + 100 reqs at `01:00.1`). | Vulnerable to boundary stampedes. |
| **Sliding Window Log** | $O(\text{Limit})$ (stores every timestamp in a queue) | Exact sliding window enforcement. | High memory footprint at $10,000+$ RPS per tenant. |
| **Token Bucket** | $O(1)$ (`double tokens`, `long lastRefillTicks`) | Permits controlled bursts up to `BucketCapacity`, then throttles to `RefillRate`. | Smooth, industry-standard for API gateways. |
| **Sliding Window Counter** | $O(1)$ (`prevCount`, `currCount`, `windowStart`) | Approximates sliding log via weighted interpolation: $\text{est} = \text{curr} + \text{prev} \times (1 - \text{elapsedRatio})$. | $O(1)$ memory while eliminating the $2\times$ boundary spike! |

```csharp
public sealed class LockFreeTokenBucketLimiter
{
    private readonly double _capacity;
    private readonly double _tokensPerTick;
    private readonly TimeProvider _timeProvider;
    private readonly object _sync = new();
    private double _availableTokens;
    private long _lastRefillTimestamp;

    public LockFreeTokenBucketLimiter(int bucketCapacity, double refillTokensPerSecond, TimeProvider? timeProvider = null)
    {
        _capacity = bucketCapacity;
        _availableTokens = bucketCapacity;
        _timeProvider = timeProvider ?? TimeProvider.System;
        _tokensPerTick = refillTokensPerSecond / _timeProvider.TimestampFrequency;
        _lastRefillTimestamp = _timeProvider.GetTimestamp();
    }

    public bool TryAcquire(int requestedTokens = 1)
    {
        lock (_sync)
        {
            long now = _timeProvider.GetTimestamp();
            long elapsedTicks = Math.Max(0, now - _lastRefillTimestamp);

            if (elapsedTicks > 0)
            {
                _availableTokens = Math.Min(_capacity, _availableTokens + elapsedTicks * _tokensPerTick);
                _lastRefillTimestamp = now;
            }

            if (_availableTokens >= requestedTokens)
            {
                _availableTokens -= requestedTokens;
                return true;
            }

            return false;
        }
    }
}
```

---

### 13.3 Inverted Index & Vector Cosine Similarity (`TensorPrimitives.CosineSimilarity` in .NET 8/9)

Modern enterprise retrieval systems (Hybrid RAG search) combine **lexical keyword retrieval** (via an **Inverted Index** with sorted posting lists intersected via Two Pointers) and **dense semantic vector search** (computing **Cosine Similarity** across float embeddings):
$$\text{CosineSimilarity}(\mathbf{A}, \mathbf{B}) = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$

In .NET 8 and .NET 9 (`System.Numerics.Tensors`), `TensorPrimitives.CosineSimilarity(ReadOnlySpan<float> x, ReadOnlySpan<float> y)` uses SIMD hardware intrinsics (AVX-512 / AVX2 / ARM AdvSIMD) to compute dot products and norms up to $16\times$ faster than a scalar `for` loop.

```csharp
using System.Numerics.Tensors;

public sealed class HybridSearchEngine
{
    private readonly Dictionary<string, List<int>> _invertedIndex = new(StringComparer.OrdinalIgnoreCase);
    private readonly Dictionary<int, float[]> _documentEmbeddings = [];

    public void IndexDocument(int docId, string text, ReadOnlySpan<float> embedding)
    {
        _documentEmbeddings[docId] = embedding.ToArray();

        foreach (var tokenRange in text.AsSpan().Split(' '))
        {
            var token = text.AsSpan(tokenRange).Trim(".,!?;:\"'()[]");
            if (token.IsEmpty) continue;

            string word = token.ToString();
            if (!_invertedIndex.TryGetValue(word, out var postings))
            {
                postings = [];
                _invertedIndex[word] = postings;
            }

            // Maintain sorted order in posting list for O(N + M) two-pointer intersection
            if (postings.Count == 0 || postings[^1] != docId)
                postings.Add(docId);
        }
    }

    // Two-Pointer Sorted Posting List Intersection: O(|P1| + |P2|) Time
    public IReadOnlyList<int> IntersectTerms(string termA, string termB)
    {
        if (!_invertedIndex.TryGetValue(termA, out var listA) ||
            !_invertedIndex.TryGetValue(termB, out var listB))
            return [];

        List<int> intersection = [];
        int i = 0, j = 0;

        while (i < listA.Count && j < listB.Count)
        {
            if (listA[i] == listB[j])
            {
                intersection.Add(listA[i]);
                i++;
                j++;
            }
            else if (listA[i] < listB[j]) i++;
            else j++;
        }

        return intersection;
    }

    // Top-K Vector Semantic Search using .NET 8/9 SIMD TensorPrimitives + Min-Heap of size K
    public IReadOnlyList<(int DocId, float Score)> TopKSemanticSearch(ReadOnlySpan<float> queryVector, int k)
    {
        var minHeap = new PriorityQueue<int, float>(k + 1);

        foreach (var (docId, docVector) in _documentEmbeddings)
        {
            float similarity = TensorPrimitives.CosineSimilarity(queryVector, docVector);
            minHeap.Enqueue(docId, similarity);

            if (minHeap.Count > k)
                minHeap.Dequeue(); // Evict lowest similarity score in O(log K)
        }

        var results = new (int DocId, float Score)[minHeap.Count];
        for (int idx = results.Length - 1; idx >= 0; idx--)
        {
            minHeap.TryDequeue(out int docId, out float score);
            results[idx] = (docId, score);
        }

        return results;
    }
}
```

---

### Section 13 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why is the Sliding Window Counter algorithm preferred over both Fixed Window Counter and Sliding Window Log in distributed API gateways?**
> **Strong answer:** Fixed Window Counter requires only one integer per tenant, but suffers from a $2\times$ boundary burst vulnerability: a client can send 100% of their quota in the last 100ms of Window $T$ and another 100% in the first 100ms of Window $T+1$, overwhelming downstream services with double the permitted rate. Sliding Window Log eliminates this boundary spike by storing the exact timestamp of every request in a sorted set (`ZSET`), but consumes $O(R)$ memory per user, which becomes prohibitive when a tier allows 50,000 requests per hour across millions of users. Sliding Window Counter achieves the best of both worlds in $O(1)$ memory (storing just `previousWindowCount` and `currentWindowCount`) by weighting the previous window's count by the unelapsed percentage of the current window.

**Q2: How do inverted index search engines intersect two posting lists when one term is ultra-common (10,000,000 docs) and the other is rare (50 docs)?**
> **Strong answer:** A linear Two-Pointer merge scan takes $O(N + M)$ operations ($10,000,050$ comparisons). When posting list sizes are highly skewed ($N \ll M$), search engines use **Galloping (Exponential) Search** or **Skip-Pointer Binary Search**: for each of the $N = 50$ document IDs in the rare posting list, we binary-search (or exponentially jump) into the $M = 10,000,000$ posting list in $O(N \log M)$ time ($\approx 50 \times 24 = 1,200$ operations), achieving an orders-of-magnitude speedup.

#### Practical Exercises
1. **Exercise 13.1:** Implement `GallopingIntersect(ReadOnlySpan<int> smallSorted, ReadOnlySpan<int> largeSorted)` in $O(N \log M)$ time and benchmark it against the standard $O(N + M)$ two-pointer intersection when $N = 32$ and $M = 1,000,000$.
2. **Exercise 13.2:** Implement a streaming deduplicator that suppresses duplicate `MessageId` values within a rolling 5-minute window using a `Queue<(Guid Id, DateTimeOffset ExpiresAt)>` paired with a `HashSet<Guid>`.

---

## Section 14 — Integrated Assessment & Capstone

### 14.1 Capstone 1: Thread-Safe High-Concurrency Sharded LRU Cache with TTL

#### Architectural Design & Concurrency Mechanics
A single global lock around an LRU cache (`Dictionary` + `LinkedList`) becomes a severe contention bottleneck under 64-core server workloads because every cache *read* must mutate the doubly linked list's head pointer.
To achieve high-concurrency $O(1)$ throughput:
1. **Lock Striping (Power-of-Two Shards):** Partition keys across $S = 2^k$ independent `CacheShard` instances using `(uint)comparer.GetHashCode(key) & (shardCount - 1)`. Threads accessing keys in different shards never contend!
2. **Lazy TTL Expiration + Capacity Eviction:** Each node stores `long ExpiresAtTimestamp` (using `TimeProvider`). Expired entries are evicted lazily on `TryGetValue` or opportunistically during `Set`.

```csharp
using System.Numerics;

public sealed class ShardedTtlLruCache<TKey, TValue> where TKey : notnull
{
    private readonly CacheShard[] _shards;
    private readonly int _shardMask;
    private readonly IEqualityComparer<TKey> _comparer;
    private readonly TimeProvider _timeProvider;

    public ShardedTtlLruCache(
        int totalCapacity,
        int shardCount = 16,
        IEqualityComparer<TKey>? comparer = null,
        TimeProvider? timeProvider = null)
    {
        int normalizedShards = (int)BitOperations.RoundUpToPowerOf2((uint)Math.Max(1, shardCount));
        int capacityPerShard = Math.Max(1, (totalCapacity + normalizedShards - 1) / normalizedShards);

        _shardMask = normalizedShards - 1;
        _comparer = comparer ?? EqualityComparer<TKey>.Default;
        _timeProvider = timeProvider ?? TimeProvider.System;
        _shards = new CacheShard[normalizedShards];

        for (int i = 0; i < normalizedShards; i++)
        {
            _shards[i] = new CacheShard(capacityPerShard, _comparer, _timeProvider);
        }
    }

    private CacheShard GetShard(TKey key) =>
        _shards[(uint)_comparer.GetHashCode(key) & (uint)_shardMask];

    public bool TryGetValue(TKey key, out TValue value) =>
        GetShard(key).TryGetValue(key, out value);

    public void Set(TKey key, TValue value, TimeSpan ttl) =>
        GetShard(key).Set(key, value, ttl);

    private sealed class CacheShard(int capacity, IEqualityComparer<TKey> comparer, TimeProvider timeProvider)
    {
        private readonly Dictionary<TKey, LinkedListNode<Entry>> _map = new(capacity, comparer);
        private readonly LinkedList<Entry> _lruList = new();
        private readonly object _gate = new();

        private readonly record struct Entry(TKey Key, TValue Value, long ExpiresAtTicks);

        public bool TryGetValue(TKey key, out TValue value)
        {
            lock (_gate)
            {
                if (_map.TryGetValue(key, out var node))
                {
                    if (timeProvider.GetUtcNow().UtcTicks >= node.Value.ExpiresAtTicks)
                    {
                        // Lazy TTL eviction
                        _lruList.Remove(node);
                        _map.Remove(key);
                        value = default!;
                        return false;
                    }

                    _lruList.Remove(node);
                    _lruList.AddFirst(node);
                    value = node.Value.Value;
                    return true;
                }

                value = default!;
                return false;
            }
        }

        public void Set(TKey key, TValue value, TimeSpan ttl)
        {
            long expiresAt = timeProvider.GetUtcNow().Add(ttl).UtcTicks;

            lock (_gate)
            {
                if (_map.TryGetValue(key, out var existing))
                {
                    _lruList.Remove(existing);
                }
                else if (_map.Count >= capacity)
                {
                    var tail = _lruList.Last!;
                    _lruList.RemoveLast();
                    _map.Remove(tail.Value.Key);
                }

                var newNode = _lruList.AddFirst(new Entry(key, value, expiresAt));
                _map[key] = newNode;
            }
        }
    }
}
```

---

### 14.2 Capstone 2: Directed Acyclic Graph (DAG) Task Orchestrator

> **Concurrency & C# Compiler Note (`CollectionsMarshal.GetValueRefOrNullRef`):**
> A standard `Dictionary<string, int>` indexer (`inDegree[depId]`) is a property, not a storage variable, so passing `ref inDegree[depId]` to `Interlocked.Decrement` causes compiler error **`CS0206`** (*A property or indexer may not be passed as an out or ref parameter*). Because `inDegree` is fully populated with all task keys during initialization and **no keys are added or removed during parallel execution**, its internal `_entries` array is never resized. We can therefore safely obtain a direct managed reference (`ref int`) to the dictionary's internal value slot via `CollectionsMarshal.GetValueRefOrNullRef(inDegree, depId)` and decrement it atomically with `Interlocked.Decrement`!

```csharp
using System.Collections.Concurrent;
using System.Runtime.InteropServices;

public sealed class DagTaskScheduler
{
    public sealed record TaskNode(string Id, Func<CancellationToken, Task> Action, IReadOnlyList<string> DependsOn);

    public async Task ExecuteAsync(IEnumerable<TaskNode> tasks, CancellationToken ct)
    {
        var taskList = tasks.ToList();
        var taskMap = taskList.ToDictionary(t => t.Id);

        // Compute in-degrees and adjacency (key set is frozen after this point)
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
                        ref int remainingDeps = ref CollectionsMarshal.GetValueRefOrNullRef(inDegree, depId);
                        if (Interlocked.Decrement(ref remainingDeps) == 0)
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

### 14.3 Capstone 3: High-Volume Sliding Window Rate Limiter

#### Sub-Microsecond Sliding Window Counter for 100,000+ RPS
To rate-limit hundreds of thousands of concurrent tenant keys with minimal GC pressure, each tenant state uses a compact class with fine-grained per-tenant locking (or striped locks) and $O(1)$ weighted window interpolation:

```csharp
using System.Collections.Concurrent;

public sealed class SlidingWindowCounterRateLimiter
{
    private readonly int _permitLimit;
    private readonly long _windowTicks;
    private readonly TimeProvider _timeProvider;
    private readonly ConcurrentDictionary<string, TenantWindowState> _tenants = new(StringComparer.Ordinal);

    public SlidingWindowCounterRateLimiter(int permitLimit, TimeSpan windowDuration, TimeProvider? timeProvider = null)
    {
        if (permitLimit <= 0) throw new ArgumentOutOfRangeException(nameof(permitLimit));
        if (windowDuration <= TimeSpan.Zero) throw new ArgumentOutOfRangeException(nameof(windowDuration));

        _permitLimit = permitLimit;
        _timeProvider = timeProvider ?? TimeProvider.System;
        _windowTicks = (long)(windowDuration.TotalSeconds * _timeProvider.TimestampFrequency);
    }

    public bool TryAcquire(string tenantId, out int retryAfterSeconds)
    {
        long nowTicks = _timeProvider.GetTimestamp();
        var state = _tenants.GetOrAdd(tenantId, static (_, ticks) => new TenantWindowState(ticks), nowTicks);

        lock (state)
        {
            long currentWindowId = nowTicks / _windowTicks;
            long stateWindowId = state.WindowStartTicks / _windowTicks;

            if (currentWindowId > stateWindowId)
            {
                // Roll window forward: if more than 1 full window elapsed, previous count is 0
                state.PreviousWindowCount = (currentWindowId == stateWindowId + 1) ? state.CurrentWindowCount : 0;
                state.CurrentWindowCount = 0;
                state.WindowStartTicks = currentWindowId * _windowTicks;
            }

            double elapsedRatio = (double)(nowTicks - state.WindowStartTicks) / _windowTicks;
            double weightedCount = state.PreviousWindowCount * (1.0 - elapsedRatio) + state.CurrentWindowCount;

            if (weightedCount + 1.0 > _permitLimit)
            {
                long remainingTicks = _windowTicks - (nowTicks - state.WindowStartTicks);
                retryAfterSeconds = Math.Max(1, (int)Math.Ceiling((double)remainingTicks / _timeProvider.TimestampFrequency));
                return false;
            }

            state.CurrentWindowCount++;
            retryAfterSeconds = 0;
            return true;
        }
    }

    private sealed class TenantWindowState(long initialTicks)
    {
        public long WindowStartTicks { get; set; } = initialTicks;
        public int PreviousWindowCount { get; set; }
        public int CurrentWindowCount { get; set; }
    }
}
```

---

### Section 14 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why is `CollectionsMarshal.GetValueRefOrNullRef(dictionary, key)` safe to use with `Interlocked.Decrement` in our `DagTaskScheduler`, and when would it cause memory corruption?**
> **Strong answer:** `CollectionsMarshal.GetValueRefOrNullRef` returns a managed interior pointer (`ref TValue`) directly into the `Dictionary<TKey, TValue>`'s internal `_entries` struct array. In `DagTaskScheduler`, all keys are inserted into `inDegree` before any worker tasks start, and no keys are ever added or removed during execution. Because the dictionary's structure is completely read-only during the parallel phase, its `_entries` array is never reallocated or resized, making atomic `Interlocked.Decrement` on each value slot 100% thread-safe and allocation-free. However, if any concurrent thread added a new key and triggered a dictionary resize while another thread held or mutated that `ref int`, the update could write to a stale, orphaned `_entries` array or corrupt internal free-list indices.

**Q2: In `ShardedTtlLruCache`, why did we constrain `shardCount` to a power of two using `BitOperations.RoundUpToPowerOf2`?**
> **Strong answer:** Standard modulo division (`hashCode % shardCount`) compiles to an integer `div` CPU instruction, which takes 10 to 25 clock cycles even on modern x86-64/ARM64 processors. When `shardCount` is a power of two ($2^k$), `shardCount - 1` produces a contiguous bitmask of $k$ ones, allowing us to compute the shard index via a single-cycle bitwise AND operation: `(uint)hashCode & (uint)(shardCount - 1)`. Additionally, casting to `uint` first avoids negative array indices when `GetHashCode()` returns `int.MinValue` (where `Math.Abs(int.MinValue)` would throw `OverflowException`).

#### Practical Exercises
1. **Exercise 14.1:** Enhance `DagTaskScheduler` so that instead of waiting for an entire wave (`await Task.WhenAll(batch)`) before launching newly unblocked tasks, it schedules dependent tasks *immediately* as soon as their `inDegree` reaches zero, bounded by a `SemaphoreSlim(maxDegreeOfParallelism)`.
2. **Exercise 14.2:** Add a background periodic eviction timer (`PeriodicTimer`) to `SlidingWindowCounterRateLimiter` that sweeps and removes idle `TenantWindowState` entries that have received zero traffic for more than $2 \times \text{windowDuration}$, preventing unbounded dictionary growth under ephemeral IP attacks.

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
| Connected components, dynamic network connectivity, cycle detection | Disjoint Set Union (DSU) | Flat Parent & Rank Arrays | Near $O(1)$ per operation ($\alpha(n)$) |
| Find minimum capacity, speed, or threshold satisfying feasibility | Binary Search on Answer | Monotonic Feasibility Function | $O(n \log(\text{range}))$ time |
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
20. The optimal number of hash functions in a Bloom Filter is $k = \frac{m}{n} \ln 2$.
21. A Trie enables prefix searching and autocomplete in $O(L)$ time, where $L$ is word length, independent of dictionary size.
22. BST deletion requires finding the In-order Successor (smallest value in the right subtree) when deleting a node with two children.
23. Red-Black trees maintain balance via color invariants and rotations, guaranteeing max height $\le 2 \log_2(n + 1)$.
24. In a binary heap stored in a zero-indexed array, the left child of index $i$ is $2i + 1$, right is $2i + 2$, and parent is $\lfloor(i - 1)/2\rfloor$.
25. Building a heap from an unsorted array takes $O(n)$ time using Floyd's bottom-up `BuildHeap`, not $O(n \log n)$.
26. Skip Lists achieve $O(\log n)$ search, insertion, and deletion probabilistically using multi-tiered linked lists without tree rotations.
27. An Adjacency List consumes $O(V + E)$ space, making it ideal for sparse graphs; an Adjacency Matrix consumes $O(V^2)$ space.
28. Breadth-First Search (BFS) computes the shortest path on unweighted graphs in $O(V + E)$ time using a FIFO queue.
29. Topological sorting is only possible on Directed Acyclic Graphs (DAGs); Kahn's algorithm detects cycles via remaining in-degrees.
30. Dijkstra's algorithm solves single-source shortest paths in $O((V + E) \log V)$ time using a min-heap, but fails with negative weights.
31. The Bellman-Ford algorithm handles negative edge weights in $O(V \cdot E)$ time and detects negative weight cycles.
32. Disjoint Set Union (DSU) with path compression and union by rank achieves near-constant amortized time $\alpha(n)$ per operation.
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
| **Interview Leadership** | Jumps into code silently; gets defensive with hints; ignores edge cases. | Communicates while coding; handles basic edge cases with guidance. | Leads the interview methodically (Clarify $\to$ Baseline $\to$ Bottleneck $\to$ Optimize $\to$ Test); tests edge cases systematically. | Drives collaborative architectural dialogue; justifies trade-offs; adapts gracefully to shifting constraints. |

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
