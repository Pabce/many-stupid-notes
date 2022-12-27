---
{"dg-publish":true,"permalink":"/neutrino-nucleus/marley-and-the-nc-cross-section/"}
---

# MARLEY and the NC cross-section

MARLEY uses the following simplified differential cross-section expression for transitions to a given final nuclear state:

$$
\frac{d \sigma}{d \cos \theta_{\ell}}=\frac{G_F^2}{2 \pi} \mathcal{F}_{\mathrm{CC}}\left[\frac{E_i E_f}{s}\right] E_{\ell}\left|\mathbf{p}_{\ell}\right|\left[\left(1+\beta_{\ell} \cos \theta_{\ell}\right) B(\mathrm{F})+\left(1-\frac{1}{3} \beta_{\ell} \cos \theta_{\ell}\right) B(\mathrm{GT})\right]
$$

Where the $B(\mathrm{GT})$ and $B(\mathrm{F})$ form factors are the matrix elements of specific operators. For NC interactions, the form of these operators changes, but the overall expression remains the same.
This comes from boiling down the [Donelly-Walecka](https://journals.aps.org/prc/pdf/10.1103/PhysRevC.6.719) formalism of the low-energy neutrino-nucleus x-sections to the allowed approximation, which consists on taking the 0-momentum transfer limit and truncating the nuclear current operator to $0^{th}$ order in $1/m_N$ (slow nucleon limit).
[Steven Gardiner's thesis](https://lss.fnal.gov/archive/thesis/2000/fermilab-thesis-2018-37.pdf) covers this in detail.
Note that this approximation works well up to 20-30 MeV but starts failing above these energies -especially for the angular distribution-, as the contribution of forbidden transitions starts to become relevant (see [this paper](https://arxiv.org/pdf/1912.10714.pdf)).


The following papers have relevant information/calculations on the NC cross-section at low energies:
- [Reactions on 40Ar involving solar neutrinos and neutrinos from core-collapsing supernovae](https://journals.aps.org/prc/pdf/10.1103/PhysRevC.83.028801). This paper uses QRPA to calculate the total cross-section for CC and NC processes up to 80 MeV. They include multipole transitions up to $J^\pi = 4^\pm$, but include no angular distribution or form factors, so it's mostly useless for the generator.
- [Neutral-current neutrino cross section and expected supernova signals for 40Ar from a three-fold increase in the magnetic dipole strength](https://arxiv.org/pdf/2210.14316.pdf). This paper provides experimental data for the transition strengths to states around 10 MeV, which are relatable to the $B(\mathrm{GT})$ element. Then they do a shell-model calculation to estimate the cross-section for a large energy range, but again fail to provide the matrix elements. 
- Same goes for the paper referenced above...

There are no complete calculations available that cover the whole energy range of interest (~4 to 100 MeV) and provide the relevant form factors (either $B(\mathrm{GT})$ and $B(\mathrm{F})$, the ones used in the MARLEY cross-section (allowed and impulse) approximation, or more general ones). 
It should be relatively straightforward to get a first decent approximation on these form factors using a HF-QRPA method, which treats our region of interest (low lying excited states) correctly. GENIE has no available model with these characteristics:
- CRPA cannot deal with the discrete states (below ~10 MeV), which are the most relevant to us.
- Most (or all?) GENIE models don't event consider NC x-sections.

So we will do it ourselves. The nuclear many-body problem is a rich and interesting problem where there is much room to explore and improve.



