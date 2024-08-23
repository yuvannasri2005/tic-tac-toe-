def print_board(board):
    """Print the game board."""
    print("  1 2 3")
    for row in range(3):
        print(row + 1, end=' ')
        for col in range(3):
            print(board[row][col], end=' ')
        print()

def check_winner(board, player):
    """Check if the current player has won."""
    win_conditions = [
        # Rows
        [board[0][0], board[0][1], board[0][2]],
        [board[1][0], board[1][1], board[1][2]],
        [board[2][0], board[2][1], board[2][2]],
        # Columns
        [board[0][0], board[1][0], board[2][0]],
        [board[0][1], board[1][1], board[2][1]],
        [board[0][2], board[1][2], board[2][2]],
        # Diagonals
        [board[0][0], board[1][1], board[2][2]],
        [board[0][2], board[1][1], board[2][0]],
    ]
    return [player] * 3 in win_conditions

def is_draw(board):
    """Check if the game is a draw."""
    return all(cell != ' ' for row in board for cell in row)

def get_move():
    """Get a valid move from the player."""
    while True:
        try:
            move = input("Enter your move (row and column): ").strip()
            row, col = map(int, move.split())
            if row not in (1, 2, 3) or col not in (1, 2, 3):
                raise ValueError
            return row - 1, col - 1
        except (ValueError, IndexError):
            print("Invalid move. Please enter row and column numbers between 1 and 3.")

def play_game():
    """Play a game of Tic Tac Toe."""
    print("Welcome to Tic Tac Toe!")
    while True:
        board = [[' ' for _ in range(3)] for _ in range(3)]
        current_player = 'X'
        while True:
            print_board(board)
            print(f"Player {current_player}'s turn.")
            
            row, col = get_move()
            
            if board[row][col] != ' ':
                print("Cell already taken. Choose another one.")
                continue

            board[row][col] = current_player
            
            if check_winner(board, current_player):
                print_board(board)
                print(f"Player {current_player} wins!")
                break
            
            if is_draw(board):
                print_board(board)
                print("It's a draw!")
                break

            # Switch player
            current_player = 'O' if current_player == 'X' else 'X'
        
        # Ask if players want to play again
        if input("Do you want to play again? (yes/no): ").strip().lower() != 'yes':
            break

if __name__ == "__main__":
    play_game()
