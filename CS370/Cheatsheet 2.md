---
dg-publish: true
tags: cs370
---
# Cheatsheet 2
## Floating Point Numbers
- **Normalized Form**: $\pm 0.d_1d_2...d_t \times \beta^p$ where $L \leq p \leq U$, $d_1 \neq 0$
- **Parameters**: ${\beta, t, L, U}$ where $\beta$ = base, $t$ = mantissa, $L$ & $U$ = exponent bounds
- **IEEE Standards**:
    - Single Precision (32 bits): ${\beta=2, t=24, L=-126, U=127}$
    - Double Precision (64 bits): ${\beta=2, t=53, L=-1022, U=1023}$
- **Errors**:
    - Absolute Error: $E_{abs} = |x_{exact} - x_{approx}|$
    - Relative Error: $E_{rel} = \frac{|x_{exact} - x_{approx}|}{|x_{exact}|}$
    - $s$ significant digits if $0.5 \times 10^{-s} \leq E_{rel} \leq 5 \times 10^{-s}$
- **Machine Epsilon** ($E$): Smallest value where $fl(1+E) > 1$
    - Rounding: $E = \frac{1}{2}\beta^{1-t}$
    - Truncation: $E = \beta^{1-t}$
- **Arithmetic Operations**: $fl(x \circ y) = (x \circ y)(1+\delta)$ where $|\delta| \leq E$
- **Cancellation Errors**: Occur when subtracting similar magnitude numbers
## Interpolation & Splines
- **Interpolation**: Given points $(x_i,y_i)$, estimate $p(x)$ where $x_1 \leq x \leq x_n$
- **Unique Polynomial**: Degree $\leq n-1$ for $n$ distinct points
- **Monomial Form**: $p(x) = \sum_{i=1}^{n} c_i x^{i-1}$
- **Lagrange Form**: $p(x) = \sum_{i=1}^{n} y_i L_i(x)$ where $L_i(x_j) = \delta_{ij}$
    - $L_i(x) = \frac{(x-x_1)...(x-x_{i-1})(x-x_{i+1})...(x-x_n)}{(x_i-x_1)...(x_i-x_{i-1})(x_i-x_{i+1})...(x_i-x_n)}$
- **Cubic Splines**: Piecewise cubic polynomials with C² continuity
    - $4(n-1)$ unknowns, $4n-6$ equations + 2 boundary conditions
    - Boundary Conditions: Clamped ($S'(x_1)$, $S'(x_n)$ specified), Natural ($S''(x_1)=S''(x_n)=0$), Periodic, Not-a-knot ($S_1’’’(x_2)=S_2’’’(x_2), S_{n-2}’’’(x_{n-1}) = S_{n-1}’’’(x_{n-1})$)
- **Parametric Curves**: $\vec{P}(t) = (x(t), y(t))$ for more general curves
## Ordinary Differential Equations
- **First-Order ODE**: $y'(t) = f(t, y(t))$, $y(t_0) = y_0$
- **Time-Stepping Methods**:
    - **Forward Euler** (explicit): $y_{n+1} = y_n + hf(t_n, y_n)$
        - LTE: $O(h^2)$, conditionally stable if $0 < h < \frac{2}{\lambda}$
    - **Backward Euler** (implicit): $y_{n+1} = y_n + hf(t_{n+1}, y_{n+1})$
        - LTE: $O(h^2)$, unconditionally stable
    - **Trapezoidal Rule** (implicit): $y_{n+1} = y_n + \frac{h}{2}[f(t_n, y_n) + f(t_{n+1}, y_{n+1})]$
        - LTE: $O(h^3)$
    - **Improved Euler** (explicit):
        - $y^*_{n+1} = y_n + hf(t_n, y_n)$
        - $y_{n+1} = y_n + \frac{h}{2}[f(t_n, y_n) + f(t_{n+1}, y^*_{n+1})]$
        - LTE: $O(h^3)$, conditionally stable if $h < \frac{2}{\lambda}$
    - **RK4** (explicit):
        - $k_1 = hf(t_n, y_n)$
        - $k_2 = hf(t_n+\frac{h}{2}, y_n+\frac{k_1}{2})$
        - $k_3 = hf(t_n+\frac{h}{2}, y_n+\frac{k_2}{2})$
        - $k_4 = hf(t_n+h, y_n+k_3)$
        - $y_{n+1} = y_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4)$
        - LTE: $O(h^5)$
- **Local vs Global Error**:
    - Local Truncation Error (LTE): Error in one step
    - Global Error ≈ Local Error × Number of steps = $O(h^{p-1})$ where $p$ is LTE order
- **Adaptive Time-Stepping**:
    - Run two methods of different orders
    - Estimate error: $err = |y^A_{n+1} - y^B_{n+1}|$
    - Adjust step size: $h_{new} = h_{old}(\frac{tol}{|y^A_{n+1} - y^B_{n+1}|})^{1/p}$