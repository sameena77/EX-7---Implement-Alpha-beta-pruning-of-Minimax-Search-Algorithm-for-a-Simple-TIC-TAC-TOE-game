<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:  SAMEENA J   </h3>
<h3>Register Number:  2305002019       </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance

## PROGRAM
```python
import math
import time

class TicTacToe:
    def __init__(self):
        self.board = [['.' for _ in range(3)] for _ in range(3)]
        self.player = 'X' 

    def print_board(self):
        for row in self.board:
            print(' | '.join(row))
        print()

    def is_valid(self, x, y):
        return 0 <= x < 3 and 0 <= y < 3 and self.board[x][y] == '.'

    def check_winner(self):
        
        for i in range(3):
            if self.board[i][0] == self.board[i][1] == self.board[i][2] != '.':
                return self.board[i][0]
            if self.board[0][i] == self.board[1][i] == self.board[2][i] != '.':
                return self.board[0][i]

        
        if self.board[0][0] == self.board[1][1] == self.board[2][2] != '.':
            return self.board[0][0]
        if self.board[0][2] == self.board[1][1] == self.board[2][0] != '.':
            return self.board[0][2]

        
        for row in self.board:
            if '.' in row:
                return None
        return '.' 
    def minimax(self, is_max, alpha, beta):
        result = self.check_winner()
        if result == 'X': return -1, None, None
        if result == 'O': return 1, None, None
        if result == '.': return 0, None, None

        if is_max:
            best = -math.inf
            move = None
            for i in range(3):
                for j in range(3):
                    if self.board[i][j] == '.':
                        self.board[i][j] = 'O'
                        val, _, _ = self.minimax(False, alpha, beta)
                        self.board[i][j] = '.'
                        if val > best:
                            best = val
                            move = (i, j)
                        alpha = max(alpha, val)
                        if beta <= alpha:
                            break
            return best, move[0], move[1]

        else:
            best = math.inf
            move = None
            for i in range(3):
                for j in range(3):
                    if self.board[i][j] == '.':
                        self.board[i][j] = 'X'
                        val, _, _ = self.minimax(True, alpha, beta)
                        self.board[i][j] = '.'
                        if val < best:
                            best = val
                            move = (i, j)
                        beta = min(beta, val)
                        if beta <= alpha:
                            break
            return best, move[0], move[1]

    def play(self):
        print("You are X, Computer is O\n")
        self.print_board()

        while True:
            # Player move
            if self.player == 'X':
                x = int(input("Enter row (0-2): "))
                y = int(input("Enter col (0-2): "))
                if not self.is_valid(x, y):
                    print("Invalid move! Try again.")
                    continue
                self.board[x][y] = 'X'
                self.player = 'O'

            else:
                print("Computer is thinking...")
                start = time.time()
                _, x, y = self.minimax(True, -math.inf, math.inf)
                end = time.time()
                print(f"Computer chose position: ({x}, {y})")
                print(f"Evaluation time: {round(end - start, 4)}s\n")
                self.board[x][y] = 'O'
                self.player = 'X'

            self.print_board()
            winner = self.check_winner()
            if winner:
                if winner == 'X':
                    print("🎉 You win!")
                elif winner == 'O':
                    print("💻 Computer wins!")
                else:
                    print("🤝 It's a draw!")
                break


if __name__ == "__main__":
    game = TicTacToe()
    game.play()

```
<hr>
<h2> Input and Output:</h2>
<img width="321" height="533" alt="image" src="https://github.com/user-attachments/assets/451b73f4-836b-46fb-a35e-6ca1e5389607" />


## RESULT
We have successfully implemented Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game.
