# Intro to Python for calculus

In this section, we'll review some of the elements of core Python that feature in our notebooks.
If you're an experienced Python programmer, you'll no doubt find some omissions and shortcomings in our documentation.
Suggestions are welcome! These labs have been written by mathematicians with no formal training in programming,
and are rather utilitarian in nature.

## Basic arithmetic operations

One thing to keep in mind, if you're coming from a C++ background, is that most of the time in Python,
we don't need to worry about specifying data types (until we do...)
If you ask Python to perform the sum `4+3`, it will do so, and return 7.
If you ask for `4/3`, you will get a floating point answer, rather than a fraction.
(If you want to get a fraction, see the [SymPy documentation](./sympy.md).)

Basic operations are:

- Addition: `4+3`
- Subtraction: `4-3`
- Multiplication: `4*3`
- Division: `4/3`
- Exponentiation: `4**3` (Caution: Python will not understand `4^3`, even if that's what you're used to.)

It's a good idea to do some playing around; in particular, do some experiments with order of operation,
and determine for yourself when parentheses are (and aren't) needed.
(Of course, a few extra parentheses won't hurt.)

**Note:** one of the most common errors that students run into in their calculus labs is forgetting the multiplication operator.
We're used to writing expressions like `2x` that have an implied multiplication,
but this will not be understood by Python. You must enter `2*x`.

## Variables and print statements

With multi-step calculations, it is often useful to assign variable names.
This is also useful if we want to later change the numbers in our calculuations.

For example, instead of computing the sum `4+3` directly, we could enter the information as follows:
```
a = 4
b = 3
c = a+b
```

If you run this code in a Jupyter code cell, nothing will happen.
Well, nothing that you can see. The computer has stored this information, but you haven't asked it to do anything with it.
If you want to see the result of the addition, you need to use the `print` command:
```
print(c)
```
Note that if we put `4+3` in a code cell and run it, we get the output immediately.

We can also store and print string variables in a similar fashion:
```
string_var = "Hey, I'm a string!"
print(string_var)
```
will produce the output `Hey, I'm a string!`.

**Caution**: running an operation like `4+3` will automatically produce output.
But in a Jupyter notebook, this is only true if it's the last (or only) line in your cell.
If you enter
```
4+3
4*3
4-3
```
and run it, the only output you'll get is `1` (the result of doing `4-3`).
If you want to get all three outputs from a single cell, you can use the `print` command.
See what happens if you do:
```
print(4+3)
print(4*3)
print(4-3)
```


## Functions

A *function* in Python is just like a function in mathematics: you define it by saying what it should do to a given input.
Then, if you give your function an input, it will provide you with the corresponding output.
The syntax for defining a function is as follows:

```
def f(x):
    return x**2+4
```

This defines the function $f(x)=x^2+4$. But note that Python will not communicate your function to you in this way.
Indeed, if you try running the command `print(f(x))`, you will get an error, 
since we haven't told the computer what `x` is!
The command `print(f)` is no better: you'll get an output like `<function f at 0x7f27cd037880>` that is probably not very illuminating.

However, your function *has* been defined, and it *will* give you output, as long as you first give it input.
Enter `f(2)` and you'll get the output `8`, which is indeed the value of $2^2+4$.

**Note:** the indentation above is an essential part of Python syntax!
Your function definition won't work without it.
Fortunately, when you're working in a Jupyter notebook,
as long as you remember the colon at the end of the first line,
the computer will add the indentation for you as soon as you hit enter.

A quicker way to define a function is to use Python's `lambda` syntax.
This is especially useful if you need to define a function inline as part of a larger program.
Instead of the function definition we did above, an equivalent syntax is:
```
f = lambda x : x**2+4
```
(It's faster, but until you get used to it, I'm not sure the syntax is any easier to remember!)

## Lists and arrays

Most of the time, we won't be interested in evaluating a function at a single point.
Instead, we'll want to evaluate a function on a whole list of points,
and produce a list of output values as a result.
(These might then be used for something like plotting a graph of the function.)

Most often, we will be working with lists when using the [NumPy library](./numpy.md) for numerical computations.
In that context, the content of our list will be floating point numbers, and the list is called an **array**.
(An array is really just a special type of list, where all the entries have the same data type, which is usually `int` or `float`.
Arrays come from libraries like NumPy and aren't built into Python.)

Lists entries don't have to be of the same type. It's also important to note that a list:
- is *ordered*
- can contain *duplicates*
- can be changed (the Python word for this is *mutable*)

In particular, we can start with an empty list and then populate it.
Some examples:
```
empty_list = []
mixed_list = [1, 3.4, "Hello world", True]
integer_list = [0,1,2,3,4,5,6,7,8,9]
```
Note that lists are always denoted by square brackets.

### Operations with lists

One of the simplest things we can do with a list is get its length.
Try running:
```
print(len(empty_list))
print(len(mixed_list))
```

The `type` command will give the data type of a list, but this is unlikely to be needed in a calculus lab.

The `append` command is quite useful, as this lets us add items to a list.
For example, if we run
```
empty_list = []
empty_list.append(3)
print(empty_list)
```
the output will be `[3]`. 

Often this is done as part of a `for` loop. If we want to append our list 10 times, we can do the following:
```
empty_list = []
for i in range(10):
    empty_list.append(i)
print(empty_list)
```

Again note the importance of the indentation for the `for` loop.
The output of the above will be `[0,1,2,3,4,5,6,7,8,9]`. We asked for 10 steps,
and the computer obliged. But the computer always starts counting at zero!

One of the things we'll need to be able to do is access list items.
Here is some of the syntax for doing so, for a list named `L`:

- the whole list: `L[:]`
- everything after (and including) index position `i`: `L[i:]`
- everything before index position `i`: `L[:i]`
- everything before the position `j` steps from the end: `L[:-j]`
- everything after (and including) the position `j` steps from the end: `L[-j:]`

(For the last two, "from the end" is meant in the sense that one step from the end is the last entry.)

For example, if `L` is a partition of an interval, and we want to do a Riemann sum,
the list `L[1:]` consists of all points in the partition except the first one, which is what you want for right endpoints.
If you want left endpoints, you would use the list `L[:-1]`, which consists of everything except the last point.

If you need further details on working with lists, you will find plenty of [help online](https://www.w3schools.com/python/python_lists.asp).



