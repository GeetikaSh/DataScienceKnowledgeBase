# Advanced Python Concepts:  Decorators, Generators, and Context Managers.

This document provides a detailed overview of three powerful and fundamental concepts in Python: **Decorators**, **Generators**, and **Context Managers**. Mastering these concepts will allow you to write more efficient, reusable, and robust code.

---

## 1. Decorators (`@`)

A decorator is a function that takes another function as an argument, adds some functionality, and returns a new function. They are a powerful tool for extending the behavior of functions without explicitly modifying them.

### Basic Structure

The `@` symbol is syntactic sugar for wrapping a function.

```python
# A simple decorator function
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

# Use the decorator with the @ syntax
@my_decorator
def say_hello():
    print("Hello from say_hello!")

# Calling the decorated function
say_hello()
```

**Output:**
```
Something is happening before the function is called.
Hello from say_hello!
Something is happening after the function is called.
```

**Practical Example: A Timing Decorator**

This decorator measures the execution time of any function.

```python
import time

def timer_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Function '{func.__name__}' took {end_time - start_time:.4f} seconds to run.")
        return result
    return wrapper

@timer_decorator
def complex_computation(n):
    total = 0
    for _ in range(n):
        total += sum(range(10000))
    return total

result = complex_computation(10)
print(f"Result: {result}")
```

## 2. Generators (yield)
Generators are a special type of function that return an iterator. They are highly memory-efficient because they produce items one at a time and only when requested. This is in contrast to regular functions that return a full list, which can consume a lot of memory for large datasets.

`yield` vs. `return`
- A function with a return statement terminates and returns a value.
- A function with a yield statement pauses its execution, saves its state, and returns a value. When called again, it resumes from where it left off.

**Simple Generator Example**
```python
def my_generator():
    yield "First item"
    yield "Second item"
    yield "Third item"

# Iterate over the generator
gen = my_generator()

for item in gen:
    print(item)

# You can also manually get the next item
print(next(gen))  # This will raise a StopIteration error after the last item is yielded
```

**Output**
```
First item
Second item
Third item
```

**Practical Example: Generating Fibonacci Numbers**

This generator can produce an infinite sequence of numbers without storing them all in memory.

```python
def fibonacci_generator():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# Get the first 10 Fibonacci numbers
fib_gen = fibonacci_generator()
for _ in range(10):
    print(next(fib_gen), end=" ")
```

**Output**
```
0 1 1 2 3 5 8 13 21 34
```

# Context Managers (`with`)

Context managers are objects that define a temporary context for a block of code. They are designed to manage resources, ensuring that they are properly acquired before the code block executes and properly released afterward, even if an error occurs. The `with` statement is the primary way to use them.

---

### Classic Example: File Handling

This is the most common use of context managers. The `with open(...)` statement ensures that the file is automatically closed, even if an error occurs within the `with` block.

```python
# The "with" statement automatically handles opening and closing the file
with open('my_file.txt', 'w') as f:
    f.write("This is a line of text.")
    # The file is open and ready to be used
    print("File is open and being written to.")

# Outside the "with" block, the file is automatically closed
print("File has been closed.")
```

### Creating Your Own Context Manager

You can create a context manager using a class with `__enter__` and `__exit__` methods.

```python
import time

class Timer:
    def __enter__(self):
        self.start_time = time.time()
        print("Starting timer...")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        end_time = time.time()
        print(f"Time elapsed: {end_time - self.start_time:.4f} seconds.")
        # If any exception occurred, this method will receive it.
        # Returning True from __exit__ would suppress the exception.

with Timer():
    print("Running some code...")
    time.sleep(1.5)
```

**Simple Context Managers with contextlib**

For simple cases, you can use the `@contextmanager` decorator from the `contextlib` module to create a context manager using a generator function.

```python
from contextlib import contextmanager

@contextmanager
def my_simple_context():
    print("Entering the context.")
    try:
        yield "Hello from inside the context!"
    finally:
        print("Exiting the context.")

with my_simple_context() as value:
    print(value)
```

**Output**
```
Entering the context.
Hello from inside the context!
Exiting the context.
```
