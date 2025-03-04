---
dg-publish: true
tags: cs370
---
# Ordinary Differential Equations
#### General for of an ODE
$$F(n, y(n), y^{(1)}(n), y^{(2)}(n), \cdots, y^{(n)}(n)) = 0$$
where $y^{(i)}(n)$ is the $i^{th}$ derivative of $y(n)$

The highest order of the derivatives is called the **order of the ordinary differential equation**.

> [!warning] A closed-form is often unavailable in practice!
> Instead we may know a **relationship** between **variable** $y$ and its **derivative** $y’$ given by a known function $f$:
> $$y'(t) = f(t, y(t))$$

>[!example] The speed $v(t)$ of a car changes based on forces applied to it:
>$$v'(t) = F(t)/m$$

## Initial Value Problem
The general form is a differential equation
$$y'(t) = f(t, y(t))$$
where $f$ is specified, and the initial values are 
$$y(t_0) = y_0$$
> [!warning] There are two ways that out ODE problems will become more complicated
> 1. By involving more than one unknown variable (not just $y$): **Systems of differential equations**
> 2. By solving second, third, or higher derivatives (not just $y’$): **Higher order differential equations**

### Systems of Differential Equations
Consider a model with **multiple** variables that **interact**:
* E.g. $x$ and $y$ coordinates of a moving object.
This gives a system of differential equations, such as
![[Pasted image 20250303093144.png]]
* The matrix notation is specially helpful when $f_1$ and $f_2$ are linear
	* The $\vec{f}$ can be decomposed as a constant matrix and a vector containing the functions
>[!example]-
>![[Pasted image 20250303093328.png]]

### Higher Order Differential Equations
To start, we consider 1st order ODEs, involving only first derivative
$$y'(t) = f(t, y(t))$$Higher derivatives occur often in real problems. The order is the highest derivative in the equation:
$$y^{(n)}(t) = f(t, y(t), y'(t), y''(t), y'''(t), \cdots, y^{(n-1)}(t))$$
### Numerical Schemes for ODEs
Numerical solution is a discrete set of time/value pairs, $(t_i, y_i)$

> [!faq] What will an approximate solution look like?
> * **$y_i$ should approximate the true value, $y(t_i)$**

### Time-Stepping
Given initial conditions, we repeatedly step sequentially forward to the next time instant, using the derivative info, $y’$, and a timestep, h. 
Set $n = 0, t = t_0, y=y_0$:
1. Compute $y_{n+1}$
2. Increment time, $t_{n+1} = t_n + h$
3. Advance, $n = n+1$
4. Repeat
#### Categorizing time-stepping methods
**Single-step vs Multistep:**
* Do we use information only from he current time or from previous timesteps too?
**Explicit vs Implicit:**
* Is $y_{n+1}$ given as an explicit function to evaluate, or do we need to solve an implicit equation?
**Timestep size:**
* Do we use a constant timestep $h$, or allow it to vary?
##### Trade-offs
**Explicit:**
* Simpler and fast to compute **per step**
* **Less stable** - require smaller timesteps to avoid “blowing up”
**Implicit:**
* Often more complex and expensive to solve **per step**
* **More stable** - can safely use larger timesteps
#### Time-Stepping as a Recurrence
Time-stepping applies a **recurrence relation** to approximate the function values at later and later times
* Given $y_0$, approximate $y_1$. Given $y_1$, approximate $y_2$. etc.
#### Time-Stepping as a “Time Integration”
Time-stepping is also known as “time-integration”:
* We are **integrating over time** to approximate $y$ from $y’$
	* Approximating area under the curve
Better time-stepping schemes correspond to better approximations of the integral

#### Error of Time-Stepping
Absolute / global error at step $n$ is $|y_n - y(t_n)|$
* We can’t measure error **exactly** without knowing $y(t)$
* We will rely on the **Taylor series**
### Forward Euler
**Explicit, single-step scheme**
1. Compute the current slope: $y’_n = f(t_n, y_n)$
2. Step in a straight line with that slope: $y_{n+1} = y_n + h\cdot y’_n$
$$y_{n+1} = y_n + hf(t_n, y_n)$$
#### System of Equations
For systems of 1st order ODEs, we apply Forward Euler to each row in exactly the same way.
> [!example]-
> ![[Pasted image 20250303101510.png]]
#### Error of Forward Euler Method
F.E. is $$y_{n+1} = y_n + hf(t_n, y_n)$$
Taylor series is:
$$y_(t_{n+1}) = y(t_n) + hy'(t_n) + \frac{h^2}{2!}y''(t_n) + \frac{h^3}{3!}y'''(t_n) + \cdots$$
The error for one step is the difference between these, assuming **exact** data at time $t_n$
* i.e. $y_n = y(t_n)$
In this case, Forward Euler becomes:
$$y_{n+1} = y(t_n) + hy'(t_n)$$
The difference is:
$$y_{n+1} - y(t_{n+1}) = - \frac{h^2}{2!}y''(t_n) + O(h^3) = O(h^2)$$
This is the **Local Truncation Error (LTE)** of Forward Euler!
* As $h$ decreases, LTE decreases *quadratically*
### More accurate time-stepping
Keeping more terms in the series will help derive higher order schemes!
>[!warning] We don’t know $y’’$!

> [!success] Use a finite difference to **approximate** $y’’$
> $$y''(t_n) = \frac{y'(t_{n+1}) - y'(t_n)}{h} + O(h)$$

### Trapezoidal Rule
Trapezoidal Scheme is:
$$y_{n+1} = y_n + \frac{h}{2}[f(t_{n+1}, y_{n+1}) + f(t_n, t_n)]$$
The **Local Truncation Error** for trapezoidal rules is $O(h^3)$
> [!tldr]- Called trapezoidal because it turns the rectangles in integration into trapezoids
> ![[Pasted image 20250303103700.png]]

>[!warning] This is an implicit scheme
>Can we make it explicit?

### Modified / Improved Euler
1. Take forward Euler step to **estimate** the end point
2. Evaluate slope there
3. Use this **approximate** end-of-step slope in the trapezoidal formula
This looks like:
* $y^*_{n+1} = y_n + hf(t_n, y_n)$
* $y_{n+1} = y_n + \frac{h}{2}(f(t_n, y_n) + f(t_{n+1}, y^*_{n+1}))$
**Explicit scheme with LTE $O(h^3)$**
### Backwards Euler Method
**Implicit Scheme**
* Similar to forward Euler
$$y_{n+1} = y_n + hf(t_{n+1}, y_{n+1})$$
Its LTE is $O(h^2)$, like forward Euler
### Explicit “Runge Kutta” schemes
![[Pasted image 20250303111155.png]]
A family of explicit schemes (including improved Euler) written as:
$k_1 = hf(t_n, y_n)$
$k_2 = hf(t_n+h, y_n+k1)$
$y_{n+1} = y_n + \frac{k_1}{2} + \frac{k_2}{2}$
#### 4th Order Runge Kutta
LTE of $O(h^5)$
Similar schemes exist for higher orders, $O(h^\alpha)$ for $\alpha = 3, 4, 5, 6,\cdots$
$k_1 = hf(t_n, y_n)$
$k_2 = hf(t_n+\frac{h}{2}, y_n+\frac{k_1}{2})$
$k_3 = hf(t_n+\frac{h}{2}, y_n+\frac{k_2}{2})$
$k_4 = hf(t_n+h, y_n+k3)$
$y_{n+1} = y_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4)$
Again, evaluate $y’(t) = f(t,y)$ at various intermediate positions, and take a specific combination to find $y_{n+1}$
### Midpoint Method
**Another explicit Runge Kutta scheme** with LTE $O(h^3)$
$k_1 = hf(t_n, y_n)$
$k_2 = hf(t_n+\frac{h}{2}, y_n+\frac{k1}{2})$
$y_{n+1} = y_n + k_2$
Equivalent Expression
$y^*_{n+\frac{1}{2}} = y_n + \frac{h}{2}f(t_n, y_n)$
$y_{n+1} = y_n + hf(t_n + \frac{h}{2}, y^*_{n+\frac{1}{2}})$
## Local vs Global Error
The **Global Error** is the **total** error accumulated at the final time $t_{final}$
* Global error is typically more important since our goal is to predict some final future value
For a constant step $h$, computing from $t_0$ to end time $t_{final}$
$$ \#steps = \frac{t_{final} - t_0}{h} = O(h^{-1})$$
Then, for a given method we have:
$$ \text{(Global Error)} \leq \text{(Local Error)}\cdot O(h^{-1})$$
i.e. **one degree lower than LTE**

## Multi-step Schemes
One way to derive them is by fitting curves to current and earlier data points, for better slope estimates.
E.g. fit a quadratic to previous, current, and next step
### Backward Differentiation Formulas Methods (BDF)
BDF1, BDF2, BDF3, etc.
* Number indicates order of global error
**BDF1 = Backward Eular**
Generalize the backwards Euler scheme
$$y_{n+1} = y_{n} + hf(t_{n+1}, y_{n+1})$$
to higher order using earlier step info.
##### BDF2 uses current and previous step data:
$$y_{n+1} = \frac{4}{3}y_n-\frac{1}{3}y_{n-1} + \frac{2}{3}hf(t_{n+1}, y_{n+1})$$
BDF has LTE $O(h^3)$ and is a multi-step scheme
##### General Form
The same approach extends to higher orders, yielding implicit schemes with the general form
$$\sum^1_{k=-s+1}a_ky_{n+k} = hf(t_{n+1}, y_{n+1})$$
With $a_k$ being the coefficients.
### Explicit Multistep Scheme
#### Adams-Bashforth
e.g. 2nd order:
$$y_{n+1} = y_n + \frac{3}{2}hf(t_n, y_n) - \frac{1}{2}hf(t_{n-1}, y_{n-1})$$
LTE is $O(h^3)$

## Higher Order ODEs
The **order** of the ODE is the highest derivative that appears
* e.g. an ODE with at most third derivates gives a 3rd order ODE
### Converting to First Order
The general form for such a higher ODE looks like
$$y^{(n)} = f(t, y(t), y^{(1)}(t), y^{(2)}(t), \cdots, y^{(n-1)}(t))$$
We can convert them to **systems of first order ODEs**
* Change of variables
For each variable $y$ with more than a first derivative, introduce new variables:
$$ y_i = y^{(i-1)}$$
for $i = 1$ to $n$, so each derivative has a corresponding new variable
Substituting the new variables into the original ODE leads to:
1. One first order equation for each original equation
2. One or more additional equations relating the new variables
## Stability of Time-Stepping Schemes
Since errors are generally $O(h^p)$ for some $p$, our schemes are less accurate for large $h$.

But, error/perturbations in initial conditions may lead to vastly different or incorrect answers.
$$y'(t) = f(t, y(t)), y(0) = y_0 + \epsilon_0$$
If some initial error $\epsilon_0$ grows exponentially for many steps, our time-stepping scheme is **unstable**.
### Test Equation
We’ll consider a simple linear ODE, our “test equation”,
$$y'(t) = -\lambda y(t), y(0) = y_0$$
for constant $\lambda >0$.
The exact solution is $y(t)=y_0e^{-\lambda t}$
* Tends to 0 as $t \rightarrow \infty$
### Our Approach
1. Apply a given time stepping scheme to our test equation
2. Find the closed form of its numerical solution and error behaviour
3. Find the conditions on the timestep $h$ that ensure stability (error approaching zero)
#### Stability of Forward Euler
It is **conditionally stable** when $0 < h < \frac{2}{\lambda}$
#### Stability of Backward/Implicit Euler
It is **unconditionally stable**
> [!warning] Stability **does not** imply accuracy!
> Large time steps still usually induce Large truncation error
#### Stability of Improved Euler
It is **conditionally stable** when $h< \frac{2}{\lambda}$
* Same as Forward Euler
### Stability in general
For our linear test equation $y’ = -\lambda y$, forward Euler gave a bound related to 
$$\lambda = |\frac{\partial}{\partial y}(\lambda y) = |\frac{\partial f}{\partial y}|$$
For **nonlinear** problems, stability depends on $\frac{\partial f}{\partial y}$ (for dynamics function $f$) evaluated at a given point in time/space
For **systems** of ODEs, stability relates to the eigenvalues of the “Jacobian” matrix
$$\frac{\partial (f_1, f_2, f_3, \cdots, f_n)}{\partial (y_1, y_2, y_3, \cdots, y_n)}$$
### Truncation Error vs Stability
**Stability** tells us what our numerical algorithm itself does to small errors
**Truncation error** tells us how the accuracy of our numerical solution scales with time step$h$
>[!tldr] Both factors should be considered to get a useful solution
#### Determining LTE
1. Replace approximations on RHS with exact versions
2. Taylor expand all RHS quantities about time $t_n$
3. Taylor expand the exact solution $y(T_{n+1})$ to compare against
4. Compute difference $y(t_{n+1}) - y_{n+1}$. Lowest degree non-cancelling power of $h$ gives the LTE
### Time Step Control
#### Trade-offs
**Smaller $h$:** many steps, computationally expensive, more accurate
**Larger $h$:** fewer steps, so cheaper, but also less accurate
Minimize effort/cost by choosing largest $h$ with error still less than a desired tolerance:
$$\text{error < tolerance}$$
#### Adaptive Time-Stepping
Rate of change of the solution often varies over time!
* **Adapt the time step** during the computation to keep error small, while minimizing wasted effort
>[!problem]
>If we knew the error for a given $h$, we could choose a good $h$ to always satisfy error < tolerance
>
>… but if we already knew the exact error, we’d also know the solution
##### Approach
Use **two** different time-stepping schemes **together**. Compare their results to estimate the error, and adjust $h$ accordingly
##### Adaptive Time-Stepping using Order $p$ and Order $p+1$ methods
**Idea:**
1. Run 2 methods simultaneously with different truncation error orders
2. Approximate the error as $err = |y^A_{n+1} - y^B_{n+1}|$ where  $y^A_{n+1}$ has $O(h^p)$ and $y^B_{n+1}$ has $O(h^{p+1})$
3. If err > threshold, reduce $h$ (halve it) and recompute the step again, until the threshold is satisfied
4. Estimate the error coefficient $c$ as
$$c \approx \frac{|y^A_{n+1} - y^B_{n+1}|}{h_{old}^p}$$
where $h_old$ is the most recent time step size. If $c$ changes slowly in time, we can estimate the next step error as:
$$err_{next} = |y^A_{n+2} - y(t_{n+2})| \approx c(h_{new})^p$$
plug in $c$:
$$err_{next} \approx \frac{|y^A_{n+1} - y^B_{n+1}|}{h_{old}^p}(h_{new})^p = (\frac{h_{new}}{h_{old}})^p|y^A_{n+1} - y^B_{n+1}|$$
Given a desired error tolerance $tol$, set $err_{next} = tol$ and solve for $h_{new}$:
$$h_{new} = h_{old}(\frac{tol}{|y^A_{n+1} - y^B_{n+1}|})^{1/p}$$
To (roughly) compensate for our approximations, we may be conservative by scaling $tol$ down by some factor $\alpha$, e.g. $\alpha=1/2$, or $\alpha = 3/4$. This will allow step size to grow larger again when it is likely safe to do so.
