# Grandpa Transit Puzzle Solver

A graph-theory based solution to the classic **Grandpa Transit Puzzle**, in which a traveler must navigate a complex transportation network using only a single paid fare and a sequence of valid free transfers.

---

## Overview

This project models the famous **Grandpa Transit Puzzle** as a graph search problem.

The original puzzle describes a transportation network in Lignite County, Pennsylvania, around 1910. Villages are connected by different transportation lines operated by three different companies:

* Red Company
* Blue Company
* Green Company

Each connection also belongs to one of four transportation types:

* Horse Car
* Cable Car
* Trolley
* Bus

The challenge is to determine whether Grandpa can travel from **Startsburg** to **Endenville** while paying only a single fare and using only valid transfer rules afterward.

---

## Problem Description

The transportation system allows free transfers under specific conditions:

1. A passenger may transfer between lines operated by the same company.
2. A passenger may transfer between lines of the same transportation type, even if operated by different companies.
3. Transfers are allowed only at village centers.
4. A passenger may not immediately reverse direction on the same line that was used to enter a village.

The goal is to find a valid route satisfying all transfer constraints while minimizing paid travel.

---

## Graph Modeling

The transportation network is modeled as an undirected graph.

### Vertices

Each village is represented as a graph node.

```text
Village -> Graph Vertex
```

### Edges

Each transportation connection is represented as a graph edge.

Every edge contains:

* Source village
* Destination village
* Company color
* Transportation type
* Unique edge identifier

Example:

```python
(0, 1, 'red', 1, 'cable')
```

Meaning:

```text
Village 0 <--> Village 1
Company: Red
Type: Cable Car
Edge ID: 1
```

---

## Data Extraction

The original map image was not suitable for reliable OCR processing.

Therefore, all graph information was manually extracted from the transportation map and encoded into Python data structures.

The extracted information includes:

* Village identifiers
* Edge connections
* Company colors
* Transportation types
* Edge weights/identifiers

---

## Data Validation

To reduce the possibility of human error during manual extraction, an automatic verification step was implemented.

The algorithm:

1. Sorts all edges by identifier.
2. Extracts every edge number.
3. Generates the expected range of identifiers.
4. Detects missing identifiers.

Example:

```python
expected_weights = set(range(1, 71))
actual_weights = set(weights)

missing_weights = expected_weights - actual_weights
```

This validation confirms that no edge was accidentally omitted during data entry.

---

## Simplified Representation

For easier processing, company names and transportation types were encoded using short symbolic values.

### Company Codes

| Code | Company |
| ---- | ------- |
| r    | Red     |
| b    | Blue    |
| g    | Green   |

### Transportation Codes

| Code | Type      |
| ---- | --------- |
| h    | Horse Car |
| c    | Cable Car |
| t    | Trolley   |
| b    | Bus       |

This significantly simplifies graph construction and traversal.

---

## Algorithm

The solution uses a recursive graph exploration strategy.

### Road Class

Stores edge information:

```python
class Road:
    def __init__(self, company='.', road_type='.'):
        self.company = company
        self.type = road_type
```

### Node Class

Represents a search state:

```python
class Node:
```

Each node stores:

* Current village
* Parent node
* Search depth
* Child states

The graph is explored recursively by generating all reachable neighboring villages.

---

## Search Procedure

1. Build the graph from transportation data.
2. Construct adjacency relationships.
3. Start from Startsburg.
4. Recursively explore reachable villages.
5. Track visited transitions.
6. Continue until Endenville is found.
7. Reconstruct the discovered path.

Pseudo-code:

```text
Start at Startsburg

while destination not found:

    explore neighboring villages

    generate child states

    continue recursively

return path
```

---

## Project Structure

```text
project/
│
├── GrandpaTransitMap.jpg
├── solver.py
├── README.md
└── results/
```

---

## Output

The algorithm produces a complete route from the starting village to the destination village.

Example:

```text
Path to node 35:
[0, 1, 0, 1, 0, 1, ... , 35]
```

The resulting path demonstrates that a route exists connecting Startsburg to Endenville through a sequence of legal transfers.

---

## Graph Theory Perspective

This project can be viewed as a:

* Graph Traversal Problem
* State Space Search Problem
* Transportation Network Optimization Problem
* Constraint-Based Path Finding Problem

The transportation rules create constraints on graph transitions, making the problem more interesting than a standard shortest-path search.

---

## Technologies Used

* Python
* Graph Modeling
* Recursive Search
* State Space Exploration

---

## Educational Value

This project demonstrates:

* Real-world graph modeling
* Manual data extraction and validation
* Recursive search algorithms
* Transportation network analysis
* Constraint-based path finding

It is a useful example of how a seemingly recreational puzzle can be transformed into a formal graph theory problem and solved computationally.

---

## Author

**Shayan Rokhva**
