---
{"dg-publish":true,"permalink":"/neutrino-nucleus/the-nuclear-many-body-problem/"}
---

# The nuclear many-body problem 🤯

A nucleus:

$$
^A X^Z_N
$$

$N=$ Neutron number
$Z=$ Proton number
$A=N+Z$

We would like to get a precise structure of the ground state and low lying energy states for a set of nuclei. This will allow us to get the form factors for neutrino interactions when the momentum transfer is low. In particular, we are interested in:
- $^{40} \text{K}^{21}_{19}$ for the CC  $\nu_e + {}^{40}\text{Ar} \rightarrow e^{-} + ^{40}\text{K}^*$ reaction (odd-odd nucleus).
- $^{40} \text{Ca}^{23}_{17}$ for the CC  $\bar{\nu}_e + {}^{40}\text{Ar} \rightarrow e^{+} + {}^{40}\text{Ca}^*$ reaction (odd-odd nucleus).
- $^{40} \text{Ar}^{22}_{18}$ for the NC  $\nu_x + {}^{40}\text{Ar} \rightarrow \nu_x + {}^{40}\text{Ar}^*$ reaction (even-even nucleus).

If I get into the nuclear deexcitation model we may need to look at others, but that would be way into the future.
 
There are mainly three (?) ways that this problem is approached.
- A **fermi gas** model or one of its variants (relativistic FG, local FG). They are quite useless at getting the accurate energy level structure, so they are not useful for our purposes.
- Some kind of **[[Neutrino-nucleus/Mean field theory\|mean field theory]]** approach, where you solve the Schrödinger equation for $A$ single particles moving in a mean field created by all the other particles, finding the ground state. This includes the Hartree-Fock method and many improvements:
    - A very relevant one for us is the inclusion of so-called _density dependent_ forces via the [[Neutrino-nucleus/The Brückner G-matrix\|Brückner G-matrix]] formalism (Brückner-HF).
    - To account for pairing (short distance, particle-particle) correlations, methods that include quasiparticles (HF-BCS, [[Neutrino-nucleus/HF-Bogoliubov\|HF-Bogoliubov]] or extensions that restore some of the broken symmetries) are used. 
    - On top of this you can add RPA (random phase approximation, see [[Neutrino-nucleus/RPA and beyond\|RPA and beyond]]) or some of its variants (QRPA, CRPA and extensions to these) to better account for long distance (particle-hole) correlations within the nucleus (helping explain vibrational states like giant resonances). This is particularly important for us as there are low-lying, collective states that cannot be accounted for in the independent particle model.
    - Sometimes it is necessary to project onto angular momentum and particle number in the above methods, as they can break these symmetries of the problem.

  Some references:
    - [This old book](http://hadron.physics.fsu.edu/~akbar/NuclearTextBook.pdf) has loads of information on these methods, just for reference.
    - [This course](https://wikihost.nscl.msu.edu/TalentDFT/doku.php?id=week1) seems excellent also.
    - [This paper](https://arxiv.org/pdf/1808.09138.pdf) using (relativistic) Brückner-HF seems to deal with asymmetric nuclei. This could be important. I think that what they present here is actually an ab-initio method! (why? I forgot)

- **Ab initio** calculations, where starting with "realistic" 2 and 3 body (NN, NNN) potentials, you attempt to solve for the full many-body Hamiltonian (this is not exactly true).
    - [This approach](https://aip.scitation.org/doi/pdf/10.1063/1.2932280) uses Quantum Monte Carlo (QMC): Variational MC (to find an upper bound of the energy by evaluating a trial wavefunction) followed by Green's Function MC (to project out the lowest energy ground state from the VMC). 
    [Here's another good paper](https://journals.aps.org/rmp/pdf/10.1103/RevModPhys.87.1067) covering the topic. And for further on, when you are working on the cross-section, [this paper](https://journals.aps.org/prx/pdf/10.1103/PhysRevX.10.031068) is worth checking out by how they also deal with the 2-body weak currents (see [[Neutrino-nucleus/MARLEY and the NC cross-section\|MARLEY and the NC cross-section]]).
    - [Other approaches](https://reader.elsevier.com/reader/sd/pii/S0375947498001468?token=5DDC10E00B1E6E8A1AA60B2FE7979D1CC9F40648B8EC53ED26B15EC42753AC1B782F5AC569B71B66ECE5F94FD65D69CD&originRegion=eu-west-1&originCreation=20221201085656) use "exact diagonalization" of the Hamiltonian. Maybe I can just use this? Apparently it is feasible already for $A=40$.
  - Expansion methods: Many body perturbation theory (MBPT), self-consistent Green function (SCGF), ...
  - Chiral effective field theory?

I have found many of these approaches only do the computations for even-even nuclei or just for magic number (2, 8, 20, 28... $p$ or $n$) nuclei. Even if they do do it for general nuclei, they just give results for certain properties like the different excitation energies, which is not enough. We need the actual wavefunctions to extract the form factors.

In any case, for our purposes we should use some form of HF-BCS/Bogoliubov with QRPA *or* an ab-initio method. The rest simply can't deal with the discrete states correctly.

## Tensor networks
As far as I can tell, it would be more interesting to use tensor networks for the *ab initio* method, as 
1. Mean field theory seems less restricted by computational resources, and more by theoretical uncertainties in the models.
2. Writing the many-body state in terms of a tensor network seems quite natural (see the references) and can reduce the computations by orders of magnitude (you know, MPS and that stuff).
3. This doesn't mean we won't need to deal with HF or its variants: it seems that an initial single-particle basis is needed in some cases.

### Some references I found
1. [Low-rank representations of nuclear interactions](https://archive.int.washington.edu/talks/WorkShops/int_21_1c/People/Tichai_A/Tichai.pdf). Talks about matrix decomposition in momentum space and "advanced tensor formats" for nuclear interactions (Presentation).
2. [This one is pretty crazy but take a look](https://archive.int.washington.edu/talks/WorkShops/int_21_1c/People/Hergert_H/Hergert.pdf) (Presentation).

**This is where the fun begins** 🔥
From here on is what I think we should use. But the previous two references are still worth checking out for context.

3. [The nuclear many-body problem for large, many-shell nuclei: An exact solution using tensor networks](https://arxiv.org/pdf/2105.07012.pdf). Here they use the density-matrix renormalization group (DMRG) to solve the pairing Hamiltonian exactly in the language of matrix-product states (MPS). They use a 1D chain. This one is pretty interesting. Q: is the pairing force they use in this paper only between proton-proton and neutron-neutron?.

	> "DMRG approach does not neglect any diagrams and does not rely on particle-hole excitation cutoffs as, e.g., in the configuration interaction approach".

5. [Symmetry reduction of tensor networks in many-body theory](https://arxiv.org/pdf/2002.05011.pdf). Paper 3 is ended by saying that including "shell model arbitrary terms" to increase the accuracy of the calculations is unfeasible, but that one avenue to do so is to exploit the rotational $SU(2)$ symmetry of the problem. This paper deals with this.
I'm still not sure whether we can use $SU(2)$ symmetry in nuclei with open shells (like ours), though. Maybe axial symmetry?
5. A problem cited in Paper 3 with this type of symmetry reduction is that, while it shrinks the Matrix Product Operator (MPO) bond dimension, it increases the size of the local basis ($D$). They suggest the need to optimise the choice of the local basis, something covered in [this paper](https://journals.aps.org/prl/pdf/10.1103/PhysRevLett.117.210402). Didn't follow it very well but the final results seem amazing. They also use DMRG and MPS! Also [this paper](https://arxiv.org/pdf/2008.08466.pdf) (still haven't read it in detail), which is much more recent. 
6. Who knows? I think we have more than enough to start with this.
