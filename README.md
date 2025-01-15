# Game Agent Implementations

This repository contains various implementations of game-playing agents in Python. These agents interact with a game environment using different decision-making strategies. The agents are designed to work with a grid-based game where each agent selects actions based on different types of algorithms.

## Overview

The following agent classes are implemented:

- **RandomAgent**: Chooses a random action from the available options.
- **PerceptronAgent**: Uses a perceptron to evaluate actions based on certain features of the game state.
- **ReflexAgent**: Selects actions based on filtering out moves that would benefit the opponent.
- **AdvancedPerceptronAgent**: An enhanced version of the PerceptronAgent with pre-trained weights.
- **MinimaxPruningAgent**: Uses the Minimax algorithm with alpha-beta pruning for decision-making.
- **ExpectimaxAgent**: An agent using the Expectimax algorithm for decision-making in uncertain environments.
- **SimpleRandomAgent**: A simpler version of the RandomAgent for a simpler game environment.
- **SimplePerceptronAgent**: Similar to PerceptronAgent but for a simplified game environment.

## Game Classes

### `Grid` Class

The `Grid` class models a single 3x3 grid in the Tic-Tac-Toe game. Each grid has its own status and a 3x3 matrix to track moves. The class includes the following methods:

- **`__init__(self)`**: Initializes a 3x3 grid with all positions set to 0 (empty). Also sets the initial status to 0 (In play).
  
- **`__str__(self)`**: Returns a string representation of the grid.
  
- **`printGrid(self)`**: Prints the grid row by row.

### Game Functions

- **`startState()`**: Initializes the starting state of the game. It creates a list of 9 `Grid` objects (representing 9 smaller grids) and sets the initial player to 0 (indicating it's player 1's turn).
  
- **`actions(state)`**: Returns a list of possible actions (moves) for a given state. The function checks if the last move made was in a grid that is still in play. If a grid is filled or finished (won/lost/tied), the action will only be allowed in a grid that is still active.

- **`findActionsInGrid(grid, gridNum)`**: Helper function that scans a specific grid for available positions (cells with 0). Returns a list of actions (coordinates) for those positions.

- **`succ(state, action)`**: Generates the next state based on the current state and an action. It updates the grid and checks if a grid's status has changed (won/lost/tied).

- **`updateGridStatus(grid)`**: Checks if any row, column, or diagonal in the grid has a winner and updates the status accordingly. If the grid is full and no winner, the status is set to 3 (tie).

- **`isEnd(state)`**: Checks if the current state represents the end of the game (either a win, tie, or ongoing).
  
- **`utility(state)`**: Returns the utility value of a state for an end state (100 for a win, -100 for a loss, and 0 for a tie).

- **`player(state)`**: Returns the index of the player whose turn it is in the given state.

## Simulation Classes

### `UltimateTicTacToeSimulator`

This class simulates a full Ultimate Tic-Tac-Toe game between two agents. It is designed to handle multiple smaller grids and manages the flow of the game, including checking the status of each grid and determining the winner.

- **`__init__(self, agent1, agent2)`**: Initializes the simulator with two agents (`agent1` and `agent2`).
  
- **`playGame(self)`**: Simulates a single game between the two agents. It returns the winner (1 for agent1, 2 for agent2) or 3 for a tie.
  
- **`playGames(self, n)`**: Simulates `n` games and returns the percentage of times `agent1` won or tied.

### `TicTacToeSimulator`

This class simulates a simpler version of the Tic-Tac-Toe game, where only one 3x3 grid is used. It follows the same structure as `UltimateTicTacToeSimulator`, but for a simpler environment.

- **`__init__(self, agent1, agent2)`**: Initializes the simulator with two agents (`agent1` and `agent2`).
  
- **`playGame(self)`**: Simulates a single game between the two agents. It returns the winner (1 for agent1, 2 for agent2) or 3 for a tie.
  
- **`playGames(self, n)`**: Simulates `n` games and returns the percentage of times `agent1` won or tied.

## Running Simulations

You can simulate matches between different agents by initializing the simulator and providing the agents you wish to use. Here’s an example of how to run simulations:

```python
from game import *
from agent import *
from simulate import *

# Example 1: Random Agent vs Random Agent
agent1 = RandomAgent() 
agent2 = RandomAgent() 
simulator = UltimateTicTacToeSimulator(agent1, agent2) 
print(simulator.playGames(1000)) 
print("Random vs Random") 

# Example 2: Perceptron Agent vs Random Agent
agent1 = PerceptronAgent() 
agent2 = RandomAgent() 
simulator = UltimateTicTacToeSimulator(agent1, agent2) 
print(simulator.playGames(1000))
print("Perceptron vs Random Agent")

# Example 3: Advanced Perceptron Agent vs Advanced Perceptron Agent
agent1 = AdvancedPerceptronAgent() 
agent2 = AdvancedPerceptronAgent() 
simulator = UltimateTicTacToeSimulator(agent1, agent2) 
print(simulator.playGames(1000))
print("Advanced Perceptron vs Advanced Perceptron Agent")
