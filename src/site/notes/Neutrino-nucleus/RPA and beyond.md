---
{"dg-publish":true,"permalink":"/neutrino-nucleus/rpa-and-beyond/"}
---


# RPA and beyond
Hartree-Fock and all it's extensions (up to [[Neutrino-nucleus/HF-Bogoliubov\|HF-Bogoliubov]] in the most general quasiparticle formalism) are static, independent particle models. By a proper definition of (quasi)particles we can explain the basic properties of the ground states of many nuclei, and also some of their excited states. 
But there are many other excited states that cannot be reproduced by the above. These missing excitations will be explained by collective, many-body (coherent) correlations within the nucleus:
1. Their EM transition probabilities are one or two orders of magnitude larger than the single-particle transitions.
2. They show up in the spectra of different nuclei with great regularity. A good example is the giant dipole resonance.

This is treated in the context of the _residual interaction_, i.e., the difference between the full, many-body potential and the HF mean field. It will give an explanation of high-lying (resonances) and low lying (bound states) collective vibrations. 
These collective states arise mostly from the long-range part of the nuclear force, i.e., the _particle-hole_ pairing force.
{ #3e8187}


>[!note] Note:
>The **Tamm-Dancoff method** is a first approach to tackling the interaction between ph-pairs. It is superseded by RPA in several ways, mainly in that TD does not take into account these correlations for the ground state, which remains unmodified.

## RPA equations from linear response theory
This section is restricted to assuming we are working with a plain HF solution (no quasiparticle spice), but it can be adapted. We can find the RPA (Random Phase Approximation) equations by investigating the influence of a weak external time-dependent field:

$$
F(t) = F e^{-i\omega t} + F^\dagger e^{i \omega t}.
$$

With $F(t) = \sum_{kl} f_{kl}(t) a^\dagger_k a_l$ a one-body operator.
The nuclear density will oscillate with this external field, and we obtain resonances whenever $\omega$ is close to an excitation energy.

The WF of the nuclear system is no longer stationary, but a wavepacket. It's single body density is:

$$
\rho_{kl}(t) = \braket{\Phi(t) | a^\dagger_k a_l| \Phi(t)}
$$

Approximations used from now on:
1. We assume $\rho(t)$ corresponds to a Slater determinant at all time. So it obeys this e.o.m.:
    $$
    i \hbar \dot{\rho} = [h[\rho] + f(t), \rho]
    $$
    where $h$ is the single-particle HF field.
	
2. The external field is weak, so it introduces only small oscillations around the stationary density $\rho^{(0)}$. We can then write
    $$
    \rho(t) = \rho^{(0)} + \delta \rho(t)
    $$
    with $\delta \rho = \rho^{(1)} e^{ -i \omega t } + \rho^{(1)^{\dagger}} e^{ i \omega t }$.  Here $\rho^{(1)}$ is the density of the excited states.

We work in the HF basis, where $\rho^{(0)}$ is diagonal, meaning:
$$
\rho_{kl}^{(0)} = \delta_{kl} \rho_{k}^{(0)} =
    \begin{cases}
      0 & \text{for particles}\\ 
      1 & \text{for holes}
    \end{cases}
$$
In [[Neutrino-nucleus/Hartree-Fock\|Hartree-Fock]] we saw that the condition $\rho^{2}=\rho$ implies that the only non-vanishing elements of $\rho^{(1)}$ are _hp_ and _ph_ elements. 
We can now expand the e.o.m. to first order in $f$:
$$
i \hbar \delta \dot{\rho} = [h_{0}, \delta \rho] + \left[ \frac{\delta h}{\delta \rho} \cdot \delta \rho, \rho^{(0)} \right] + [f, \rho^{(0)}]
$$
(we have used some [[Neutrino-nucleus/Appendix#Commutator properties\|commutator algebra]] here). Using the properties of [[Neutrino-nucleus/Appendix#Densities of Slater determinants\|Slater determinant densities]] we see that the _pp_ and _hh_ components of the above equation vanish. We 

##  QRPA
This is the most complete way of treating harmonic perturbations, and can be used as a plug-in to [[Neutrino-nucleus/HF-Bogoliubov\|HFB]]