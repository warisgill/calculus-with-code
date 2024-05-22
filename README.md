Let's break down the concept of matching a quadratic function to another function in a simpler way, without involving the Taylor series.

### Understanding Quadratic Function Approximation

Imagine you have a complex function, like the sine function, and you want to approximate it with a simpler function, specifically a quadratic function (which is a parabola). A quadratic function looks like this:

\[ g(x) = ax^2 + bx + c \]

Our goal is to find the coefficients \( a \), \( b \), and \( c \) so that this quadratic function behaves similarly to our complex function near a specific point. 

### Steps to Approximate a Function with a Quadratic Function

1. **Select a Point \( x_0 \):**
   - This is the point where you want the quadratic function to closely match the complex function. For example, you might choose \( x_0 = -1.5 \), \( 0.0 \), or \( 2.0 \).

2. **Match the Function Value at \( x_0 \):**
   - Ensure that the quadratic function \( g(x) \) has the same value as the complex function at \( x_0 \). 
   - For sine function, this means setting \( g(x_0) = \sin(x_0) \).

3. **Match the Slope at \( x_0 \):**
   - The slope (rate of change) of the quadratic function at \( x_0 \) should be the same as the slope of the sine function at \( x_0 \). 
   - The slope of the sine function is given by the cosine function, so we ensure \( g'(x_0) = \cos(x_0) \).

4. **Match the Curvature at \( x_0 \):**
   - The curvature (how much the function bends) of the quadratic function at \( x_0 \) should be the same as the curvature of the sine function at \( x_0 \).
   - For the sine function, the curvature at \( x_0 \) can be derived from its second derivative, which is related to the sine function itself.

### Applying These Steps in Code

The provided code does exactly this:

1. **Compute the Sine Function:**
   ```python
   xs = torch.arange(-torch.pi, torch.pi, 0.01)
   plots = [torch.sin(xs)]
   ```
   - `xs` generates values from `-π` to `π`.
   - `plots` initially contains the sine values for these points.

2. **Compute Quadratic Approximations:**
   ```python
   for x0 in [-1.5, 0.0, 2.0]:
       plots.append(torch.sin(torch.tensor(x0)) + (xs - x0) * torch.cos(torch.tensor(x0)) - (xs - x0)**2 * torch.sin(torch.tensor(x0)) / 2)
   ```
   - For each point \( x_0 \), it calculates the quadratic approximation.
   - The formula used ensures the quadratic function \( g(x) \) matches the sine function’s value, slope, and curvature at \( x_0 \).

3. **Plotting:**
   ```python
   d2l.plot(xs, plots, 'x', 'f(x)', ylim=[-1.5, 1.5])
   ```
   - This plots the sine function and its quadratic approximations.

### Real-Life Applications

1. **Simplifying Complex Functions:**
   - Approximations make complex functions easier to work with. For instance, in physics, it’s often useful to approximate complex motions with simple quadratic equations for small intervals.

2. **Optimization Problems:**
   - In many fields like economics and machine learning, finding optimal points (like maximum profit or minimum error) can be simplified by using quadratic approximations.

3. **Computer Graphics:**
   - Quadratic curves are used to render smooth shapes and surfaces efficiently.

### Summary

The idea is to create a simpler quadratic function that mimics the behavior of a more complex function around a chosen point. This involves matching the value, slope, and curvature of the quadratic function to the original function at that point. This approximation helps in simplifying calculations and solving real-world problems efficiently.