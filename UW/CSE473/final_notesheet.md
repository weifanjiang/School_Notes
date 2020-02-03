# CSE 473 Final Notesheet

<h2>Overview</h2>
AI is the science of making machines which <b>acts rationaly</b>: maximize expected utility.

Agent: entity that preceives and acts:
* Reflex agent: act on how the world IS (no predictions)
* Goal based agent: act on how the world would be (must have a model on how the world would evolve in response to actions)
* Utility based agents: act on how the world would likely be (reason about probability of outcomes)

Environments:
* Fully/partially observe
* Single/Multi agent
* Deterministic/Stochastic: is there uncertainty how the world works?
* Episodic (next action doesn't depend on previous)/Sequential
* Discrete/Continuous: finite number of possible environment states

<h2>Search</h2>
Search through a problem space:
* input:
    * Set of problem space
    * start/end state
    * transition function
    * goal test
* output: path between start state and goal

General Tree Search Algorithm:
```
add start node to fringe
keep do:
    if there are no candidate to expand:
        return false
    get a node from fringe by strategy
    if the node is goal:
        return node
    expand the node and add to the fringe
```
Search-question properties:
* Complete: gaurantees to find solution
* Optimal: gaurantees to find least-cost path
* Time/space complexity

Depth-first Search:
* Expand deepest node first/fringe is LIFO stack
* Time: `O(b^m)`, Space: `O(bm)`, Complete, not optimal

Breadth-first Search:
* Expand shallowest node first/fringe is FIFO stack
* Time: `O(b^d)`, Space: `O(b^d)`, Complete, optimal(if each edge has same cost)

Iterative Deepening:
* Perform DFS with maximum depth 1, 2, 3...
* Some redundent work, but Optimal and saves space

Uniform Cost Search:
* Expand cheapest node first/fringe is Priority Queue (Dijkstra)
* Complete and Optimal

A* Search:
* Combine USC and Greedy (expand on node which is closer to the goal)
* Heuristic: estimate of cost to goal
    * admissible (optimistic): estimated cost <= actual cost
    * dominance of heuristics: greater estimate on every state
    * Consistency of heuristics: heuristic arc <= actual cost<br />
     `h(c) - h(a) <= true cost from a to c`<br />
    * Consistency implies admissibility
* Tree Search: optimal if heuristic is admissible
* Graph Search: optimal if heuristic is consistent

