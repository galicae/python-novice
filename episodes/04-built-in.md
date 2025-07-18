---
title: Built-in Functions and Help
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose of functions.
- Correctly call built-in Python functions.
- Correctly nest calls to built-in functions.
- Use help to display documentation for built-in functions.
- Correctly describe situations in which SyntaxError and NameError occur.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I use built-in functions?
- How can I find out what they do?
- What kind of errors can occur in programs?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use comments to add documentation to programs

```python
# This sentence isn't executed by Python.
adjustment = 0.5   # Neither is this - anything after '#' is ignored.
```

## A function may take zero or more arguments

- We have seen some functions already --- now let's take a closer look.
- An *argument* is a value passed into a function.
- `len` takes exactly one.
- `int`, `str`, and `float` create a new value from an existing one.
- `print` takes zero or more.
- `print` with no arguments prints a blank line.
  - Must always use parentheses, even if they're empty,
    so that Python knows a function is being called.

```python
print('before')
print()
print('after')
```

```output
before

after
```

## Every function returns something

- Every function call produces some result.
- If the function doesn't have a useful result to return,
  it usually returns the special value `None`. `None` is a Python
  object that stands in anytime there is no value.

```python
result = print('example')
print('result of print is', result)
```

```output
example
result of print is None
```

## Commonly-used built-in functions include `max`, `min`, and `round`

- Use `max` to find the largest value of one or more values.
- Use `min` to find the smallest.
- Both work on character strings as well as numbers.
  - "Larger" and "smaller" use (0-9, A-Z, a-z) to compare letters.

```python
print(max(1, 2, 3))
print(min('a', 'A', '0'))
```

```output
3
0
```

## Functions may only work for certain (combinations of) arguments

- `max` and `min` must be given at least one argument.
  - "Largest of the empty set" is a meaningless question.
- And they must be given things that can meaningfully be compared.

```python
print(max(1, 'a'))
```

```error
TypeError                                 Traceback (most recent call last)
<ipython-input-52-3f049acf3762> in <module>
----> 1 print(max(1, 'a'))

TypeError: '>' not supported between instances of 'str' and 'int'
```

## Functions may have default values for some arguments

- `round` will round off a floating-point number.
- By default, rounds to zero decimal places.

```python
round(3.712)
```

```output
4
```

- We can specify the number of decimal places we want.

```python
round(3.712, 1)
```

```output
3.7
```

## Functions attached to objects are called methods

- Functions take another form that will be common in the pandas episodes.
- Methods have parentheses like functions, but come after the variable.
- Some methods are used for internal Python operations, and are marked with double underlines.

```python
my_string = 'Hello world!'  # creation of a string object 

print(len(my_string))       # the len function takes a string as an argument and returns the length of the string

print(my_string.swapcase()) # calling the swapcase method on the my_string object

print(my_string.__len__())  # calling the internal __len__ method on the my_string object, used by len(my_string)

```

```output
12
hELLO WORLD!
12
```

- You might even see them chained together.  They operate left to right.

```python
print(my_string.isupper())          # Not all the letters are uppercase
print(my_string.upper())            # This capitalizes all the letters

print(my_string.upper().isupper())  # Now all the letters are uppercase
```

```output
False
HELLO WORLD
True
```

:::::::::::::::::::::::::::::::::::::::  challenge

## More built-in string functions!

Strings are very common value types, and we will be using them constantly. In particular, when
reading files, everything is mostly assumed to be a string until defined otherwise. Have a look at
the [string methods](https://www.w3schools.com/python/python_strings_methods.asp). Which of those
methods might be useful to us?

:::::::::::::::  solution

## Solution

All of the methods have a reason for existing, and they are very useful in their context. However,
for our immediate future, there are a couple that could make our life much easier if they are on our
short-term memory (or cheat sheet!):

- [startswith()](https://www.w3schools.com/python/ref_string_startswith.asp),
  [endswith()](https://www.w3schools.com/python/ref_string_endswith.asp), and
  [find()](https://www.w3schools.com/python/ref_string_find.asp) are all very good at locating
  words or letters within bigger strings. One use example: we are scanning the rows of a file and
  looking for all rows that start with a special symbol.
- [count()](https://www.w3schools.com/python/ref_string_count.asp): finds and counts all occurrences
  of a word/letter within a bigger string.
- [replace()](https://www.w3schools.com/python/ref_string_replace.asp): given a string, replace all
  occurrences of a letter/word with another letter/word.
- [lstrip()](https://www.w3schools.com/python/ref_string_lstrip.asp),
  [rstrip()](https://www.w3schools.com/python/ref_string_rstrip.asp), and plain
  [strip()](https://www.w3schools.com/python/ref_string_strip.asp) are great for removing whitespace
  characters (like newlines) at the beginning/end of strings. This is very useful when reading text
  files.
- [split()](https://www.w3schools.com/python/ref_string_split.asp): if a string (e.g. a line of a
  text file) has some sort of delimiter (e.g. the comma in the row of a CSV file), we can use this
  function to break up the string into the chunks indicated by the delimiter.


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Practice!

Using just string built-in methods, solve the Rosalind exercises
[DNA](https://rosalind.info/problems/dna/) and [RNA](https://rosalind.info/problems/rna/)!

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## GC content

The GC content of a DNA string is the percentage of guanine or cytosine in the sequence, and it is a
useful indicator of sequence origin (e.g. bacterial sequences often have much higher GC content than
metazoan ones). Calculate the GC content of the following sequence:

```python
dna = "CCACCCTCGTGGTATGGCTAGGCATTCAGGAACCGGAGAACGCTTCAGACCAGCCCGGACTGGGAACCTGCGGGCAGTAGGTGGAAT"
```

::::::::::::::::::::::::::::::::::::::::::::::::::


## Use the built-in function `help` to get help for a function

- Every built-in function has online documentation.

```python
help(round)
```

```output
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.
    
    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

## The Jupyter Notebook has two ways to get help

- Option 1: Place the cursor near where the function is invoked in a cell
  (i.e., the function name or its parameters),
  - Hold down <kbd>Shift</kbd>, and press <kbd>Tab</kbd>.
  - Do this several times to expand the information returned.
- Option 2: Type the function name in a cell with a question mark after it. Then run the cell.

## Python reports a syntax error when it can't understand the source of a program

- Won't even try to run the program if it can't be parsed.

```python
# Forgot to close the quote marks around the string.
name = 'Feng
```

```error
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
```

```python
# An extra '=' in the assignment.
age = = 52
```

```error
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
```

- Look more closely at the error message:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- The message indicates a problem on first line of the input ("line 1").
  - In this case the "ipython-input" section of the file name tells us that
    we are working with input into IPython,
    the Python interpreter used by the Jupyter Notebook.
- The `-6-` part of the filename indicates that
  the error occurred in cell 6 of our Notebook.
- Next is the problematic line of code,
  indicating the problem with a `^` pointer.

## Python reports a runtime error when something goes wrong while a program is executing {#runtime-error}

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError                                 Traceback (most recent call last)
<ipython-input-59-1214fb6c55fc> in <module>
      1 age = 53
----> 2 remaining = 100 - aege # mis-spelled 'age'

NameError: name 'aege' is not defined
```

- Fix syntax errors by reading the source and runtime errors by tracing execution.

## Other ways to get help
There are several other ways that people often get help when they are stuck with their Python code.

* Search the internet: 
  paste the last line of your error message or the word "python" and a short description of what you want to do into your favourite search engine 
  and you will usually find several examples where other people have encountered the same problem and came looking for help.
    * [StackOverflow](https://stackoverflow.com/questions) can be particularly helpful for this: answers to questions are presented as a ranked thread ordered according to how useful other users found them to be.
    * **Take care:** copying and pasting code written by somebody else is risky unless you understand exactly what it is doing!
* ask somebody "in the real world". 
  If you have a colleague or friend with more expertise in Python than you have, show them the problem you are having and ask them for help.
* Sometimes, the act of articulating your question can help you to identify what is going wrong.
  This is known as ["rubber duck debugging"](https://en.wikipedia.org/wiki/Rubber_duck_debugging) among programmers.

### Generative AI

::::::::::::::::::::::::::::: instructor

### Choose how to teach this section
The section on generative AI is intended to be concise but Instructors may choose to devote more time to the topic in a workshop.
Depending on your own level of experience and comfort with talking about and using these tools, you could choose to do any of the following:

* Explain how large language models work and are trained, and/or the difference between generative AI, other forms of AI that currently exist, and the limits of what LLMs can do (e.g., they can't "reason").
* Demonstrate how you recommend that learners use generative AI.
* Discuss the ethical concerns listed below, as well as others that you are aware of, to help learners make an informed choice about whether or not to use generative AI tools.

This is a fast-moving technology. 
If you are preparing to teach this section and you feel it has become outdated, please open an issue on the lesson repository to let the Maintainers know and/or a pull request to suggest updates and improvements.

::::::::::::::::::::::::::::::::::::::::

It is increasingly common for people to use _generative AI_ chatbots such as ChatGPT to get help while coding. 
You will probably receive some useful guidance by presenting your error message to the chatbot and asking it what went wrong. 
However, the way this help is provided by the chatbot is different. 
Answers on StackOverflow have (probably) been given by a human as a direct response to the question asked. 
But generative AI chatbots, which are based on an advanced statistical model, respond by generating the _most likely_ sequence of text that would follow the prompt they are given.

While responses from generative AI tools can often be helpful, they are not always reliable. 
These tools sometimes generate plausible but incorrect or misleading information, so (just as with an answer found on the internet) it is essential to verify their accuracy.
You need the knowledge and skills to be able to understand these responses, to judge whether or not they are accurate, and to fix any errors in the code it offers you.

In addition to asking for help, programmers can use generative AI tools to generate code from scratch; extend, improve and reorganise existing code; translate code between programming languages; figure out what terms to use in a search of the internet; and more.
However, there are drawbacks that you should be aware of.

The models used by these tools have been "trained" on very large volumes of data, much of it taken from the internet, and the responses they produce reflect that training data, and may recapitulate its inaccuracies or biases.
The environmental costs (energy and water use) of LLMs are a lot higher than other technologies, both during development (known as training) and when an individual user uses one (also called inference). For more information see the [AI Environmental Impact Primer](https://huggingface.co/blog/sasha/ai-environment-primer) developed by researchers at HuggingFace, an AI hosting platform. 
Concerns also exist about the way the data for this training was obtained, with questions raised about whether the people developing the LLMs had permission to use it.
Other ethical concerns have also been raised, such as reports that workers were exploited during the training process.

**We recommend that you avoid getting help from generative AI during the workshop** for several reasons:

1. For most problems you will encounter at this stage, help and answers can be found among the first results returned by searching the internet.
2. The foundational knowledge and skills you will learn in this lesson by writing and fixing your own programs  are essential to be able to evaluate the correctness and safety of any code you receive from online help or a generative AI chatbot. 
   If you choose to use these tools in the future, the expertise you gain from learning and practising these fundamentals on your own will help you use them more effectively.
3. As you start out with programming, the mistakes you make will be the kinds that have also been made -- and overcome! -- by everybody else who learned to program before you. 
  Since these mistakes and the questions you are likely to have at this stage are common, they are also better represented than other, more specialised problems and tasks in the data that was used to train generative AI tools.
  This means that a generative AI chatbot is _more likely to produce accurate responses_ to questions that novices ask, which could give you a false impression of how reliable they will be when you are ready to do things that are more advanced.


:::::::::::::::::::::::::::::::::::::::  challenge

## What Happens When

1. Explain in simple terms the order of operations in the following program:
  when does the addition happen, when does the subtraction happen,
  when is each function called, etc.
2. What is the final value of `radiance`?

```python
radiance = 1.0
radiance = max(2.1, 2.0 + min(radiance, 1.1 * radiance - 0.5))
```

:::::::::::::::  solution

## Solution

1. Order of operations:
  1. `1.1 * radiance = 1.1`
  2. `1.1 - 0.5 = 0.6`
  3. `min(radiance, 0.6) = 0.6`
  4. `2.0 + 0.6 = 2.6`
  5. `max(2.1, 2.6) = 2.6`
2. At the end, `radiance = 2.6`
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Spot the Difference

1. Predict what each of the `print` statements in the program below will print.
2. Does `max(len(rich), poor)` run or produce an error message?
  If it runs, does its result make any sense?

```python
easy_string = "abc"
print(max(easy_string))
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

:::::::::::::::  solution

## Solution

```python
print(max(easy_string))
```

```output
c
```

```python
print(max(rich, poor))
```

```output
tin
```

```python
print(max(len(rich), len(poor)))
```

```output
4
```

`max(len(rich), poor)` throws a TypeError. This turns into `max(4, 'tin')` and
as we discussed earlier a string and integer cannot meaningfully be compared.

```error 
TypeError                                 Traceback (most recent call last)
<ipython-input-65-bc82ad05177a> in <module>
----> 1 max(len(rich), poor)

TypeError: '>' not supported between instances of 'str' and 'int'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Why Not?

Why is it that `max` and `min` do not return `None` when they are called with no arguments?

:::::::::::::::  solution

## Solution

`max` and `min` return TypeErrors in this case because the correct number of parameters
was not supplied. If it just returned `None`, the error would be much harder to trace as it
would likely be stored into a variable and used later in the program, only to likely throw
a runtime error.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Last Character of a String

If Python starts counting from zero,
and `len` returns the number of characters in a string,
what index expression will get the last character in the string `name`?
(Note: we will see a simpler way to do this in a later episode.)

:::::::::::::::  solution

## Solution

`name[len(name) - 1]`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reflection exercise

Reflect on and discuss the following:

- What are the different kinds of errors Python will report?
- Did the code always produce the results you expected? If not, why?
- Is there something we can do to prevent errors when we write code?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Explore the Python docs!

The [official Python documentation](https://docs.python.org/3/) is arguably the most complete
source of information about the language. It is available in different languages and contains a lot of useful
resources. The [Built-in Functions page](https://docs.python.org/3/library/functions.html) contains a catalogue of
all of these functions, including the ones that we've covered in this lesson. Some of these are more advanced and
unnecessary at the moment, but others are very simple and useful.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use comments to add documentation to programs.
- A function may take zero or more arguments.
- Commonly-used built-in functions include `max`, `min`, and `round`.
- Functions may only work for certain (combinations of) arguments.
- Functions may have default values for some arguments.
- Use the built-in function `help` to get help for a function.
- The Jupyter Notebook has two ways to get help.
- Every function returns something.
- Python reports a syntax error when it can't understand the source of a program.
- Python reports a runtime error when something goes wrong while a program is executing.
- Fix syntax errors by reading the source code, and runtime errors by tracing the program's execution.

::::::::::::::::::::::::::::::::::::::::::::::::::