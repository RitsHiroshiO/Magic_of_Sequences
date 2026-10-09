# 1. Magic of Sequences: Open Educational Resources for Physics-Math-Computing via Simple Recurrence Relations (V.1.0.4)
[「数列のマジック」 README 日本語版](README.md)

> While compiling this repository, I realized that the "Magic of Sequences" will also help **AI-generation students** develop their ability **to notice that even a slight numerical difference can result in a large physical difference**. I hope that the "Magic of Sequences" and this open resource will give readers a chance to recognize **the importance and appeal of physics** again.

## 1.1 Quick Start: Interactive Web App
Experience the "Magic of Sequences" right now in your browser!

* **[Launch the Interactive App (https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)**
* **Try this:** Pick (a,b) for $u_n = a \times u_{n-1} - b \times u_{n-2}$ with buttons  `(1.9999, 1)`, `(1.99, 1)`, `(1.99, 0.99)`, `(1.98, 0.99)`. Enjoy watching how the curves drastically transform from straight lines to oscillations and damping.
* **Then, enjoy observing drastic change even with subtle change in the above a or b by the slide bars! Adjust scale if needed.**

## 1.2 Project Overview & Educational Vision

This GitHub repository provides the programming codes and instructional materials for "Magic of Sequences," an open educational resource designed to seamlessly connect high school mathematics (recurrence relations) with foundational university-level physics, data science, digital signal processing, and AI technologies.
Modern STEM education, e.g., Caballero & Odden (2024, Nature Physics)`[1]` emphasizes the urgent need to strengthen student literacy in computation for AI and data science. This GitHub repository provides an introductory curriculum that starts with a simple high school linear recurrence relation and connects it directly to core concepts in university physics (mechanics and wave theory), data science, digital signal processing (DSP), computer graphics (CG), and deep learning. It is designed so that students can learn without detailed mathematical explanations of the methods frequently used in conventional physics simulation education (such as the Euler method based on forward differences) `[2]`.

As Richard Feynman famously noted, *"What I cannot create, I do not understand."* In today's digital era, where generative AI can instantaneously output complex codes, providing students with the experience of building and evaluating models from the absolute ground up is critical. By writing their own loops and observing the accumulation of microscopic errors, students develop the "error-detecting objectivity" and design confidence required in the AI era.

While engaging in an extended dialogue with a generative AI for this project, I realized that reviewing the historical positioning of numerical analysis—specifically the Euler and Runge–Kutta methods and the central difference method (Störmer–Verlet method)—offers fascinating insights. It was a profound learning experience for me to trace how our predecessors, from the era of paper and pencil to modern computers, exercised their ingenuity under various constraints to reach where we are today. I have added these reflections to the repository. While the content might be challenging for incoming first-year students, I hope it serves as a valuable reference. This GitHub content, V.1.0.4, has received important corrections and additions with the help of Claude Opus 5.5. Because verification showed that V.1.0.2 contained errors and unsupported anecdotes, especially in its historical descriptions, they have been revised on the basis of primary sources (see the note at the beginning of Chapter 6). The technical descriptions have also become more precise.

## 1.3 Repository Structure and Contents

This GitHub repository consists of the following interlinked components. Please refer to the respective files based on your computing environment and level of expertise.

* **[index_en.html](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)**: An interactive HTML application that allows users to adjust the coefficients of the finite difference equation directly in their browser. It enables visual exploration of how the numerical approximate solution behaves—transitioning from simple harmonic oscillation to damped oscillation and divergence.

* **[Magic_of_Sequence_MATLAB_en.mlx (with corresponding Python codes)](Magic_of_Sequence_MATLAB_en.mlx)**: This is the main MATLAB Live Script based on the materials used in the very first class of the first semester for first-year university students. It provides clear explanations, ranging from the "Magic of Sequences" to creating simple 1D and 2D wave propagation animations. Additionally, with the help of generative AI, we have newly added Python code for Google Colab, which can be run on mobile browsers. We also added an accuracy comparison with the Runge–Kutta method (the MATLAB function `ode45`) for undergraduate students in specialized courses (confirming that, in the "Magic of Sequences", the amplitude, a quantity corresponding to energy, is maintained over long times).
Supposed readers include university students in the first week in the first semester and advanced high school students. It also provides an accessible explanation of how initial value problems correspond to "impulse responses" in digital signal processing. It provides detailed program explanations along with the simulation execution environment, and is directly linked with the MATLAB File Exchange. MATLAB R2021a or later is needed to enjoy this mlx file.

* **[3_Magic_of_Sequence_Plain_en.md](3_Magic_of_Sequence_Plain_en.md)**: A Markdown formatted text export of the MATLAB Live script with corresponding Python code and plain explanation, "Magic_of_Sequence_MATLAB_en.mlx", for readers not familiar with MATLAB. Except for the executability on MATLAB, the contents are identical to "Magic_of_Sequence_MATLAB_en.mlx". 

* **[4_Magic_of_Sequence_Advanced_en.md](4_Magic_of_Sequence_Advanced_en.md)**: A mathematically rigorous analytical document intended for second-year undergraduates and above. It covers pole placement analysis of transfer functions using characteristic equations, coefficient derivation via finite difference approximation, and system identification of AR models using the method of least squares.

* **[5_Magic_of_Sequence_Edu_Significance_en.md](5_Magic_of_Sequence_Edu_Significance_en.md)**: Please read this alongside the conceptual map in Section 1.4, which shows what each thread of "Magic of Sequences" connects to. Please find more details on its educational significance within the university curriculum.

* **[6_Historical_Context_via_AI_en.md](6_Historical_Context_via_AI_en.md)**: A review of the historical positioning of the Euler and Runge–Kutta methods and the central difference method (Störmer–Verlet method) in numerical analysis (revised in October 2026 on the basis of the literature). In compiling this with the help of generative AI, I strongly felt the necessity of conveying the fascination and importance of physical thinking to students who enter STEM programs without having selected physics in their university entrance exams.

The educational materials in this repository (such as [index_en.html](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html) and [Magic_of_Sequence_MATLAB_en.mlx](Magic_of_Sequence_MATLAB_en.mlx) or [3_Magic_of_Sequence_Plain_en.md](3_Magic_of_Sequence_Plain_en.md)) can also be used as a visual and intuitive introduction (an icebreaker) when teaching the concept of "Poles and Zeros" of characteristic equations in control engineering and signal processing.

## 1.4 Conceptual Map: The Recurrence Relation as an Educational Hub

```text
=============================================================================================
【 Core Concept: Magic of Sequences (2nd-Order Linear Difference Equation) 】
  u(n) = a * u(n-1) - b * u(n-2)
=============================================================================================
         │
         ├───────────────────────────┼───────────────────────────┐
         ▼                           ▼                           ▼
【 Academic Development 】          【 Practical Application 】   【 Educational Value 】
  │                           │                           │
  ├─► [Mechanics & Comp. Phys.]├─► [CG Physics Engines]    ├─► [High School Students]
  │   Störmer–Verlet Method   │   Realistic game physics  │   Foundational math for AI
  │   Central Difference Scheme│   Inertial scrolling      │   Broadening career visions
  │                           │                           │
  ├─► [Differential Equations] ├─► [Digital Signal Proc.]  ├─► [Physics Non-Majors]
  │   Characteristic Equations│   Transfer function poles │   Building confidence by
  │   Stability analysis      │   Impulse response design │   coding models from scratch
  │                           │                           │
  ├─► [Continuum & Wave Theory]├─► [Digital Image Proc.]   ├─► [Physics Majors]
  │   Multidimensional (Laplacian) Spatial filtering       │   Limits of discrete models
  │   Diffusion & Wave eqs.   │   Laplacian edge detection│   Accumulated phase error (Beats)
  │                           │                           │
  └─► [Advanced AI Mathematics]└─► [Data Sci. & Finance]   └─► [Educators]
      Autoregressive (AR) Model   Time-series forecasting │   Developing "error-detecting
      ResNet / Neural ODE         Least-squares system ID │   objectivity" in the AI era
=============================================================================================

```

## 1.5 Glossary (Technical Terms and Plain Explanations)

This repository presents concise, precise expressions using technical terms together with plain explanations for non-specialist readers. The main correspondences are summarized below.

| Technical term | Plain explanation | Where it mainly appears |
| --- | --- | --- |
| Three-term recurrence relation (2nd-order linear constant-coefficient difference equation) $u_n = a u_{n-1} - b u_{n-2}$ | A rule that decides the next value from the previous value and the one before it | Throughout |
| Forward difference (forward Euler method) | A method that takes one step forward using the current slope (velocity) | Ch. 3, Ch. 6 |
| Euler–Cromer method (semi-implicit Euler method, symplectic Euler method) | A method that first updates the velocity and then takes one step using that new velocity. Written in terms of position only, it gives the same equation as the "Magic of Sequences" | Ch. 3, Ch. 5 |
| Central difference (Störmer–Verlet method, Verlet method, leapfrog method) | A method that decides the next position from the previous and current positions. This is the "Magic of Sequences" itself | Ch. 3–6 |
| Runge–Kutta methods (explicit one-step methods) | Methods that try the slope several times within one step and average them, so as to advance one step accurately | Ch. 3, Ch. 6 |
| Classical fourth-order Runge–Kutta method (RK4) | The best-known Runge–Kutta method, which keeps the step size fixed and tries the slope four times within one step | Ch. 3 |
| MATLAB's `ode45` (Dormand–Prince 5(4) method, variable step) | A Runge–Kutta method that automatically changes the step size while estimating the error. It is different from "the fourth-order Runge–Kutta method" | Ch. 3 |
| Tolerances (RelTol, AbsTol) | Settings that determine how much error is allowed in each step. The default (RelTol=1e-3) is about 0.1% | Ch. 3 |
| Phase error | An error in which the size of the oscillation is correct, but its timing gradually shifts. The cause of the "beating" | Ch. 3, Ch. 4 |
| Numerical dissipation | The oscillation becoming smaller than it should be because of calculation errors | Ch. 3, Ch. 6 |
| Symplectic (symplecticity, symplectic integrators) | The property (or a calculation method having the property) that advancing the calculation by one step does not change areas on the graph of position and velocity. The oscillation does not grow or shrink by itself, even in long calculations. See also the note below | Ch. 4 (Section 4.3.4), Ch. 6 |
| Area preservation (for one degree of freedom, the same as symplecticity); the case $b=1$ | The property that the area occupied by a set of points on the graph of position and velocity does not change. This is why the size of the oscillation neither grows nor shrinks | Ch. 4 (Section 4.3.4), Ch. 6 |
| Modified Hamiltonian (shadow Hamiltonian); in the "Magic of Sequences", $I = u_n^2 + u_{n-1}^2 - a u_n u_{n-1}$ | A quantity almost the same as the true energy, which is kept (almost) constant during the calculation | Ch. 4, Ch. 6 |
| Roots of the characteristic equation (poles of the transfer function) | Numbers that tell how much the value is multiplied and rotated in each step. If their absolute value is 1, the oscillation stays constant | Ch. 4, Ch. 5 |
| Autoregressive (AR) model | A model that predicts the next value from a weighted sum of past values | Ch. 4, Ch. 5 |

**About "symplectic" (a plain explanation)**: This may be the least familiar word in this repository. Consider a motion in which position and velocity change together as a pair, like the oscillation of a spring. On a graph with position on the horizontal axis and velocity on the vertical axis, consider a group of slightly different starting points, and advance them all by one step at the same time. A calculation method for which the area occupied by the group does not change is called "symplectic" (this is for the case of a single pair of position and velocity; when there are many pairs, the property is extended accordingly). With a method in which the area expands a little in every step (such as the forward Euler method), the oscillation keeps growing, and with a method in which the area shrinks a little, the oscillation gradually becomes smaller. With a method that keeps the area unchanged, the size of the oscillation neither grows nor shrinks, even after tens of thousands of steps. The coefficient $b$ of the "Magic of Sequences" is exactly the number that tells "by what factor the area is multiplied in each step", and $b=1$ is the symplectic case.

A more technical, detailed explanation using the determinant, and the derivation of the quantity $I$ that is exactly conserved during the calculation (the modified Hamiltonian), are given in Section 4.3.4 of [4_Magic_of_Sequence_Advanced_en.md](4_Magic_of_Sequence_Advanced_en.md).

## 1.6 License

The programming codes and instructional materials in this repository are provided under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

## 1.7 Author and Citation

**Hiroshi Ogasawara**
* Research Organization of Science and Technology (formerly College of Science and Engineering), Ritsumeikan University
*  [![ORCID](ORCID-0000--0002--8193--7174-A6CE39.svg)](https://orcid.org/0000-0002-8193-7174) ORCID: [https://orcid.org/0000-0002-8193-7174](https://orcid.org/0000-0002-8193-7174)

If you use or reference the program codes, instructional materials, or the web simulator in this GitHub repository, please cite it using the following persistent DOI issued by Zenodo:

[![DOI](zenodo.22250218.svg)](https://doi.org/10.5281/zenodo.22250218)  DOI: [https://doi.org/10.5281/zenodo.22250218](https://doi.org/10.5281/zenodo.22250218)

This persistent DOI automatically resolves to the latest version. 
**Note:** If you wish to cite or refer to other specific versions, please check the GitHub Releases page or the "Versions" section on Zenodo.

## References

`[1]`: [M.D. Caballero, T.O.B. Odden "Computing in physics education", Nature Physics **20** (2024) 339–341](https://doi.org/10.1038/s41567-023-02371-2) 

`[2]`: Examples of textbooks, prior studies, and public teaching materials for introductory computational physics: N. J. Giordano, H. Nakanishi, *Computational Physics*, 2nd ed. (Pearson, 2006) / H. Gould, J. Tobochnik, W. Christian, *An Introduction to Computer Simulation Methods*, 3rd ed. (Addison-Wesley, 2007) / [A. Cromer, "Stable solutions using the Euler approximation", *Am. J. Phys.* **49** (1981) 455–459](https://doi.org/10.1119/1.12478) / [A. Ogura, "Mechanics lessons using the leapfrog method" (in Japanese), *Journal of the Physics Education Society of Japan* **61**(1) (2013) 21–22](https://doi.org/10.20653/pesj.61.1_21) / [AAPT Undergraduate Curriculum Task Force (2016) AAPT Recommendations for Computational Physics in the Undergraduate Physics Curriculum](https://www.aapt.org/resources/upload/aapt_uctf_compphysreport_final_b.pdf) / [Ministry of Education, Culture, Sports, Science and Technology, Japan "Teaching Materials for High School Informatics Teachers 'Informatics I' (Chapter 3: Computers and Programming)" (2020) pp. 118-123](https://www.mext.go.jp/content/20200722-mxt_jogai02-100013300_005.pdf).
