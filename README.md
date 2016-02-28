# laberinto-gfernan6
laberinto-gfernan6 created by Classroom for GitHub
import java.util.Scanner;

public class Labyrinth3 {

    private static int n;
    private static char matrix[][];
    private static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        n = sc.nextInt();
        matrix = new char[n][n];
        intializeMatrix();
        fillMatrix();
        //showMatrix();
        System.out.println(calculateArea());
    }

    private static void intializeMatrix() {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = '.';
            }
        }
    }
    
    private static void fillMatrix() {
        for (int i = 0; i < n; i++) {
            String line = sc.next();
            for (int j = 0; j < n; j++) {
                if(line.charAt(j) == '#') {
                   matrix[i][j] = '#';
                }
            }
        }
    }

    private static void showMatrix() {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(matrix[i][j]);
            }
            System.out.println();
        }
    }

    private static int calculateArea() {
        int sum = 0;

        // Throw rigth down
        int dir = 0;
        int i = 0;
        int j = 0;
          
        do {
            if (dir == 0) { // Rigth
                if (matrix[i][j + 1] == '.') {
                    sum++;
                    j++;
                    if (j == n - 1) {
                        dir = 1;
                        if (!(i == n - 1 && j == n - 1)) {
                            sum++;
                        }
                    }
                } else {
                    dir = 1;
                }
            } else if(dir == 1) { // Down
                if (matrix[i + 1][j] == '.') {
                    i++;
                    if (i != n -1) {
                        sum++;
                    }
                    if (j != n - 1) {
                        dir = 0;
                    }
                } else { // Left
                    sum++;
                    j--;
                }
            }
        } while(!(i == n - 1 && j == n - 1));
        
        // Throw left up
        dir = 2;
        i = n - 1;
        j = n - 1;
          
        do {
            if (dir == 2) { // Left
                if (matrix[i][j - 1] == '.') {
                    sum++;
                    j--;
                    if (j == 0) {
                        dir = 3;
                        sum++;
                    }
                } else {
                    dir = 3;
                }
            } else if(dir == 3) { // Up
                if (matrix[i - 1][j] == '.') {
                    i--;
                    if (i != 0) {
                        sum++;
                    }
                    if (j != 0) {
                        dir = 2;
                    }
                } else { // Right
                    sum++;
                    j++;
                }
            }
        } while(!(i == 0 && j == 0));
        
        return sum * 9;
    }
}
