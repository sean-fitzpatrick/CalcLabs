# Intro to SymPy for Calculus

By Raheem Mir

Python has many powerful librairies that add convenience and functionality. One of them being SymPy, a feature rich library designed for symbolic mathematics. We can use it to simplify algebraic expressions, solve equations, and perform calculus tasks like evaluating limits or computing integrals. SymPy gives us exact symbolic answers instead of numerical approximations, handling math like we would on paper, which makes it a great tool for intuitively exploring calculus concepts.

If you want to try the code on this page, you can open it as an [interactive notebook](./IntrotoSymPy.ipynb)

## Getting Started With SymPy

To begin using SymPy we start by "importing" the library:


```python
import sympy as sy
sy.init_printing() 
```

`import sympy as sy` loads in the SymPy library for us to use. We give it the shorthand name `sy`, so every time we call something from SymPy, we prefix it with `sy.`. This is a good way to keep things organized when we are working with multiple libraries.

`sy.init_printing()` calls SymPy's `init_printing()` function, which gets the output to be displayed as nicely formatted mathematics.

A good next step is telling SymPy the variables we would like to use with the `symbols()` function:


```python
x, y = sy.symbols('x y')  # this makes x and y symbols
```

When creating a symbol using the `symbols()` function, we can specify additional arguments that can modify SymPy's assumptions when it's dealing with the symbol. These assumptions determine how SymPy handles a symbol in situations like square roots, solving, simplifications, and so on. For instance, `positive=True` tells SymPy that a particular symbol is a positive number, while using `real=True` indicates that a symbol represents a real number. 

A common task in SymPy is creating symbolic expressions to represent functions. The syntax is no different from assigning a variable.  
Let's represent $f(x) = x^2 - 2x + 1$ in SymPy!


```python
f = x**2 -2*x + 1  # defining a symbolic expression
```


```python
f # outputting f(x)
```

It is important to note that we are not actually creating a Python function here, which would be defined on an input/output basis, rather we are creating a symbolic representation of a function, that can be easily manipulated with algebra and/or calculus. As such, trying something like `f(5)` would return an error. To substitute values into `f`, we would use the `subs()` function:


```python
f.subs(x, 4) #substituting 4 in for x
```

SymPy also gives us a function for factoring a polynomial, `factor()`:


```python
sy.factor(f)
```

SymPy implements many of the common mathematical functions as well:


```python
sy.cos(x)
```


```python
sy.tan(x)
```


```python
sy.pi, sy.exp(x)  # constants pi and e
```


```python
sy.Abs(x)  # absolute value
```

## Limits

With SymPy, we can use its `limit()` function to compute and evaluate limits. The syntax is as follows:

```python
sy.limit(expression, variable, value)
```

`expression` is the SymPy representation of the function whose limit we are trying to find.  
`variable` represents the variable that is approaching a specific value, and must be a SymPy symbol.  
`value` represents the value the variable is approaching. If we are dealing with limits at infinity, we can use `sy.oo` and `-sy.oo` to dentote positive and negative infinity. 

To compute one-sided limits, we can add a fourth argument to the function, either a `'+'` or `'-'` for a right or left hand limit.

Let's evaluate $\displaystyle \lim_{x\to 0}\frac{\sin(x)}{x}$ with the `limit()` function:


```python
f = sy.sin(x) / x   # representing the function
f
```


```python
sy.limit(f, x, 0)  # calling the limit() function
```

Since we set our symbolic representation equal to a variable, `f`, we could have also called `limit()` like this:


```python
f.limit(x, 0)
```

Note that we can also directly pass in a SymPy expression to the `limit()` function instead of using a variable. 

Let's use the `limit()` function to find the value of $\displaystyle \lim_{x\to 0}\dfrac{\cos(x) - 1}{x}$. 


```python
sy.limit((sy.cos(x) - 1)/x, x, 0)
```

Let's try adding a fourth argument in our call to `limit()`, and work with one-sided limits:  
$\displaystyle \lim_{x\to 0^-}\dfrac{1}{x}$ 


```python
sy.limit(1/x, x, 0, '-')
```

$\displaystyle \lim_{x\to 0^+}\dfrac{1}{x}$


```python
sy.limit(1/x, x, 0, '+')
```

Now let's explore a limit where $x$ is approaching $\infty$: 

$\displaystyle \lim_{x\to \infty}\dfrac{x^2 - 1}{3 - x}$


```python
sy.limit((x**2 - 1) / (3 - x), x, sy.oo)
```

## Derivatives

To take derivatives we can use SymPy's `diff()` function:

```python
sy.diff(function,variable, ...)
```

`function` is the function we are differentiating. Note that this is a SymPy represenation of a function, not a traditional Python function.  
`variable` is the variable with respect to which we are differentiating. This must be defined as a SymPy symbol.  
`...` represents the possibility of adding further arguments, namely for higher order derivatives.


Given the function $f(x) = 4x^2 + 6x - 2$ let's find $f'(x)$ using the `diff()` function:


```python
f = 4*x**2 + 6*x - 2  # defining a symbolic representation of f(x)
f  
```


```python
f_prime = sy.diff(f, x)   # differentiating f with respect to x
f_prime
```

Like before, we have some freedom with the syntax when calling the `diff()` function:


```python
f_prime = f.diff(x) 
f_prime
```

Now let's differentiate $g(x) = x^2\sin(x)$ with `diff()`:


```python
g = sy.sin(x)*x**2
g_prime = g.diff(x)
g_prime
```

The `diff()` function can also compute higher order derivatives, as we simply add more arguments to our function call! This is not unlike how we add a tick (or prime) to our notation when taking the next higher order derivative when working on paper.

Given $f(x) = \sin(x)$ let's find its second and third derivatives:


```python
f1 = sy.sin(x)
fpp = f1.diff(x, x) # second derivative of f(x)
fppp = f1.diff(x, x, x) # third derivative of f(x)

print(fpp, fppp)
```

Instead of writing out a particular variable multiple times, we can also compute higher order derivatives like this:


```python
fpp = f1.diff(x, 2)
fppp = f1.diff(x, 3)

print(fpp, fppp)
```

## Plotting

SymPy also provides functionality for visualizing / plotting functions:

We simply use the `plot()` function, like so:  
```python
sy.plot(f, domain, ...)
```
`f` represents the function (or functions) we are visualizing, which can be written explicitly or passed in as a variable.   

`domain` refers to the interval we are the plotting the function(s) over, the default is $[-10, 10]$.    

`...` alludes to the many optional arguments we can use to change the plot's appearance and behaviour.   
An example would be the argument `show=False`, which stops the graph from being displayed until we use the command, `.show()`.

Let's plot $f(x) = x^2$ over the interval $[-5, 5]$:


```python
p = sy.plot(x**2, (x, -5, 5))  # notice how we input the domain
```

Interestingly, we don't need to type `p` on the next line for the plot to output, like we'd have to when using other SymPy functions. Also, we save our plot to a variable as it's more efficient when we are manipulating/adjusting an existing plot, or wanting more control over customization. 

Now let's plot $f(x) = \sin(5x)$ on the interval $[0, 2\pi]$ and add an optional argument to change the color of the line!


```python
p1 = sy.plot(sy.sin(5*x), (x, 0, sy.pi*2), line_color='purple')   # using SymPy's built in functions for sin and pi
```

Here we plot $f(x) = \ln(x)$ on the interval $[-10, 10]$. Like with the trigonomtric functions, we'll be using SymPy's built in function for natural logarithms, `sy.ln()`. Remember that $[-10, 10]$ is the default domain so we don't need to write it.


```python
p2 = sy.plot(sy.ln(x), line_color="green")
```


SymPy's plotting functionality also gives us the ability to plot multiple functions together, allowing us to combine different plots. 

Let's illustrate this with an example, by plotting the following equations:  

$y = x$, $y = x^2$ , $y = x^3$, and $y = x^4$ over the interval $[0, 2]$:


```python
multi_plot = sy.plot(x, x**2, x**3, x**4, (x, 0, 2), legend=True)  # adding a legend to our plot
```

SymPy also lets us combine existing plots, with the `extend()` function:


```python
plot_a = sy.plot(-x**2, show=False) 
plot_b = sy.plot(-x, show=False)
plot_a.extend(plot_b)
plot_a.show()
```

Notice how we added the `show=False` parameter to our plots, so they do not output until we use `.show()`. 

## Integration

To compute integrals we can use SymPy's `integrate` function:

For indefinite integrals (antiderivatives), the syntax is quite similar to the `diff()` function: 
```python
sy.integrate(expression, variable)
```

`expression` is a SymPy representation of the function we want to integrate.  

`variable` is the variable of integration and must be defined as a SymPy symbol.

One thing to note is that SymPy does not include a constant of integration (the "$+ c$").

For definite integrals the syntax changes a bit:
```python
sy.integrate(expression, (variable, lower_limit, upper_limit)) 
```
`expression` is the same as with indefinite integrals, a SymPy representation of the function we want to integrate. 

`(variable, lower_limit, upper_limit)` is known as a tuple in Python, a container of more arguments, where:  

`variable` is the same as with indefinite integrals, the variable of integration that must be defined as a SymPy symbol.  

`lower_limit` and `upper_limit` are the lower and upper bounds of integration.


Let's evaluate the indefinite integral $\int \sin(x) \ dx$ with the `integrate()` function:


```python
indef_integral = sy.integrate(sy.sin(x), x)
indef_integral
```

Now let's evaluate the indefinite integral $\int x^3 \ dx$ with `integrate()`:


```python
indef_integral1 = sy.integrate(x**3, x)
indef_integral1
```

Next, let's look at evaluating definite integrals with the `integrate()` function:

$\int_{-3}^{3} x^7 - x^3 \, dx$



```python
def_integral = sy.integrate(x**7 - x**3, (x, -3, 3))
def_integral 
```

Now, let's evaluate the definite integral $\int_{1}^{2} e^x \, dx$


```python
def_integral1 = sy.integrate(sy.exp(x), (x, 1, 2))
def_integral1 
```

After computing $\int_{1}^{2} e^x \, dx$ symbolically (the result is kept as an exact value), we can also find its numerical value with SymPy's `evalf()` function:


```python
numerical_result = def_integral1.evalf()
numerical_result
```