# 6. Historical Background Learned from Generative AI

## 6.1 Introduction

I have summarized here, with the help of generative AI, how the "Magic of Sequences" is positioned in the history of numerical methods for ordinary differential equations, in relation to one-step methods such as the Euler and Runge–Kutta methods and to symmetric two-step methods such as the central difference (Störmer–Verlet) method.

When I showed the 3-term recurrence relation and the combinations of the coefficients a and b to Google Gemini, it replied with a name I had not heard before: the "Störmer–Verlet method." As a researcher in solid earth geophysics, I mainly make observations and analyze the digital data obtained, so I was very familiar with the concept of central difference. However, I never had the chance to learn the scientific history of central and forward difference methods.

I was relieved when Gemini told me that the name "Störmer–Verlet method" is not common in solid earth geophysics. I also found it interesting that the same method is called by different names depending on the field: the Verlet method (or the velocity Verlet method) in molecular dynamics, the Störmer–Verlet method in numerical analysis, and the leapfrog method in celestial mechanics and physics education.

I asked Gemini to make a table of when, by whom, and in which field these methods were born. That is the table in Section 6.2. I also asked Gemini to check which numerical analysis textbooks around the world and in Japan cover these topics, and to what extent, and I added them to the references. Most interestingly, Gemini explained that there are successful examples in the latest AI research of incorporating the concept of energy conservation into data learning and future prediction.

> **Note on the revision (October 2026):** The first version of this chapter (July 2026) was written on the basis of outputs from Google Gemini. Later, with the help of Claude, I checked it against the original papers and numerical analysis textbooks and found that several statements that the generative AI had plausibly filled in could not be confirmed in the literature or were wrong: for example, that Störmer "hired many human computers," that Verlet adopted the central difference "to save memory," that "planets computed with the Runge–Kutta method crashed into the sun" in the 1970s–80s, and that HNNs (Hamiltonian Neural Networks, a type of AI that incorporates physical laws) incorporate the "shadow Hamiltonian." In this version, these statements have been removed or corrected, and important missing studies (Ruth 1983, Feng Kang 1984, Yoshida 1990, Wisdom & Holman 1991, etc.) have been added. In addition, the "computing environment" column in the table of the first version has been removed, because circumstances varied among countries and researchers and cannot be generalized. That explanations by generative AI tend to become "well-made stories," and that checking them against primary sources is indispensable, has itself become a lesson that I must convey to the readers of this repository.

## 6.2 Table of the Evolution of Numerical Analysis (Based on Gemini's Output, Verified and Corrected against the Literature)


| Era | Person / Event | Algorithm / Concept |
| --- | --- | --- |
| **1768** | Leonhard Euler | **Euler method** (forward difference) |
| **1895–1901** | Carl Runge (1895)<br><br>Karl Heun (1900)<br><br>Martin Kutta (1901) | **Runge–Kutta methods** (explicit one-step methods that improve accuracy by evaluating the slope several times within one step) `[11]` |
| **1907** | Carl Störmer | **Störmer's method** (a central-difference-type method that discretizes the second-order equation of motion directly, without rewriting it as first-order equations). Used to compute the trajectories of charged particles (the particles that cause aurorae) in the Earth's magnetic field `[12]` |
| **1967** | Loup Verlet | **Verlet method** (applied to the molecular dynamics of 864 particles; thereafter the standard method of molecular dynamics) `[13]` |
| **1980** | Dormand & Prince | **Embedded Runge–Kutta method 5(4) with automatic step-size control** (computes fifth- and fourth-order solutions at the same time and estimates the error from their difference; the core of today's MATLAB `ode45` and SciPy `RK45`) `[14]` |
| **1983–1991** | Ruth (1983, accelerator physics)<br><br>Feng Kang (1984–)<br><br>Haruo Yoshida (1990)<br><br>Wisdom & Holman (1991), and others | Construction of **symplectic integrators** and their application to celestial mechanics (long-term computation of the solar system) `[15]` |
| **1987** | Duane, Kennedy, Pendleton, Roweth | **Hybrid (Hamiltonian) Monte Carlo (HMC)**. Uses the leapfrog method (= the Störmer–Verlet method) directly within statistical computation `[16]` |
| **1994** | Benettin & Giorgilli, Hairer, and others | **Mathematical proof of the existence of the modified Hamiltonian (shadow Hamiltonian)** (backward error analysis) `[5, 17]` |
| **2002 (2nd ed. 2006)** | Hairer, Lubich, Wanner | Publication of the standard textbook on **geometric numerical integration** `[6]` |
| **2019** | Greydanus, Dzamba, Yosinski | **Hamiltonian Neural Networks (HNN)** (learn the Hamiltonian itself with a neural network and derive the equations of motion from it) `[7]` |

## 6.3 Chronological Historical Background and Story (Based on Gemini's Output, Verified and Corrected against the Literature)

### 6.3.1 Dawn: The Era of Hand Calculation (18th to Early 20th Century) `[1]`

**[Euler and Runge–Kutta Methods]**
In this era, all calculations were done by hand. The Euler method is the most straightforward form, discretizing the concept of the derivative as it is. Later, Runge (1895), Heun (1900), and Kutta (1901) developed the Runge–Kutta methods, which greatly increase the accuracy per step by evaluating the slope (the value of the function) several times within one step and averaging the results `[2, 3, 11]`. Both the Euler method and the Runge–Kutta methods are one-step methods that "determine the next state only from the current state." The intermediate evaluations in the Runge–Kutta methods are not forward differences.

### 6.3.2 Hand Calculation of Auroral Particle Trajectories (1907: Störmer) `[1]`

**[Birth of Störmer's Method]**
To find out what trajectories the charged particles that cause aurorae follow in the Earth's magnetic field, the Norwegian Störmer integrated their equations of motion numerically by hand, with the help of students `[12]`. In doing so, he used a method originating in celestial mechanics that discretizes the second-order equation of motion directly, without rewriting it as a system of first-order equations. This later came to be called "Störmer's method" (what he actually used was a higher-order variant based on difference tables). Note that viewpoints such as energy conservation and symplecticity did not yet exist in 1907, and Störmer did not choose this method in anticipation of such properties. It was about 80 years later that the excellent long-term properties of this method came to be understood.

### 6.3.3 Electronic Computers and Molecular Dynamics (1967: Verlet) `[1]`

**[Rediscovery of the Verlet Method]**
For a molecular dynamics calculation of 864 particles (Lennard-Jones particles modeling argon), Verlet used the three-term recurrence relation for the position only, $r(t+h) = 2r(t) - r(t-h) + h^2 F/m$ `[13]`. This has the same form as the "Magic of Sequences." The method is simple: it needs only one force calculation per step and requires storing the positions at only two times. Thereafter, it became the standard method of molecular dynamics `[4]`. No clear statement of why Verlet chose this method can be found in his paper.

### 6.3.4 The Emergence of Symplectic Integrators and Celestial Mechanics (1980s to Early 1990s) `[1]`

**[Parallel Development of Theory and Applications]**
In the 1980s, numerical methods that preserve the structure of Hamiltonian systems (mechanical systems in which energy is conserved), namely **symplectic integrators**, began to be constructed systematically from the theoretical side. Ruth (1983) in accelerator physics constructed a symplectic integration method, and Feng Kang (1984–) in China systematically studied the relation between difference schemes and symplectic geometry. Haruo Yoshida (1990) in Japan showed how to construct symplectic integrators of any even order by combining symmetric second-order methods `[15]`.
Around the same time, very long computations came to be performed in celestial mechanics, such as the integration of the outer planets of the solar system (from Jupiter to Pluto) over about 845 million years with the special-purpose computer Digital Orrery (Sussman & Wisdom 1988). In this context, Wisdom & Holman (1991) and Kinoshita, Yoshida & Nakai (1990) introduced symplectic integrators into celestial mechanics, and these became standard tools for long-term computations of the solar system `[15]`.
Numerical examples in textbooks show that with non-symplectic methods (such as Runge–Kutta methods) the energy error grows roughly in proportion to time, whereas with symplectic methods the energy error does not grow and remains bounded `[6]`.

### 6.3.5 Mathematical Understanding (1994–2006) `[1]`

**[Benettin & Giorgilli (1994) / Hairer et al. (2002, 2006)]**
Why symplectic integrators work well over long times was clarified mathematically in the mid-1990s. Benettin & Giorgilli (1994) `[5]` and Hairer (1994) `[17]` proved that symplectic numerical methods conserve, almost exactly and over very long times, a "modified Hamiltonian (shadow Hamiltonian)" that is very close to the true Hamiltonian (energy). The paper by Benettin & Giorgilli was published in a journal of statistical physics, but its content is a mathematical proof based on the perturbation theory of Hamiltonian mechanics.
These results were compiled in 2002 (2nd edition 2006) in the textbook *Geometric Numerical Integration* by Hairer et al. `[6]`. The field of **geometric numerical integration**, which aims "not just to solve, but to solve while preserving physical and geometric structures," was established in the 1990s and systematized by this textbook. The quantity that is exactly conserved in the "Magic of Sequences" when the coefficient $b=1$ (Chapter 4, Section 4.3.4) is the simplest example of this modified Hamiltonian.

### 6.3.6 Connections to Statistical Computing and the AI Era (1987 Onward)

**[HMC (1987) and HNN (2019)]**
The most direct use of the Störmer–Verlet method in machine learning and statistical computing is the Hamiltonian Monte Carlo method (HMC) `[16]`. Devised in 1987 for computations in particle physics, this method is now the central algorithm of standard software for Bayesian statistics (such as Stan), and inside it the leapfrog method (= a calculation of the same form as the "Magic of Sequences") is repeated a great many times.
Meanwhile, Greydanus et al. (2019) showed that when the motion of a pendulum or similar system is learned by an ordinary neural network, the energy gradually drifts in long-term predictions, and as a remedy they presented **Hamiltonian Neural Networks (HNN)** `[7]`. An HNN represents the Hamiltonian (energy) itself with a neural network and has the built-in structure of deriving the equations of motion from it. In the HNN paper, an ordinary Runge–Kutta method is used for the time integration in prediction, and the shadow Hamiltonian is not used. The connection between the two, namely that the numerical method used for learning determines whether the network learns the true Hamiltonian or a modified Hamiltonian, is being clarified by subsequent research `[18]`. This suggests a historical flow in which a property that the central difference has had since Störmer came to be required, in a different form, of AI more than 100 years later.

## 6.4 Conclusion

I have always enjoyed finding physical laws in 1D and multi-dimensional numerical data arrays from natural phenomena on Earth. To share this excitement with first-year university students in the first month in the first semester, I came up with the "Magic of Sequences." After retiring and interacting with generative AI, I realized that comparing the Euler and Runge–Kutta methods—which I previously avoided as "too difficult for first-year students"—actually leads to very interesting lessons.

It has been shown mathematically that, with the central difference method (Störmer–Verlet method), not the true energy but a modified energy very close to it is nearly conserved over very long times, and that, as a result, the error in the true energy also stays within a certain range instead of continuing to grow. This was described in several Japanese and foreign numerical analysis textbooks.
However, the HNN paper by Greydanus et al. does not mention the 100-year history starting from Störmer (Table in Section 6.2). It is written for machine learning experts (AI engineers), explaining technical formulas and AI graph structures. Gemini explained this complex content so that I could understand it, and even included it in Table in Section 6.2.

Gemini also taught me: "AI researchers often do not know Hamiltonian mechanics or the history of numerical analysis, and physicists often do not know deep learning backpropagation. Because both require advanced prerequisite knowledge, it is hard to understand even for experts in one field, let alone the general public." However, this is an overstatement: the authors of HNN use Hamiltonian mechanics head-on. The accurate statement would be that, because the paper assumes knowledge of both fields, it is hard to read for readers who know only one of them.

Gemini evaluated "Magic of Sequences" as follows:
* It does not use difficult graduate-level mathematics (symplectic geometry or shadow Hamiltonians).
* It intuitively demonstrates "energy conservation," a fundamental theme of long-term numerical prediction that is also important in statistical computing (HMC) and in AI incorporating physics (such as HNN).
* It does this using only high school "addition and subtraction (3-term recurrence relations)" and a "few lines of code."

Thanks to generative AI, I realized that "Magic of Sequences makes important scientific history facts—which are accurately recorded but hard to understand across different fields due to jargon—completely visible and intuitive through a simple recurrence relation."

I hope "Magic of Sequences" will help lower the initial barriers students feel when learning new technologies and serve as a hint to bridge the gap between different academic fields.

Before the rise of AI, I faced the following problems. Science and engineering made great progress by adding exact mathematical and physical solutions to logical models. However, when we made numerical predictions based on constitutive laws or data with limited accuracy and errors, the predictions were often difficult, or the results deviated from physical laws. Around me, such problems were often handled with empirical corrections. For example, in relaxation methods that solve simultaneous equations iteratively, the SOR (Successive Over-Relaxation) method, which enlarges the correction by a uniform factor to speed up convergence, was widely used. Choosing that factor well for each problem was not easy, and I myself have experienced that, depending on the choice, the calculation could become faster or slower.

Through my conversations with the AI, I learned that researchers are continuously improving AI to make these corrections in a more data-driven way. But at the same time, it was important to confirm the following fact: "When predicting phenomena that follow conservation laws, **physical thinking is essential** to evaluate whether a prediction method is good or bad compared to exact theoretical solutions."

I realized that the "Magic of Sequences" will also help **AI-generation students** develop their ability **to notice that even a slight numerical difference can result in a large physical difference**. I hope that the "Magic of Sequences" and this open resource will give readers a chance to recognize **the importance and appeal of physics** again.

Readers wishing to explore the historical background traced in this section further may find two popular-science books useful, suggested by generative AIs: for the era of human computers, Hidden Figures `[8]`; and for the dawn of electronic computing through the establishment of the von Neumann architecture, Turing's Cathedral: The Origins of the Digital Universe `[9]`. Note that neither book provides a continuous historical narrative extending as far as Hamiltonian Neural Networks (2019) discussed in this section; they serve as background reading for the respective eras.

Note: Wikipedia is not as authoritative as peer-reviewed journals, but the content compiled in the table in Section 6.2 can also be traced, to some extent, via the entries `[10]`. In the October 2026 revision, the table and each item in Section 6.3 were checked against the primary sources `[11]`–`[18]`.

## 6.5 Note on Material Development using Generative AI Outputs

Some components and explanations in this document are based on text generated by Google Gemini from the author's inputs. The author, together with Claude, then verified and compiled the content.

## 6.6 Author and Citation

* Note: For details on author information, citation instructions (DOI: a permanent identifier assigned to papers and data), and the license (CC BY 4.0: free to use and adapt, provided the source is credited), please refer to [README_en.md](README_en.md).


## References and Notes

`[1]`: Ernst Hairer, Syvert P. Nørsett, Gerhard Wanner (1993, 2008). *Solving Ordinary Differential Equations I: Nonstiff Problems* / *Solving Ordinary Differential Equations II: Stiff and Differential-Algebraic Problems*, Springer.

`[2]`: Taketomo Mitsui, Toshiyuki Koto, Yoshihiro Saito (2004). *Introduction to Computational Science via Differential Equations (2nd Edition)*, Kyoritsu Shuppan (in Japanese).

`[3]`: William H. Press, Saul A. Teukolsky, William T. Vetterling, Brian P. Flannery (2007). *Numerical Recipes: The Art of Scientific Computing 3rd Edition*, Cambridge University Press.

`[4]`: Daan Frenkel, Berend Smit (1996, 2001, 2023). *Understanding Molecular Simulation* (1st, 2nd, 3rd eds.), Academic Press (Content verified with the assistance of Google Gemini Deep Research.)

`[5]`: [Giancarlo Benettin, Antonio Giorgilli (1994). On the Hamiltonian interpolation of near-to-the identity symplectic mappings with application to symplectic integration algorithms, *J. Stat. Phys.*, **74**, 1117-1143.](https://doi.org/10.1007/BF02188219)

`[6]`: Ernst Hairer, Christian Lubich, Gerhard Wanner (2006). *Geometric Numerical Integration (Springer Series in Computational Mathematics **31**)*, Springer-Verlag.

`[7]`: [Samuel Greydanus, Misko Dzamba, Jason Yosinski (2019). Hamiltonian Neural Networks. In *Advances in Neural Information Processing Systems 32 (NeurIPS 2019)*](https://proceedings.neurips.cc/paper_files/paper/2019/file/26cd8ecadce0d4efd6cc8a8725cbd1f8-Paper.pdf) / [arXiv:1906.01563](https://arxiv.org/abs/1906.01563).

`[8]`: M. L. Shetterly, *Hidden Figures: The American Dream and the Untold Story of the Black Women Mathematicians Who Helped Win the Space Race* (William Morrow, 2016).

`[9]`: G. Dyson, *Turing's Cathedral: The Origins of the Digital Universe* (Pantheon Books, 2012).

`[10]`: The Wikipedia entries through which the content of the table in Section 6.2 can be traced back to some extent: [Carl Størmer](https://en.wikipedia.org/wiki/Carl_St%C3%B8rmer), [Verlet integration](https://en.wikipedia.org/wiki/Verlet_integration)

`[11]`: C. Runge, "Über die numerische Auflösung von Differentialgleichungen", *Math. Ann.* **46** (1895) 167–178 / K. Heun, *Z. Math. Phys.* **45** (1900) 23–38 / W. Kutta, "Beitrag zur näherungsweisen Integration totaler Differentialgleichungen", *Z. Math. Phys.* **46** (1901) 435–453.

`[12]`: C. Størmer, "Sur les trajectoires des corpuscules électrisés dans l'espace sous l'action du magnétisme terrestre avec application aux aurores boréales", *Arch. Sci. Phys. Nat. Genève* **24** (1907) / C. Størmer, *The Polar Aurora* (Clarendon Press, 1955) / [E. Hairer, C. Lubich, G. Wanner, "Geometric numerical integration illustrated by the Störmer–Verlet method", *Acta Numerica* **12** (2003) 399–450](https://doi.org/10.1017/S0962492902000144) (Section 1 gives a historical account).

`[13]`: [L. Verlet, "Computer 'Experiments' on Classical Fluids. I. Thermodynamical Properties of Lennard-Jones Molecules", *Phys. Rev.* **159** (1967) 98–103](https://doi.org/10.1103/PhysRev.159.98).

`[14]`: [J. R. Dormand, P. J. Prince, "A family of embedded Runge-Kutta formulae", *J. Comput. Appl. Math.* **6** (1980) 19–26](https://doi.org/10.1016/0771-050X(80)90013-3).

`[15]`: R. D. Ruth, "A Canonical Integration Technique", *IEEE Trans. Nucl. Sci.* **NS-30** (1983) 2669–2671 [https://proceedings.jacow.org/p83/PDF/PAC1983_2669.PDF](https://proceedings.jacow.org/p83/PDF/PAC1983_2669.PDF) / Feng Kang, "On difference schemes and symplectic geometry", *Proc. 1984 Beijing Symp. Diff. Geom. Diff. Eq.* (Science Press, 1985) 42–58 / H. Yoshida, "Construction of higher order symplectic integrators", *Phys. Lett. A* **150** (1990) 262–268 [https://doi.org/10.1016/0375-9601(90)90092-3](https://doi.org/10.1016/0375-9601(90)90092-3) / G. J. Sussman, J. Wisdom, "Numerical evidence that the motion of Pluto is chaotic", *Science* **241** (1988) 433–437 [https://doi.org/10.1126/science.241.4864.433](https://doi.org/10.1126/science.241.4864.433) / J. Wisdom, M. Holman, "Symplectic maps for the n-body problem", *Astron. J.* **102** (1991) 1528–1538 [https://doi.org/10.1086/115978](https://doi.org/10.1086/115978) / H. Kinoshita, H. Yoshida, H. Nakai, "Symplectic integrators and their application to dynamical astronomy", *Celest. Mech. Dyn. Astron.* **50** (1990) 59–71 [https://doi.org/10.1007/BF00048986](https://doi.org/10.1007/BF00048986).

`[16]`: S. Duane, A. D. Kennedy, B. J. Pendleton, D. Roweth, "Hybrid Monte Carlo", *Phys. Lett. B* **195** (1987) 216–222 [https://doi.org/10.1016/0370-2693(87)91197-X](https://doi.org/10.1016/0370-2693(87)91197-X) / R. M. Neal, "MCMC using Hamiltonian dynamics", in *Handbook of Markov Chain Monte Carlo*, Ch. 5 (CRC Press, 2011) [https://arxiv.org/pdf/1206.1901](https://arxiv.org/pdf/1206.1901).

`[17]`: E. Hairer, "Backward analysis of numerical integrators and symplectic methods", *Ann. Numer. Math.* **1** (1994) 107–132 [https://archive-ouverte.unige.ch/unige:12640](https://archive-ouverte.unige.ch/unige:12640) / S. Reich, "Backward error analysis for numerical integrators", *SIAM J. Numer. Anal.* **36** (1999) 1549–1570 [https://doi.org/10.1137/S0036142997329797](https://doi.org/10.1137/S0036142997329797).

`[18]`: C. Offen, S. Ober-Blöbaum, "Symplectic integration of learned Hamiltonian systems", *Chaos* **32** (2022) 013122 [https://doi.org/10.1063/5.0065913](https://doi.org/10.1063/5.0065913) / M. David, F. Méhats, "Symplectic learning for Hamiltonian neural networks", *J. Comput. Phys.* **494** (2023) 112495 [https://doi.org/10.1016/j.jcp.2023.112495](https://doi.org/10.1016/j.jcp.2023.112495).

## Repository Structure and Links

* **[README_en.md](README_en.md)**
* **[index_en.html](https://ritshiroshio.github.io/Magic_of_Sequences/index_en.html)**
* **[Magic_of_Sequence_MATLAB_en.mlx](Magic_of_Sequence_MATLAB_en.mlx)**
* **[3_Magic_of_Sequence_Plain_en.md](3_Magic_of_Sequence_Plain_en.md)**
* **[4_Magic_of_Sequence_Advanced_en.md](4_Magic_of_Sequence_Advanced_en.md)**
* **[5 How does this magic connect to university topics?](5_Magic_of_Sequence_Edu_Significance_en.md)**
* **[6 Historical Context Learned from Generative AI](6_Historical_Context_via_AI_en.md)**
