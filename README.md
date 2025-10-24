<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: Aravindan T </h3>
<h3>Register Number: 2305001003</h3>
<h2>Aim:</h2>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h2>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h2>

<p>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</p>
<p>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</p>
<h2>IMPLEMENTATION</h2>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h2>The Minimax algorithm</h2>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h2>Alpha-Beta pruning</h2>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance

## PROGRAM
```python
import math

# Initialize board
board = [' ' for _ in range(9)]

# Print the Tic-Tac-Toe board
def print_board(board):
    for i in range(3):
        print(board[3*i] + ' | ' + board[3*i + 1] + ' | ' + board[3*i + 2])
        if i < 2:
            print("---------")

# Check for winner
def check_winner(board):
    win_conditions = [
        [0,1,2], [3,4,5], [6,7,8],  # Rows
        [0,3,6], [1,4,7], [2,5,8],  # Columns
        [0,4,8], [2,4,6]            # Diagonals
    ]
    for a, b, c in win_conditions:
        if board[a] == board[b] == board[c] and board[a] != ' ':
            return board[a]
    if ' ' not in board:
        return 'Draw'
    return None

# Minimax function with Alpha-Beta Pruning
def minimax(board, depth, is_maximizing, alpha, beta):
    winner = check_winner(board)
    if winner == 'X':
        return -10 + depth
    elif winner == 'O':
        return 10 - depth
    elif winner == 'Draw':
        return 0

    if is_maximizing:
        max_eval = -math.inf
        for i in range(9):
            if board[i] == ' ':
                board[i] = 'O'
                eval = minimax(board, depth + 1, False, alpha, beta)
                board[i] = ' '
                max_eval = max(max_eval, eval)
                alpha = max(alpha, eval)
                if beta <= alpha:
                    break
        return max_eval
    else:
        min_eval = math.inf
        for i in range(9):
            if board[i] == ' ':
                board[i] = 'X'
                eval = minimax(board, depth + 1, True, alpha, beta)
                board[i] = ' '
                min_eval = min(min_eval, eval)
                beta = min(beta, eval)
                if beta <= alpha:
                    break
        return min_eval

# Find the best move for the computer
def best_move(board):
    best_val = -math.inf
    move = None
    for i in range(9):
        if board[i] == ' ':
            board[i] = 'O'
            move_val = minimax(board, 0, False, -math.inf, math.inf)
            board[i] = ' '
            if move_val > best_val:
                best_val = move_val
                move = i
    return move

# Main game loop
def play_game():
    print("Welcome to Tic-Tac-Toe!")
    print("You are 'X' and Computer is 'O'")
    print_board(board)

    while True:
        # Player Move
        move = int(input("Enter your move (1-9): ")) - 1
        if board[move] != ' ':
            print("Invalid move! Try again.")
            continue
        board[move] = 'X'

        print_board(board)
        if check_winner(board):
            result = check_winner(board)
            print("Result:", result)
            break

        # Computer Move
        print("Computer is thinking...")
        comp_move = best_move(board)
        board[comp_move] = 'O'
        print_board(board)

        result = check_winner(board)
        if result:
            print("Result:", result)
            break

# Run the game
if __name__ == "__main__":
    play_game()

```
<hr>
<h2>Input and Output:</h2>
<img width="457" height="518" alt="image" src="https://github.com/user-attachments/assets/67154f9d-9372-44df-b816-b962512fa1e3" />
<img width="434" height="486" alt="image" src="https://github.com/user-attachments/assets/5eb88bd5-8394-49a0-85b0-21b9490a6b6c" />
<img width="400" height="488" alt="image" src="https://github.com/user-attachments/assets/71589a00-6f3a-47cb-82c2-ede62a41e89a" />
<img width="391" height="213" alt="image" src="https://github.com/user-attachments/assets/e2670ce4-5a0c-45d0-9c36-203455b8b35c" />
<h2>RESULT</h2>
We have successfully implemented Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game.
