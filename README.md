# Tic-Tac-Toe Engine and Solver

This project implements a tic-tac-toe game engine and a solver using the min-max algorithm. The engine supports a generalized version of tic-tac-toe called NMK, which allows for customizable board sizes and victory conditions. The solver can determine the optimal moves for a given game state.

## Generalized Tic-Tac-Toe (NMK)

The NMK version of tic-tac-toe accepts three parameters: N, M, and K. 

- N x M represents the size of the board.
- K determines the victory condition, where K neighboring fields forming a continuous horizontal, vertical, or diagonal line section lead to a win.

The game engine provides the following features:

1. Generate all possible moves.
2. Mark the state of the game and determine if the game has ended and which player won/tied/lost.

In the basic version of tic-tac-toe (NMK 3, 3, 3), the generated moves for an empty initial board are:

```
100 010 001 000 000 000 000 000 000
000 000 000 100 010 001 000 000 000
000 000 000 000 000 000 100 010 001
```

In the enhanced version, if one of the generated states is final (a player wins or the board is full, resulting in a tie), the engine will generate only that state. If multiple states are possible, only the first win/tie state will be generated.

## Min-Max Solver

The project also includes an algorithm that solves an NMK game state using the min-max algorithm with some enhancements. The solver can determine if the game, assuming both players play optimally, ends in a win, loss, or tie.

The enhancements for the min-max algorithm include:

1. Early termination of the search when a winning move (score of 1) is found during the min search or a losing move (score of -1) is found during the max search. This optimization avoids unnecessary further exploration.

2. Identifying situations where a player has a winning move in the next move. These situations involve lengths (K-1) that have the possibility of adding a token at the ends. If there is only one such situation, the opponent can still defend themselves. However, if there are two or more such situations and the opponent has not created a threat before, they are already in a losing position. This observation helps in determining the outcome of the game.

## Usage

The project provides three commands to interact with the tic-tac-toe engine and solver:

1. `GEN_ALL_POS_MOV N M K ActivePlayer` - Generate all possible moves and their count for a given NMK game state.
   
   **Example:**
   ```
   Input:
   GEN_ALL_POS_MOV 3 3 3 2
   1 0 0
   0 0 0
   0 0 0
   
   Output:
   8
   1 2 0
   0 0 0
   0 0 0
   
   1 0 2
   0 0 0
   0 0 0
   
   1 0 0
   2 0 0
   0 0 0
   
   1 0 0
   0 2 0
   0 0 0
   
   1 0 0
   0 0 2
   0 0 0
   
   1 0 0
   0 0 0
  

 2 0 0
   
   1 0 0
   0 0 0
   0 2 0
   
   1 0 0
   0 0 0
   0 0 2
   ```

2. `GEN_ALL_POS_MOV_CUT_IF_GAME_OVER N M K ActivePlayer` - Generate feasible moves and their count. If any of the moves results in a win or tie, only the first such move is generated.

   **Example:**
   ```
   Input:
   GEN_ALL_POS_MOV_CUT_IF_GAME_OVER 3 3 3 1
   1 2 0
   0 0 0
   0 0 0
   
   Output:
   7
   1 2 1
   0 0 0
   0 0 0
   
   1 2 0
   1 0 0
   0 0 0
   
   1 2 0
   0 1 0
   0 0 0
   
   1 2 0
   0 0 1
   0 0 0
   
   1 2 0
   0 0 0
   1 0 0
   
   1 2 0
   0 0 0
   0 1 0
   
   1 2 0
   0 0 0
   0 0 1
   ```

3. `SOLVE_GAME_STATE N M K ActivePlayer` - Solve the game state and determine one of the possible outcomes: `FIRST_PLAYER_WINS`, `SECOND_PLAYER_WINS`, or `BOTH_PLAYERS_TIE`.

   **Example:**
   ```
   Input:
   SOLVE_GAME_STATE 3 3 3 2
   1 0 0
   0 0 0
   0 0 0
   
   Output:
   BOTH_PLAYERS_TIE
   ```

**Note:** The input and output in the examples are formatted for readability. The actual input should follow the provided syntax.

## Code

The implementation code for the tic-tac-toe engine and solver can be found in the code file [here](code.cpp).

To run the project, compile and execute the code. Make sure to provide the appropriate inputs and follow the specified command syntax.

```shell
$ g++ main.cpp -o tic_tac_toe
$ ./tic_tac_toe
```
Make sure to adjust the file paths if you plan to save the output to a file instead of printing it to the console.

## Results

The results can be displayed in two ways: either in the console or by writing them to a file. This is determined by the `file` global variable, which indicates whether the results should be written to a file.

To write the results to a file, set `file` to `true` and provide the desired file path using the `out_file` variable:

```c++
std::ofstream out_file{ "../results.txt" };
bool file = true;
```

By default, if `file` is set to `false`, the results will be outputted to the console.

Feel free to modify the `file` variable and provide a different file path if you want to write the results to a specific file.
