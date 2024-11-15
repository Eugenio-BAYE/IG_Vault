---
title: AI_Search_Agents_EN
author: Eugénio BAYE
lecture author: Tiberiu STRATULAT
lecture: AI and Mutli-Agent Systems, Polytech Montpellier
date: 2024-11-15
update: 2024-11-15
copyright: Polytech Montpellier, Tiberiu STRATULAT
---
# AI Search Agents

## Goal-Based Agents
- **Reflex agents**: Use a *mapping* from *states* to *actions*.
- **Goal-based agents**: *Problem-solving* agents or *planning* agents.

## Goal-Based Agents
- Agents that work *towards a goal*.
- Agents consider the *impact of actions* on *future states*.
- The agent’s job is to *identify* the action or series of actions that *lead to the goal*.
- *Formalized* as a search through possible solutions.

> [!example] Maze 
> ![[Search_Agent_FIG1.png]]

> [!example] 8-queen problem
> The 8-queen problem:
>- On a chess board, place *8 queens* so that *no queen is attacking any other* vertically, horizontally or diagonally
>- Number of possible sequences to investigate:
>	- $64*63*62*...*57=10¹⁴$
> 
> ![[Search_Agent_FIG2.png]]


## Problem Solving as Search
1. *Define* the problem through:
   - **Goal formulation**: Define what the Agent is *trying to achieve*.
   - **Problem formulation**: Define the *structure* of a problem in terms that an agent can use to search for a solution
2. Solve the problem as a two-stage process:
   - *Search* "Mental" or "offline" *exploration* of several possibilities.
   - *Execute* the *solution* found (*Implement*).
> [!tip] Definition
> **Mental, offline Exploration**: Process where an *agent* *plans* and searches for a solution in a hypothetical or *simulated environment*.
>- Example: In a chess game, the AI Agent (simulated player) simulates different moves and their outcomes before choose the best move. 
>
> **Implement**: *Execution* phase where the agent carries out the *chosen plan*.
>- Example: Make the chess move
## Problem-Solving Agent
- A problem-solving agent first *formulates a goal* and a *problem*, searches for a *sequence of actions* that would solve the problem, and then *executes the actions* one at a time.
- When this is complete, it formulates *another goal and starts over*.


> [!tip] Code
> ``` java
> function SIMPLE-PROBLEM-SOLVING-AGENT(percept) returns an action`
>     `static: seq, an action sequence, initially empty`
>             `state, some description of the current world state`
>             `goal, a goal, initially null`
>             `problem, a problem formulation`
> 
>     `state ← UPDATE-STATE(state, percept)`
>     `if seq is empty then`
>         `goal ← FORMULATE-GOAL(state)`
>         `problem ← FORMULATE-PROBLEM(state, goal)`
>         `seq ← SEARCH(problem)`
>         `if seq = failure then return a null action`
>     `action ← FIRST(seq)`
>     `seq ← REST(seq)`
>     `return action`
> ```


## Problem Formulation
- **Initial state**: The state in which the agent *starts*.
- **States**: All *states reachable* from the *initial state* by any sequence of actions (state space).
- **Actions**: Possible *actions available to the agent*. At a state `s`, `Actions(s)` returns the set of actions that can be executed in state `s` (action space).
- **Transition model**: A description of what *each action does* `Result(s, a)`.
- **Goal test**: Determines if a given state is a *goal state*.
- **Path cost**: Function that *assigns a numeric cost* to a path with respect to a *performance measure*.

>[!example] 8-queen
> *States*: All arrangements of 0 to 8 queens on the board.
> *Initial State*: No queen on the board
> *Actions*: Add a queen to any empty square.
> *Transition Model*: Updates the board with a new queen placement
> *Goal Test*: 8 queens on the board with none attacking each other

> [!example] 8-Puzzle Problem
> - *States*: Location of each of the 8 tiles in the 3x3 grid.
> - *Initial State*: Any configuration of tiles.
> - *Actions*: Move tiles left, right, up, or down.
> - *Transition Model*: Given a state and an action, returns the resulting state.
> - *Goal Test*: Checks if the current state matches the goal state.
> - *Path Cost*: Each move costs 1; the total cost is the number of moves.
> ![[Search_Agent_FIG3.png]]


> [!example] Real-World Problem: Route Finding
> - *States*: `In(City)` where `City ∈ {Arad, Sibiu, ...}`.
> - *Initial State*: `In(Arad)`.
> - *Actions*: Possible moves, e.g., `Go(Sibiu)`.
> - *Transition Model*: `Result(In(Arad), Go(Sibiu)) = In(Sibiu)`.
> - *Goal Test*: `In(Bucharest)`.
> - *Path Cost*: Distance in kilometers.
> 
>  ROMANIA NUMBER ONE:
>  ![[Search_Agent_FIG4_ROMANIA_NUMBER_ONE.png]]

> [!exmaple] Real-World Problems
> 
> 1. *Route-Finding Problems*: Used in applications like Google Maps, Waze, etc., to find the best path between locations.
> 2. *Traveling Salesperson Problem (TSP)*: Finding the shortest possible route that visits each city exactly once and returns to the origin.
> 3. *VLSI Layout*: Arranging millions of components and connections on a chip to minimize area and shorten delays.
> 4. *Robot Navigation*: A special case of route finding where a robot navigates in a 2D or 3D space without predefined routes, making the state and action space potentially infinite.
> 5. *Automatic Assembly Sequencing*: Determining the order in which parts should be assembled, a complex and expensive geometric search problem.
> 6. *Protein Design*: Designing amino acid sequences that fold into a 3D structure with properties to cure diseases
## Search Algorithm Concepts
- **State space**: The set of all physical configurations.
- **Search space**: An abstract configuration represented as a search tree or graph of possible solutions.
- **Search tree**: Models the sequence of actions:
  - **Root**: Initial state.
  - **Branches**: Actions.
  - **Nodes**: Resulting states, each node has a parent, children, depth, path cost, and an associated state in the state space.
- **Expand**: A function that generates all child nodes from a given node.

> [!tip] State vs. Node
> ![[Search_Agent_FIG5.png]]

## Search Space Regions
- The search space is divided into three regions:
  1. **Explored** (Closed List, Visited Set)
  2. **Frontier** (Open List, Fringe)
  3. **Unexplored**
- The essence of a search strategy is moving nodes from unexplored to frontier to explored in a specific order.

> [!failure] Image Placeholder: Illustrate search space regions and the transition of nodes between these regions.

