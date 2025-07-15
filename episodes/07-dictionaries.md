---
title: Dictionaries
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives



::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I store multiple values that are not indexed by position?

::::::::::::::::::::::::::::::::::::::::::::::::::

Based on Toby Hodges' dictionary chapter in the EMBL ITPP course.

## Looking up data

Lists store many values together; this is fine if you are really really careful and you don’t need
to change the arrays that much. Otherwise, it is prone to errors. Dictionaries are similar to lists,
but instead of holding an ordered collection of values, they hold key-value pairs.

- Use a *dictionary* to store many key-value pairs together.
  - Contained within angled brackets `{...}`.
  - Values separated by commas `,`.
  - key-value pairs connected with colons `:`.
- Use `len` to find out how many key-value pairs are in a dictionary.

```python
student_numbers = { 'Bioscience Technology': 16, 
                    'Computational Biology': 12,
                    'Post-Genomic Biology': 20,
                    'Ecology and Environmental Management': 3,
                    'Maths in the Living Environment': 0
                  }
print('#students:', student_numbers)
print('length:', len(student_numbers))
```

```output
#students: {'Bioscience Technology': 16, 'Computational Biology': 12, 'Post-Genomic Biology': 20, 'Ecology and Environmental Management': 3, 'Maths in the Living Environment': 0}
length: 5
```

## Use a value's key to fetch it from a dictionary

```python
print('#students in Bioscience Technology:', student_numbers['Bioscience Technology'])
print('#students in Post-Genomic Biology:', student_numbers['Post-Genomic Biology'])
```

```output
#students in Bioscience Technology: 16
#students in Post-Genomic Biology: 20
```

There is also a method called get() that will give you the same result:

```python
print('#students in Bioscience Technology:', student_numbers.get('Bioscience Technology'))
```

```output
#students in Bioscience Technology: 16
```

## Get Keys

The keys() method will return a list of all the keys in the dictionary.

```python
student_numbers.keys()
```

```output
dict_keys(['Bioscience Technology', 'Computational Biology', 'Post-Genomic Biology', 'Ecology and Environmental Management', 'Maths in the Living Environment'])
```

## Dictionaries' values can be replaced by assigning to them

- Use a key on the left of assignment to replace a value.

```python
student_numbers['Bioscience Technology'] = 2
print('student_numbers is now:', student_numbers)
```

```output
student_numbers is now: {'Bioscience Technology': 2, 'Computational Biology': 12, 'Post-Genomic Biology': 20, 'Ecology and Environmental Management': 3, 'Maths in the Living Environment': 0}
```

The same effect can be achieved with the `update()` function:

```python
student_numbers.update({'Maths in the Living Environment'}: 120)
print('student_numbers is now:', student_numbers)
```

```output
student_numbers is now: {'Bioscience Technology': 2, 'Computational Biology': 12, 'Post-Genomic Biology': 20, 'Ecology and Environmental Management': 3, 'Maths in the Living Environment': 120}
```

- `update` is a *method* of dictionaries.
  - Like a function, but tied to a particular object.
- Use `object_name.method_name` to call methods.
  - Deliberately resembles the way we refer to things in a library.

## Adding items to a dictionary

If you try to assign a value to a key that doesn’t exist, Python creates the entry for you
automatically. This is how new items are usually added to the dictionary, by using a new index key
and assigning a value to it.

```python
temperatures = {
    "Monday": 22,
    "Tuesday": 24,
    "Wednesday": 21,
    "Thursday": 23,
    "Friday": 25
}
print('temperatures is initially:', temperatures)

temperatures["Saturday"] = 24
print('temperatures has become:', temperatures)
```

```output
temperatures is initially: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25}
temperatures has become: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25, 'Saturday': 24}
```

The same can be achieved with the `update()` function:

```python
temperatures.update({"Sunday": 26})
print('temperatures has become: ', temperatures)
```

```output
temperatures has become: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25, 'Saturday': 24, 'Sunday': 26}
```


- We will meet other methods of lists as we go along.
  - Use `help(list)` for a preview.
- `extend` is similar to `append`, but it allows you to combine two lists.  For example:

```python
teen_primes = [11, 13, 17, 19]
middle_aged_primes = [37, 41, 43, 47]
print('primes is currently:', primes)
primes.extend(teen_primes)
print('primes has now become:', primes)
primes.append(middle_aged_primes)
print('primes has finally become:', primes)
```

```output
primes is currently: [2, 3, 5, 7]
primes has now become: [2, 3, 5, 7, 11, 13, 17, 19]
primes has finally become: [2, 3, 5, 7, 11, 13, 17, 19, [37, 41, 43, 47]]
```

Note that while `extend` maintains the "flat" structure of the list, appending a list to a list means
the last element in `primes` will itself be a list, not an integer. Lists can contain values of any
type; therefore, lists of lists are possible.

## Use `del` to remove items from a list entirely

- We use `del list_name[index]` to remove an element from a list (in the example, 9 is not a prime number) and thus shorten it.
- `del` is not a function or a method, but a statement in the language.

```python
primes = [2, 3, 5, 7, 9]
print('primes before removing last item:', primes)
del primes[4]
print('primes after removing last item:', primes)
```

```output
primes before removing last item: [2, 3, 5, 7, 9]
primes after removing last item: [2, 3, 5, 7]
```

## The empty list contains no values

- Use `[]` on its own to represent a list that doesn't contain any values.
  - "The zero of lists."
- Helpful as a starting point for collecting values
  (which we will see in the [next episode](07-for-loops.md)).

## Lists may contain values of different types

- A single list may contain numbers, strings, and anything else.

```python
goals = [1, 'Create lists.', 2, 'Extract items from lists.', 3, 'Modify lists.']
```

## Character strings can be indexed like lists

- Get single characters from a character string using indexes in square brackets.

```python
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
```

```output
zeroth character: c
third character: b
```

## Character strings are immutable

- Cannot change the characters in a string after it has been created.
  - *Immutable*: can't be changed after creation.
  - In contrast, lists are *mutable*: they can be modified in place.
- Python considers the string to be a single value with parts,
  not a collection of values.

```python
element[0] = 'C'
```

```error
TypeError: 'str' object does not support item assignment
```

- Lists and character strings are both *collections*.

## Indexing beyond the end of the collection is an error

- Python reports an `IndexError` if we attempt to access a value that doesn't exist.
  - This is a kind of [runtime error](04-built-in.md).
  - Cannot be detected as the code is parsed
    because the index might be calculated based on data.

```python
print('99th element of element is:', element[99])
```

```output
IndexError: string index out of range
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Fill in the Blanks

Fill in the blanks so that the program below produces the output shown.

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

:::::::::::::::  solution

## Solution

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:]
print('second time:', values)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## How Large is a Slice?

If `start` and `stop` are both non-negative integers,
how long is the list `values[start:stop]`?

:::::::::::::::  solution

## Solution

The list `values[start:stop]` has up to `stop - start` elements.  For example,
`values[1:4]` has the 3 elements `values[1]`, `values[2]`, and `values[3]`.
Why 'up to'? As we saw in [episode 2](02-variables.md),
if `stop` is greater than the total length of the list `values`,
we will still get a list back but it will be shorter than expected.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## From Strings to Lists and Back

Given this:

```python
print('string to list:', list('tin'))
print('list to string:', ''.join(['g', 'o', 'l', 'd']))
```

```output
string to list: ['t', 'i', 'n']
list to string: gold
```

1. What does `list('some string')` do?
2. What does `'-'.join(['x', 'y', 'z'])` generate?

:::::::::::::::  solution

## Solution

1. [`list('some string')`](https://docs.python.org/3/library/stdtypes.html#list) converts a string into a list containing all of its characters.
2. [`join`](https://docs.python.org/3/library/stdtypes.html#str.join) returns a string that is the *concatenation*
  of each string element in the list and adds the separator between each element in the list. This results in
  `x-y-z`. The separator between the elements is the string that provides this method.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Working With the End

What does the following program print?

```python
element = 'helium'
print(element[-1])
```

1. How does Python interpret a negative index?
2. If a list or string has N elements,
  what is the most negative index that can safely be used with it,
  and what location does that index represent?
3. If `values` is a list, what does `del values[-1]` do?
4. How can you display all elements but the last one without changing `values`?
  (Hint: you will need to combine slicing and negative indexing.)

:::::::::::::::  solution

## Solution

The program prints `m`.

1. Python interprets a negative index as starting from the end (as opposed to
  starting from the beginning).  The last element is `-1`.
2. The last index that can safely be used with a list of N elements is element
  `-N`, which represents the first element.
3. `del values[-1]` removes the last element from the list.
4. `values[:-1]`
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Stepping Through a List

What does the following program print?

```python
element = 'fluorine'
print(element[::2])
print(element[::-1])
```

1. If we write a slice as `low:high:stride`, what does `stride` do?
2. What expression would select all of the even-numbered items from a collection?

:::::::::::::::  solution

## Solution

The program prints

```python
furn
eniroulf
```

1. `stride` is the step size of the slice.
2. The slice `1::2` selects all even-numbered items from a collection: it starts
  with element `1` (which is the second element, since indexing starts at `0`),
  goes on until the end (since no `end` is given), and uses a step size of `2`
  (i.e., selects every second element).
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Slice Bounds

What does the following program print?

```python
element = 'lithium'
print(element[0:20])
print(element[-1:3])
```

:::::::::::::::  solution

## Solution

```output
lithium

```

The first statement prints the whole string, since the slice goes beyond the total length of the string.
The second statement returns an empty string, because the slice goes "out of bounds" of the string.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Sort and Sorted

What do these two programs print?
In simple terms, explain the difference between `sorted(letters)` and `letters.sort()`.

```python
# Program A
letters = list('gold')
result = sorted(letters)
print('letters is', letters, 'and result is', result)
```

```python
# Program B
letters = list('gold')
result = letters.sort()
print('letters is', letters, 'and result is', result)
```

:::::::::::::::  solution

## Solution

Program A prints

```output
letters is ['g', 'o', 'l', 'd'] and result is ['d', 'g', 'l', 'o']
```

Program B prints

```output
letters is ['d', 'g', 'l', 'o'] and result is None
```

`sorted(letters)` returns a sorted copy of the list `letters` (the original
list `letters` remains unchanged), while `letters.sort()` sorts the list
`letters` in-place and does not return anything.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Copying (or Not)

What do these two programs print?
In simple terms, explain the difference between `new = old` and `new = old[:]`.

```python
# Program A
old = list('gold')
new = old      # simple assignment
new[0] = 'D'
print('new is', new, 'and old is', old)
```

```python
# Program B
old = list('gold')
new = old[:]   # assigning a slice
new[0] = 'D'
print('new is', new, 'and old is', old)
```

:::::::::::::::  solution

## Solution

Program A prints

```output
new is ['D', 'o', 'l', 'd'] and old is ['D', 'o', 'l', 'd']
```

Program B prints

```output
new is ['D', 'o', 'l', 'd'] and old is ['g', 'o', 'l', 'd']
```

`new = old` makes `new` a reference to the list `old`; `new` and `old` point
towards the same object.

`new = old[:]` however creates a new list object `new` containing all elements
from the list `old`; `new` and `old` are different objects.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A list stores many values in a single structure.
- Use an item's index to fetch it from a list.
- Lists' values can be replaced by assigning to them.
- Appending items to a list lengthens it.
- Use `del` to remove items from a list entirely.
- The empty list contains no values.
- Lists may contain values of different types.
- Character strings can be indexed like lists.
- Character strings are immutable.
- Indexing beyond the end of the collection is an error.

::::::::::::::::::::::::::::::::::::::::::::::::::


