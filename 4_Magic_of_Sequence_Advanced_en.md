# 4. Advanced Analysis: Characteristic Equations and Coefficient Derivation via Finite Difference Approximation V.1.0.4

## 4.1 Introduction

As of July 2026, processing specific ranges of numerical arrays from 1D sequences to 2D matrices using consistent local rules and sliding windows has become a widely implemented technique. This technology is commonly used in modern smartphones.

This document provides a mathematically rigorous explanation of the theoretical background, analytical solutions, and numerical derivation methods for the "Magic of Sequences". It is designed for upper-level undergraduate students and researchers who have foundational knowledge in mathematical sciences, physics, digital signal processing (DSP), and computer engineering. Please find further details in typical text books `[1]`.

In engineering terms, the process of solving the 3-term linear recurrence relation (a 2nd-order linear constant-coefficient finite difference equation) in this repository directly corresponds to **analyzing the pole-placement of a "Transfer Function" and evaluating the impulse response in DSP**.

Additionally, this document serves as a chronological record of identical mathematical queries compiled from multiple major generative AI models as of July 2026. It functions as a concrete case study to evaluate the performance of current AI models in eliminating programming barriers.

## 4.2 Mathematical Model and Prompt Conditions used for Verification

For verification, the following mathematical conditions and implementation stub were inputted into each generative AI model:

> **[Input Prompt]**
> How can we determine the coefficients $a$ and $b$ for the 3-term recurrence relation `u(1)=0; u(2)=1; for n=3:1000; u(n)=u(n-1)*a-u(n-2)*b; end` so that it matches $100\sin(t)$ as closely as possible? Assume a finite time step of $\Delta t = 0.01$ for each increment of $n$ (step size is $1/100$).

## 4.3 Mathematical Approaches for Determining Coefficients (Summary of AI Responses)

### 4.3.1 Rigorous Derivation Based on the Characteristic Equation (DSP Pole-Placement)
Assuming a solution of the form $u_n = \lambda^n$ (or applying the $z$-transform) for the given linear finite difference equation $u_n - a u_{n-1} + b u_{n-2} = 0$, we obtain the following characteristic equation:

$$
\lambda^{2} - a\lambda + b = 0 \quad \cdots (1)
$$

The target function, which is the continuous theoretical exact solution $y(t) = 100 \sin(t)$, represents an undamped harmonic oscillation with a constant amplitude. In a discrete-time system, the mathematical condition for a signal to oscillate without amplification or decay requires **the poles (characteristic roots $\lambda$) of the transfer function to lie precisely on the unit circle (absolute value of 1) in the complex $z$-plane**.
Since the phase advances by a finite amount $\theta = 0.01\text{ rad}$ for each time step increment, the configuration of the poles as complex conjugate roots is expressed as follows:

$$
\lambda = 1 \cdot e^{\pm i\theta} = \cos\theta \pm i\sin\theta
$$

Using Vieta's formulas (the relationship between roots and coefficients), the coefficients $a$ and $b$ are derived from the sum and product of the two poles:

$$
a = \lambda_{1} + \lambda_{2} = 2\cos\theta
$$

$$
b = \lambda_{1} \cdot \lambda_{2} = \cos^{2}\theta + \sin^{2}\theta = 1
$$

Substituting the target finite phase change $\theta = 0.01$ into these equations yields the exact coefficients:

$$
a = 2\cos(0.01) \approx 1.99990000083333, \quad b = 1
$$

### 4.3.2 Derivation Based on the Central Difference Approximation of the Second Derivative
As a physical approach, we start with the continuous ordinary differential equation (the equation of motion for a harmonic oscillator) satisfied by the continuous theoretical exact solution $y(t) = 100 \sin(t)$:

$$
\frac{d^{2}y}{dt^{2}} + y = 0
$$

We discretize this continuous differential equation using the **central difference of the second derivative** (second-order accurate) with a finite time step $\Delta t$. Approximating the continuous 2nd-order derivative at time $t$ using the differences between discrete steps gives the following expression:

$$
\frac{u_{n+1} - 2u_{n} + u_{n-1}}{\Delta t^{2}} + u_{n} = 0
$$

Rearranging this equation to solve for $u_{n+1}$ by multiplying both sides by $\Delta t^2$ and moving the terms to the right side gives:

$$
u_{n+1} = (2 - \Delta t^{2})u_{n} - u_{n-1}
$$

Comparing the coefficients of each term with our target finite difference equation $u_{n+1} = a u_{n} - b u_{n-1}$, we find:

$$
a = 2 - \Delta t^{2}, \quad b = 1
$$

Substituting the finite time step $\Delta t = 0.01$ gives:

$$
a = 2 - 0.01^{2} = 2 - 0.0001 = 1.9999, \quad b = 1
$$

*Note: This finite difference approximation value ($a = 1.9999$) perfectly matches the value obtained by taking the Maclaurin series expansion (Taylor expansion) of the value $2\cos(0.01)$ obtained from the exact pole placement above, up to the second-order term.*

### 4.3.3 Influence of Initial Values on Impulse Response Amplitude
The given initial conditions for our numerical calculation are $u_1 = 0$ and $u_2 = 1$.
From the roots $e^{\pm i\theta}$ of the characteristic equation, the general solution is expressed as $u_n = A \sin((n-1)\theta) + B \cos((n-1)\theta)$. The initial condition $u_1 = 0$ gives $B = 0$.
From the second step condition $u_2 = 1$, the relation $A \sin(0.01) = 1$ must hold. Therefore, the amplitude $A$ of the discrete impulse response is determined as follows:

$$
A = \frac{1}{\sin(0.01)} \approx 100.00167
$$

This numerical approximate amplitude is extremely close to the continuous target amplitude of $100$. This demonstrates that the discrete initial condition $u_2 = 1$ is reasonably and accurately matched via the small-angle approximation ($\sin(\theta) \approx \theta$).

Note that the coefficient $a = 1.9999$ actually used in the code differs slightly from $2\cos(0.01)$, so the phase per step is $\theta = \arccos(1.9999/2) = 0.0100000417$ rad, and the amplitude is $1/\sin\theta \approx 100.00125$.

### 4.3.4 Why the Amplitude Neither Decreases nor Increases: $b=1$ and Area Preservation (Symplecticity)

Figure 6 in Chapter 3 shows the case of $\Delta t=0.1$ and $a=1.99$; even after 300,000 steps, the amplitude of the "Magic of Sequences" did not decrease. The reason is that the coefficient $b$ is exactly 1.

**(Technical explanation)** If we regard the recurrence relation $u_{n+1} = a u_n - b u_{n-1}$ as a map that advances the pair of consecutive terms $(u_n, u_{n-1})$ by one step, it can be written as

$$
\begin{bmatrix} u_{n+1} \\ u_n \end{bmatrix}
=
\begin{bmatrix} a & -b \\ 1 & 0 \end{bmatrix}
\begin{bmatrix} u_n \\ u_{n-1} \end{bmatrix}
$$

The determinant of this matrix is $b$. Therefore, when $b=1$, this map preserves area in the two-dimensional plane (corresponding to position and velocity). For a system with one degree of freedom, area preservation means the same as symplecticity.

Furthermore, when $b=1$, the following quantity $I$ is conserved **exactly** (substituting and rearranging confirms $I_{n+1}=I_n$):

$$
I_n = u_n^{2} + u_{n-1}^{2} - a\, u_n u_{n-1}
$$

When $a = 2 - \Delta t^2$, letting $\bar{u} = (u_n + u_{n-1})/2$ be the midpoint position of two adjacent terms and $v = (u_n - u_{n-1})/\Delta t$ the velocity between them, we can rewrite this as

$$
\frac{I_n}{\Delta t^{2}} = \bar{u}^{2} + \left(1 - \frac{\Delta t^{2}}{4}\right) v^{2}
$$

This differs from (twice) the true energy, $u^2 + v^2$, only by an amount of order $\Delta t^2$. In other words, $I$ is not the true energy, but a "modified energy" very close to it. For symplectic numerical methods, it has been proven in general that such a modified energy (modified Hamiltonian, shadow Hamiltonian) is nearly conserved over very long times `[2]`. The "Magic of Sequences" is the simplest example in which this modified Hamiltonian can be written down by hand as an exactly conserved quantity.

Because of the conserved quantity $I$, the numerical approximate solution keeps going around a fixed ellipse in the $(u_n, u_{n-1})$ plane, and its amplitude neither increases nor decreases. However, the angle advanced in one step is $\theta = \arccos(a/2)$, which for $a = 2-\Delta t^2$ is $\theta \approx \Delta t\,(1 + \Delta t^2/24)$, slightly larger than the true value $\Delta t$. The accumulation of this period mismatch (phase error) is the "beating" seen in Figure 6 of Chapter 3.

For comparison, if the same simple harmonic oscillation is solved with the forward Euler method and the velocity is eliminated to obtain a recurrence relation for the position only, we get $a=2$ and $b=1+\Delta t^2$. Because $b>1$, the area expands by a factor of $(1+\Delta t^2)$ in every step, and the amplitude keeps growing. Conversely, making $b<1$ shrinks the area, which gives the damped oscillation in the table of Chapter 3.

**(Plain explanation)** $b$ is the number that determines "by what factor the size of the oscillation (more precisely, the area on the graph of position and velocity) is multiplied in each step". If $b=1$, the factor is exactly one, so the size of the oscillation does not change, no matter how many tens of thousands of times the calculation is repeated. Instead, the timing of the oscillation becomes slightly earlier little by little, and the mismatch with the exact answer appears as "beating".

## 4.4 Determining Coefficients via the Least-Squares Method (System Identification of an AR Model)

When the target time-series data $x_n$ is given as a known dataset, we can use a data-science approach to optimize the constant parameters. By using the **least-squares method**, we can perform **system identification**. This process is mathematically identical to "parameter estimation of an Autoregressive (AR) model" in statistical science.

$$
x_n \approx a x_{n-1} - b x_{n-2} \quad (n=3, 4, \dots, N)
$$

We can expand this into a matrix form, which is the standard model for system identification:

$$
\begin{bmatrix} 
x_2 & -x_1 \\ 
x_3 & -x_2 \\ 
\vdots & \vdots \\ 
x_{N-1} & -x_{N-2} 
\end{bmatrix} 
\begin{bmatrix} 
a \\ 
b 
\end{bmatrix} 
\approx 
\begin{bmatrix} 
x_3 \\ 
x_4 \\ 
\vdots \\ 
x_N 
\end{bmatrix}
$$

Letting the data matrix be $X$, the output vector be $y$, and the parameter vector be $p = [a, b]^T$, the numerical least-squares solution is obtained from the Normal Equation as follows:

$$
p = \begin{bmatrix} a \\ b \end{bmatrix} = (X^T X)^{-1}X^T y
$$

Below is a concrete implementation example of this least-squares identification algorithm in MATLAB:

* **MATLAB**
```matlab
% Parameter identification from time-series data 'x' (Solving the inverse problem of an AR model)
X = [x(2:end-1).'  -x(1:end-2).'];
y = x(3:end).';
p = X \ y;      % Calculating the least-squares solution using the backslash operator
a = p(1);
b = p(2);

```

## 4.5 Output Characteristics of Generative AI Models and Disclaimer

The mathematical derivation processes and explanations recorded in this document are based on the author's prompts. The dynamic outputs generated by the following AI models have been academically reviewed and compiled by the author, together with Claude. While the generative AI converted the formulas into LaTeX and compiled the layout, the core logical arguments are based on the outputs generated as of July 2026.

* **Microsoft Copilot** (Verified: July 5, 2026)
* **Google Search AI Mode** (Verified: July 5, 2026)
* **Google Gemini** (Verified: July 5, 2026)
* **MATLAB Copilot** (Verified: July 5, 2026)

## 4.6 Author and Citation

* Note: For details on author information, citation instructions (DOI), and the license (CC BY 4.0), please refer to [README_en.md](README_en.md).


## References and notes

`[1]`: e.g., A. V. Oppenheim, R. W. Schafer, *Discrete-Time Signal Processing*, 3rd ed. (Pearson/Prentice Hall, 2010). / [I. Goodfellow, Y. Bengio, A. Courville, Deep Learning (MIT Press, 2016)](https://www.deeplearningbook.org/).

`[2]`: [G. Benettin, A. Giorgilli, "On the Hamiltonian interpolation of near-to-the identity symplectic mappings with application to symplectic integration algorithms", *J. Stat. Phys.* **74** (1994) 1117–1143](https://doi.org/10.1007/BF02188219) / E. Hairer, C. Lubich, G. Wanner, *Geometric Numerical Integration*, 2nd ed. (Springer, 2006), Chapter IX / [E. Hairer, C. Lubich, G. Wanner, "Geometric numerical integration illustrated by the Störmer–Verlet method", *Acta Numerica* **12** (2003) 399–450](https://doi.org/10.1017/S0962492902000144).

## Repository Structure and Links

* **[README_en.md](README_en.md)**
* **[index_en.html](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)**
* **[Magic_of_Sequence_MATLAB_en.mlx](Magic_of_Sequence_MATLAB_en.mlx)**
* **[3_Magic_of_Sequence_Plain_en.md](3_Magic_of_Sequence_Plain_en.md)**
* **[4_Magic_of_Sequence_Advanced_en.md](4_Magic_of_Sequence_Advanced_en.md)**
* **[5 How does this magic connect to university topics?](5_Magic_of_Sequence_Edu_Significance_en.md)**
* **[6 Historical Context Learned from Generative AI](6_Historical_Context_via_AI_en.md)**
