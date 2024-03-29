---
{"dg-publish":true,"permalink":"/personal-notes/paula-pitch/"}
---

# Paula pitch
## Problem statement
We would like to get a precise structure of the ground state and low lying energy states for a set of nuclei. This will allow us to get the form factors for neutrino interactions when the momentum transfer is low.

## Why do we have a problem?
I study the low energy regime neutrinos (below 100 MeV) in the DUNE experiment, in particular supernova neutrinos, but solar and atmospheric neutrinos also fall in this regime. 

One of the major sources of systematic uncertainty in the study of neutrinos at all energies is the understanding of the neutrino-nucleus interaction cross section. 
These uncertainties are especially large at low energies where experimental data is scarce, yet understanding and quantifying them is extremely important for the whole low energy physics program (supernova physics, supernova pointing, solar neutrinos, etc).

The current event generator used for low energy interactions in DUNE (MARLEY) has two major shortcomings:
- Missing interaction channels:
    - CC (charged current) antineutrino: $\bar{\nu}_e + {}^{40}\text{Ar} \rightarrow e^{+} + {}^{40}\text{Ca}^*$ reaction (odd-odd nucleus).
    - NC (neutral current): $\nu_x + {}^{40}\text{Ar} \rightarrow \nu_x + {}^{40}\text{Ar}^*$ reaction (even-even nucleus).
    
- Based on a simplified cross section model that starts failing at energies above 15-20 MeV. While the total cross section per energy it predicts (for the CC neutrino channel) is within the expected range, it gets the angular distribution and the transition rates to each individual excited nuclear state is wrong. This is important for several reasons:
    - The angular distribution, other than for the general study of the supernova physics, is very important for supernova pointing. DUNE will be part of the Supernova Early Warning System (SNEWS), where neutrino experiments alert telescopes around the world that a supernova is coming so they can point to the precise direction in the sky (as SN neutrinos arrive earlier than light).
    - Knowing the transition probability to a given nuclear state for a given neutrino energy is crucial to estimate its energy: each state has a specific deexcitation pattern and we rely on measuring the deexcitation products (mainly photons) to reconstruct the energy.
    
We need to expand the generator capabilities to design a more realistic low energy physics program.

## Workplan
I intend to work on improving the generator in two stages:
1. Implement the missing channels using the cross section model already in place.
2. Improve the cross section model.

Both these steps require **solving the nucleus**.

## Why do *I* need to solve the nucleus? And how?
1. Because I want to and I think it's an interesting problem.
2. There are several published calculations that give total cross section estimates for the missing channels. But this is useless for our generator as they do not compute the individual matrix elements that describe the transitions to each individual nuclear state. 
3. The generators used for oscillation energy simulations use more sophisticated models, but completely ignore the discrete region as it is uninteresting for them: the final state after a high energy neutrino scatters will always be unbound, and most of the time will come with one or more nucleon knockouts. In the low energy case, however, the region that accumulates most of the total cross section is where the energy transfer is low enough that the transition is from the nuclear ground state to a excited bound state. Tl;dr: existing generators are not suited for our problem.
4. There are already mean-field solvers ready to use, but most are not tailored to our needs and act like black boxes (bad experiences with black boxes in this collaboration...).

## Why tensor networks are promising
The usual way of solving the nucleus (other than pure ab-initio methods, which are another beast in themselves) is through incremental improvements of mean field theory:


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/neutrino-nucleus/mean-field-theory/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




# Mean field theory

```mermaid
    flowchart TD
        id1(No central field!)
        id2(Shell model)
        id3(Hartree-Fock)
        id4(HF-BCS)
        id5(HF-Bogoliuvob)
        id6(QRPA)
        id7(Brückner-HF)
        
        id1-->|Average phenomenological potential|id2
        id1-->|Self consistent field from a 2-particle potential|id3
        id3-->|"Add pairing (pp) correlations"|id4
        id4-->|Generalize pairing/HF with quasiparticles|id5
        id5-->|"Add long distance (ph) correlations"|id6
        id3-->|Density dependent forces|id7
        id7-.->id4
```

</div></div>


In brief summary: you solve for a mean field and then add residual interactions not accountable by this mean field. These can basically be divided into short distance "pairing" particle-particle (*pp*) correlations and long distance particle-hole (*ph*) correlations.
Adding these extra correlations are essential to describing the excited states of the nucleus (e.g., the vibrational states of the nucleus can only be accounted for by the *ph* correlations).

Some problems that this approach faces:
- HF-BCS and HF-Bogoliubov, that address the close range pairing nature of the nuclear force, explicitly break particle number conservation and other symmetries. Restoring them can be a huge pain.
- The most common method of including *ph* correlations (RPA and friends) provides a good correction for the ground state energy and qualitatively predicts the vibrational states well. However, it does embarrassingly badly at predicting the precise energy levels and the giant resonances in the continuum region. One of the reasons is that we only include 1p1h excitations. Including higher orders of excitations is ugly and expensive (search for boson expansion methods if you are interested).
- We usually only include a few levels above and below the Fermi surface, and expanding the configuration space comes with an exponential slowdown of calculations.

How the method in the tensor network paper (TNP) deals with them:
- The TNP Hamiltonian explicitly preserves all symmetries of the problem.
- Citing the paper: "we emphasize that the DMRG approach does not neglect any diagrams and does not rely on particle-hole excitation cutoffs." This is a huge deal for us.
- The TNP method seems to just destroy huge configuration spaces in a few minutes or seconds, which is also amazing.

Also, the TNP  Hamiltonian seems very flexible to expand. 
And it is a novel use case for tensor networks, as as far as I'm aware they haven't been used in this context outside this paper and a couple references. We will need to include different forces than the paper does and this makes it completely new. This is cool!

If you're wondering why the hell all these problems aren't addressed in the models our current neutrino generators use is because most of them are irrelevant for oscillation energy physics!


## What do I have to do, and what does Paula
The Hamiltonian used in the TNP is:
$$
H=\sum_j \epsilon_j\left(2 L_j^z+\Omega_j\right)-\sum_{j j^{\prime}} G_{j j^{\prime}} L_j^{+} L_{j^{\prime}}^{-}
$$
The "free parameters" are the $G_{jj'}$ coefficients, which roughly represent the interaction strengths between the different sites on the 1D lattice. Innocent enough as they seem, they are a nightmare to calculate, and that is my job. All the information about the potential between the nucleons is contained there.

Paula's job is to find a representation for the operators (MPO?) and implement the MPS/DMRG. All the operators are a linear combination of fermionic creation and destruction operators for different $j,m$ values.

There is a more sophisticated Hamiltonian in the paper (and it can get more sophisticated still), but the principle is exactly the same.