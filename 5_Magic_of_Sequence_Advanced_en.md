# 5. Advanced Analysis: Characteristic Equations and Coefficient Derivation via Finite Difference Approximation

## 5.1 Introduction

As of July 2026, processing specific ranges of numerical arrays from 1D sequences to 2D matrices using consistent local rules and sliding windows has become a widely implemented technique. This technology is commonly used in modern smartphones.

This document provides a mathematically rigorous explanation of the theoretical background, analytical solutions, and numerical derivation methods for the "Magic of Sequences". It is designed for upper-level undergraduate students and researchers who have foundational knowledge in mathematical sciences, physics, digital signal processing (DSP), and computer engineering.

In engineering terms, the process of solving the 3-term linear recurrence relation (a 2nd-order linear constant-coefficient finite difference equation) in this repository directly corresponds to **analyzing the pole-placement of a "Transfer Function" and evaluating the impulse response in DSP**.

Additionally, this document serves as a chronological record of identical mathematical queries compiled from multiple major generative AI models as of July 2026. It functions as a concrete case study to evaluate the performance of current AI models in eliminating programming barriers.

## 5.2 Mathematical Model and Prompt Conditions used for Verification

For verification, the following mathematical conditions and implementation stub were inputted into each generative AI model:

> **[Input Prompt]**
> How can we determine the coefficients $a$ and $b$ for the 3-term recurrence relation `u(1)=0; u(2)=1; for n=3:1000; u(n)=u(n-1)*a-u(n-2)*b; end` so that it matches $100\sin(t)$ as closely as possible? Assume a finite time step of $\Delta t = 0.01$ for each increment of $n$ (step size is $1/100$).

## 5.3 Mathematical Approaches for Determining Coefficients (Summary of AI Responses)

### 5.3.1 Rigorous Derivation Based on the Characteristic Equation (DSP Pole-Placement)
Applying the $z$-transform (or assuming a characteristic equation) to the given linear finite difference equation $u_n - a u_{n-1} + b u_{n-2} = 0$, we obtain the following quadratic equation:

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

### 5.3.2 Derivation Based on the 2nd-Order Central Finite Difference Approximation
As a physical approach, we start with the continuous ordinary differential equation (the equation of motion for a harmonic oscillator) that satisfies the continuous theoretical exact solution $y(t) = 100 \sin(t)$:

$$
\frac{d^{2}y}{dt^{2}} + y = 0
$$

We discretize this continuous differential equation using a **2nd-order central finite difference** with a finite time step $\Delta t$. Approximating the continuous 2nd-order derivative at time $t$ using the differences between discrete steps gives the following expression:

$$
\frac{u_n - 2u_{n-1} + u_{n-2}}{\Delta t^{2}} + u_{n-1} = 0
$$

Rearranging this equation to solve for $u_n$ by multiplying both sides by $\Delta t^2$ and moving the terms to the right side gives:

$$
u_n = (2 - \Delta t^{2})u_{n-1} - u_{n-2}
$$

Comparing the coefficients of each term with our target finite difference equation $u_n = a u_{n-1} - b u_{n-2}$, we find:

$$
a = 2 - \Delta t^{2}, \quad b = 1
$$

Substituting the finite time step $\Delta t = 0.01$ gives:

$$
a = 2 - 0.01^{2} = 2 - 0.0001 = 1.9999, \quad b = 1
$$

*Note: This finite difference approximation value ($a = 1.9999$) perfectly matches the value obtained by taking the Maclaurin series expansion (Taylor expansion) of the strict analytical solution $2\cos(0.01)$ up to the second-order term.*

### 5.3.3 Influence of Initial Values on Impulse Response Amplitude
The given initial conditions for our numerical calculation are $u_1 = 0$ and $u_2 = 1$.
In general, the solution derived from the characteristic equation can be expressed as $u_n = A \sin((n-1)\theta)$.
From the second step condition $u_2 = 1$, the relation $A \sin(0.01) = 1$ must hold. Therefore, the amplitude $A$ of the discrete impulse response is determined as follows:

$$
A = \frac{1}{\sin(0.01)} \approx 100.00167
$$

This numerical approximate amplitude is extremely close to the continuous target amplitude of $100$. This demonstrates that the discrete initial condition $u_2 = 1$ is reasonably and accurately matched via the small-angle approximation ($\sin(\theta) \approx \theta$).

## 5.4 Determining Coefficients via the Least-Squares Method (System Identification of an AR Model)

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

## 5.5 Output Characteristics of Generative AI Models and Disclaimer

The mathematical derivation processes and explanations recorded in this document are based on the author's prompts. The dynamic outputs generated by the following AI models have been academically reviewed and compiled by the author. While the author converted the formulas into LaTeX and organized the layout, the core logical arguments are based on the outputs generated as of July 2026.

* **Microsoft Copilot** (Verified: July 5, 2026)
* **Google Chrome AI mode** (Verified: July 5, 2026)
* **Google Gemini** (Verified: July 5, 2026)
* **MATLAB Copilot** (Verified: July 5, 2026)

## 5.6 License

The programming codes and instructional materials in this repository are provided under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

## 5.7 Citation

If you use the programs, data, or instructional materials in this GitHub repository, please cite the following persistent DOI issued by Zenodo:
[Insert Zenodo DOI here]

## Repository Structure and Contents

* **[README_en.md](https://www.google.com/search?q=README_en.md)**
* **[index_en.html](https://www.google.com/search?q=index_en.html)**
* **[Magic_of_Sequence_MATLAB_en.mlx](https://www.google.com/search?q=Magic_of_Sequence_MATLAB_en.mlx)**
* **[4_Magic_of_Sequence_Plain_en.md](https://www.google.com/search?q=4_Magic_of_Sequence_Plain_en.md)**
* **[5_Magic_of_Sequence_Advanced_en.md](https://www.google.com/search?q=5_Magic_of_Sequence_Advanced_en.md)**
* **[6 How does this magic connect to university topics?](https://www.google.com/search?q=6_Magic_of_Sequence_Edu_Significance_en.md)**
* **[7 Historical Context Learned from Generative AI](7_Historical_Context_via_AI_en.md)**
