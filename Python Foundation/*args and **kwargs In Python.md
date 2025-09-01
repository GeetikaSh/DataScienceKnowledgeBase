# *args and **kwargs in Python

In Python, `*args` and `**kwargs` are used in function definitions to allow passing a variable number of arguments.

## *args

- `*args` allows a function to accept any number of positional arguments.
- The arguments are received as a tuple.

**Example:**
```python
def print_args(*args):
    for arg in args:
        print(arg)
print_args(1, 2, 3)
# Output:
# 1
# 2
# 3
```

## **kwargs
- **kwargs allows a function to accept any number of keyword arguments.
- The arguments are received as a dictionary.

```python
def print_kwargs(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_kwargs(a=1, b=2)
# Output:
# a: 1
# b: 2
```

## Using Both Together
You can use both in the same function to accept any combination of positional and keyword arguments.

**Example:**
```python
def demo(*args, **kwargs):
    print("args:", args)
    print("kwargs:", kwargs)

demo(1, 2, a=3, b=4)
# Output:
# args: (1, 2)
# kwargs: {'a': 3, 'b': 4}
```

## When to Use
- When you want your function to be flexible and accept any number of arguments.
- Useful for wrapper functions, decorators, and APIs.

```
*args = variable positional arguments (tuple)
**kwargs = variable keyword arguments (dict)
```