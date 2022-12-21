---
{"dg-publish":true,"permalink":"/neutrino-nucleus/appendix/"}
---

# Useful stuff
### Commutator properties
$[A,B+C]=[A,B] + [A,C]$
$[A+B,C]=[A,C] + [B,C]$
$[A,BC]=B[A,C] + [A,B]C$
$[AB,C]=A[B,C] + [A,C]B$

### Densities of Slater determinants
>[!tip] Theorem
>A wavefunction $\Psi(1\dots N)$ is a Slater determinant _iff_ it's density matrix $\rho_{\Psi}$ is a projector in the single-particle Hilbert space $\iff$ $\rho^{2}_{\Psi}=\rho_{\Psi}$.

> [!tip] Theorem (Baranger and Veneroni)
> Any density matrix $\rho$ that belongs to a Slater determinant $(\rho = \rho^{2})$ can be decomposed in the following way: 
> $$
> \rho = e^{ i \chi } \rho_{0} e^{ -i \chi }
> $$
> Where $\chi$ and $\rho_{0}$ are Hermitian matrices which are even under time reversal.

The above decomposition is unique if:
1. $\chi$ has only _ph_ and _hp_ matrix elements in the basis in which $\rho_{0}$ is diagonal:
    $$
    \rho_{0} \chi \rho_{0} = \sigma_{0}\chi \sigma_{0} = 0
    $$
    ($\sigma_{0} =1-\rho_{0}$ projects onto particle states.)

2. The eigenvalues of $\chi$ obey:
    $$
    -\frac{\pi}{4} \leq \chi_{\mu} < \frac{\pi}{4}
    $$
    We are not proving these theorems 🤫.

#### Some rules for calculating with Slater determinant densities
An arbitrary matrix A has the following "parts" in a basis in which $\rho$ is diagonal:
$$
A^{pp}=\sigma A \sigma; \qquad A^{hh}=\rho A \rho; \qquad A^{ph}=\sigma A \rho; \qquad A^{hp}=\rho A \sigma.
$$
The three following statements are equivalent:
$$
A=A \rho + \rho A \iff A = \sigma A + A \sigma \iff A^{pp} = A^{hh} =0.
$$

If two matrices $A$, $B$ obey $B=[A, \rho]$, then:
$$
A^{ph}=B^{ph}; \qquad A^{hp}=-B^{hp}; \qquad B^{pp} = B^{hh} =0.
$$
If $A^{pp}=A^{hh}=0$, then $A=[B, \rho]$. For Hermitian matrices $A$, $B$, with vanishing _pp_ and _hh_ elements, we can define these useful vectors:
$$
\begin{pmatrix} A \\ A^* \end{pmatrix} = \begin{pmatrix} A_{mi} \\ A^{*}_{mi} \end{pmatrix},
$$
and find:
$$
(A^* A)\begin{pmatrix} B \\ B^* \end{pmatrix} = \mathrm{Tr}(A \cdot B)
$$
$$
(A^* A)\begin{pmatrix} B \\ -B^* \end{pmatrix} = \mathrm{Tr}(A \cdot [B, \rho]).
$$



### Densities of HF-BCS and HFB states
zzz