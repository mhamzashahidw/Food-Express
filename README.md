# 🚴 FoodExpress Dispatch Optimization Engine

A high-performance, console-driven logistics and route optimization system built in C++. This project simulates an enterprise-grade food delivery dispatch grid (modeled around a 15-node mapping of Lahore), using complex, non-linear data structures to handle priority order scheduling, real-time load balancing, driver allocation, and historical rollbacks.

---

## 🛠️ Data Structures & Complexity Matrix

This platform moves away from standard STL containers, implementing native memory-managed data structures optimized for real-time transactional throughput:

| Module | Core Data Structure | Algorithmic Mechanism | Time Complexity |
| :--- | :--- | :--- | :--- |
| **Order Scheduling** | `Max-Heap` (Priority Queue) | Bubble-Up / Bubble-Down on composite scores (Priority + Deadline Aging) | O(\log n) |
| **Kitchen Balancing** | `Circular Queue` | Fixed-array boundary pointers with modulo arithmetic wrappers | O(1) |
| **Rider Fleet Pool** | `Singly Linked List` | Runtime node chains filtering multi-variable constraint matches | Insertion: O(1) <br> Search: O(n) |
| **Route Optimization** | `Adjacency Matrix Graph` | Dijkstra's Pathfinding calculating true shortest distance in kilometers | O(V^2) |
| **Search Directory** | `Chained Hash Table` | Polynomial rolling hash indexing with linked collision resolution | Average: O(1) <br> Worst: O(n) |
| **State Undo Matrix** | `Array-Backed Stack` | LIFO transactional tracking for historical status rollbacks | O(1) |

---

## 📂 System Architecture Blueprint

The monolithic architecture insulates structural components logically to mimic decoupled database layouts:

```text
├── Entity Management (Profile Primities)
│   ├── Customer       # Insulates tier categories (Regular, Premium, VIP)
│   ├── Rider          # Fleet states tracking current workload capacity limits
│   ├── Restaurant     # Enforces maximum concurrent kitchen threshold capacities
│   └── Order          # Structural data model containing priorities and deadlines
├── Algorithmic Core Data Structures
│   ├── OrderPriorityQueue     # Max-Heap handling high-frequency priority escalations
│   ├── KitchenCircularQueue   # Non-shifting ring buffer tracking kitchen backlogs
│   ├── RiderLinkedList        # Linear chain evaluating optimal workload distributions
│   ├── CityRouteGraph         # Adjacency matrix grid driving Dijkstra routing pipelines
│   ├── SearchHashTable        # Low-latency directory parsing string keys via index hashes
│   └── OrderHistoryStack      # LIFO log capturing multi-state transaction rollbacks
└── Analysis Engines
    ├── PerformanceAnalyzer    # Mathematical simulator tracking structural scalability
    └── FoodExpressSystem      # Master aggregator orchestrating flat-file I/O synchronization
