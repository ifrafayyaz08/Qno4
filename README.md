import java.util.Scanner;

public class Knapsack {
    
    // Method to solve the 0/1 Knapsack problem
    public static void knapsack(int[] weights, int[] values, int n, int W) {
        int[][] dp = new int[n + 1][W + 1];
        
        // Build the dp table
        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                if (i == 0 || w == 0) {
                    dp[i][w] = 0;
                } else if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(dp[i - 1][w], values[i - 1] + dp[i - 1][w - weights[i - 1]]);
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }
        
        // Display the dp table
        System.out.println("Dynamic Programming Table:");
        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                System.out.print(dp[i][w] + "\t");
            }
            System.out.println();
        }
        
        // Find the items included in the knapsack
        int res = dp[n][W];
        int w = W;
        System.out.print("Items included (weight, value): ");
        for (int i = n; i > 0 && res > 0; i--) {
            if (res != dp[i - 1][w]) {
                System.out.print("(" + weights[i - 1] + "," + values[i - 1] + ") ");
                res -= values[i - 1];
                w -= weights[i - 1];
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Input number of items and max weight
        System.out.print("Enter the number of items: ");
        int n = scanner.nextInt();
        System.out.print("Enter the maximum weight: ");
        int W = scanner.nextInt();

        int[] weights = new int[n];
        int[] values = new int[n];

        // Input weights and values
        System.out.println("Enter the weights and values of the items:");
        for (int i = 0; i < n; i++) {
            System.out.print("Item " + (i + 1) + " weight: ");
            weights[i] = scanner.nextInt();
            System.out.print("Item " + (i + 1) + " value: ");
            values[i] = scanner.nextInt();
        }

        // Solve the knapsack problem
        knapsack(weights, values, n, W);

        scanner.close();
    }
}
