import java.util.Random;
import java.util.Scanner;

public class TicTacToe {

    static char[][] board = new char[3][3];
    static char currentPlayer = 'X'; // Human is 'X', Computer is 'O'

    public static void main(String[] args) {
        initializeBoard();
        while (true) {
            printBoard();
            if (currentPlayer == 'X') {
                humanMove();
                if (checkWin('X')) {
                    printBoard();
                    System.out.println("Human wins!");
                    break;
                }
                currentPlayer = 'O';
            } else {
                computerMove();
                if (checkWin('O')) {
                    printBoard();
                    System.out.println("Computer wins!");
                    break;
                }
                currentPlayer = 'X';
            }
            if (isBoardFull()) {
                printBoard();
                System.out.println("It's a draw!");
                break;
            }
        }
    }

    public static void initializeBoard() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
    }

    public static void printBoard() {
        System.out.println("  0 1 2");
        for (int i = 0; i < 3; i++) {
            System.out.print(i + " ");
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j]);
                if (j < 2) System.out.print("|");
            }
            System.out.println();
            if (i < 2) System.out.println("  -----");
        }
    }

    public static void humanMove() {
        Scanner scanner = new Scanner(System.in);
        int row, col;
        while (true) {
            System.out.println("Enter row and column (0, 1, or 2): ");
            row = scanner.nextInt();
            col = scanner.nextInt();
            if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
                board[row][col] = 'X';
                break;
            } else {
                System.out.println("This move is not valid.");
            }
        }
    }

    public static void computerMove() {
        Random rand = new Random();
        int row, col;
        while (true) {
            row = rand.nextInt(3);
            col = rand.nextInt(3);
            if (board[row][col] == ' ') {
                board[row][col] = 'O';
                break;
            }
        }
    }

    public static boolean checkWin(char player) {
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == player && board[i][1] == player && board[i][2] == player) {
                return true;
            }
            if (board[0][i] == player && board[1][i] == player && board[2][i] == player) {
                return true;
            }
        }
        if (board[0][0] == player && board[1][1] == player && board[2][2] == player) {
            return true;
        }
        if (board[0][2] == player && board[1][1] == player && board[2][0] == player) {
            return true;
        }
        return false;
    }

    public static boolean isBoardFull() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true;
    }
}
