# 1205-python local variable

python会先把函数解析成bytecode再在调用的时候运行，解析的时候还会把变量的作用域分析好。

```
lmax = 100
def modify_lmax():
    lmax = lmax + 100  # Error: lmax is referenced before assignment
    print(lmax)
```

所以这样写是不行的

GPT:

Yes, Python will **analyze your function's code during the function definition phase (compilation phase)** to determine the scope of variables **before executing the function.**

This means that when you define a function, Python identifies which variables are local, global, or nonlocal within the function **before it starts running the function's body.** This scope determination happens during the compilation of the function into bytecode.

***

#### How Python Analyzes Your Code

When Python encounters a function definition, it:

1. **Reads the entire function body** (but does not execute it yet).
2. Determines which variables are assigned values within the function. These are marked as **local** by default unless explicitly declared as `global` or `nonlocal`.
3. Sets up the function's scope based on this analysis.

***

#### Why This Causes an Error

Because Python analyzes the function **before execution**, it already knows that the variable is assigned within the function. As a result, it marks that variable as local.

If the function then tries to read the variable **before the local assignment occurs**, Python raises an `UnboundLocalError` because it assumes you're referencing a local variable that hasn't been initialized yet.

***

#### Example of Python's Behavior

```python
x = 10  # Global variable

def example():
    print(x)  # Accessing `x` here
    x = 20  # Local assignment

example()
```

**Steps Python Takes:**

1. During the function's definition phase:
   * Python sees that `x` is assigned a value (`x = 20`) within the function.
   * Python concludes that `x` is a **local variable** for this function.
2. During execution:
   * When `print(x)` is executed, Python tries to access the local `x`.
   * The local `x` hasn't been assigned yet (the assignment happens after `print(x)`), so Python raises an `UnboundLocalError`.

***

#### Proof of Early Analysis

You can confirm this behavior by adding a function attribute **before the line that causes the error**:

```python
x = 10  # Global variable

def example():
    example.some_attribute = 42  # Adding an attribute to the function
    print(x)  # Accessing `x` here
    x = 20  # Local assignment

example()
```

This code will still raise:

```
UnboundLocalError: local variable 'x' referenced before assignment
```

Even though the line `example.some_attribute = 42` runs successfully, Python already decided during the definition phase that `x` is a local variable.

***

#### How to Avoid This Issue

1.  **Declare `global` or `nonlocal`** if you intend to modify a variable from an outer scope:

    ```python
    x = 10

    def example():
        global x  # Declare `x` as global
        print(x)  # Access the global `x`
        x = 20  # Modify the global `x`

    example()
    ```
2.  **Use a different local variable name** to avoid shadowing:

    ```python
    x = 10

    def example():
        print(x)  # Access the global `x`
        local_x = 20  # Use a different local variable name
        print(local_x)

    example()
    ```
3.  **Pass the variable as an argument**:

    ```python
    x = 10

    def example(x):
        print(x)  # Use the passed value
        x = 20
        return x

    x = example(x)  # Update the global `x` explicitly
    ```

***

#### Summary

Yes, Python analyzes the entire function during the **function definition phase** to determine the scope of variables. This is why you get an `UnboundLocalError` even if the code doesn't reach the problematic line during execution—the scope decision is already made.
