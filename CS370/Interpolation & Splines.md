---
dg-publish: true
tags: cs370
---
# Interpolation & Splines
## Interpolation
> [!tldr] The basic problem of interpolation
> Given a set of data points from an (unknown) function $y=p(x)$, can we approximate $p$’s value at other points?
> 
> e.g. Given $p(x_1)=y_1, p(x_2)=y_2, \cdots, p(x_n) = y_n$
> 	Estimate $y=p(x)$ for any point $x$ such that $x_1\leq x \leq x_n$

#### Theorem (Unisolvence Theorem)
Given $n$ data pairs $(x_i, y_i), i = 1, \cdots, n$ with distinct $x_i$, there is a **unique** polynomial $p(x)$ of degree $\leq n - 1$ that interpolates the data.
### Vandermonde Matrices
![[Pasted image 20250302203411.png]]
$V$ is called a Vandermonde matrix

>[!tldr] Polynomial interpolation reduces to solving systems of equations
### The monomial basis
The familiar form $p(x) = c_1 + c_2x + c_3x^2 + \cdots + c_n^{n-1}$ is called the **monomial form**, and can also be written as
$$p(x) = \sum^n_{i=1}c_ix^{i-1}$$
The sequence, $1, x, x^2, \cdots$ is called the **monomial basis**.
Monomial form is a sum of coefficients $c_i$ times basis functions $x^i$.
### The Lagrange basis
We will define the Lagrange basis functions, $L_i(x)$, to construct a polynomial as
$$p(x) = y_1L_1(x) + y_2L_2(x) + \cdots + y_nL_n(x) = \sum_{i=1}^ny_iL_i(x)$$
where $y_i$ are the coefficients **and also our data values,** $y_i = p(x_i)$.

Given $n$ data points $(x_i, y_i)$, we define
$$L_i(x) = \frac{(x-x_1)\cdots(x-x_{i-1})(x-x_{i+1})\cdots(x-x_n)}{(x_i-x_1)\cdots(x_i-x_{i-1})(x_i-x_{i+1})\cdots(x_i-x_n)}$$
When $i=j$, $L_i(x_j)$ has same numerator and denominator.
When $i\neq j$, $L_i(x_j)$ has numerator = 0, denominator $\neq 0$
**Ensures $p(x)$ must interpolate each $x_i$**
* $p(x_i) = y_i$ by construction

>[!important] Monomial vs Langrangian basis
>1. They give the same interpolating polynomial
>2. We can directly write down the polynomial from the Lagrange basis functions
>	1. **No need to solve a linear system**

### Polynomial Interpolation for many points
Fitting a “high degree” ($n\approx 7,8,9$) polynomial often gives excessive oscillation
* **Runge’s phenomenon**
## Piecewise Interpolation
### Hermite Interpolation
The problem of fitting a polynomial given function values and derivatives
#### Closed-form Solution
Defining the polynomial on the $i^{th}$ interval, $p_i(x)$, as
$$p_i(x) = a_i + b_i(x-x_i) + c_i(x-x_i)^2 + d_i(x-x_i)^3$$
We saw that the direct formulas for the polynomial coefficients are:
$$a_i = y_i, b_i = s_i,c_i=\frac{3y'_i-2s_i-s_{i+1}}{\Delta x_i}, d_i=\frac{s_{i+1}+s_i-2y'_i}{\Delta x_i^2}$$
where we define
$$\Delta x_i=x_{i+1} - x_i$$
and
$$y_i'=\frac{y_{i+1}-y_i}{\Delta x_i}$$
![[Pasted image 20250302214032.png]]
#### Some Terminology
**Knots:** Points where the interpolant transitions from one polynomial/interval to another
**Nodes:** Points where some control points/data is specified
* For Hermite interpolation, these are the same
* For other curve types (e.g. Bezier Curves), they can differ
![[Pasted image 20250302214409.png]]

>[!faq] More common problem: no derivative information $s_i$ is given, only values $y_i$
>Can we still fit a piecewise cubic to the set of points?
>* Yes, but each “piece” needs data from more than just its 2 endpoints

## Cubic Splines
Fit a cubic, $S_i(x)$, on each interval, but now require matching first and second derivatives between intervals.
Require **interpolating conditions** on each interval $[x_i, x_{i+1}]$,
$$S_i(x_i) = y_i, S_i(x_{i+1}) = y_{i+1}$$
and **derivative conditions** at each interior point $x_{i+1}$
$$S'_i(x_{i+1})=S'_{i+1}(x_{i+1}), S''_i(x_{i+1}) = S''_{i+1}(x_{i+1})$$
#### Counting Unknowns
Assuming $n$ data points, we have $4(n-1)$ unknowns
* 4 unknowns for each of $n-1$ intervals
#### Counting Equations
Assuming $n$ data points, we have $2(2n-3)$ equations
* 2 interpolating conditions per interval: $2(n-1)$
* 2 derivative conditions per interior point: $2(n-2)$
>[!faq] $4n-6$ equations, $4n-4$ unknowns, can we solve the system?
>No! Not enough information for unique solution!
>Need 2 more equations
>* Usually at domain endpoints
>* **Boundary conditions** or **end conditions**

### Boundary Conditions
#### Clamped
Slope set to specific value
* $S’(x_1), S’(x_n)$ specified
If both boundaries clamped, it is a complete or clamped spline
#### Free/natural/variational
$$S''(x_1) = S''(x_n) = 0$$
If both boundaries are free, called a *natural cubic spline*.
* Curve “straightens out”
#### Periodic boundary
* $S’(x_1)=S’(x_n), S’’(x_1)=S’’(x_n)$
* Start and end derivates match each other
#### “Not-a-knot” boundary conditions
* Match 3rd derivates on end segments
	* $S_1’’’(x_2)=S_2’’’(x_2), S_{n-2}’’’(x_{n-1}) = S_{n-1}’’’(x_{n-1})$
	* Last two segments on an end become the **same** polynomial
### Hermite vs. Cubic Splines
**Hermite Interpolation:** each interval can be found independently
**Cubic Spline:** must solve for all polynomials together at once!

### Basic cubic spline approach
For $n$ points, we have $n-1$ intervals / cubic polynomials, so $4n-4$ unknowns.
Write down:
* **$2(n-1)$ interpolating conditions**: match inputs at interval endpoints
* **$n-2$ first derivative conditions**: match first derivatives at interior nodes
* **$n-2$ second derivative conditions**: match second derivatives at interior nodes
* Additional **boundary conditions** for the 2 ends
Solve linear system of $4n-4$ equations for all polynomial coefficients

### Cubic Splines via Hermite Interpolation
**Use Hermite interpolation as a stepping stone to build a cubic spline!**
1. Express unknown polys with closed form Hermite equations
2. Treat the $s_i$ as unknowns
3. Solve for $s_i$ that gives continuous 2nd derivates
4. Given $s_i$, plug into closed form Hermite equations to recover poly coefficients.
#### Efficient Splines Summary
Interior nodes $(i=2, \cdots, n-1)$:
$$\Delta x_i s_{i-1} + 2(\Delta x_{i-1}+\Delta x_i)s_i + \Delta x_{i-1}s_{i+1} = 3 (\Delta x_iy'_{i-1} + \Delta x_{i-1}y'_i)$$
where we define
$$\Delta x_i=x_{i+1} - x_i$$
and
$$y_i'=\frac{y_{i+1}-y_i}{\Delta x_i}$$
Clamped BC:
$$s_1 = s_1^*, s_n=s_n*$$
Free BC:
$$s_1 + \frac{s_2}{2} = \frac{3}{2}y_1', \frac{s_{n-1}}{2}+s_n = \frac{3}{2}y'_{n-1}$$
#### Matrix Form
We can write this linear system for the slopes in **matrix/vector form**
![[Pasted image 20250303081103.png]]
New system has one equation per node, no matrix size is $n\times n$. This system is smaller in size by a **constant factor 4.**
##### Matrix Structure
The matrix is **tridiagonal**. Only the entries on the diagonal and its two neighbours are ever non-zero!
![[Pasted image 20250303081502.png]]
### Shortcomings So Far
Cannot handle curve that has different $y$ for same $x$.
![[Pasted image 20250303081735.png]]
## Parametric Curves
**Lets us handle more general curves**
* Cannot express as $y=p(x)$
#### Solution
Let $x$ and $y$ each be separate functions to a new parameter, $t$.
Then a point’s position is given by the vector $\vec{P(t)}=(x(t). y(t))$.
![[Pasted image 20250303082110.png]]
Parameter $t$ **increases monotonically** along the curve, but $x$ and $y$ may increase and decrease as needed to describe any shape.
>[!tldr] Parametric curves are a more powerful/flexible way of describing curves **in general**

#### Non-Uniqueness
A given curve can be “parameterized” in different ways, while yielding the exact same shape.
* Can traverse $t$ in opposite direction
#### Speeds
2 parameterizations can also traverse the curve in the same direction, but at **different speeds/rates**
#### Repeated Points
Curves with self-intersections are supported easily
#### Piecewise Parametric Curves
>[!example]- The unit square
>![[Pasted image 20250303082910.png]]

### Arc-Length Parameterization
Common to choose $t$ as the distance along the curve
![[Pasted image 20250303083024.png]]
This gives *unit speed* traversal of the curve
* Travel 1 unit of distance in 1 unit of time
### Parametric Curves using Interpolation
Parametric curves are just the **general concept**
We can combine existing interpolant types with parametric curves by considering $x(t)$ and $y(t)$ separately
* Use two **Lagrange polynomials**, $x(t), y(t)$, to fit small set of $(t_i, x_i, y_i)$
* use **Hermite interpolation** for $x(t), y(t)$ given $(t_i, x_i, y_i, sx_i, sy_i)$
* Fit separate **cubic splines** to $x(t), y(t)$, given many points
### Parameterizations for Piecewise Polynomials
Given ordered $(x_i,y_i)$ point data, we don’t yet have a parameterization.
* We need data for $t$, to form $(t_i, x_i)$ and $(t_i, y_i)$ pairs to fit curves to
**Option 1:** Use node index $i$ as the parameterization
**Option 2:** Approximate arc-length parameterization
* set $t_1=0$ at first node
* Recursively compute $t_{i+1} = t_i + \sqrt{(x_{i+1}^2 - x_i)^2 +(y_{i+1}^2 - y_i)^2}$
	* Distance between $(x_i, y_i)$ and $(x_{i+1}, y_{i+1})$
* 