---
dg-publish: true
tags: cs370
---
# Cheatsheet 5
**CONTINUOUS FOURIER SERIES (CFS)**
Represents a periodic function $f(t)$ with period $T$ ($f(t \pm T) = f(t)$) as an infinite sum of sines and cosines.
- **General Form**: $f(t) = a_0 + \sum_{k=1}^{\infty}a_k\cos(\frac{2\pi kt}{T})+\sum_{k=1}^{\infty}b_k\sin(\frac{2\pi kt}{T})$
- **Coefficients (for $T=2\pi$)**:
    - $a_0 = \frac{1}{2\pi}\int_0^{2\pi}f(t)dt$ (Average value)
    - $a_k = \frac{1}{\pi}\int_0^{2\pi}f(t)\cos(kt)dt$ (for $k>0$)
    - $b_k = \frac{1}{\pi}\int_0^{2\pi}f(t)\sin(kt)dt$ (for $k>0$)
- **Orthogonality (for $T=2\pi$)**: Used to find coefficients.
    - $\int_0^{2\pi}\cos(kt)\sin(jt)dt = 0$
    - $\int_0^{2\pi}\cos(kt)\cos(jt)dt = \pi\delta_{k,j}$ (for $k,j > 0$)
    - $\int_0^{2\pi}\sin(kt)\sin(jt)dt = \pi\delta_{k,j}$ (for $k,j > 0$)
    - $\int_0^{2\pi}\cos(kt)dt = 0$, $\int_0^{2\pi}\sin(kt)dt = 0$ (for $k>0$)

**COMPLEX EXPONENTIAL FORM**
- **Euler's Formula**: $e^{i\theta} = \cos(\theta) + i\sin(\theta)$
- **Sine/Cosine**: $\cos(\theta) = \frac{e^{i\theta}+e^{-i\theta}}{2}$, $\sin(\theta) = \frac{e^{i\theta}-e^{-i\theta}}{2i}$
- **Complex CFS**: $f(t)=\sum_{k=-\infty}^{+\infty}c_ke^{ikt}$ (for $T=2\pi$)
- **Complex Coefficients (for $T=2\pi$)**: $c_k=\frac{1}{2\pi}\int_0^{2\pi}f(t)e^{-ikt}dt$
- **Relation to $a_k, b_k$**: $a_0=c_0$, $c_k = \frac{a_k - ib_k}{2}$, $c_{-k}=\frac{a_k + ib_k}{2} = \bar{c_k}$ (for $k>0$)
- **Magnitude**: $|c_k|=|c_{-k}|=\frac{1}{2}\sqrt{a_k^2+b_k^2}$
- **Truncation Approx**: $f(t)\approx\sum_{k=-M}^{+M}c_ke^{ikt}$

**DISCRETE FOURIER TRANSFORM (DFT)**
Transforms discrete data $f_0, ..., f_{N-1}$ (sampled at $t_n = nT/N$) to frequency coefficients $F_0, ..., F_{N-1}$.
- **$N^{th}$ Root of Unity**: $W = e^{\frac{2\pi i}{N}}$. Satisfies $W^N = 1$. $W^k = e^{\frac{2\pi ik}{N}}$ are points on the unit circle in the complex plane.
- **Inverse DFT (Synthesis)**: $f_n = \sum_{k=0}^{N-1}F_kW^{nk}$
- **Forward DFT (Analysis)**: $F_k=\frac{1}{N}\sum_{n=0}^{N-1}f_nW^{-nk}$
- **Orthogonality**: $\sum_{j=0}^{N-1}W^{j(k-l)} = N\delta_{k,l}$
- **Properties**:
    - **Periodicity**: $F_{k+N} = F_k$
    - **Conjugate Symmetry (if $f_n$ real)**: $F_k = \overline{F_{N-k}}$. Implies $|F_k| = |F_{N-k}|$.
- **$F_0$ Coefficient**: $F_0=\frac{1}{N}\sum_{n=0}^{N-1}f_n$ (Average or DC component).
- **Power Spectrum**: Plot of $|F_k|$ vs $k$. Shows magnitude of frequencies, ignores phase. Symmetric for real data about $k=N/2$.

**FAST FOURIER TRANSFORM (FFT)**
An efficient algorithm to compute the DFT.
- **Complexity**: DFT is $O(N^2)$, FFT is $O(N \log N)$.
- **Method**: Divide and conquer. Recursively split DFT of size $N$ into two DFTs of size $N/2$. Requires $N$ to be a power of 2 (pad with zeros if needed).
- **Butterfly Operation**: Basic computation combining pairs of inputs.
- **Output Order**: Coefficients are in bit-reversed order.
- **Inverse FFT**: Can use the same algorithm structure with $W$ instead of $W^{-1}$ and scaling by $N$. $f_n = \sum_{k=0}^{N-1}F_kW^{nk}$.

**APPLICATIONS & ALIASING**
- **Image Compression (1D/2D)**:
    - Perform DFT/FFT on pixel data (rows then columns for 2D).
    - Discard coefficients $F_k$ (or $F_{k,l}$) with small magnitude $|F_k| < tol$.
    - Reconstruct using Inverse DFT/FFT with remaining coefficients. Store fewer coefficients = compression.
    - **2D DFT**: $F_{k,l}=\frac{1}{NM}\sum_{n=0}^{N-1}\sum_{j=0}^{M-1}f_{n,j}W^{-nk}_NW^{-jl}_M$. Complexity $O(MN(\log M + \log N))$. Often done on blocks ($8\times 8$, $16\times 16$).
- **Aliasing**: Occurs when sampling rate (1/$\Delta t$) is too low for high frequencies in the continuous signal. High frequencies appear as lower frequencies in the discrete data.
    - **Cause**: $F_k = \sum_{m=-\infty}^{\infty} c_{k+mN}$. High freq. continuous coefficients $c_{k \pm N}, c_{k \pm 2N}, ...$ contribute to discrete coefficient $F_k$.
    - **Nyquist Frequency**: Max frequency representable is $k=N/2$. Frequencies $|k|>N/2$ alias.
    - **Treatment**: Increase sampling rate ($N$ for fixed $T$), or apply a low-pass (anti-aliasing) filter *before* sampling.

**PAGE RANK ALGORITHM**
Ranks web pages based on link structure (importance).
- **Model**: Web as directed graph. Random surfer follows links. Importance $\propto$ probability of landing on a page.
- **Markov Matrix**: $P_{ij} = 1/\deg(j)$ if link $j \to i$, else 0. Columns sum to 1.
- **Handling Dead Ends**: $P' = P+\frac{1}{R}ed^T$ where $d_j=1$ if page $j$ is dead end, $e$ is vector of 1s, $R$ is total pages. Allows teleportation from dead ends.
- **Handling Cycles (Google Matrix)**: $M=\alpha P'+(1-\alpha)\frac{1}{R}ee^T$. With probability $\alpha$ (e.g., 0.85) follow links (via $P'$), with $1-\alpha$ teleport randomly. $M$ is a dense Markov matrix (columns sum to 1, $0 \le M_{ij} \le 1$).
- **Iteration**: Start with $p^0 = \frac{1}{R}e$ (uniform probability). Iterate $p^{n+1}=Mp^n$.
- **Convergence**: $p^n \to p^\infty$ as $n \to \infty$. $p^\infty$ is the principal eigenvector of $M$ corresponding to eigenvalue $\lambda_1=1$. Convergence rate depends on $|\lambda_2|$ (second largest eigenvalue magnitude), approx $|\lambda_2| \approx \alpha$. Smaller $\alpha \implies$ faster convergence but less reliance on link structure.
- **Efficiency**:
    - **Precomputation**: Compute $p^\infty$ offline.
    - **Sparsity**: Avoid forming dense $M$. Compute $Mp^n$ using sparse $P$: $Mp^n = \alpha Pp^n + \frac{\alpha}{R}e(d^Tp^n)+\frac{(1-\alpha)}{R}e(e^Tp^n) = \alpha Pp^n + (\frac{\alpha}{R}(d^Tp^n)+\frac{(1-\alpha)}{R})e$. $P$ is sparse, $Pp^n$ is fast. Iterate until $\|p^{n+1}-p^n\|_\infty < tol$.

**GAUSSIAN ELIMINATION (GE)**
Solves $Ax=b$.
- **LU Factorization**: Factor $A=LU$ where $L$ is unit lower triangular, $U$ is upper triangular.
    - **Algorithm**: Eliminate entries below diagonal, column by column. Store multipliers $L_{ik} = a_{ik}/a_{kk}$ in $L$.
    - **Cost**: $\approx \frac{2}{3}n^3$ FLOPs.
- **Solving $Ax=b$ via LU**:
    1. Factor $A=LU$ (or $PA=LU$, see Pivoting). Cost $\approx \frac{2}{3}n^3$.
    2. Solve $Lz=b$ (Forward substitution). Cost $\approx n^2$.
    3. Solve $Ux=z$ (Backward substitution). Cost $\approx n^2$.
    - Total cost dominated by factorization. Efficient if solving for multiple $b$'s.
- **Pivoting (Partial)**: To avoid division by small/zero $a_{kk}$ and reduce error.
    - **Strategy**: In step $k$, find row $p \ge k$ with max $|a_{pk}|$. Swap row $k$ and row $p$.
    - **Permutation Matrix**: Row swaps tracked by $P$. Factorization becomes $PA=LU$. Solve $LUx=Pb$.
- **Cost Comparison**: GE ($O(n^3)$) is cheaper and more stable than finding $A^{-1}$ and computing $x=A^{-1}b$.

**NORMS & CONDITIONING**
- **Vector Norms ($p$-norms)**: Measure vector magnitude. $\|x\|_p=\left(\sum^n_{i=1}|x_i|^p\right)^{1/p}$
    - $\|x\|_1=\sum |x_i|$ (Manhattan)
    - $\|x\|_2=\sqrt{\sum x_i^2}$ (Euclidean)
    - $\|x\|_\infty = \max_i|x_i|$ (Max)
    - **Properties**: $\|x\| \ge 0$ ( $\|x\|=0 \iff x=0$), $\|\alpha x\| = |\alpha|\|x\|$, $\|x+y\| \leq \|x\|+\|y\|$ (Triangle Inequality).
- **Matrix Norms (Induced)**: $\|A\| = \max_{\|x\|\neq 0}\frac{\|Ax\|}{\|x\|}$
    - $\|A\|_1 = \max_j\sum_{i}|A_{ij}|$ (Max abs column sum)
    - $\|A\|_\infty = \max_i\sum_{j}|A_{ij}|$ (Max abs row sum)
    - $\|A\|_2 = \sqrt{\max |\lambda_i(A^TA)|}$ (Spectral norm, largest singular value)
    - **Properties**: Like vector norms, plus $\|AB\|\leq \|A\|\|B\|$, $\|Ax\|\leq \|A\|\|x\|$.
- **Conditioning**: Sensitivity of output to input perturbations for a problem ($Ax=b$).
    - **Well-conditioned**: Small input change $\implies$ small output change.
    - **Ill-conditioned**: Small input change $\implies$ large output change.
- **Condition Number**: $\kappa(A) = \|A\|\|A^{-1}\|$. (Uses a consistent norm, often $\|.\|_2$).
    - $\kappa(A) \ge 1$. $\kappa(A) \approx 1$ is well-conditioned. $\kappa(A) \gg 1$ is ill-conditioned.
    - **Error Bounds**: Relative error in $x$ due to perturbation $\Delta b$ or $\Delta A$:
        - $\frac{\|\Delta x\|}{\|x\|}\leq \kappa(A)\frac{\|\Delta b\|}{\|b\|}$
        - $\frac{\|\Delta x\|}{\|x + \Delta x\|}\leq \kappa(A)\frac{\|\Delta A\|}{\|A\|}$
- **Residual**: $r = b - Ax_{approx}$. Measurable quantity indicating how well $x_{approx}$ satisfies $Ax=b$.
- **Residual vs. Error**: $\frac{\|x-x_{approx}\|}{\|x\|} \leq \kappa(A) \frac{\|r\|}{\|b\|}$. Small residual only guarantees small error if $\kappa(A)$ is small.
- **GE Accuracy**: For GE with pivoting, computed solution $\hat{x}$ is the exact solution to $(A+\Delta A)\hat x = b$ with $\|\Delta A\|/\|A\| \approx \epsilon_{machine}$. The relative error is bounded: $\frac{\|x-\hat x\|}{\|\hat x\|}\lesssim \kappa(A)\epsilon_{machine}$. Accuracy limited by condition number, even with stable algorithms.

**LINEAR ALGEBRA HELPER FACTS**
- **Matrix-Vector Product**: $Mx$ is a linear combination of columns of $M$. $(Mx)_i = (\text{row } i \text{ of } M) \cdot x$.
- **Matrix-Matrix Product**: $(MN)_{ij} = (\text{row } i \text{ of } M) \cdot (\text{col } j \text{ of } N)$. Column $j$ of $MN$ is $M (\text{col } j \text{ of } N)$.
- **Transposes**: $(MN)^T = N^T M^T$. $x \cdot y = x^T y$. $x \cdot My = (M^T x) \cdot y$.
- **Isometry** ($M^T=M^{-1}$, e.g., rotation, permutation): $\|Mx\|_2 = \|x\|_2$, $Mx \cdot My = x \cdot y$.
- **Spectral Theorem**: If $M=M^T$, there exists an orthonormal basis of eigenvectors for $M$.
- **Eigenvalues**: If $Ax=\lambda x$, then $A^{-1}x = (1/\lambda)x$. $\det(A) = \prod \lambda_i$. $\text{trace}(A) = \sum A_{ii} = \sum \lambda_i$. $A$ invertible $\iff \lambda=0$ is not an eigenvalue.
