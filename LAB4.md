# Lab 04: Hill-Climbing Search with the N-Queens Problem

Implementation of Hill-Climbing and Random-Restart algorithms to solve the N-Queens problem.

## 1. Objective

The objective of this lab is to implement Hill-Climbing and Random-Restart Hill-Climbing algorithms in Python and apply them to the N-Queens problem.

The lab explores local search, evaluation functions, neighboring states, local maxima, and the effect of restarting the search from different random initial states.

## 2. Problem Description

The N-Queens problem requires placing N queens on an N × N chessboard so that no two queens attack each other.

Queens attack each other when they share:

- The same row.
- The same column.
- The same diagonal.

A valid solution has zero attacking pairs.

## 3. State Representation

The board is represented using a Python list.

For example:

```python
state = [1, 3, 0, 2]
```

The index represents the column, and the value represents the row where the queen is placed.

This representation automatically ensures that each column contains exactly one queen.

## 4. Tasks Completed

### Task 1: State Representation

Created a Python list to represent the positions of queens and printed the state.

### Task 2: Random Initial State

Implemented `random_state(n)` to generate a random row position for each queen.

### Task 3: Conflict Counting

Implemented `count_conflicts(state)` to count pairs of queens attacking each other.

The function checks:

- Same-row conflicts.
- Diagonal conflicts.

### Task 4: Evaluation Function

Implemented the evaluation function:

\[
Evaluation(state)=-count\_conflicts(state)
\]

A higher score is better, and zero represents a valid solution.

### Task 5: Neighbor Generation

Implemented `get_neighbors(state)` to generate all possible states obtained by moving one queen to another row in the same column.

The number of neighbors is:

\[
N(N-1)
\]

For N = 8:

\[
8(8-1)=56
\]

### Task 6: Basic Hill-Climbing

Implemented `hill_climbing(n)`.

The algorithm:

1. Generates a random initial state.
2. Evaluates the current state.
3. Generates neighboring states.
4. Selects the neighbor with the highest evaluation score.
5. Moves to that neighbor if it improves the score.
6. Stops when no better neighbor exists.

### Task 7: Running Basic Hill-Climbing

Tested the algorithm with eight queens and checked whether the final state had zero conflicts.

### Task 8: Chessboard Visualization

Implemented `print_board(state)` to display the queen positions using:

- `Q` for a queen.
- `.` for an empty position.

### Task 9: Evaluation Graph

Used Matplotlib to plot the evaluation score over the iterations of a single Hill-Climbing run.

The graph shows how the algorithm improves its current state and where it terminates.

### Task 10: Different Board Sizes

Tested the algorithm with N = 4, 8, 10, and 12.

Repeated experiments were performed for N = 4, N = 8, and N = 10 to observe how random starting states affect the results.

**Experimental results using random seed 42:**

| N | Run | Final Conflicts | Iterations | Solved? |
|---:|---:|---:|---:|---|
| 4 | 1 | 1 | 2 | No |
| 4 | 2 | 0 | 3 | Yes |
| 8 | 1 | 0 | 6 | Yes |
| 8 | 2 | 2 | 3 | No |
| 8 | 3 | 1 | 3 | No |
| 10 | 1 | 1 | 3 | No |
| 10 | 2 | 1 | 7 | No |
| 10 | 3 | 2 | 4 | No |

**Observation:** The same board size can produce different results because each run may start from a different random state.

### Task 11: Random-Restart Hill-Climbing

Implemented `random_restart_hill_climbing(n, max_restarts=100)`.

The algorithm repeatedly starts basic Hill-Climbing from new random states until:

- A valid solution is found, or
- The maximum restart limit is reached.

It also keeps track of the best state found during the attempts.

### Task 12: Running Random-Restart Hill-Climbing

Tested Random-Restart Hill-Climbing with eight queens and checked the final number of conflicts and restarts performed.

### Task 13: Random-Restart Progress Graph

Used Matplotlib to plot the best evaluation score found so far after each restart.

The graph shows how the best-known solution improves across repeated attempts.

### Task 14: Comparison of Both Algorithms

Both algorithms were tested five times using eight queens.

**Experimental results using random seed 123:**

| Run | Basic Conflicts | Basic Iterations | Basic Solved? | Random-Restart Conflicts | Restarts | Solved? |
|---:|---:|---:|---|---:|---:|---|
| 1 | 1 | 6 | No | 0 | 7 | Yes |
| 2 | 1 | 5 | No | 0 | 7 | Yes |
| 3 | 0 | 4 | Yes | 0 | 1 | Yes |
| 4 | 2 | 4 | No | 0 | 8 | Yes |
| 5 | 2 | 3 | No | 0 | 7 | Yes |

**Observation:** Basic Hill-Climbing found a solution in one of five runs, while Random-Restart found a solution in all five runs in this experiment.

### Task 15: Extension Task (N = 20)

Extended the experiment to a board containing 20 queens.

**Experimental results using random seed 2026:**

| Algorithm | Run | Final Conflicts | Iterations / Restarts | Solved? |
|---|---:|---:|---:|---|
| Basic Hill-Climbing | 1 | 4 | 8 iterations | No |
| Basic Hill-Climbing | 2 | 2 | 11 iterations | No |
| Basic Hill-Climbing | 3 | 2 | 9 iterations | No |
| Random-Restart | 1 | 0 | 43 restarts | Yes |
| Random-Restart | 2 | 0 | 39 restarts | Yes |
| Random-Restart | 3 | 0 | 33 restarts | Yes |

**Observation:** Random-Restart found valid solutions in all three example runs, while basic Hill-Climbing stopped with remaining conflicts.

## 5. Lab Questions and Answers

### Q1. What is the purpose of the evaluation function in Hill-Climbing?

The evaluation function measures the quality of a state. In this lab, it counts attacking pairs of queens and returns the negative of that number. Hill-Climbing uses this score to select better neighboring states.

### Q2. Why is an evaluation score of zero the best result?

A score of zero means there are no attacking pairs of queens. Therefore, the N-Queens problem has been solved.

### Q3. What is the difference between a local maximum and a global maximum?

A local maximum is a state whose score is at least as high as the scores of its immediate neighbors. A global maximum is the highest possible score in the entire search space.

### Q4. Why can basic Hill-Climbing stop without finding a solution even when a solution exists?

It only examines neighboring states and stops when none improves the current score. A solution may exist elsewhere, but reaching it may require temporarily moving to a worse state.

### Q5. Does reaching a local maximum always mean that the algorithm has failed?

No. If the local maximum is also the global maximum, the algorithm has succeeded. In this lab, a score of zero represents success. A negative local maximum means the algorithm stopped without solving the puzzle.

### Q6. For N = 8, how many neighbors does each state have?

Each of the eight queens has seven alternative rows:

\[
8(8-1)=56
\]

Therefore, each state has 56 neighbors.

### Q7. What does the evaluation-score graph tell you?

It shows how the evaluation score changes during the search. The score increases with accepted moves and stops changing when no better neighbor exists. A final score of zero indicates a solution.

### Q8. Explain probabilistic completeness in your own words.

Probabilistic completeness means that if a solution exists and each independent attempt has a nonzero probability of finding it, the probability of finding a solution approaches 100% as the number of attempts increases.

### Q9. Why does Random-Restart improve the chance of finding a solution?

It starts Hill-Climbing from different random initial states. This provides additional opportunities to avoid unsuccessful local maxima and find a valid solution.

### Q10. Does probabilistic completeness guarantee a solution within 100 restarts?

No. It describes how the probability of success increases as the number of independent attempts grows. A fixed limit of 100 restarts can still result in failure.

## 6. Additional Analysis

### Hill-Climbing vs. Random-Restart Hill-Climbing

| Basic Hill-Climbing | Random-Restart Hill-Climbing |
|---|---|
| Uses one initial state | Uses multiple random initial states |
| Stops when no better neighbor exists | Can restart after an unsuccessful run |
| May get stuck at a non-goal local maximum | Provides additional opportunities to find a solution |
| Uses fewer attempts | May require multiple restarts |
| Does not guarantee a solution | Improves the probability of finding a solution |

### Local Search vs. Traditional Search

Traditional search algorithms such as BFS, DFS, and A* explore states to find a path to a goal.

Local search focuses on improving the current state rather than finding a path. Hill-Climbing is an example of local search because it repeatedly moves to a better neighboring state.

## 7. Conclusion

In this lab, I implemented Hill-Climbing and Random-Restart Hill-Climbing and tested using the N-Queens problem.

The experiments demonstrated that basic Hill-Climbing can stop at a non-goal local maximum even when a valid solution exists.

Random-Restart Hill-Climbing improves the probability of finding a solution by starting new searches from different random states.

The experiments also demonstrated how evaluation functions, neighboring states, and repeated randomized searches are used in local search algorithms.

**Key Takeaway:** Hill-Climbing improves the current state until no better neighbor is available. Random restarts provide additional opportunities to find a valid solution, but they do not guarantee success within a fixed number of attempts.
