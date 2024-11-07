# Lexicographic Ordering

Lexicographical order is essentially alphabetical order, but it applies to any characters, not just letters. It's the same way words are ordered in a dictionary. When comparing characters:

1. Each character has a specific ASCII or Unicode value
2. Characters are compared based on these values
3. 'a' comes before 'b', 'b' before 'c', and so on

## Examples of Lexicographical Comparison

- `'a' < 'b'` _(a is lexicographically smaller than b)_
- `'z' < 'aa'`
- `'B' < 'b'` _(uppercase letters come before lowercase in ASCII)_
- `'1' < 'A'` _(numbers come before letters in ASCII)_

## Examples in a problem

When the problem asks for the "smallest character that is lexicographically greater than target", it's asking for the next character that would come after the target in dictionary order.

### Example I:

```
Input: letters = ['c','f','j'], target = 'd'
Output: 'f'
Explanation: 'f' is the next available character that comes after 'd' in dictionary order
```

### Example 2:

```
Input: letters = ['c','f','j'], target = 'j'
Output: 'c'
Explanation: No character in the array comes after 'j', so we return the first character
```
