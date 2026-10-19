<div align="center">

  <h1>Ground State of the Deuteron</h1>
  <p><strong>Variational Solution in a 3D Harmonic Oscillator Basis with the Minnesota Potential</strong></p>

  <p>
    <img src="https://img.shields.io/badge/Physics-Nuclear%20Physics-blue?style=for-the-badge" alt="Physics" />
    <img src="https://img.shields.io/badge/Method-Harmonic%20Oscillator%20Expansion-orange?style=for-the-badge" alt="Method" />
    <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
    <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License" />
  </p>

  <p>
    <a href="#-theoretical-background">Theory</a> •
    <a href="#-spin-isospin-decomposition">Spin-Isospin</a> •
    <a href="#-matrix-elements">Matrix Elements</a> •
    <a href="#-quick-start">Quick Start</a> •
    <a href="#-numerical-results">Results</a> •
    <a href="#-project-structure">Structure</a>
  </p>

</div>

---

## 📖 Theoretical Background

The deuteron ($^2\text{H}$) is a bound state of a proton and a neutron ($A=2$). In the center-of-mass frame and within the **$s$-wave approximation** ($L=0$), the relative wave function factorizes into a spatial radial component and a spin-isospin component:

$$\Psi(\vec{r}, \sigma_1, \tau_1, \sigma_2, \tau_2) = \sum_{n=0}^{M-1} \sum_{j \in \{A,B,C,D\}} c_{nj} R_n(r) \Phi_j(\sigma_1, \tau_1, \sigma_2, \tau_2)$$

Because the $s$-wave spatial wave function is symmetric under particle exchange ($\vec{r} \to -\vec{r}$), the generalized Pauli exclusion principle requires the spin-isospin state to be **strictly antisymmetric** under $p \leftrightarrow n$ exchange.

---

## 🧮 Formalism & Key Derivations

### 1. Radial Basis Functions & Normalization
The radial basis functions are chosen as 3D isotropic harmonic oscillator states ($L=0$):

$$R_n(r) = N_n(\nu) \frac{e^{-\nu r^2}}{r} H_{2n+1}\left(\sqrt{2\nu} r\right)$$

where $\nu = \frac{\mu \omega}{2\hbar}$, $\mu = \frac{m_N}{2}$ is the reduced mass, and $H_k(x)$ are Hermite polynomials.

Using the substitution $x = \sqrt{2\nu}r$ and the Hermite orthogonality relation $\int_{-\infty}^\infty e^{-x^2} H_m(x) H_n(x) \, dx = \sqrt{\pi} 2^n n! \delta_{mn}$, the normalization condition $\int_0^\infty r^2 |R_n(r)|^2 dr = 1$ yields:

$$N_n(\nu) = \left[ \frac{\sqrt{2\nu / \pi}}{2^{2n} (2n+1)!} \right]^{1/2}$$

---

### 2. Spin-Isospin Decomposition
The antisymmetric spin-isospin subspace is spanned by 4 basis vectors:

$$
\begin{aligned}
|\Phi_A\rangle &= \frac{1}{\sqrt{2}} \left( |\!\uparrow\uparrow\uparrow\downarrow\rangle - |\!\uparrow\downarrow\uparrow\uparrow\rangle \right) \quad &(S=1, T=0, M_S=+1, M_T=0) \\
|\Phi_B\rangle &= \frac{1}{\sqrt{2}} \left( |\!\uparrow\uparrow\downarrow\downarrow\rangle - |\!\downarrow\downarrow\uparrow\uparrow\rangle \right) \quad &(S=1, T=0, M_S=0, M_T=0) \\
|\Phi_C\rangle &= \frac{1}{\sqrt{2}} \left( |\!\downarrow\uparrow\downarrow\downarrow\rangle - |\!\downarrow\downarrow\downarrow\uparrow\rangle \right) \quad &(S=1, T=0, M_S=-1, M_T=0) \\
|\Phi_D\rangle &= \frac{1}{\sqrt{2}} \left( |\!\downarrow\uparrow\uparrow\downarrow\rangle - |\!\uparrow\downarrow\downarrow\uparrow\rangle \right) \quad &(S=0, T=1, M_S=0, M_T=0)
\end{aligned}
$$

Acting with the spin exchange operator $\hat{P}_\sigma$:
- **States A, B, C (Triplet $S=1$, Isospin Singlet $T=0$):** $\hat{P}_\sigma |\Phi_{A,B,C}\rangle = +1 |\Phi_{A,B,C}\rangle \implies \hat{V} = V_R(r) + V_t(r)$
- **State D (Singlet $S=0$, Isospin Triplet $T=1$):** $\hat{P}_\sigma |\Phi_D\rangle = -1 |\Phi_D\rangle \implies \hat{V} = V_R(r) + V_s(r)$

The Hamiltonian is **block-diagonal** in this basis. The physical deuteron ground state lives strictly in the **spin-triplet / isospin-singlet ($S=1, T=0$)** sector.

---

### 3. Matrix Elements

The total Hamiltonian is given by $\hat{H} = -\frac{\hbar^2}{2\mu}\nabla^2 + \hat{V}(r)$:

1. **Kinetic Energy:** Evaluated analytically using the recurrence and derivative relations for Hermite polynomials:
   $$H'_n(x) = 2n H_{n-1}(x)$$
2. **Potential Energy (Minnesota Potential):**
   $$\hat{V} = V_R(r) + \frac{1 + \hat{P}_\sigma}{2} V_t(r) + \frac{1 - \hat{P}_\sigma}{2} V_s(r), \quad V_i(r) = \pm v_{0,i} e^{-k_i r^2}$$
   Matrix elements are integrated using high-order **Gauss-Hermite quadrature** (exact to machine precision) or by analytic Gaussian expansion.

---
> **Conclusion:** 
> - **Converged Ground State Energy:** $E_0 \approx -2.225 \text{ MeV}$ (consistent with empirical deuteron binding energy $E_B \approx 2.2246\text{ MeV}$).
> - **Quantum Numbers:** Total spin **$S = 1$**, total isospin **$T = 0$**.
> - **Stability:** Independence of basis size cutoff $M \ge 15$ across widely varying $\nu$.

---
