---
dg-publish: true
tags: cs370
---
# Cheatsheet 3
**1 Floating Point Numbers**
**Normalized Form of Real Numbers**
- **Representation**: $\pm 0.d_1d_2d_3...d_t \times \beta^p$ where $d_1 \neq 0$
- **System Parameters**: ${\beta, t, L, U}$ where:
    - $\beta$ = base
    - $t$ = precision (mantissa length)
    - $L, U$ = exponent bounds
- **IEEE Standards**:
    - Single Precision (32 bits): ${\beta=2, t=24, L=-126, U=127}$
    - Double Precision (64 bits): ${\beta=2, t=53, L=-1022, U=1023}$
**Error Metrics**
- **Absolute Error**: $E_{abs} = |x_{exact} - x_{approx}|$
- **Relative Error**: $E_{rel} = \frac{|x_{exact} - x_{approx}|}{|x_{exact}|}$
- **Rule of Thumb**: Result correct to $s$ digits if $E_{rel} \approx 10^{-s}$
- **Machine Epsilon** ($E$): Smallest value where $fl(1+E) > 1$
    - Rounding: $E = \frac{1}{2}\beta^{1-t}$
    - Truncation: $E = \beta^{1-t}$
**Round-off Error Analysis**
For $(a \oplus b) \oplus c$, error bound: $$E_{rel} \leq \frac{|a|+|b|+|c|}{|a+b+c|}(2E + E^2)$$
**Catastrophic Cancellation**
- Occurs when subtracting numbers of similar magnitude containing errors
- Critical when $|a+b+c| \ll |a|+|b|+|c|$
**Algorithm Stability**
- **Well-conditioned problem**: Small changes in input → small changes in output
- **Ill-conditioned problem**: Small changes in input → large changes in output
- **Stable algorithm**: Does not magnify errors in computation


**2 Interpolation & Splines**
**Polynomial Interpolation**
- **Unisolvence Theorem**: Given $n$ distinct data points, there exists a unique polynomial of degree $\leq n-1$ that interpolates the data
- **Monomial Form**: $p(x) = \sum_{i=1}^n c_i x^{i-1}$
- **Lagrange Form**: $p(x) = \sum_{i=1}^n y_i L_i(x)$ where: $$L_i(x) = \prod_{j=1,j\neq i}^n \frac{x-x_j}{x_i-x_j}$$
**Hermite Interpolation**
- Fits polynomials given function values and derivatives
- On interval $[x_i, x_{i+1}]$: $p_i(x) = a_i + b_i(x-x_i) + c_i(x-x_i)^2 + d_i(x-x_i)^3$
- Coefficients:
    - $a_i = y_i$
    - $b_i = s_i$
    - $c_i = \frac{3y'_i-2s_i-s_{i+1}}{\Delta x_i}$
    - $d_i = \frac{s_{i+1}+s_i-2y'_i}{\Delta x_i^2}$
    - Where $\Delta x_i = x_{i+1} - x_i$ and $y'_i = \frac{y_{i+1}-y_i}{\Delta x_i}$
**Cubic Splines**
- **Piecewise cubic polynomials** with continuous first and second derivatives
- **Requirements**: $n$ data points, $4(n-1)$ unknowns
- **Constraints**:
    - Interpolation: $S_i(x_i) = y_i$, $S_i(x_{i+1}) = y_{i+1}$
    - First derivatives match: $S'_i(x_{i+1}) = S'_{i+1}(x_{i+1})$
    - Second derivatives match: $S''_i(x_{i+1}) = S''_{i+1}(x_{i+1})$
    - Plus 2 boundary conditions
**Boundary Conditions**
- **Clamped**: Specified first derivatives at endpoints
- **Natural/Free**: $S''(x_1) = S''(x_n) = 0$
- **Periodic**: $S'(x_1) = S'(x_n)$, $S''(x_1) = S''(x_n)$
- **Not-a-knot**: Third derivatives match at second and second-to-last knots
	* $S_1’’’(x_2)=S_2’’’(x_2), S_{n-2}’’’(x_{n-1}) = S_{n-1}’’’(x_{n-1})$
**Efficient Tridiagonal System**
For interior nodes $(i=2,...,n-1)$: $$\Delta x_i s_{i-1} + 2(\Delta x_{i-1}+\Delta x_i)s_i + \Delta x_{i-1}s_{i+1} = 3(\Delta x_i y'_{i-1} + \Delta x_{i-1}y'_i)$$
**Parametric Curves**
- Represent curve as $\vec{P}(t) = (x(t), y(t))$
- Can handle self-intersections and vertical segments
- **Arc-length parameterization**: $t$ represents distance along curve
- **Common parameterizations**:
    - Node index: $t_i = i$
    - Approximate arc-length: $t_{i+1} = t_i + \sqrt{(x_{i+1}-x_i)^2 + (y_{i+1}-y_i)^2}$


**3 Ordinary Differential Equations**
**Initial Value Problem**
- Form: $y'(t) = f(t, y(t))$ with $y(t_0) = y_0$
- **Systems of ODEs**: Multiple interacting variables (vector form)
- **Higher-Order ODEs**: Involve derivatives of order > 1
    - Convert to first-order system by substitution: $y_i = y^{(i-1)}$
**Time-Stepping Methods**
- **Local Truncation Error (LTE)**: Error in a single step
- **Global Error**: Total accumulated error (typically one order less than LTE)
**Forward Euler (Explicit, Single-step)**
- $y_{n+1} = y_n + hf(t_n, y_n)$
- LTE: $O(h^2)$
- Conditionally stable: $0 < h < \frac{2}{\lambda}$
**Backward Euler (Implicit, Single-step)**
- $y_{n+1} = y_n + hf(t_{n+1}, y_{n+1})$
- LTE: $O(h^2)$
- Unconditionally stable
**Improved/Modified Euler (Explicit, Single-step)**
- $y^*_{n+1} = y_n + hf(t_n, y_n)$
- $y_{n+1} = y_n + \frac{h}{2}[f(t_n, y_n) + f(t_{n+1}, y^*_{n+1})]$
- LTE: $O(h^3)$
- Conditionally stable: $h < \frac{2}{\lambda}$
**Trapezoidal Rule (Implicit, Single-step)**
- $y_{n+1} = y_n + \frac{h}{2}[f(t_{n+1}, y_{n+1}) + f(t_n, y_n)]$
- LTE: $O(h^3)$
**Midpoint Method (Explicit, Single-step)**
- $y^*_{n+\frac{1}{2}} = y_n + \frac{h}{2}f(t_n, y_n)$
- $y_{n+1} = y_n + hf(t_n + \frac{h}{2}, y^*_{n+\frac{1}{2}})$
- LTE: $O(h^3)$
**4th Order Runge-Kutta (Explicit, Single-step)**
- $k_1 = hf(t_n, y_n)$
- $k_2 = hf(t_n+\frac{h}{2}, y_n+\frac{k_1}{2})$
- $k_3 = hf(t_n+\frac{h}{2}, y_n+\frac{k_2}{2})$
- $k_4 = hf(t_n+h, y_n+k_3)$
- $y_{n+1} = y_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4)$
- LTE: $O(h^5)$

**Multi-step Methods**
**BDF (Implicit, Multi-step)**
- BDF1 = Backward Euler
- BDF2: $y_{n+1} = \frac{4}{3}y_n - \frac{1}{3}y_{n-1} + \frac{2}{3}hf(t_{n+1}, y_{n+1})$
- LTE: $O(h^3)$
**Adams-Bashforth (Explicit, Multi-step)**
- 2nd order: $y_{n+1} = y_n + \frac{3}{2}hf(t_n, y_n) - \frac{1}{2}hf(t_{n-1}, y_{n-1})$
- LTE: $O(h^3)$
**Adaptive Time-Stepping**
1. Run methods of order $p$ and $p+1$
2. Estimate error: $err = |y^A_{n+1} - y^B_{n+1}|$
3. Adjust step size: $h_{new} = h_{old}(\frac{\alpha \cdot tol}{|y^A_{n+1} - y^B_{n+1}|})^{1/p}$