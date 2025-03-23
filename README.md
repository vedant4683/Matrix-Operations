# Matrix-Operations
#include <stdio.h>
#include <stdlib.h>

// Function to input matrix elements
void input(int rows, int cols, int matrix[rows][cols]) {
    printf("Enter elements of Matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
}

// Function to display matrix
void display(int rows, int cols, int matrix[rows][cols]) {
    printf("Matrix elements:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d\t", matrix[i][j]);
        }
        printf("\n");
    }
}

// Function to add two matrices
void add(int rows, int cols, int result[rows][cols], int matrix1[rows][cols], int matrix2[rows][cols]) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            result[i][j] = matrix1[i][j] + matrix2[i][j];
        }
    }
}

// Function to multiply two matrices
void multiply(int rows1, int cols1, int matrix1[rows1][cols1],
              int rows2, int cols2, int matrix2[rows2][cols2],
              int result[rows1][cols2]) {
    if (cols1 != rows2) {
        printf("Matrix multiplication not possible!\n");
        return;
    }

    for (int i = 0; i < rows1; i++) {
        for (int j = 0; j < cols2; j++) {
            result[i][j] = 0;
            for (int k = 0; k < cols1; k++) {  // Fixed multiplication formula
                result[i][j] += matrix1[i][k] * matrix2[k][j];
            }
        }
    }
}

// Function to transpose a matrix
void transpose(int rows, int cols, int matrix[rows][cols], int result[cols][rows]) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            result[j][i] = matrix[i][j];
        }
    }
}

int main() {
    int rows1, cols1, rows2, cols2;
    int matrix1[10][10], matrix2[10][10], result[10][10];
    int choice;

    // Input for first matrix
    printf("Enter number of rows and columns of 1st matrix: ");
    scanf("%d %d", &rows1, &cols1);
    input(rows1, cols1, matrix1);

    // Input for second matrix
    printf("Enter number of rows and columns for 2nd matrix: ");
    scanf("%d %d", &rows2, &cols2);
    input(rows2, cols2, matrix2);

    do {
        // Menu
        printf("\n1. Display both matrices\n");
        printf("2. Add matrices\n");
        printf("3. Multiply matrices\n");
        printf("4. Transpose matrices\n");
        printf("5. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("First Matrix:\n");
                display(rows1, cols1, matrix1);
                printf("Second Matrix:\n");
                display(rows2, cols2, matrix2);
                break;

            case 2:
                if (rows1 == rows2 && cols1 == cols2) {
                    add(rows1, cols1, result, matrix1, matrix2);
                    printf("Addition Result:\n");
                    display(rows1, cols1, result);
                } else {
                    printf("Matrices must have the same dimensions for addition!\n");
                }
                break;

            case 3:
                multiply(rows1, cols1, matrix1, rows2, cols2, matrix2, result);
                printf("Multiplication Result:\n");
                display(rows1, cols2, result);
                break;

            case 4:
                transpose(rows1, cols1, matrix1, result);
                printf("Transpose of Matrix 1:\n");
                display(cols1, rows1, result);

                transpose(rows2, cols2, matrix2, result);
                printf("Transpose of Matrix 2:\n");
                display(cols2, rows2, result);
                break;

            case 5:
                exit(0);

            default:
                printf("Invalid choice!\n");
        }
    } while (choice != 5);

    return 0;
}
