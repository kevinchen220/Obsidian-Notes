---
dg-publish: true
tags: cs370
---
# Cheatsheet
## Floating Point Numbers
### Floating Point System Parameters
- System defined by ${\beta, t, L, U}$ where:
    - $\beta =$ base (usually 2)
    - $t =$ mantissa digits (precision)
    - $L, U =$ exponent bounds
- Normalized form: $\pm0.d_1d_2d_3...d_t \times \beta^p$ where $d_1 \neq 0$ and $L \leq p \leq U$
- IEEE Single Precision (32 bits): ${\beta=2, t=24, L=-126, U=127}$
- IEEE Double Precision (64 bits): ${\beta=2, t=53, L=-1022, U=1023}$
### Error Measures
- Absolute error: $E_{abs} = |x_{exact} - x_{approx}|$
- Relative error: $E_{rel} = \frac{|x_{exact} - x_{approx}|}{|x_{exact}|}$
- $s$ significant digits if: $0.5 \times 10^{-s} \leq E_{rel} \leq 5 \times 10^{-s}$
- Machine epsilon (round to nearest): $E = \frac{1}{2}\beta^{1-t}$
- Machine epsilon (truncation): $E = \beta^{1-t}$
### Floating Point Arithmetic
- Round-off magnification: $\frac{|a|+|b|+|c|}{|a+b+c|}$
- Catastrophic cancellation occurs when subtracting similar-magnitude numbers
## Interpolation & Splines
### Polynomial Interpolation
- **Lagrange Form**: $p(x) = \sum_{i=1}^n y_i L_i(x)$ where:
    - $L_i(x) = \prod_{j=1,j\neq i}^n \frac{x-x_j}{x_i-x_j}$
- Warning: High-degree polynomials may oscillate (Runge's phenomenon)
### Cubic Splines
- Cubic polynomial on each interval: $S_i(x) = a_i + b_i(x-x_i) + c_i(x-x_i)^2 + d_i(x-x_i)^3$
- Interpolation conditions: $S_i(x_i) = y_i$, $S_i(x_{i+1}) = y_{i+1}$
- Continuity conditions: $S_i'(x_{i+1}) = S_{i+1}'(x_{i+1})$, $S_i''(x_{i+1}) = S_{i+1}''(x_{i+1})$
- Boundary conditions:
    - Clamped: $S'(x_1)$ and $S'(x_n)$ specified
    - Natural/free: $S''(x_1) = S''(x_n) = 0$
    - Not-a-knot: Match 3rd derivatives between end segments
### Hermite Interpolation
- Given points and derivatives: $(x_i, y_i, s_i)$
- $p_i(x) = a_i + b_i(x-x_i) + c_i(x-x_i)^2 + d_i(x-x_i)^3$ where:
    - $a_i = y_i$
    - $b_i = s_i$
    - $c_i = \frac{3y'_i-2s_i-s_{i+1}}{\Delta x_i}$
    - $d_i = \frac{s_{i+1}+s_i-2y'_i}{\Delta x_i^2}$
    - $\Delta x_i = x_{i+1} - x_i$, $y'_i = \frac{y_{i+1}-y_i}{\Delta x_i}$
## Ordinary Differential Equations (ODEs)
### First-Order ODE Methods (for $y'(t) = f(t,y(t))$, $y(t_0) = y_0$)

| Method         | Formula                                                                                                                                                                                                                  | Error    | Stability                            |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ------------------------------------ |
| Forward Euler  | $y_{n+1} = y_n + hf(t_n, y_n)$                                                                                                                                                                                           | $O(h^2)$ | Conditional: $h < \frac{2}{\lambda}$ |
| Backward Euler | $y_{n+1} = y_n + hf(t_{n+1}, y_{n+1})$                                                                                                                                                                                   | $O(h^2)$ | Unconditional                        |
| Improved Euler | $y_{n+1} = y_n + hf(t_n, y_n)$ <br> $y_{n+1} = y_n + \frac{h}{2}[f(t_n, y_n) + f(t_{n+1}, y_{n+1})]$                                                                                                                     | $O(h^3)$ | Conditional: $h < \frac{2}{\lambda}$ |
| Midpoint       | $y_{n+\frac{1}{2}} = y_n + \frac{h}{2}f(t_n, y_n)$ <br> $y_{n+1} = y_n + hf(t_n + \frac{h}{2}, y_{n+\frac{1}{2}})$                                                                                                       | $O(h^3)$ | Conditional                          |
| RK4            | $k_1 = hf(t_n, y_n)$ <br> $k_2 = hf(t_n+\frac{h}{2}, y_n+\frac{k_1}{2})$ <br> $k_3 = hf(t_n+\frac{h}{2}, y_n+\frac{k_2}{2})$ <br> $k_4 = hf(t_n+h, y_n+k_3)$ <br> $y_{n+1} = y_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4)$ | $O(h^5)$ | Conditional                          |

### Higher-Order ODEs
- Convert to system of first-order ODEs using $y_i = y^{(i-1)}$ for $i = 1,2,...,n$
### Adaptive Time-Stepping
1. Use two methods of different order
2. Estimate error: $err = |y^A_{n+1} - y^B_{n+1}|$
3. Adjust step size: $h_{new} = h_{old}(\frac{tol}{|y^A_{n+1} - y^B_{n+1}|})^{1/p}$
### Error Analysis
- Local Truncation Error (LTE): Error in one step, assuming exact previous data
- Global Error: Total accumulated error, typically one order lower than LTE
- For a method with LTE $O(h^{p+1})$, global error is $O(h^p)$