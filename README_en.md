# 1. Magic of Sequences: Open Educational Resources for Physics-Math-Computing via Simple Recurrence Relations
[｢数列のマジック｢｣ README 日本語版](README.md)

> While compiling this repository, I realized that the "Magic of Sequences" will also help **AI-generation students** develop their ability **to notice that even a slight numerical difference can result in a large physical difference**. I hope that the "Magic of Sequences" and this open resource will give readers a chance to recognize **the importance and appeal of physics** again.

## 1.1 Quick Start: Interactive Web App
Experience the "Magic of Sequences" right now in your browser!

* **[Launch the Interactive App (https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)**
* **Try this:** Pick (a,b) for $u_n = a \times u_{n-1} - b \times u_{n-2}$ with buttons  `(1.9999, 1)`, `(1.99, 1)`, `(1.99, 0.99)`, `(1.98, 0.99)`. Enjoy watching how the curves drastically transform from straight lines to oscillations and damping.
* **Then, enjoy observing drastic change even with subtle change in the above a or b by the slide bars! Adjust scale if needed.**

## 1.2 Project Overview & Educational Vision

This GitHub repository provides the programming codes and instructional materials for "Magic of Sequences," an open educational resource designed to seamlessly connect high school mathematics (recurrence relations) with foundational university-level physics, data science, digital signal processing, and AI technologies.
Modern STEM education, e.g., Caballero & Odden (2024, Nature Physics)`[1]` emphasizes the urgent need to strengthen student literacy in computational literacy for AI and data science. This GitHub repository provides an introductory curriculum that starts with a simple high school linear recurrence relation and connects it directly to core concepts in university physics (mechanics and wave theory), data science, digital signal processing (DSP), computer graphics (CG), and deep learning. It is designed so that students can learn without detailed mathematical explanations of the forward difference method (Euler method) `[2]`, which is frequently used in introductory computer education.

As Richard Feynman famously noted, *"What I cannot create, I do not understand."* In today's digital era, where generative AI can instantaneously output complex codes, providing students with the experience of building and evaluating models from the absolute ground up is critical. By writing their own loops and observing the accumulation of microscopic errors, students develop the "error-detecting objectivity" and design confidence required in the AI era.

While engaging in an extended dialogue with a generative AI for this project, I realized that reviewing the historical positioning of numerical analysis—specifically the forward difference and central difference methods—offers fascinating insights. It was a profound learning experience for me to trace how our predecessors, from the era of paper and pencil to modern computers, exercised their ingenuity under various constraints to reach where we are today. I have added these reflections to the repository. While the content might be challenging for incoming first-year students, I hope it serves as a valuable reference.

## 1.3 Repository Structure and Contents

This GitHub repository consists of the following interlinked components. Please refer to the respective files based on your computing environment and level of expertise.

* **[index_en.html](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)**: An interactive HTML application that allows users to adjust the coefficients of the finite difference equation directly in their browser. It enables visual exploration of how the numerical approximate solution behaves—transitioning from simple harmonic oscillation to damped oscillation and divergence.

* **[Magic_of_Sequence_MATLAB_en.mlx (with corresponding Python codes)](Magic_of_Sequence_MATLAB_en.mlx)**: This is the main MATLAB Live Script based on the materials used in the very first class of the first semester for first-year university students. It provides clear explanations, ranging from the "Magic of Sequences" to creating simple 1D and 2D wave propagation animations. Additionally, with the help of generative AI, we have newly added Python code for Google Colab, which can be run on mobile browsers. We also added an accuracy comparison with the fourth-order Runge-Kutta method (verifying energy-conserving properties) for undergraduate students in specialized courses.
Supposed readers include university students in the first week in the first semester and advanced high school students. It also provides an accessible explanation of how initial value problems correspond to "impulse responses" in digital signal processing. It provides detailed program explanations along with the simulation execution environment, and is directly linked with the MATLAB File Exchange. MATLAB 2022a or later is needed to enjoy this mlx file.

* **[3_Magic_of_Sequence_Plain_en.md](3_Magic_of_Sequence_Plain_en.md)**: A Markdown formatted text export of the MATLAB Live script with corresponding Python code and plain explanation, "Magic_of_Sequence_MATLAB_en.mlx", for readers not familiar with MATLAB. Except for the executability on MATLAB, the contents are identical to "Magic_of_Sequence_MATLAB_en.mlx". 

* **[4_Magic_of_Sequence_Advanced_en.md](4_Magic_of_Sequence_Advanced_en.md)**: A mathematically rigorous analytical document intended for second-year undergraduates and above. It covers pole placement analysis of transfer functions using characteristic equations, coefficient derivation via finite difference approximation, and system identification of AR models using the method of least squares.

* **[5_Magic_of_Sequence_Edu_Significance_en.md](5_Magic_of_Sequence_Edu_Significance_en.md)**: How does this magic connect to university topics? A tailored guide summarizing the educational value of this model for various audiences, ranging from high school students to university educators. It outlines the model's seamless connection to university physics curricula (mechanics, mathematical physics, wave theory) and its practical applications in digital image processing (spatial filters) and data science.

* **[6_Historical_Context_via_AI_en.md](6_Historical_Context_via_AI_en.md)**: A review of the historical positioning of the forward difference and central difference methods in numerical analysis. In compiling this with the help of generative AI, I strongly felt the necessity of conveying the fascination and importance of physical thinking to students who enter STEM programs without having selected physics in their university entrance exams.

The educational materials in this repository (such as index.html and Magic_of_Sequence_MATLAB.mlx) can also be used as a visual and intuitive introduction (an icebreaker) when teaching the concept of "Poles and Zeros" of characteristic equations in control engineering and signal processing. For advanced theoretical background on this topic, please refer to 4_Magic_of_Sequence_Advanced_en.md, and for its educational significance within the curriculum, refer to 5_Magic_of_Sequence_Edu_Significance_en.md and 6_Historical_Context_via_AI_en.md.

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
  │   Stormer-Verlet Method   │   Realistic game physics  │   Foundational math for AI
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

## 1.5 License

The programming codes and instructional materials in this repository are provided under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

## 1.6 Citation

If you use the programs, data, or instructional materials in this GitHub repository, please cite the following persistent DOI issued by Zenodo:
[Insert Zenodo DOI here]

## References

`[1]`: [M.D. Caballero, T.O.B. Odden "Computing in physics education", Nature Physics **20** (2024) 339–341](https://doi.org/10.1038/s41567-023-02371-2) 

`[2]`: Examples of prior research and public teaching materials: [F.Goldberg, S.Bendall, Am. J. Phys. 63 (1995) 978](https://doi.org/10.1119/1.18085). / [AAPT Undergraduate Curriculum Task Force (2016) AAPT Recommendations for Computational Physics in the Undergraduate Physics Curriculum](https://www.aapt.org/resources/upload/aapt_uctf_compphysreport_final_b.pdf) / [Ministry of Education, Culture, Sports, Science and Technology, Japan "Teaching Materials for High School Informatics Teachers 'Informatics I' (Chapter 3: Specialized Problem Solving and Programming)" (2019) pp. 118-123](https://www.mext.go.jp/content/20200722-mxt_jogai02-100013300_005.pdf).
