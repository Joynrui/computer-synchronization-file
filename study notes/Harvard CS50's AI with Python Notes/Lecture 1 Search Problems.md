# Lecture 1 Search Problems

------*Harvard CS50's Artificial Intelligence with Python Note*

- agent: Entity that perceives its environment and acts upon that environment.  
- state: A configuration of the agent and its environment.

## Initial state

The beginning of the state.

- action: choices that can be made in a state.

>ACTION(*s*) returns the set of actions that can be executed in state *s*.

## Transition model

A description of what state results from performing any applicable action in any state.

> RESULT(*s, a*) returns the state resulting from performing action *a* in state *s*.

- state space: the set of all states reachable from the initial state by any sequence of actions.

## Goal test

A way to determine whether a given state is a goal state.

- path cost: the numerical cost associated with a given path.

**solution**: a sequence of actions that leads from the initial state to a goal state.

**optimal solution**: a solution that has the lowest path cost among all solutions.

**node**: a data structure that keeps track of

> - a state
> - a parent(node that generated this node)
> - an action(action applied to parent to get node)
> - a path cost(from initial state to node)



---

## Depth-first Search

The search algorithm always expands the deepest node in the frontier. 

- Use **Stack** data structure to implement. (FILO)

## Breadth-first Search

 The search algorithm always expands the shallowest node in the frontier.

- Use **Queue** data structure to implement. (FIFO)



## Maze Question

Give you a maze, try to find a way from the original point to the final point.

1. The basic structure of the modal:

```python
class Node():
    def __init__(self, state, parent, action):
        self.state = state
        self.parent = parent
        self.action = action

class StackFrontier():
    def __init__(self) -> None:
        self.frontier = []
    
    def add(self, node): 
        self.frontier.append(node)
    def contains_state(self, state):
        return any(node.state == state for node in self.frontier)
    def empty(self):
        return len(self.frontier) == 0
    
    def remove(self):
        if self.empty():
            raise Exception("empty frontier")
        else:
            # frontier[-1] means the last item of the frontier list
            node = self.frontier[-1]
            # "self.frontier[:-1]" removes the last item of the frontier 
            # and return the list back to self.frontier 
            self.frontier = self.frontier[:-1]
            # return the item which you removed
            return node

# format like this means QueueFrontier does same things that StackFrontier can do, 
# also called extends
class QueueFrontier(StackFrontier):
    def remove(self):
        if self.empty():
            raise Exception("empty frontier")
        else:
            node = self.frontier[0]
            # Add the changed frontier list(index from 1 to the last ) to self.frontier 
            self.frontier = self.frontier[1:]
            return node
```

2. key function:

```python
def solve(self):
    """Finds a solution to maxe, if one exists."""
    # Kepp track of number of states explored
    self.num_explored = 0
    # Initialize frontier to just the starting position
    start = Node(state=self.start, parent=None, action=None)
    # If algorithm use StackFrontier which means the used algorithm is DFS
    frontier = StackFrontier()
    frontier.add(start)
    
    # Initialize an empty explored set
    self.explored = set()
    
    # Keep looping until solution found
    while True:
        # If nothing left in frontier, then no path
       	if frontier.empty():
            raise Exception("no solution")
        # Choose a node from the frontier
        node = frontier.remove()
        self.num_explored += 1
        
        # goal test
        # If node is the goal, then we have a solution
        if node.state == self.goal:
            action = []
            cells = [] 
            
            # Follow parent nodes to find solution
            while node.parent is not None:
                action.append(node.action)
                cells.append(node.state)
                node = node.parent
            action.reverse()
            cells.reverse()
            self.solution = (actions, cells)
            return
```



## Uninformed search

The search strategy uses no problem-specific knowledge.



## Informed search

the search strategy uses problem-specific knowledge to find solutions more efficiently.



## Greedy best-first search

The search algorithm expands the node that is closest to the goal, as estimated by a heuristic function `h(n)`.

heuristic function: proceeding to a solution by trial and error or by rules that are only loosely defined.

## A* search

search algorithm that expands node with  lowest value of `g(n) + h(n)`.

`g(n)`: cost to reach node

`h(n)`: estimated cost to goal 

- Optimal if
    - `h(n)` is admissible (never overestimates the true cost), and
    - `h(n)` is consistent (for every node n and successor n' with step cost c, `h(n) ≤ h(n') + c`)



___



## Adversarial search

Adversarial search is used to find a way to win state for the agent itself. Also means defeating the adversary agent.

## Minimax

The Minimax Algorithm is used to solve the adversarial search problem. 

Minimax has two functions:

- `MAX(X)`: aims to maximize score.
- `MIN(O)`: aims to minimize score.



We have a game to learn the minimax algorithm:

The game has five functions:

- S1: initial state
- `PLAYER(s)`: returns which player to move in state s
- `ACTIONS(s)`: returns legal moves in state s
- `RESULT(s, a)`: returns state after action a taken in state s
- `TERMINAL(s)`: checks if state s is a terminal state
- `UTILITY(s)`: final numerical value for terminal state 



The problem-handling logic of the Minimax uses the following methods:

- Given a state *s*:
    - `MAX` picks action *a* in `ACTIONS(s)` that produces highest value of `MIN-VALUE(RESULT(s, a))`
    - `MIN` picks action *a* in `ACTION(s)` that produces smallest value of `MAX-VALUE(RESULT(s, a))`

`MAX-VALUE(state)` like this:

```python
function MAX-VALUE(state):
    if TERMINAL(state):
        return UTILITY(state)
    v = negativeInfinity
    for action in ACTIONS(state):
        v = MAX(v, MIN-VALUE(RESULT(state, action)))
    return v
```

`MIN-VALUE(state)` like this:

```python
function MIN-VALUE(state):
    if TERMINAL(state):
        return UTILITY(state)
    v = infinity
    for action in ACTIONS(state):
        v = MAX(v, MAX-VALUE(RESULT(state, action)))
    return v
```



---



## Optimization

...



## Alpha-Beta Pruning

...



## Depth-Limited Minimax

...

## Evaluation function

The function that estimates the expected utility of the game from a given state.