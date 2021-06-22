---
title: Entanglement detection in quantum fields
date: 2021-05-05T17:10:47.648Z
summary: A brief summary of our research into the detection of entanglement in quantum fields.
draft: false
featured: false
links: []

authors:
- stockdale

projects:
- entanglement
---
Entanglement is an inherently quantum phenomenon with no classical counterpart. It has baffled Einstein, Heisenberg, and nearly every physicist since.

At its most fundamental level, entanglement means that a combined description of many subsystems cannot be written as a product of the subsystems. This is best demonstrated with an example. 

Consider two spin-$\frac{1}{2}$ particles, such as two electrons, where their total spin is zero. That is, if one were to measure the spin of particle A to be spin up, we know the second (without even measuring it) would be in the spin down state. The wave function of the combined system would then be

$$|\psi\rangle_{AB} = \frac{1}{\sqrt{2}}\left[|\hspace{-0.1cm}\uparrow\rangle_A|\hspace{-0.1cm}\downarrow\rangle_B + |\hspace{-0.1cm}\downarrow\rangle_A|\hspace{-0.1cm}\uparrow\rangle_B\right].$$

This system is entangled as the state is not separable, i.e., $|\psi\rangle\_{AB} \neq |\psi\rangle\_{A}\otimes|\psi\rangle_{B}$. In this example, the measurement of the spins are perfectly (anti-)correlated.

### **Why bother studying entanglement?**

The study of entanglement is a popular research topic within the physics community for many reasons. In terms of practical uses, it has gained significant interest within quantum information theory. Entanglement is a crucial resource for quantum computing, quantum communication, and quantum key distribution ­− all of which are promising future technologies that are widely believed to advance and outperform our current capabilities.

Beyond its practical uses, entanglement has attracted interest at a fundamental physics level. It's thought to provide insight into areas such as statistical mechanics and quantum field theory (see, e.g., Amico *et al.,* [Rev. Mod. Phys. **80**, 517 (2008)](https://doi.org/10.1103/RevModPhys.80.517) for a comprehensive review).

### **Into the many-body regime**

For the simple two-particle system discussed above, determining whether it is entangled is relatively straightforward and there are many methods for witnessing the entanglement. However, in the many-body limit, where there are tens of thousands of particles, detecting entanglement becomes increasingly difficult. One method that has been identified as a promising witness is entropic uncertainty relations (see, e.g., Coles *et al.,* [Rev. Mod. Phys. **89**, 015002 (2017)](https://doi.org/10.1103/RevModPhys.89.015002) for a review).

Closely related to Heisenberg's uncertainty principle, the entropy we measure in a system is bounded from below. Consider a system with two observables $\hat{X}$ and $\hat{Z}$. For a finite-dimensional system, the entropic uncertainty relation is

$$H(\hat{X}) + H(\hat{Z}) \geq -\log_2 c + S(\hat{\rho}),$$

where $H(\hat{X})$ is the Shannon entropy, $c$ is the maximum overlap between any two eigenvectors of the observables, and $S(\hat{\rho})$ is the von Neumann entropy of the quantum state $\hat{\rho}$.

In the case of two systems like the spin-$\frac{1}{2}$ example, we can extend the above relation to account for the bipartite nature. The corresponding entropic uncertainty relation reads

$$H(\hat{X}_A|\hat{X}_B) + H(\hat{Z}_A|\hat{Z}_B) \geq -\log_2 c + S(\hat{\rho}_A|\hat{\rho}_B).$$

Here, $H(\hat{X}_A|\hat{X}_B)$ represents the *conditional* entropy. This gives the entropy of $H(\hat{X}_A$ given we measure system $B$. For the case of a separable state (i.e., not entangled), $S(\hat{\rho}_A|\hat{\rho}_B)=0$. Therefore, $-H(\hat{X}_A|\hat{X}_B) - H(\hat{Z}_A|\hat{Z}_B) -\log_2 c$ serves as an entanglement witness.

### Entanglement in Heidelberg

We aim to apply the concept of entropic uncertainty relations to witness entanglement in Rubidium-87 spinor Bose-Einstein condensates (see, e.g., Kunkel *et al.,* [Science **360** (2018)](https://doi.org/10.1126/science.aao2254) for experimental details on entanglement generation).

In collaboration with experiments, we perform numerical simulations and analytical calculations to better understand entanglement within these systems. Our research applies entropic uncertainty relations to these systems hoping to better constrain measurements on entanglement and improve upon current theories.

Our two central aims of the project are:

* Use entropic uncertainty relations to understand the evolution of entanglement out of the Gaussian regime
* Investigate the behaviour of entanglement in a system where multiple spatial modes of the condensate are excited

An infographic (aimed at a general audience) for the first point can be found [here](entanglement.pdf).
