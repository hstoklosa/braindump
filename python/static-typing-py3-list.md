# Static Typing in Python 3

## Using `typing` module vs built-in types

Until Python 3.9 added support for type hinting using standard collections, you had to use `typing.Tuple` and `typing.List` to annotate the types of elements in a list or tuple.

```python
def f(points: Tuple[float, float]):
    return map(do_stuff, points)
```

Up until Python 3.8, `tuple` and `list` did not support being [_used as generic types_](https://docs.python.org/3/library/typing.html#generics). The above example documents that the function f requires the points argument to be a tuple with 2 float values.

> **∗** &nbsp;[`typing.Tuple`](https://docs.python.org/3/library/typing.html#typing.Tuple) lets you specify a specific number of elements expected and the type of each position. Use ellipsis if the length is not set and the type should be repeated .

> **∗** &nbsp;`Tuple[float, ...]` describes a variable-length tuple with floats.

For [`typing.List`](https://docs.python.org/3/library/typing.html#typing.List) and other sequence types you generally only specify the type for all elements; `List[str]` is a list of strings, of any size.

Note that functions should preferentially take [`typing.Sequence`](https://docs.python.org/3/library/typing.html#typing.Sequence) as arguments and `typing.List` is typically only used for return types.

In general, most functions would take any sequence and only iterate, but when you return a `list`, you really are returning a specific, mutable sequence type.

Implementing a custom container type with the type supporting generics requires either:

- implementing a [\_\_class_getitem\_\_ hook](https://docs.python.org/3/reference/datamodel.html#emulating-generic-types)
- inheriting from [`typing.Generic`](https://docs.python.org/3/library/typing.html#typing.Generic), which subsequently implements \_\_class_getitem\_\_

## TL;DR - list vs List

Not all lists are the same from a typing perspective.

The program won't fail a static type checker, even though it won't run.

```python
def f(some_list: list):
    return [i+2 for i in some_list]

f(['a', 'b', 'c'])
```

By contrast, you can specify the contents of the list using the abstract types from typing will fail, as it should.

```python
def f(some_list: List[int]) -> List[int]:
    return [i+2 for i in some_list]

f(['a', 'b', 'c'])
```

> Note: PEP 585 changes in Python 3.9 enables `list[int]` ...

## References

- [Using List/Tuple/etc from typing vs directly referring type as list/tuple/etc](https://stackoverflow.com/a/39458225)

- [Static typing in python3: list vs List](https://stackoverflow.com/a/52629475)
