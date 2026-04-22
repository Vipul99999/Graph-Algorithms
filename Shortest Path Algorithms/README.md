Here are the main shortest path algorithms for graphs, and when to use each.

**1. BFS**
Use when all edges have the same weight, or the graph is unweighted.

* Finds shortest path by number of edges
* Time: **O(V + E)**
* Very simple and fast

Example use:

* Fewest hops in a social network
* Shortest moves in a grid where each move costs the same

**2. Dijkstra’s Algorithm**
Use when edge weights are non-negative.

* Finds shortest path from one source to all nodes
* Greedy algorithm
* Time:

  * **O(V²)** with array
  * **O((V + E) log V)** with priority queue

Good for:

* Road networks
* Routing where distances or costs are never negative

Limitation:

* Does **not** work correctly with negative edge weights

**3. Bellman–Ford**
Use when edges may have negative weights.

* Finds shortest path from one source to all nodes
* Can detect negative cycles
* Time: **O(VE)**

Good for:

* Graphs with penalties, gains, or credits
* Situations where negative edges matter

Limitation:

* Slower than Dijkstra

**4. Floyd–Warshall**
Use when you need shortest paths between **every pair** of vertices.

* Dynamic programming approach
* Time: **O(V³)**
* Works with negative edges, but not negative cycles

Good for:

* Dense graphs
* All-pairs shortest path problems

Limitation:

* Expensive for large graphs

**5. Johnson’s Algorithm**
Use for all-pairs shortest paths on sparse graphs, especially with negative edges but no negative cycles.

* Reweights edges
* Runs Bellman–Ford once, then Dijkstra from each node
* Faster than Floyd–Warshall on sparse graphs

**6. A***
Use when you want shortest path from source to target and have a good heuristic.

* Like Dijkstra, but guided toward the goal
* Often much faster in practice
* Optimal if heuristic is admissible

Good for:

* Maps
* Games
* Pathfinding on grids

## Quick selection guide

* **Unweighted graph** → BFS
* **Weighted, no negative edges** → Dijkstra
* **Negative edges possible** → Bellman–Ford
* **All-pairs shortest paths** → Floyd–Warshall
* **All-pairs on sparse graph** → Johnson
* **Single target with heuristic** → A*

## Comparison table

| Algorithm      |          Weighted? | Negative edges? | All-pairs? |                     Time |
| -------------- | -----------------: | --------------: | ---------: | -----------------------: |
| BFS            | No / equal weights |              No |         No |                 O(V + E) |
| Dijkstra       |                Yes |              No |         No |         O((V + E) log V) |
| Bellman–Ford   |                Yes |             Yes |         No |                    O(VE) |
| Floyd–Warshall |                Yes |             Yes |        Yes |                    O(V³) |
| Johnson        |                Yes |             Yes |        Yes | Better for sparse graphs |
| A*             |                Yes |      No usually |         No |     Depends on heuristic |

## Core idea differences

* **BFS** explores level by level
* **Dijkstra** always expands the currently cheapest known node
* **Bellman–Ford** repeatedly relaxes all edges
* **Floyd–Warshall** builds answers for all pairs using intermediate nodes
* **A*** uses estimated distance to goal to guide search

## Common interview point: relaxation

Many shortest path algorithms use **relaxation**:

For an edge `(u, v)` with weight `w`:

* if `dist[u] + w < dist[v]`
* then update `dist[v]`

That is the key step in Dijkstra, Bellman–Ford, and others.

## Example

For edges:

* A → B = 4
* A → C = 1
* C → B = 2

Shortest path from A to B is:

* direct: 4
* through C: 1 + 2 = 3

So the shortest path is **A → C → B** with cost **3**.

