---
share: "true"
---

## Identifying a search problem
A typical search problem will consist of these elements:

- initial state
- actions: all available actions. The solution space
- transition model: a function that returns the state after an action is taken
- goal test: how do I know I have reached the goal
- path cost: use to find an optimize path

## Solving search problems
Defining support structures:
#### Node
- state
- parent
- action
- path cost: from initial state
#### Frontier
A collection of nodes that we can explore from the current state
### Naive Approach
1. Start with a frontier that contains the initial state
2. Loop:
	1. If the frontier is empty => no solution
	2. Remove a node from the frontier
	3. If removed node is the goal => apply goal test => return
	4. Add neighbors of the removed node to the frontier
Problems that are not handled:
1. Loops in the graph => infinite loop
	Solution: Add explored node into a set to check if we have visited it
2. How to choose which node to remove from the frontier:
	Solution: **Use a queue for BFS, stack for DFS**

## Informed search
### Greedy Best-First-Search
Idea: use a heuristic function (h(n)) to reason which path is better
Pitfall: h(n) may increase later into the path of the lower value
### A* Search
Idea: Add a function g(n) that evaluates cost to reach node, then use g(n) + h(n) to choose node
Pitfall: only optimal if:
- h(n) nevers overestimates
- h(n) needs to be consistent => cost of previous step <= cost of this step + step cost'

# Adversarial search
Example problem: tic-tac-toe
### Minimax
Idea: 
- maximize or minimize the score
- Recursively evaluate next state as the *opposite* player, assuming both sides play optimally
Must define:
- Init state
- player(state): whose turn is this
- result(state): transition into a new state
- terminal(state): has the game ended
- action(state): available action

Pitfall and improvement:
- Action tree can be huge => alpha-beta pruning => Keep track of min-max of current path to terminate paths early
- Limit the depth of search => Need an estimation function for terminal value