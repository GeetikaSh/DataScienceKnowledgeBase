# Python Decorators: A Core Concept for Aspiring ML Engineers

This document provides a comprehensive overview of Python **Decorators**, tailored for aspiring Machine Learning Engineers preparing for interviews. It clarifies key concepts, highlights their relevance in the ML domain, and addresses common interview questions.

---

## What is a Decorator?
A **Decorator** in Python is a special function that modifies the behavior of another function or class method without permanently changing its code.

- **Analogy**: Think of a decorator like a gift wrap. The object (function) remains the same inside, but the wrapping (decorator) changes how it looks or behaves when presented.

---

## Why Use Decorators?
1. **Code Reusability**: Apply the same logic (e.g., logging, timing, validation) to multiple functions without repeating code.
2. **Separation of Concerns**: Keep core logic clean while handling cross-cutting concerns (e.g., caching, authentication).
3. **Readability**: Provides a concise syntax with `@decorator_name`.

---

## Basic Syntax
A decorator is applied with the `@` symbol above a function definition.

```python
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

**Output:**
```
Before function call
Hello!
After function call
```

---

## Real-World Examples in ML Engineering

### 1. Logging Function Calls
```python
def log_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with arguments {args}, {kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@log_decorator
def add(a, b):
    return a + b

add(5, 10)
```

---

### 2. Timing Function Execution
Useful for profiling ML training steps.

```python
import time

def time_it(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} executed in {end - start:.4f}s")
        return result
    return wrapper

@time_it
def train_model():
    time.sleep(2)
    return "Model trained!"

train_model()
```

---

### 3. Access Control / Authentication
In production ML systems, restrict access to certain endpoints.

```python
def require_api_key(func):
    def wrapper(*args, **kwargs):
        if kwargs.get("api_key") != "secret123":
            raise PermissionError("Invalid API key!")
        return func(*args, **kwargs)
    return wrapper

@require_api_key
def get_predictions(data, api_key=None):
    return {"prediction": "cat"}

# Example:
# get_predictions([1,2,3], api_key="secret123") ✅
# get_predictions([1,2,3], api_key="wrong") ❌
```

---

## Chaining Multiple Decorators
You can apply multiple decorators to a single function.

```python
@time_it
@log_decorator
def multiply(a, b):
    return a * b

multiply(3, 4)
```

Order matters: the decorator closest to the function runs first.

---

## Common Built-in Decorators
- `@staticmethod` – Defines a method that doesn’t access class or instance state.
- `@classmethod` – Defines a method that operates on the class, not an instance.
- `@property` – Defines a method as a read-only attribute.

---

## Interview Tips
- **Q: Why are decorators useful in ML pipelines?**
  - To log training metrics, time model training steps, or enforce security in APIs.
- **Q: What’s the difference between a decorator and a wrapper?**
  - A wrapper is the inner function inside a decorator; a decorator is the outer function that returns the wrapper.
- **Q: Can decorators take arguments?**
  - Yes, by adding another level of nesting.

---

## Example: Parameterized Decorator
```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello {name}")

greet("Alice")
```

**Output:**
```
Hello Alice
Hello Alice
Hello Alice
```

---

## Key Takeaways
- Decorators let you **extend behavior** without modifying function code.
- They are heavily used in ML frameworks (e.g., TensorFlow uses `@tf.function`).
- Mastering decorators improves code modularity and interview confidence.
