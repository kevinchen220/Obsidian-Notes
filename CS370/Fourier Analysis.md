---
dg-publish: true
tags: cs370
---
# Fourier Analysis
## Fourier Transforms Introduction
The **Fourier Transform** applies to continuous functions or discrete data can provide useful insights and tools for many applications
* **Examples:**
	* signal processing
		* filtering
		* denoising
	* sound/audio manipulation
### Basic Idea
1. Transform some function/data into a form that reveals **frequencies** of information in the data
2. Process/analyse it it in this “frequency domain” form
3. Transform back again
The original data/function is said to be in the…
* “time domain” if $f$ is a function of time, $f(t)$
* “spatial domain” if $f$ is a function of space/position, $f(x)$
>[!tldr] Convert time or space-dependent data into the representation
>$$f(t) = a_0+a_1\cos(qt) + b_1\sin(qt)+a_2\cos(2qt) + b_2\sin(2qt)$$
>i.e. infinite sum of increasingly high frequency **sine/cosines**
>Could view this as:
>* a weird (non-polynomial) interpolation problem:
>	* what coefficients let us fit the particular summation form to a given function?
>* an expansion/approximation of the function as an infinite sum of sines/cosines
>	* e.g. compare to Taylor series

### Main topics:
* How do we find the coefficients for this frequency-based representation?
* What if our input data are discrete values: $f_0, f_1, f_2,\cdots, f_N$ instead of a smooth continuous function $f(t)$
	* **Discrete Fourier Transform, DFT**
* How can we transform data into the frequency-domain **efficiently**
	* **Fast Fourier Transform, FFT**
## Continuous Fourier Series
Consider some continuous **periodic** function $f(t)$ with period $T$, so$$f(t\pm T) = f(t)$$i.e., $f$ repeats after one length/period $T$.
e.g. $\sin(\frac{2\pi kt}{T})$ or $\cos(\frac{2\pi kt}{T})$ satisfy this for all integers $k$
$$\cos(\frac{2\pi k(t+T)}{T}) = \cos(\frac{2\pi kt}{T} + 2k\pi) = \cos(\frac{2\pi kt}{T})$$
Goal is to represent any $f(t)$ as an infinite sum of trig functions:$$f(t) = a_0 + \sum_{k=1}^{\infty}a_k\cos(\frac{2\pi kt}{T})+\sum_{k=1}^{\infty}b_k\sin(\frac{2\pi kt}{T})$$$a_k, b_k$ indicate the **”information”/amplitude for each sinusoid** of a specific period $\frac{T}{k}$ or frequency $\frac{k}{T}$
* Higher integer $k$ indicates shorter period & higher waver frequency
### Determining the Coefficients
Assume for now that $t\in [0,2\pi]$ and period $T=2\pi$
Then we have$$f(t) = a_0 + \sum_{k=1}^{\infty}a_k\cos(kt)+\sum_{k=1}^{\infty}b_k\sin(kt)$$
#### Handy Identities (Orthogonality)
$$\int_0^{2\pi}\cos(kt)\sin(jt)dt  = 0\;\;\;\;\;\text{for any integers }k,j$$
i.e. the integral of the product of $\cos(kt)$ and $\sin(jt)$ over $[0,2\pi]$ is 0.
We say these two functions are **orthogonal** to each other
#### More Orthogonality Relations
$$\int_0^{2\pi}\cos(kt)\cos(jt)dt  = 0\;\;\;\;\;\text{for }k\neq j$$
$$\int_0^{2\pi}\sin(kt)\sin(jt)dt  = 0\;\;\;\;\;\text{for }k\neq j$$
$$\int_0^{2\pi}\sin(kt)dt  = 0$$
$$\int_0^{2\pi}\cos(kt)dt  = 0$$
We can use these to extract a single Fourier coefficient at a time!

#### Example
##### Determining coefficient $a_0$
We want $$f(t) = a_0 + \sum_{k=1}^{\infty}a_k\cos(kt)+\sum_{k=1}^{\infty}b_k\sin(kt)$$Integrate over $[0,2\pi]$ to use some of our orthogonality identities:
$$\int_0^{2\pi}f(t)dt = a_0\int_0^{2\pi}dt + \sum_{k=1}^{\infty}a_k\int_0^{2\pi}\cos(kt)dt+\sum_{k=1}^{\infty}b_k\int_0^{2\pi}\sin(kt)dt$$
Therefore:
$$a_0 = \frac{\int_0^{2\pi}f(t)dt}{\int_0^{2\pi}dt} = \frac{1}{2\pi}\int_0^{2\pi}f(t)dt$$
i.e., $a_0$ is the average value of $f$ over $[0, 2\pi]$
##### Determining coefficient $a_l$ (for integer $l>0$)
Again start with$$f(t) = a_0 + \sum_{k=1}^{\infty}a_k\cos(kt)+\sum_{k=1}^{\infty}b_k\sin(kt)$$Multiply by $cos(lt)$ and integrate over $[0, 2\pi]$
$$\int_0^{2\pi}f(t)\cos(lt)dt = \int_0^{2\pi}a_0\cos(lt)dt + \sum_{k=1}^{\infty}a_k\int_0^{2\pi}\cos(kt)\cos(lt)dt+\sum_{k=1}^{\infty}b_k\int_0^{2\pi}\sin(kt)\cos(lt)dt$$
The result is 0 **except when $k=l$**. Hence, $$\int_0^{2\pi}f(t)\cos(lt)dt =a_l\int_0^{2\pi}\cos^2(lt)dt=a_l\pi$$
Thus, $$a_l = \frac{1}{\pi}\int_0^{2\pi}f(t)\cos(lt)dt$$
#### Summary
So if we have $f$, we can find all the coefficients by solving integrals
$$a_0 = \frac{\int_0^{2\pi}f(t)dt}{\int_0^{2\pi}dt} = \frac{1}{2\pi}\int_0^{2\pi}f(t)dt$$
$$a_k = \frac{\int_0^{2\pi}f(t)\cos(kt)dt}{\int_0^{2\pi}\cos^2(kt)dt} = \frac{1}{\pi}\int_0^{2\pi}f(t)\cos(kt)dt$$
$$b_k = \frac{\int_0^{2\pi}f(t)\sin(kt)dt}{\int_0^{2\pi}\sin^2(kt)dt} = \frac{1}{\pi}\int_0^{2\pi}f(t)\sin(kt)dt$$
>[!faq] How does phase of the sinusoids come in?
>A sine is a translated cosine! All “in-between” shifts are just linear combinations of sin/cos

### Complex Number Review
For $z \in \mathbb{C}$, we write $z=a+bi$ where the **imaginary number** $i = \sqrt{-1}$
Visualized as points on the **complex plane** $(a, b)$:
* The vector length and angle are often called **modulus** and **argument** respectively
![[Pasted image 20250422160754.png]]
For $z=a+bi$, we can define additional operations
* **Conjugate:** $\bar{z} = a-bi$
* **Modulus/norm:** $|z| = \sqrt{a^2+b^2}$
* **Argument/phase/angle:** $Arg(z) = a\tan 2(b,a)$
	* converts rectangular coordinates $(x, y)$ to polar $(r, \theta)$
### Using Euler’s Formula
We will find **Euler’s formula** very useful:
$$e^{i\theta} = \cos(\theta) + i\sin(\theta)$$
Also$$e^{-i\theta} = \cos(-\theta) + i\sin(-\theta) = \cos(\theta)-\sin(\theta)$$Adding/subtracting these lead to two key identities:
$$\cos(\theta) = \frac{e^{i\theta}+e^{-i\theta}}{2}$$
$$\sin(\theta) = \frac{e^{i\theta}-e^{-i\theta}}{2}$$
### Fourier Series with Complex Exponentials
Now, given our earlier sinusoidal expression of a function $f(t)$$$f(t) = a_0 + \sum_{k=1}^{\infty}a_k\cos(kt)+\sum_{k=1}^{\infty}b_k\sin(kt)$$we can express it more concisely as$$f(t)=\sum_{k=-\infty}^{+\infty}c_ke^{ikt}$$where the $c_k$ coefficients are **complex numbers**
There exists a simple conversion: $c_k \iff a_k, b_k$
* Specifically for $k>0$:$$a_0=c_0, c_k = \frac{a_k}{2}-\frac{ib_k}{2}, c_{-k}=\frac{a_k}{2}+\frac{ib_k}{2}$$And we have the relationships:$$|a_0|=|c_0|,\;\text{and }\;|c_k|=|c_{-k}|=\frac{1}{2}\sqrt{a_k^2+b_k^2}$$
#### Finding $c_k$ coefficients
We can also find **$c_k$ directly**, similar to what we did for $a_k$ and $b_k$
The corresponding **orthogonality property** is:$$\int_0^{2\pi}e^{ikt}e^{-ikt}=\begin{cases}0; k\neq l\\2\pi; k=l\end{cases}$$from which we can determine the coefficient formula,$$c_k=\frac{1}{2\pi}\int_0^{2\pi}e^{-ikt}f(t)dt$$
### Truncating
An *approximation* of a function could be achieved by **truncating** the series to a **finite** number of sinusoids:$$f(t)\approx\sum_{k=-M}^{+M}c_ke^{ikt}$$
### Discrete Input Data
Consider now a vector of **discrete data**
* e.g. $f_0, f_1, f_2, \cdots, f_{N-1}$ for $N$ uniformly spaces data points ($N$ assumed **even**)
Assume data are from an **unknown** function $f(t)$, evaluated at each
$t_n=n\Delta t=\frac{nT}{N}$, for $n-0,1,\cdots, N-1$
* i.e. $f_n=f(t_n)$
### DFT as Interpolation
We have $N=128$ points, and period $T=32$
For $N$ points, we will use **$N$ degrees of freedom** (i.e $N$ coefficients) to exactly **interpolate** the data
Assuming $N$ **is even**, we can approximate with a truncated Fourier series as:
$$f(t)\approx\sum_{-\frac{N}{2}+1}^{N/2}c_ke^{\frac{(2\pi i)kt}{T}}$$If $T=2\pi$, then we will have the simplified version of it as $f(t)\approx\sum_{-\frac{N}{2}+1}^{N/2}c_ke^{ikt}$
Plugging in each of our $N$ data points $(t_n, f_n)$ into the expression will give us $N$ **equations**, involving **unknowns coefficients, $c_k$**
This will lead towards our Discrete Fourier Transform
## Discrete Fourier Transform
For notational convenience we defined:$$W = e^{\frac{2\pi i}{N}}$$$W$ is an **$N$th Root of Unity**, since it satisfies$$W^N = e^{2\pi i} = 1$$So$$f_n = \sum_{k=0}^{N-1}F_ke^{i(\frac{2\pi n k}{N})} = \sum_{k=0}^{N-1}F_kW^{nk}$$Discrete data $f_n$ is expressed as a sum of coefficient, $F_k$, times complex exponentials, $W^{nk}$
### Roots of Unity
With $W = e^{\frac{2\pi i}{N}}$, then 
$$W^k = e^{\frac{2\pi ik}{N}}$$are also **Nth roots of unity,** for all integers $k$
For example:
* for $N=3$, the roots of unity have the form $W^k = e^{k(\frac{2\pi i}{3})}$
* for $N=8$, the roots of unity have the form $W^k = e^{k(\frac{2\pi i}{8})}=e^{k\frac{i \pi}{4}}$
#### Complex Plane
![[Pasted image 20250422165915.png]]
**Each Nth root** corresponds to a point on the unit circle, in the complex plane
Let $\theta = \frac{2\pi k}{N}$, then$$W_k = e^{i\theta} = \cos\theta + i\sin\theta$$Modulus is always 1, since $\sqrt{\cos^2\theta + \sin^2\theta} = 1$
### Discrete Fourier Transform
To be useful, operations we need are:
1. Convert input time-domain data $f_n$ to frequency-domain $F_k$
2. Convert **frequency-domain data $F_k$** back to time-domain $f_n$
We derived #2; given Fourier coefficients $F_k$, we have:
$$f_n = \sum_{k=0}^{N-1}F_kW^{nk}$$
What about #1? How can we solve for the $F_k=???$
#### Another Orthogonality Idea
To find $F_k$, we’ll need another useful property of our Nth roots of unity:
$$\sum_{j=0}^{N-1}W^{jk}W^{-jl} = \sum_{k=0}^{N-1}W^{j(k-l)} = N\delta_{k,l}$$assuming (for now) that $k,l\in[0, N-1]$
The symbol $\delta_{k,l}$ indicates the **Kronecker delta** function defined by:
$$\delta_{k,l}=\begin{cases}0; k\neq l\\1; k=l\end{cases}$$
### A Discrete Fourier Transform (DFT) pair
**Inverse DFT:**$$f_n = \sum_{k=0}^{N-1}F_kW^{nk}$$
**DFT:**$$F_k=\frac{1}{N}\sum_{n=0}^{N-1}f_nW^{-nk}$$The Discrete Fourier Transform is **invertible**
#### Two Properties of the DFT
As consequences of the properties of Nth roots of unity…
1. The sequence $\{F_k\}$ is **doubly infinite** and **periodic**
	* i.e. If we allow $k<0$ or $k>N-1$, the $F_k$ coefficients repeat
2. **Conjugate symmetry:** if data $f_n$ is real, $F_k = \overline{F_{N-k}}$ 
Hence, the $|F_k|$ are symmetric about $k=\frac{N}{2}$
### Power/ Fourier Spectrum
The **power spectrum** visualizes the Fourier coefficients by plotting their moduli/magnitudes $|F_k|$:
![[Pasted image 20250422183354.png]]
This expresses the magnitude of the frequencies, but **ignores phase**
#### Discrete Data - Observations
Coefficient $F_0$ is always the average of data values, $F_0=\frac{1}{N}\sum_{n=0}^{N-1}f_n$
* sometimes called the **direct current** or **DC**
![[Pasted image 20250422184748.png]]
The smooth bump had one dominant frequency/wave; therefore one coefficient pair, $F_1$ and $F_8$, had large magnitude
![[Pasted image 20250422184824.png]]
The rough bump had more irregularity, so more active (higher) frequencies.
* Main hump still dominates, so low frequencies $F_1$ and $F_8$ remain largest

The Fourier $(F_k)$ plots are **symmetric,** since the data was **real**
## Fast Fourier Transform
### Making Fourier Transforms Fast
**Questions:**
* What is the complexity of the naïve method?
* What property of the DFT allows it to be sped up?
* How can we construct an algorithm from this property?
* What is the complexity of the new method?
#### Slow Fourier Transform
A direct implementation of $F_k=\frac{1}{N}\sum_{n=0}^{N-1}f_nW^{-nk}$ takes $O(N^2)$ **complex floating-point operations**
Essentially two nested **for loops:**
![[Pasted image 20250422185249.png]]
#### A Faster Fourier Transform
Design a **divide and conquer strategy**
1. **Split** the full DFT into two DFT’s of half the length
2. **Repeat** recursively
3. Finish at the base case of individual numbers
(If $N\neq 2^m$ for some $m$, we can pad our initial data with zeros)
##### Dividing it up
We can express the usual DFT with two new arrays of **half the length** ($N/2$):
$$g_n=\frac{1}{2}(f_n+f_{n+\frac{N}{2}})$$$$h_n=\frac{1}{2}(f_n-f_{n+\frac{N}{2}})W^{-n}$$
where $n\in [0, \frac{N}{2}-1]$.
Then, $F_{even}=G=DFT(g)$ and $F_{odd}=DFT(h)$.
##### Visualizing - A Butterfly Operation
We can think of each step as taking a pair of numbers and producing two outputs:
![[Pasted image 20250422190321.png]]
###### Big Picture - Recursive Butterfly FFT Algorithm
![[Pasted image 20250422190428.png]]
$N=8=2^3$, so we have 3 recursive stages
**Note:** **Coefficient output order is scrambled**
![[Pasted image 20250422190751.png]]
* Each step applies an even-odd index splitting for the result location. So, the output ends up in **bit-reversed positions**
![[Pasted image 20250422190758.png]]
##### Is it actually faster?
* We spend $O(N)$ operations to split the arrays in two, at each stage
* Data has length $N=2^m$, so we need m = $\log_2N$ stages
* Total cost $O(N\log_2N)$ operations
	* compared to $O(N^2)$ of DFT
### Inverse Fast Fourier Transform
Consider the **generic expression:** $$f'_k=\frac{1}{N}\sum_{n=0}^{N-1}f_nU^{nk}$$If $U+W^{-1}$, this is our **forward DFT**
* $U = W^{-1}, f’k=F_k, f_n=f_n \rightarrow F_k=\frac{1}{N}\sum_{n=0}^{N-1}f_nW^{-nk}$
If $U=W$, and we post-multiply by $N$, this is the inverse FFT
* $U=W, f'_k=f_n, f_n=F_k \rightarrow f_n = \sum_{k=0}^{N-1}F_kW^{nk}$
## Fourier Application: Image Data/Compression
### 1D Grayscale Image
We can think of a 1D array of grayscale values as a **1D image**
* Each entry gives the pixels’ intensity/grey values
#### Processing 1D Images
For greyscale images, we can perform a DFT on the pixels’ intensity/grey values
![[Pasted image 20250422194813.png]]
**Notice:** Plot is only the first 16 coefficients, since real data implies conjugate symmetry
* Overall pattern has **few coefficients active**
	* Can store it cheaply just with $F_0, F_4, F_8, F_12$
If we destroyed the repetition (e.g. flat line top for the 3rd bump)
* Many more Fourier coefficients will become active/non-zero
* becomes expensive to store
![[Pasted image 20250422195129.png]]
* Although many coefficients are non-zero, many still have fairly small moduli/magnitude…
	* so those frequencies contribute less to the image
##### Compression Strategy
* Create an **approximate** compressed version of the image, $f_n$, by **throwing away** small Fourier coefficients
	* $|F_k|< tol$
* To reconstruct the image, run the **inverse DFT** to get modified data (pixels), $\hat f_n$
* Discard the imaginary parts of $\hat f_n$, to ensure new data is strictly **real**
##### Comparison
![[Pasted image 20250422195707.png]]
Recovered “image” hopefully has small deviations from the original “true” data
* But! We store **fewer** Fourier coefficients and so **save space!**
### Image Processing in 2D
![[Pasted image 20250422195824.png]]
>[!faq] How does the DFT work for 2D (greyscale) image data?

We apply a 2D extension of the DFT definition to the data, like so:
$$F_{k,l}=\frac{1}{NM}\sum_{n=0}^{N-1}\sum_{j=0}^{M-1}f_{n,j}W^{-nk}_NW^{-jl}_M$$
Essentially two standard (1D) DFT’s combined.
Two (possibly distinct) roots of unity are used, one per dimension:
$$W_N=e^{\frac{2\pi i}{N}} \text{ and } W_M=e^{\frac{2\pi i}{M}}$$
Result is a **2D array** of Fourier coefficients, $F_{k,l}$
#### 2D Fast Fourier Transform
![[Pasted image 20250422200410.png]]
The 2D FFT can be computed efficiently using nested 1D FFTs:
1. Transform each row (separately) using 1D FFTs
2. Transform each column on the result, again using 1D FFTs
##### Complexity
Performing $M$ 1D FFT’s of length $N$: $M\times O(N\log_2N)=O(MN\log_2N)$
Performing $N$ 1D FFT’s of length $M$: $N\times O(M\log_2M)=O(MN\log_2M)$
So total complexity is $O(MN(\log_2M+\log_2N))$
#### Block-based Image Compression
![[Pasted image 20250422200752.png]]
Often an image is **subdivided into smaller blocks:** $16\times 16$ or $8\times 8$ pixels
* Compression is performed on each block **independently**
**Idea:** Pixels within a block often have similar/related data, and hopefully compress effectively
## Fourier Application: Understanding Aliasing
### Sampling of Signals: Aliasing
If a real input signal contains high frequencies, but the spacing of our discretely sampled data points is inadequate, **aliasing** can occur
![[Pasted image 20250422202037.png]]
A truly high frequency signal (red) **aliases as** a lower frequency signal (blue) in the discrete result
#### Takeaway
Our DFT coefficients $F_k$ are sums of true continuous Fourier series coefficients $c_k$ of increasing frequency:
$$F_k=c_k+c_{k+N}+c_{k-N}+c_{k+2N}+c_{k-2N}+\cdots$$
Hence, high frequencies from $c_k\notin\left[-\frac{N}{2}+1,\frac{N}{2}\right]$ in the real signal contribute to (“alias as”) low frequency $F_k$ for $k \in \left[-\frac{N}{2}+1,\frac{N}{2}\right]$.
### Nyquist Frequency
If the original continuous signal has frequencies $c_k\neq 0$ for $|k|>\frac{N}{2}$ those frequencies “alias” to a lower frequency
* Once a signal is discretely sampled, there is **no way to distinguish** aliased (high) frequencies from real (low) frequencies
### Treating Aliasing
Two (partial) solutions:
* **Increase** the sampling resolution to **capture higher frequencies**
* Filter before sampling to **remove** (too) high frequencies
	* so they don’t cause aliasing
#### Example:
Digital Cameras often have **optical lowpass filters** or **anti-aliasing filters** that physically blur the incoming light, before it hits the image sensor