# N-Queens Local Search Solver

This repository contains Python implementations of various local search algorithms—specifically Hill Climbing variants—to solve the classic N-Queens problem. The project includes an experimental comparison of their performance metrics (success rate, average time, and average steps) for N=20.

## The N-Queens Problem

The N-Queens problem is the challenge of placing N non-attacking queens on an N x N chessboard. This means no two queens can share the same row, column, or diagonal.

## Algorithms Implemented

This project compares three algorithms:

1.  ### Basic Hill Climbing
    * **Strategy:** At each step, the algorithm moves to a neighbor (a state with one queen moved) that results in the lowest possible number of conflicts.
    * **Tie-breaking:** If multiple neighbors share the minimum conflict count, one is chosen uniformly at random.
    * **Limitation:** Prone to getting stuck in local minima.

2.  ### Hill Climbing with Random Restarts
    * **Strategy:** Runs the Basic Hill Climbing algorithm. If it gets stuck in a local minimum (a state where no neighbor is better), the process is restarted from a new, randomly generated board.
    * **Goal:** Attempts up to K random restarts (where K=10 and K=100 were tested) to find a global optimum (a zero-conflict state).

3.  ### Stochastic Hill Climbing
    * **Strategy:** Instead of looking for the best neighbor, it selects a move uniformly at random from the set of **improving neighbors** (neighbors with strictly fewer conflicts than the current state).
    * **Benefit:** Allows the search to occasionally follow less steep paths, potentially avoiding some local minima compared to basic Hill Climbing.

## How to Run

The code is contained in a single Jupyter notebook, `CS404_HW2_Elif_Zorlu.ipynb`.

1.  Ensure you have Python installed, along with the standard libraries (`random`, `time`, `math`, etc.).
2.  Open the notebook in a Jupyter environment (e.g., JupyterLab or Google Colab).
3.  Execute all cells to run the experiments for N=20 over 100 runs.

## Experimental Results (N=20, 100 Runs)

The following results were obtained from the final execution cell in the notebook:

| Algorithm | Success Rate (out of 100) | Average Time (s) | Average Steps (per run) |
| :--- | :--- | :--- | :--- |
| **Basic Hill Climbing** | 5 | 0.114 | 9.27 |
| **Random Restart (K=10)** | 15 | 1.056 | 86.61 |
| **Random Restart (K=100)** | 83 | 5.189 | 427.46 |
| **Stochastic Hill Climbing** | 2 | 0.183 | 15.85 |

### Key Observations

* **Random Restart (K=100)** achieved the highest success rate (83%), confirming that restarting the search effectively overcomes local minima, though at the cost of significantly higher total steps and time.
* **Basic Hill Climbing** and **Stochastic Hill Climbing** had low success rates for N=20, indicating that the search landscape for this problem size is highly rugged with many local minima.
* **Stochastic Hill Climbing** performed poorly in terms of success rate (2%), suggesting that for the N=20 landscape, the randomized choice among improving moves was less effective than finding the steepest descent.

---
