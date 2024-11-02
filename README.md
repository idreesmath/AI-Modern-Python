Here's a Python function that efficiently calculates the Fibonacci sequence using **memoization** with **type hinting** for better code clarity. I'll explain each part through comments to make it easy to understand.

```python
from typing import Dict

# Define a memoization function that will store computed Fibonacci values
def memoize(fn):
    # Cache will store previously computed Fibonacci values
    cache: Dict[int, int] = {}

    # This inner function will handle the memoization logic
    def memoized_fn(n: int) -> int:
        # Check if the result is already in the cache
        if n in cache:
            return cache[n]
        
        # If not in cache, compute the result and store it
        result = fn(n)
        cache[n] = result
        return result
    
    # Return the memoized version of the function
    return memoized_fn

# Define the recursive Fibonacci function with type hinting
def fibonacci(n: int) -> int:
    """
    Calculates the nth Fibonacci number.
    
    :param n: The position in the Fibonacci sequence to calculate.
    :return: The Fibonacci number at position n.
    """
    # Base cases: Fib(0) = 0, Fib(1) = 1
    if n == 0:
        return 0
    if n == 1:
        return 1

    # Recursive case: Fib(n) = Fib(n-1) + Fib(n-2)
    return fibonacci(n - 1) + fibonacci(n - 2)

# Apply memoization to optimize the Fibonacci function
memoized_fibonacci = memoize(fibonacci)

# Example usage
if __name__ == "__main__":
    # Calculate the 10th Fibonacci number
    print(memoized_fibonacci(10))  # Output: 55
```

### Explanation:

1. **Type Hinting**:
   - The type hint `Dict[int, int]` in the `memoize` function specifies that the cache will store keys and values as integers. Type hints improve code readability and allow static type checking tools to catch potential issues early.
   - The `fibonacci` function is type hinted to return an `int` and accept an `int` argument (`n: int -> int`), which describes that the input `n` is an integer, and the function will return an integer.

2. **Memoization**:
   - The `memoize` function wraps another function and adds caching behavior. 
   - It creates a `cache` dictionary to store previously computed Fibonacci values. Before computing `Fib(n)`, it checks if `n` exists in the cache. If found, it returns the cached value, otherwise computes it, stores it in the cache, and returns the result.

3. **Fibonacci Calculation**:
   - The `fibonacci` function uses the recursive definition of the Fibonacci sequence. It checks the base cases (`Fib(0) = 0` and `Fib(1) = 1`) and then recursively computes higher values.
   - With memoization, the repeated recursive calls are optimized as the results of earlier calls are cached.

4. **Efficiency**:
   - This implementation avoids recomputing the same Fibonacci numbers multiple times, reducing the time complexity from exponential `O(2^n)` (without memoization) to linear `O(n)`.

5. **Example Usage**:
   - The `memoized_fibonacci(10)` call calculates the 10th Fibonacci number efficiently and prints `55`.

This function is highly efficient for calculating Fibonacci numbers, even for large `n`, thanks to memoization.
