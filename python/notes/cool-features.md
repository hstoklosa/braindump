# Cool Features

## 1. Functional Programming

### Lambda Functions

```python
def square_fn(x):
    return x * x

square_ld = lambda x: x * x

for i in range(10):
    assert square_fn(i) == square_ld(i)
```

### Higher-Order Functions

#### Map and Filter

`map(fn, iterable)` applies the fn to all elements of the `iterable` and returns a new iterable with the results.

```python
nums = [1/3, 333/7, 2323/2230, 40/34, 2/3]
nums_squared = [num * num for num in nums]

print(nums_squared)

> [0.1111111, 2263.04081632, 1.085147, 1.384083, 0.44444444]
```

equivalent to calling `map` with a callback function:

```python
nums_squared_1 = map(square_fn, nums)
nums_squared_2 = map(lambda x: x * x, nums)

print(list(nums_squared_1))

> [0.1111111, 2263.04081632, 1.085147, 1.384083, 0.44444444]
```

You can also use `map` with more than one iterable.

```python
a, b = 3, -0.5
xs = [2, 3, 4, 5]
labels = [6.4, 8.9, 10.9, 15.3]

# Method 1: using a loop
errors = []
for i, x in enumerate(xs):
    errors.append((a * x + b - labels[i]) ** 2)
result1 = sum(errors) ** 0.5 / len(xs)

# Method 2: using map
diffs = map(lambda x, y: (a * x + b - y) ** 2, xs, labels)
result2 = sum(diffs) ** 0.5 / len(xs)

print(result1, result2)

> 0.35089172119045514 0.35089172119045514
```

```python
bad_preds = filter(lambda x: x > 0.5, errors)

print(list(bad_preds))

> [0.8100000000000006, 0.6400000000000011]
```

```python
product = 1
for num in nums:
    product *= num

print(product)

> 12.95564683272412
```

equivalent to calling using `reduce` with a lambda:

```python
from functools import reduce
product = reduce(lambda x, y: x * y, nums)

print(product)

> 12.95564683272412
```

### Note on lambda functions

Lambda functions are meant for one time use. Each time `lambda x: f(x)` is called, the function has to be recreated, which negatively impacts performance.

## 2. List Manipulation

### 2.1 Unpacking

```python
elems = [1, 2, 3, 4]
a, b, c, d = elems

print(a, b, c, d)

> 1 2 3 4
```

```python
a, *new_elems, d = elems

print(a)
print(new_elems)
print(d)

> 1
> [2, 3]
> 4
```

### 2.2 Slicing

```python
elems = list(range(10))

print(elems)

> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(elems[::-1])

> [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

```python
del elems[::2]
print(elems)

==> [1, 3, 5, 7, 9]
```

### 2.3 Insertion

```python
elems = list(range(10))
elems[1] = 10

print(elems)

> [0, 10, 2, 3, 4, 5, 6, 7, 8, 9]
```

```python
elems = list(range(10))
elems[1:2] = [20, 30, 40]

print(elems)

> [0, 20, 30, 40, 2, 3, 4, 5, 6, 7, 8, 9]
```

```python
elems = list(range(10))
elems[1:1] = [0.2, 0.3, 0.5]

print(elems)

> [0, 0.2, 0.3, 0.5, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 2.4 Flattening

```python
list_of_lists = [[1], [2, 3], [4, 5, 6]]

sum(list_of_lists, [])

> [1, 2, 3, 4, 5, 6]
```

Nested lists can be flattened using a recursive function.

```python
nested_lists = [[1, 2], [[3, 4], [5, 6], [[7, 8], [9, 10], [[11, [12, 13]]]]]]
flatten = lambda x: [y for l in x for y in flatten(l)] if type(x) is list else [x]

flatten(nested_lists)
```

### 2.5 List vs generator

```python
tokens = ['i', 'want', 'to', 'go', 'to', 'school']

def ngrams(tokens, n):
    length = len(tokens)
    grams = []

    for i in range(length - n + 1):
        grams.append(tokens[i:i+n])

    return grams

print(ngrams(tokens, 3))

> [['i', 'want', 'to'],
   ['want', 'to', 'go'],
   ['to', 'go', 'to'],
   ['go', 'to', 'school']]
```

Instead, you can use a generator to save memory i.e., _O(m+n)_ instead of _O(mn)_.

```python
def ngrams(tokens, n):
    length = len(tokens)
    for i in range(length - n + 1):
        yield tokens[i:i+n]

ngrams_generator = ngrams(tokens, 3)

print(ngrams_generator)

> <generator object ngrams at 0x1069b26d0>

for ngram in ngrams_generator:
    print(ngram)

> [['i', 'want', 'to'],
   ['want', 'to', 'go'],
   ['to', 'go', 'to'],
   ['go', 'to', 'school']]
```

Another way is to use slices.

```python
def ngrams(tokens, n):
    length = len(tokens)
    slices = (tokens[i:length-n+i+1] for i in range(n))
    return zip(*slices)

ngrams_generator = ngrams(tokens, 3)
print(ngrams_generator)

> <zip object at 0x1069a7dc8> # zip objects are generators

for ngram in ngrams_generator:
    print(ngram)

> [['i', 'want', 'to'],
   ['want', 'to', 'go'],
   ['to', 'go', 'to'],
   ['go', 'to', 'school']]
```

## 3. Classes and magic methods

```python
class Node:
    """ A struct to denote the node of a binary tree.
    It contains a value and pointers to left and right children.
    """
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

root = Node(5)
print(root)

> <__main__.Node object at 0x1069c4518>
```

```python
class Node:
    """ A struct to denote the node of a binary tree.
    It contains a value and pointers to left and right children.
    """
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

    def __repr__(self):
        strings = [f'value: {self.value}']
        strings.append(f'left: {self.left.value}' if self.left else 'left: None')
        strings.append(f'right: {self.right.value}' if self.right else 'right: None')
        return ', '.join(strings)

left = Node(4)
root = Node(5, left)
print(root)

> 5, 4, None
```

```python
class Node:
    """ A struct to denote the node of a binary tree.
    It contains a value and pointers to left and right children.
    """
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

    def __eq__(self, other):
        return self.value == other.value

    def __lt__(self, other):
        return self.value < other.value

    def __ge__(self, other):
        return self.value >= other.value


left = Node(4)
root = Node(5, left)
print(left == root)
print(left < root)
print(left >= root)

> False
> True
> False
```

List of all magic methods in the [docs](https://docs.python.org/3/reference/datamodel.html#special-method-names).

Also check out the answer [this answer](https://stackoverflow.com/a/28059785) on StackOverflow.

```python
class Node:
    """ A struct to denote the node of a binary tree.
    It contains a value and pointers to left and right children.
    """
    __slots__ = ('value', 'left', 'right')
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right
```

## 4. local namespace, object's attributes

```python
class Model1:
    def __init__(self, hidden_size=100, num_layers=3, learning_rate=3e-4):
        print(locals())
        self.hidden_size = hidden_size
        self.num_layers = num_layers
        self.learning_rate = learning_rate

model1 = Model1()

> {'learning_rate': 0.0003, 'num_layers': 3, 'hidden_size': 100, 'self': <__main__.Model1 object at 0x1069b1470>}
```

```python
print(model1.__dict__)

> {'hidden_size': 100, 'num_layers': 3, 'learning_rate': 0.0003}
```

```python
class Model2:
    def __init__(self, hidden_size=100, num_layers=3, learning_rate=3e-4):
        params = locals()
        del params['self']
        self.__dict__ = params

model2 = Model2()
print(model2.__dict__)

> {'learning_rate': 0.0003, 'num_layers': 3, 'hidden_size': 100}
```

```python
class Model3:
    def __init__(self, **kwargs):
        self.__dict__ = kwargs

model3 = Model3(hidden_size=100, num_layers=3, learning_rate=3e-4)
print(model3.__dict__)

> {'hidden_size': 100, 'num_layers': 3, 'learning_rate': 0.0003}
```

## 5. Wild import

This will import everything in module, even the imports of that module.

```python
from parts import *
```

e.g., `parts.py`

```python
import numpy
import tensorflow

class Encoder:
    ...

class Decoder:
    ...

class Loss:
    ...

def helper(*args, **kwargs):
    ...

def utils(*args, **kwargs):
    ...
```

```python
 __all__ = ['Encoder', 'Decoder', 'Loss']
import numpy
import tensorflow

class Encoder:
    ...
```

## 6. Decorator to time your functions

```python
def fib_helper(n):
    if n < 2:
        return n
    return fib_helper(n - 1) + fib_helper(n - 2)

def fib(n):
    """ fib is a wrapper function so that later we can change its behavior
    at the top level without affecting the behavior at every recursion step.
    """
    return fib_helper(n)

def fib_m_helper(n, computed):
    if n in computed:
        return computed[n]
    computed[n] = fib_m_helper(n - 1, computed) + fib_m_helper(n - 2, computed)
    return computed[n]

def fib_m(n):
    return fib_m_helper(n, {0: 0, 1: 1})
```

```python
for n in range(20):
    assert fib(n) == fib_m(n)
```

```python
import time

start = time.time()
fib(30)

print(f'Without memoization, it takes {time.time() - start:7f} seconds.')

> Without memoization, it takes 0.267569 seconds.

start = time.time()
fib_m(30)

print(f'With memoization, it takes {time.time() - start:.7f} seconds.')

> With memoization, it takes 0.0000713 seconds.
```

<br />

Decorators allow programmers to change the behavior of a function or class.

```python
def timeit(fn):
    # *args and **kwargs are to support positional and named arguments of fn
    def get_time(*args, **kwargs):
        start = time.time()
        output = fn(*args, **kwargs)
        print(f"Time taken in {fn.__name__}: {time.time() - start:.7f}")
        return output  # make sure that the decorator returns the output of fn
    return get_time
```

```python
@timeit
def fib(n):
    return fib_helper(n)

@timeit
def fib_m(n):
    return fib_m_helper(n, {0: 0, 1: 1})

fib(30)
fib_m(30)

> Time taken in fib: 0.2787242
> Time taken in fib_m: 0.0000138
```

## 7. Caching with @functools.lru_cache

For more information on cache, see [here](https://docs.python.org/3/library/functools.html).

```python
import functools

@functools.lru_cache()
def fib_helper(n):
    if n < 2:
        return n
    return fib_helper(n - 1) + fib_helper(n - 2)

@timeit
def fib(n):
    """ fib is a wrapper function so that later we can change its behavior
    at the top level without affecting the behavior at every recursion step.
    """
    return fib_helper(n)

fib(50)
fib_m(50)

> Time taken in fib: 0.0000412
> Time taken in fib_m: 0.0000281
```

<br>

_Source: [https://github.com/chiphuyen/python-is-cool](https://github.com/chiphuyen/python-is-cool)_
