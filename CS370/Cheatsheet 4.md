---
dg-publish: true
tags: cs370
---
# Cheatsheet 4
**FLOATING POINT NUMBERS**
**Normalized Form**: $\pm0.d_1d_2d_3...d_t \times \beta^p$ where $L \leq p \leq U$ and $d_1 \neq 0$
- **Parameters**: ${\beta, t, L, U}$ where $\beta$ = base, $t$ = mantissa length, $L$/$U$ = exponent bounds
- **IEEE Standards**:
    - Single Precision (32 bits): ${\beta=2, t=24, L=-126, U=127}$
    - Double Precision (64 bits): ${\beta=2, t=53, L=-1022, U=1023}$

**Error Measures**:
- Absolute Error: $E_{abs} = |x_{exact} - x_{approx}|$
- Relative Error: $E_{rel} = \frac{|x_{exact} - x_{approx}|}{|x_{exact}|}$
- Result correct to ~$s$ digits if $E_{rel} \approx 10^{-s}$ or $0.5 \times 10^{-s} \leq E_{rel} \leq 5 \times 10^{-s}$

**Machine Epsilon** ($\varepsilon$): Smallest value where $fl(1+\varepsilon) > 1$
- Rounding to nearest: $\varepsilon = \frac{1}{2}\beta^{1-t}$
- Truncation: $\varepsilon = \beta^{1-t}$
- Rule: $fl(x) = x(1+\delta)$ where $|\delta| \leq \varepsilon$

**Overflow/Underflow**:
- Underflow: Result rounds to 0
- Overflow: Results in $\pm\infty$ or NaN

**IEEE Arithmetic Operations**:
- For $w, x \in F$: $w \oplus x = fl(w+x) = (w+x)(1+\delta)$ where $|\delta| \leq \varepsilon$
- Associativity is broken: $(a\oplus b) \oplus c \neq a \oplus (b\oplus c)$

**Cancellation Errors**: Occur when subtracting similar-magnitude numbers with different signs
- Error bound for $(a\oplus b) \oplus c$: $E_{rel} \leq \frac{|a|+|b|+|c|}{|a+b+c|}(2\varepsilon + \varepsilon^2)$
- Catastrophic when $|a+b+c| \ll |a|+|b|+|c|$

**Numerical Stability**: Initial errors not magnified by algorithm
**Conditioning**:
- Well-conditioned problem: Small input changes → small output changes
- Ill-conditioned problem: Small input changes → large output changes



**INTERPOLATION & SPLINES**
**Polynomial Interpolation**: Given points $(x_i,y_i)$, find polynomial $p(x)$ where $p(x_i)=y_i$
- **Uniqueness Theorem**: For $n$ distinct data points, exists unique polynomial of degree $\leq n-1$

**Monomial Form**: $p(x) = c_1 + c_2x + c_3x^2 + ... + c_nx^{n-1} = \sum^n_{i=1}c_ix^{i-1}$
**Lagrange Form**: $p(x) = \sum_{i=1}^n y_i L_i(x)$ where: $L_i(x) = \frac{(x-x_1)...(x-x_{i-1})(x-x_{i+1})...(x-x_n)}{(x_i-x_1)...(x_i-x_{i-1})(x_i-x_{i+1})...(x_i-x_n)}$
- Direct computation without solving linear system
- High-degree polynomials (n>8) often exhibit Runge's phenomenon (excessive oscillation)

**Hermite Interpolation**: Uses function values and derivatives
- For interval $[x_i,x_{i+1}]$: $p_i(x) = a_i + b_i(x-x_i) + c_i(x-x_i)^2 + d_i(x-x_i)^3$
- $a_i = y_i, b_i = s_i, c_i=\frac{3y'_i-2s_i-s_{i+1}}{\Delta x_i}, d_i=\frac{s_{i+1}+s_i-2y'_i}{\Delta x_i^2}$
- $\Delta x_i = x_{i+1}-x_i$ and $y'_i = \frac{y_{i+1}-y_i}{\Delta x_i}$

**Cubic Splines**: Piecewise cubic polynomials with continuous first and second derivatives
- For $n$ points: $4(n-1)$ unknowns and $4n-6$ equations
- Need 2 boundary conditions:
    - **Clamped**: Set $S'(x_1), S'(x_n)$
    - **Natural/Free**: $S''(x_1) = S''(x_n) = 0$
    - **Periodic**: $S'(x_1)=S'(x_n), S''(x_1)=S''(x_n)$
    - **Not-a-knot**: $S_1'''(x_2)=S_2'''(x_2), S_{n-2}'''(x_{n-1}) = S_{n-1}'''(x_{n-1})$

**Efficient Cubic Spline Equations** (Interior nodes, $i=2,...,n-1$): $\Delta x_i s_{i-1} + 2(\Delta x_{i-1}+\Delta x_i)s_i + \Delta x_{i-1}s_{i+1} = 3(\Delta x_i y'_{i-1} + \Delta x_{i-1}y'_i)$
- Forms tridiagonal system for slopes

**Parametric Curves**: Express curve as $\vec{P}(t)=(x(t),y(t))$ where $t$ is parameter
- Handles multi-valued functions (vertical lines, loops)
- Parameterization options:
    - Node index ($t=i$)
    - Arc-length approximation: $t_{i+1} = t_i + \sqrt{(x_{i+1}-x_i)^2+(y_{i+1}-y_i)^2}$


**ORDINARY DIFFERENTIAL EQUATIONS (ODEs)**
**First-Order ODE Form**: $y'(t) = f(t,y(t))$ with initial condition $y(t_0) = y_0$
**Higher-Order ODE**: $y^{(n)}(t) = f(t, y(t), y'(t),...,y^{(n-1)}(t))$
- Convert to system of first-order ODEs by defining new variables: $y_i = y^{(i-1)}$

**Systems of ODEs**: $\vec{y}'(t) = \vec{f}(t,\vec{y}(t))$ with initial $\vec{y}(t_0) = \vec{y}_0$
**Numerical Methods Categories**:
- Single-step vs. Multi-step
- Explicit vs. Implicit
- Fixed vs. Variable timestep

**Errors**:
- Local Truncation Error (LTE): Error in one step assuming exact previous values
- Global Error: Total accumulated error ($\text{Global} \approx \text{Local} \cdot O(h^{-1})$)

**Determining LTE**
1. Replace approximations on RHS with exact versions
2. Taylor expand all RHS quantities about time $t_n$
3. Taylor expand the exact solution $y(T_{n+1})$ to compare against
4. Compute difference $y(t_{n+1}) - y_{n+1}$. Lowest degree non-cancelling power of $h$ gives the LTE

**Test Equation**
1. Apply a given time stepping scheme to our test equation ($y'=-\lambda y$)
2. Find the closed form of its numerical solution and error behaviour
3. Find the conditions on the timestep $h$ that ensure stability (error approaching zero)

**Forward Euler** (Explicit, single-step):
- $y_{n+1} = y_n + hf(t_n,y_n)$
- LTE = $O(h^2)$, Global Error = $O(h)$
- Conditionally stable: $0 < h < \frac{2}{\lambda}$ for test equation $y'=-\lambda y$

**Backward Euler** (Implicit, single-step):
- $y_{n+1} = y_n + hf(t_{n+1},y_{n+1})$
- LTE = $O(h^2)$, Global Error = $O(h)$
- Unconditionally stable

**Improved/Modified Euler** (Explicit, single-step):
- $y^*_{n+1} = y_n + hf(t_n,y_n)$
- $y_{n+1} = y_n + \frac{h}{2}[f(t_n,y_n) + f(t_{n+1},y^*_{n+1})]$
- LTE = $O(h^3)$, Global Error = $O(h^2)$
- Conditionally stable: $h < \frac{2}{\lambda}$

**Midpoint Method** (Explicit, single-step):
- $y^*_{n+\frac{1}{2}} = y_n + \frac{h}{2}f(t_n,y_n)$
- $y_{n+1} = y_n + hf(t_n+\frac{h}{2},y^*_{n+\frac{1}{2}})$
- LTE = $O(h^3)$, Global Error = $O(h^2)$

**Runge-Kutta Methods** (Explicit, single-step):
- 4th Order RK (RK4):
    - $k_1 = hf(t_n,y_n)$
    - $k_2 = hf(t_n+\frac{h}{2},y_n+\frac{k_1}{2})$
    - $k_3 = hf(t_n+\frac{h}{2},y_n+\frac{k_2}{2})$
    - $k_4 = hf(t_n+h,y_n+k_3)$
    - $y_{n+1} = y_n + \frac{1}{6}(k_1+2k_2+2k_3+k_4)$
    - LTE = $O(h^5)$, Global Error = $O(h^4)$

**Multi-step Methods**:
- **BDF2** (Implicit): $y_{n+1} = \frac{4}{3}y_n-\frac{1}{3}y_{n-1} + \frac{2}{3}hf(t_{n+1},y_{n+1})$
    - LTE = $O(h^3)$, Global Error = $O(h^2)$
- **Adams-Bashforth** (Explicit): $y_{n+1} = y_n + \frac{3}{2}hf(t_n,y_n) - \frac{1}{2}hf(t_{n-1},y_{n-1})$
    - LTE = $O(h^3)$, Global Error = $O(h^2)$

**Adaptive Time-Stepping**:
1. Use two methods of different order
2. Estimate error: $err = |y^A_{n+1} - y^B_{n+1}|$
3. Adjust step size: $h_{new} = h_{old}(\frac{tol}{|y^A_{n+1}-y^B_{n+1}|})^{1/p}$ where $p$ is order of lower method
4. Often use safety factor $\alpha$ (0.5-0.9) to avoid too-large steps