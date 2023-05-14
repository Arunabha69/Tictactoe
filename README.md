#include <stdio.h>

char board[3][3]; // 2D array to represent the game board

char currentPlayer = 'X'; // start with player X

// function to initialize the board

void init_board() {

    int i, j;

    for (i = 0; i < 3; i++) {

        for (j = 0; j < 3; j++) {

            board[i][j] = ' ';

        }

    }

}

// function to print the board

void print_board() {

    printf("\n");

    printf(" %c | %c | %c\n", board[0][0], board[0][1], board[0][2]);

    printf("---+---+---\n");

    printf(" %c | %c | %c\n", board[1][0], board[1][1], board[1][2]);

    printf("---+---+---\n");

    printf(" %c | %c | %c\n", board[2][0], board[2][1], board[2][2]);

    printf("\n");

}

// function to check if the game has ended

int game_ended() {

    int i, j;

    // check rows

    for (i = 0; i < 3; i++) {

        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ') {

            return 1;

        }

    }

    // check columns

    for (j = 0; j < 3; j++) {

        if (board[0][j] == board[1][j] && board[1][j] == board[2][j] && board[0][j] != ' ') {

            return 1;

        }

    }

    // check diagonals

    if ((board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ') ||

        (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')) {

        return 1;

    }

    // check if the board is full

    for (i = 0; i < 3; i++) {

        for (j = 0; j < 3; j++) {

            if (board[i][j] == ' ') {

                return 0;

            }

        }

    }

    return 2;

}

// function to get the next player

void next_player() {

    if (currentPlayer == 'X') {

        currentPlayer = 'O';

    } else {

        currentPlayer = 'X';

    }

}

// function to make a move

void make_move() {

    int row, col;

    printf("%c's turn. Enter row (1-3) and column (1-3) separated by space: ", currentPlayer);

    scanf("%d %d", &row, &col);

    row--; // convert to 0-based index

    col--;

    if (row < 0 || row > 2 || col < 0 || col > 2) {

        printf("Invalid move. Row and column must be between 1 and 3.\n");

        return;

    }

    if (board[row][col] != ' ') {

        printf("Invalid move. Cell already occupied.\n
