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

The `keys()` method will return a list of all the keys in the dictionary.

```python
student_numbers.keys()
```

```output
dict_keys(['Bioscience Technology', 'Computational Biology', 'Post-Genomic Biology', 'Ecology and Environmental Management', 'Maths in the Living Environment'])
```

## Get Values

Similarly, the `values()` method will return a list of all the values in the dictionary.

```python
student_numbers.values()
```

```output
dict_values([16, 12, 20, 3, 0])
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Both? Why not both?

If you wish to get keys and values at the same time (for example to iterate over them and do
something with each key/value pair), you can use the `items()` method. We will revisit this later,
when we talk about loops.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Dictionaries are ordered

The way that dictionaries are implemented in Python fundamentally changed in v3.6, resulting in them
taking up ~1/2 the space and working ~2x as fast as they used to. A side effect of this is that
dictionary objects in Python 3.6 remember the order that entries were created in and you should be
able to access their entries in this order. Regardless, in the examples and exercises in this
course, we assume that this order cannot be relied upon - this is not yet considered a 'stable'
feature of the language i.e. future versions of Python are not guaranteed to preserve the order of
dictionaries. When writing your own code, if you want to access dictionary entries in a particular
order, you should make sure to do so by providing keys in a specific order.


::::::::::::::::::::::::::::::::::::::::::::::::::


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
    'Monday': 22,
    'Tuesday': 24,
    'Wednesday': 21,
    'Thursday': 23,
    'Friday': 25
}
print('temperatures is initially:', temperatures)

temperatures['Saturday'] = 24
print('temperatures has become:', temperatures)
```

```output
temperatures is initially: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25}
temperatures has become: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25, 'Saturday': 24}
```

The same can be achieved with the `update()` function:

```python
temperatures.update({'Sunday': 26})
print('temperatures has become: ', temperatures)
```

```output
temperatures has become: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25, 'Saturday': 24, 'Sunday': 26}
```

Like lists, dictionaries can contain values of any type; therefore, dictionaries of lists or
dictionaries of dictionaries are possible.

:::::::::::::::::::::::::::::::::::::::  challenge

## Nested dictionaries

Fill in the blanks so that the program below produces the indicated output:

```python
grades = {'Juan': {'Maths': 2},
          'John': {'History': 1, 'Biology': 3},
          'Gianni': {'Biology': 1}}

grades['Juan'][______] = 2
grades['Juan'][______] = 1

grades[______]['Maths'] = 1

grades[______]['History'] = 4
grades[______][______] = 3

print(grades)
```

```output
{'Juan': {'Maths': 2, 'History': 2, 'Biology': 1}, 'John': {'History': 1, 'Biology': 3, 'Maths': 1}, 'Gianni': {'Biology': 1, 'History': 4, 'Maths': 3}}
```

:::::::::::::::  solution

## Solution

You can choose how you want to fill in the gaps; but if we assign the subjects by the order they
were introduced, this would be the solution:

```python
grades = {'Juan': {'Maths': 2},
          'John': {'History': 1, 'Biology': 3},
          'Gianni': {'Biology': 1}}

grades['Juan']['History'] = 2
grades['Juan']['Biology'] = 1

grades['John']['Maths'] = 1

grades['Gianni']['History'] = 4
grades['Gianni']['Maths'] = 3

print(grades)
```

```output
{'Juan': {'Maths': 2, 'History': 2, 'Biology': 1}, 'John': {'History': 1, 'Biology': 3, 'Maths': 1}, 'Gianni': {'Biology': 1, 'History': 4, 'Maths': 3}}
```

Notice that the subject order reflects the order in which the key/value pairs were added!

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use `del` to remove items from a dictionary entirely

- We use `del dict_name[key]` to remove an element from a dictionary (in the example, 'Everyday' is
  not a day of the week).
- `del` is not a function or a method, but a statement in the language.

```python
temperatures = {
    'Monday': 22,
    'Tuesday': 24,
    'Wednesday': 21,
    'Thursday': 23,
    'Friday': 25,
    'Everyday': 49    
}
print('temperature before removing Everyday:', temperatures)
del temperatures['Everyday']
print('temperature after removing Everyday:', temperatures)
```

```output
temperature before removing Everyday: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25, 'Everyday': 49}
temperature after removing Everyday: {'Monday': 22, 'Tuesday': 24, 'Wednesday': 21, 'Thursday': 23, 'Friday': 25}
```

## The empty dictionary contains no values

- Use `{}` on its own to represent a dictionary that doesn't contain any values.
  - "The zero of dictionaries."
- Helpful as a starting point for collecting values.


## Indexing will not work on dictionaries

- If we want to retrieve the 4th item of a dictionary, we can't simply ask for it by index:

```python
print(temperatures[3])
```

```output
Traceback (most recent call last):
  File "<python-input-19>", line 1, in <module>
    print(temperatures[3])
          ~~~~~~~~~~~~^^^
KeyError: 3
```

Python reports a `KeyError`; this indicates that it searched the dictionary's keys for the key `3`
(careful: 3 the integer, not the string "3"), and didn't find it. If we _really, really_ want the
fourth item of the dictionary (see ["Dictionaries are ordered"](#dictionaries-are-ordered) above),
we can ask for the value associated with _the fourth key_:

```python
keys = list(temperatures.keys())
fourth_key = keys[3]
print('temperature on the fourth day:', temperatures[fourth_key])
```

```output
temperature on the fourth day: 23
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Practice

Complete the W3Schools training exercises for

- [dictionaries](https://www.w3schools.com/python/exercise.asp?x=xrcise_dictionaries1)
- [accessing dictionaries](https://www.w3schools.com/python/exercise.asp?x=xrcise_dictionaries_access1)
- [changing dictionaries](https://www.w3schools.com/python/exercise.asp?x=xrcise_dictionaries_change1)
- [adding items](https://www.w3schools.com/python/exercise.asp?x=xrcise_dictionaries_add1)

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Nested dictionaries

Consider this syntax:

```python
a = {'name' : 'John', 'age' : '20'}
b = {'name' : 'May', 'age' : '23'}
customers = {'c1' : a, 'c2' : b}
```

what will be a correct syntax for printing the name 'May'?

- `print(customers['c2']['name'])`
- `print(customers.c2.b['name'])`
- `print(customers.c2.name)`

:::::::::::::::  solution

## Solution

To access a value in a dictionary we need to use its key. May is customer "c2", so first we need to
specify that:

```python
may_customer = customers['c2']
```

The variable `may_customer` contains the value saved under the key `'c2'`, namely the dictionary
`b`. Within that, the value "May" is saved under the key `'name'`:

```python
print(may_customer['name'])
```

```output
May
```

Let's put it together:

```python
print(customers['c2']['name'])
```

```output
May
```


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A dictionary stores many values as key-value pairs.
- Use the key of a value to fetch it from a dictionary.
- Dictionaries' values can be replaced by assigning to them.
- Setting a value to a key will update it, if it exists, or create it, if it doesn't.
- Use `del` to remove items from a dictionary entirely.
- The empty dictionary contains no key/value pairs.
- Dictionaries may contain keys and values of different types.
- Trying to use indices to summon key/value pairs is an error.

::::::::::::::::::::::::::::::::::::::::::::::::::


