
# Minimum Edit Distance Visualizer & Solver

A Python-based interactive tool that calculates the **Minimum Edit Distance (Levenshtein Distance)** between two strings. It visualizes the Dynamic Programming (DP) matrix and backtracks to output the exact sequence of edit operations (Insertions, Deletions, and Substitutions) required to transform the source string into the destination string.

## Features

- **Dynamic Programming Table Visualization**: Prints an aligned grid representing the `dp` state table with custom dimensions for arbitrary inputs.
- **Optimal Alignment Backtracking**: Resolves and lists the exact step-by-step operations (`Insert`, `Delete`, `Substitute`, or `Ignore`).
- **Customizable Costs**: Currently configured with standard edit weights:
  - **Insertion**: Cost of 1
  - **Deletion**: Cost of 1
  - **Substitution**: Cost of 2 (Standard Levenshtein metric)
- **Interactive Console Loop**: Run multiple experiments in one session without restarting the script.

---

## Live Demonstration & Output

When transforming the source word **"flaw"** to the destination word **"lawn"**, the tool produces the following visualization:

```text
--- New Experiment ---
Enter SOURCE word: flaw
Enter DESTINATION word: lawn

DP Table (Source on Top, Destination on Left)

          f   l   a   w   
      0   1   2   3   4
l     1   2   1   2   3
a     2   3   2   1   2
w     3   4   3   2   1
n     4   5   4   3   2

Minimum Edit Distance = 2

Edit Operations:
- Delete 'f' (Cost 1)
- Ignore 'l'
- Ignore 'a'
- Ignore 'w'
- Insert 'n' (Cost 1)
```

---

## How It Works

### 1. The Recurrence Relation
For source string $X$ of length $M$ and destination string $Y$ of length $N$, we build a matrix `dp` of size $(N+1) \times (M+1)$ where `dp[i][j]` stores the minimum edit distance between the prefix $Y[0..i-1]$ and $X[0..j-1]$:

$$
DP[i][j] = \min \begin{cases} 
DP[i][j-1] + 1 & \text{(Deletion)} \\
DP[i-1][j] + 1 & \text{(Insertion)} \\
DP[i-1][j-1] + \text{cost} & \text{(Substitution / Identity)}
\end{cases}
$$
*Where $\text{cost} = 0$ if $Y[i-1] == X[j-1]$, else $\text{cost} = 2$.*

### 2. Backtracking for Operations
Starting from the bottom-right corner `dp[N][M]`, the algorithm backtracks to `dp[0][0]` by matching current cell values against the predecessor cell weights to reconstruct the alignment path.

---

## Getting Started

### Prerequisites
- **Python 3.x** (No external library dependencies required)

### Running the Application

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/minimum-edit-distance.git
   cd minimum-edit-distance
   ```
2. Run the script:
   ```bash
   python edit_distance.py
   ```
3. Type your Source and Destination words when prompted. Type `quit` to exit.
```
