# [Lecture 0-Search Problem](https://cs50.harvard.edu/ai/2020/weeks/0/)

## search

- agent

  An entity that perceives its environment and acts upon that environment. In a navigator app, for example, the agent would be a representation of a car that needs to decide on which actions to take to arrive at the destination.

- state

  - initial state
    The state from which the search algorith starts.In a navigator app, that would be the current location

- actions
  More precisely,actions can be defined as a function. Upon receiving state $s$ as input, $Action(s)$ returns as output the set of actions that can be executed in state $s$. 

- trasition model
  More precisely, the transition model can be defined as a function. Upon receiving state $s$ and action $a$ as input, $Results(s,a)$ returns the state resulting from performing action $a$ in state $s$.

- goal test
  The condition that determines whether a given state is a goal state

- path cost function
  A numerical cost associated with a given path.

## solving search problems

### Depth-First Search(DFS)

search algorithm that always expands the deepest node in the frontier

#### node

a data structure that keep tracks of

- a state
- a parent(node that generated this node)
- an action(action applied to parent to get node)
- a path cost(from initial state to the node)

#### approach

- startinf with a **frontier** that contains the initial state.
- repeat:
  1. If the **frintier** is empty,then no solution
  2. Remove a node from the **frontier**
  3. If node contains goal state,return the solution
  4. Expand node,add resulting nodes to the **frontier**

#### revised approach

- start with a **frontier** that contains initial state
- start with an empty explored set
- repeat:
  1. If the **frintier** is empty,then no solution
  2. Remove a node from the **frontier**
  3. If node contains goal state,return the solution
  4. add the node to the explored seet
  5. expand node, add resulting nodes to the frontier if they aren't already in the **frontier** or the explored set 

#### stack(used to structure frontier)

last-in first-out data type  

#### code example:

```py
# Define the function that removes a node from the frontier and returns it.
    def remove(self):
    	  # Terminate the search if the frontier is empty, because this means that there is no solution.
        if self.empty():
            raise Exception("empty frontier")
        else:
        	  # Save the last item in the list (which is the newest node added)
            node = self.frontier[-1]
            # Save all the items on the list besides the last node (i.e. removing the last node)
            self.frontier = self.frontier[:-1]
            return node
```



### Breadth-First Search(BFS)

search algorithm that always expands the **shallowest** node in the frontier

#### queue(instead of stark)

first-in first-out data type 

#### code example:

```py
# Define the function that removes a node from the frontier and returns it.
    def remove(self):
    	  # Terminate the search if the frontier is empty, because this means that there is no solution.
        if self.empty():
            raise Exception("empty frontier")
        else:
            # Save the oldest item on the list (which was the first one to be added)
            node = self.frontier[0]
            # Save all the items on the list besides the first one (i.e. removing the first node)
            self.frontier = self.frontier[1:]
            return node
```



### uninformed search(like BFS and DFS)

search strategy that uses **no problem-specific knowledge**

### informed search

search strategy that uses **problem-specific knowledge** to find solutions more efficiently

### greedy best-first search

search algorithm that expands the node that is closest to the goal, extimated by a **heuristic function** *h(n)*

### A* search

search algorithm that expands node with lowest valus of $g(n)+h(n)$, a developent of the *greedy best-first* algorithm.

$g(n)$=cost to reach node

$h(n)$=estimated cost to goal

optimal if

- $h(n)$ is admissible (never overestimates the true cost), and
- $h(n)$ is consistent (for every node n and successor n' with step cos c, $h(n)\le h(n')+c$)

## Adversarial Search

### Minimax

- $MAX(x)$ aims to maximize score

- $MIN(O)$ aims to minimize score

**Game**:

- $S_0$ :initia state
- $PLAYER(s)$:returns which player to move in state $s$
- $ACTION(s)$:returns legal moves in state $s$
- $RESULt(s,a)$:returns state after action $s$ taken in state $s$
- $TERMINAL(s)$:checks if state $s$ is a terminal state
- $UTILITY(s)$:final numerical value for terminal state $s$

Given a state s:

- $MAX$ picks action $a$ in $ACTION(s)$ that produces highest value of $MIN-VALUE(RESULT(s,a))$
- $MIN$ picks action $a$ in $ACTION(s)$ that produces smallest value of $MAX-VALUE(RESULT(s,a))$

**function $MAX-VALUE(state)$**:
	if  $TERMINAl(state)$:
		return $UTILITY(state)$
	$v=-\infin$
	for action in $ACTION(state)$:
		$v=MAX(v,MIN-VAlUE(RESULT(state,action)))$
	return $v$

**functiom $MIN-VALUE(state)$**
	if  $TERMINAL(state)$:
		return $UTILITY(state)$
	$v=\infin$
	for action in $ACTION(state)$:
		$v=MIN(v,MAX-VALUE(RESULT(state,action)))$
	return $v$

![Minimax in Tic Tac Toe](https://cs50.harvard.edu/ai/2020/notes/0/minimax_tictactoe.png)

**Alpha-Beta Pruning**

A way to optimize **Minimax**, **Alpha-Beta Pruning** skips some of the recursive computations that are decidedly unfavorable. 

### Depth-Limited Minimax

**evaluation function**:

function that extimates the expected utility of the game from a gven state. **Depth-limited Minimax** considers only apre-defined number of moves before it stops, without ever getting to a terminal state. *Depth-limited Minimax* relies on an evaluation function that estimaates the expected utility of the game from a given state, or, in other word, assigns values to states.  





​		

















