# Tic Tac Toe Game — C++

```cpp
#include <iostream>
using namespace std;

// Function to display the game board
void displayBoard(char board[3][3]) {
    cout << "\n";
    cout << "       TIC TAC TOE\n";
    cout << "=====================\n";

    for (int i = 0; i < 3; i++) {
        cout << "       ";

        for (int j = 0; j < 3; j++) {
            cout << board[i][j];

            if (j < 2)
                cout << " | ";
        }

        cout << "\n";

        if (i < 2)
            cout << "      ---+---+---\n";
    }

    cout << "=====================\n";
}

// Function to check whether a player has won
bool checkWin(char board[3][3], char player) {

    // Check rows
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player &&
            board[i][1] == player &&
            board[i][2] == player) {
            return true;
        }
    }

    // Check columns
    for (int j = 0; j < 3; j++) {
        if (board[0][j] == player &&
            board[1][j] == player &&
            board[2][j] == player) {
            return true;
        }
    }

    // Check diagonals
    if (board[0][0] == player &&
        board[1][1] == player &&
        board[2][2] == player) {
        return true;
    }

    if (board[0][2] == player &&
        board[1][1] == player &&
        board[2][0] == player) {
        return true;
    }

    return false;
}

// Function to check for a draw
bool checkDraw(char board[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] >= '1' && board[i][j] <= '9') {
                return false;
            }
        }
    }

    return true;
}

// Main game function
void playGame() {

    char board[3][3] = {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}
    };

    char currentPlayer = 'X';
    int choice;
    int row, column;

    while (true) {

        displayBoard(board);

        cout << "\nPlayer " << currentPlayer;
        cout << ", enter your position (1-9): ";
        cin >> choice;

        // Validate input
        if (choice < 1 || choice > 9) {
            cout << "\nInvalid position! Please enter 1 to 9.\n";
            continue;
        }

        // Convert position to row and column
        row = (choice - 1) / 3;
        column = (choice - 1) % 3;

        // Check whether the position is already occupied
        if (board[row][column] == 'X' ||
            board[row][column] == 'O') {

            cout << "\nPosition already occupied! Try again.\n";
            continue;
        }

        // Place player's symbol
        board[row][column] = currentPlayer;

        // Check whether the player has won
        if (checkWin(board, currentPlayer)) {

            displayBoard(board);

            cout << "\n********************************\n";
            cout << "       PLAYER " << currentPlayer << " WINS!\n";
            cout << "********************************\n";

            break;
        }

        // Check whether the game is a draw
        if (checkDraw(board)) {

            displayBoard(board);

            cout << "\n********************************\n";
            cout << "          GAME DRAW!\n";
            cout << "********************************\n";

            break;
        }

        // Change player
        if (currentPlayer == 'X')
            currentPlayer = 'O';
        else
            currentPlayer = 'X';
    }
}

int main() {

    char replay;

    cout << "====================================\n";
    cout << "       WELCOME TO TIC TAC TOE\n";
    cout << "====================================\n";

    do {

        playGame();

        cout << "\nDo you want to play again? (Y/N): ";
        cin >> replay;

    } while (replay == 'Y' || replay == 'y');

    cout << "\nThank you for playing Tic Tac Toe!\n";
    cout << "Game Over. Goodbye!\n";

    return 0;
}
```