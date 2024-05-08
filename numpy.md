# Intro to NumPy for Calculus (markdown)

By Raheem Mir

When it comes numerical computation, NumPy is the Python package / library of choice, offering performance and lots of functionality, making it a powerful tool for doing calculus.

## Getting Started With NumPy

To begin using NumPy, we start by "importing" the library:


```python
import numpy as np
```

`import numpy as np` loads in NumPy for us to use. We give it the shorthand name `np`, meaning every time we call something from NumPy, we prefix it with `np.`. This is a good way to keep things organized when we are working with multiple libraries.

NumPy implements many of the common mathematical functions, like trigonometric functions, logarithms and more: 


```python
np.sin(0) 
```


```python
np.pi/4
```


```python
np.tan(np.pi/4)
```


```python
np.arctan(1)
```


```python
np.e
```


```python
np.log(np.e)  #np.log is the natural logarithm, NumPy also offers base 10 and base 2 logarithms
```

## Working with Arrays

The defining feature of NumPy is the NumPy array, a powerful data structure optimized for numerical computation. Think of them as the Python lists we've seen before (in Intro to Python for Calculus), but significantly more efficient and powerful, well suited for performing calculus tasks. Additionally, the many mathematical functions (as well as others) implemented in NumPy can be directly applied to arrays without the need for loops (less code, more functionality).

Creating a NumPy array is straightforward, generally we use the `np.array()` function:


```python
primes = np.array([2,3,5,7,11,13])  # creating an array of prime numbers
print(primes)
```

NumPy also provides specialized functions for creating arrays, one of them being `np.linspace()`, which generates a set of evenly spaced values over a given interval (inclusive). This function is particularly useful for calculus tasks, from generating $x$-values to plot a function, to defining intervals for numerical approximations like Riemann sums. 

The syntax is as follows:
```python
np.linspace(a, b, N)
```
`a` is the beginning of the interval, while `b` is the end of the interval.    
`N` specifies the number of values to generate in between `a` and `b`.

Here we create a NumPy array of 11 evenly spaced values between 0 and 1:


```python
x = np.linspace(0, 1, 11)
print(x) 
```

Like with lists, we can access individual elements of a NumPy array by specifying their index, which **starts at 0** (i.e. the first element is at index 0).

Here's how we would access (and output) the first two elements of the array `x`:


```python
print(x[0], x[1])
```

To access elements from the end of an array, we use negative indices. For instance, `[-1]` would specify the last index of an array.  

Below is how we would access the last three elements of `x`:


```python
print(x[-3], x[-2], x[-1])
```

Using a colon `:` inside the `[]`  allows us to select a range of elements from an array, which is known as "slicing". For example, `x[:]` would access the entire array:


```python
x[:] # retrieves all the elements of the array
```

To retrieve the entries after a certain index, we would place the `:` to the right of the index value inside the `[]`:


```python
x[2:] # outputs the elements from the third index onwards 
```

To retrieve the entries before a particular index, we would place the `:` to the left of the index value inside the `[]`:


```python
x[:7] # outputs the first 7 elements
```

We can also explicitly state the starting and ending index of what we want to access:


```python
x[3:8] # Retrieves elements from index 3 up to, but not including, index 8
```

Although we'll most often be using `np.linspace()` for our NumPy arrays, here is a brief overview of some of the other functions available:

`np.arange(a, b, step)` generates a NumPy array with values starting at `a` up to, but not including, `b`. The `step` parameter let's you control the difference between consecutive values in the array.   

`np.ones(N)` generates an array of only 1's, with a length of N.

`np.zeros(N)` is similar to `np.ones()`, generating an array of only 0's, with a length of N.


```python
even_numbers = np.arange(0, 20, 2)
print(even_numbers)
```


```python
ones = np.ones(10)
print(ones)
```


```python
zeros = np.zeros(20)
print(zeros)
```

## Plotting With NumPy and Matplotlib

We can use NumPy in conjunction with Matplotlib, the popular Python plotting library, to visualize functions.

First, we have to import Matplotlib, in particular, its `pyplot` module:


```python
import matplotlib.pyplot as plt
```

Here is the general framework for creating a basic plot:

1. Generating $x$ values: This often involves using the `np.linspace()` function.
   
3. Generating $y$ values: This typically includes defining or using a function to compute the `y` values.
   
5. Creating the plot: Call the `plt.plot()` function, passing in the $x$ and $y$ values, to create the plot.
   
7. Customize the plot (Optional): Use additional Matplotlib functions, such as `plt.xlabel()`, or `plt.grid()`, to customize the plot.
   
9. Displaying the plot: Use the `plt.show()` function to display the plot. In a Jupyter Notebook environment, this step is not neccessary, as plots display automatically when you call `plt.plot()`. However, it is still recommended to use `plt.show()`, for a cleaner output and proper rendering.

Now let's plot $\cos(x)$ over the interval $[-2\pi, 2\pi]$:

First, let's generate our $x$-values using `np.linspace()`:


```python
x1 = np.linspace(-2*np.pi, 2*np.pi, 100)
```

Next, we can define $y$ as a function $x$ using NumPy's `np.cos()` function:


```python
y1 = np.cos(x1)
```

Now we can create and display our plot, passing in our $x$ and $y$ values to the `plt.plot()` function, as well as calling the `plt.show()` function to display it. You'll notice that we've added some axis labels as well.


```python
plt.plot(x1,y1)  # creating the plot
plt.xlabel('x')  
plt.ylabel('cos(x)')
plt.show()  # displaying the plot
```

Now, let's try plotting the function $f(x) = x^3 - x^2 -x + 1$ over the interval $[-5, 5]$:

First, let's generate our $x$-values with `np.linspace()`:


```python
x2 = np.linspace(-5, 5, 500)  
```

Next, let's define the function we want to plot and generate our $y$-values:


```python
def f(x):
    return x**3 - x**2 - x + 1
```


```python
y2 = f(x2)
```

 To create and display the plot, we use the `plt.plot()` and `plt.show()` functions:


```python
plt.plot(x2,y2)  # creating the plot
plt.xlabel('x')  
plt.ylabel('f(x)')
plt.show()
```
