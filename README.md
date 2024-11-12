# Tic-Tac-Toe Game in Python (Terminal)

def print_board(board):
    # Print the current state of the board
    for row in board:
        print(" | ".join(row))
        print("-" * 9)


def check_winner(board, player):
    # Check rows, columns, and diagonals for a win
    for i in range(3):
        if all([spot == player for spot in board[i]]):  # Row
            return True
        if all([board[j][i] == player for j in range(3)]):  # Column
            return True
    # Diagonals
    if board[0][0] == board[1][1] == board[2][2] == player:
        return True
    if board[0][2] == board[1][1] == board[2][0] == player:
        return True
    return False


def check_draw(board):
    # Check if all spots are filled
    return all([spot != " " for row in board for spot in row])


def tic_tac_toe():
    # Initialize the board
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

    # Game loop
    while True:
        print_board(board)
        print(f"Player {current_player}'s turn.")
        
        # Get user input
        try:
            row = int(input("Enter row (0, 1, or 2): "))
            col = int(input("Enter column (0, 1, or 2): "))
            if board[row][col] != " ":
                print("Spot is already taken! Try again.")
                continue
        except (ValueError, IndexError):
            print("Invalid input! Please enter numbers between 0 and 2.")
            continue

        # Update board
        board[row][col] = current_player

        # Check for win or draw
        if check_winner(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break
        elif check_draw(board):
            print_board(board)
            print("It's a draw!")
            break

        # Switch players
        current_player = "O" if current_player == "X" else "X"


if __name__ == "__main__":
    tic_tac_toe()
