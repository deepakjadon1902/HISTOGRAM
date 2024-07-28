import java.util.Scanner;
import java.util.Stack;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read number of bars in the histogram
        int n = scanner.nextInt();
        
        // Read the heights of the bars
        long[] heights = new long[n];
        for (int i = 0; i < n; i++) {
            heights[i] = scanner.nextLong();
        }

        System.out.println(findMaxRectangleArea(heights));
    }

    public static long findMaxRectangleArea(long[] heights) {
        Stack<Integer> stack = new Stack<>();
        long maxArea = 0;
        int n = heights.length;

        for (int i = 0; i < n; i++) {
            // Maintain the stack in increasing order of heights
            while (!stack.isEmpty() && heights[i] < heights[stack.peek()]) {
                int height = (int) heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, (long) height * width);
            }
            stack.push(i);
        }

        // Calculate area for remaining bars in stack
        while (!stack.isEmpty()) {
            int height = (int) heights[stack.pop()];
            int width = stack.isEmpty() ? n : n - stack.peek() - 1;
            maxArea = Math.max(maxArea, (long) height * width);
        }

        return maxArea;
    }
}
