# Dynamic Programming

## Introduction

Dynamic programming is an optimization technique used to solve problems more efficiently by breaking them down into smaller overlapping subproblems. It is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it, using Dynamic Programming. By breaking a problem into smaller components, solving each subproblem only once, and storing the results in a table, dynamic programming avoids redundant work when encountering the same subproblem.

## Key points
### Table or Memoization:

Dynamic programming often involves the use of a table or memoization to store the results of subproblems.

### Top-Down vs. Bottom-Up:

Two main approaches include top-down (recursion with memoization) and bottom-up (solving from smaller to larger subproblems).

## Example: Fibonacci Numbers

The Fibonacci sequence is a classic example of dynamic programming.

```csharp
public class Fibonacci
{
    public static int Calculate(int n)
    {
        int[] fib = new int[n + 1];
        fib[0] = 0;
        fib[1] = 1;

        for (int i = 2; i <= n; i++)
        {
            fib[i] = fib[i - 1] + fib[i - 2];
        }

        return fib[n];
    }
}

// Example usage:
int result = Fibonacci.Calculate(5);
Console.WriteLine(result); // Output: 5
```
