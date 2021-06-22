---
title: 'What are dynamical gauge fields ? A simplistic introduction by an AMO experimentalist.'

authors:
- jendrzejewski
- Torsten V. Zache
- hauke

tags:
- dynamical gauge fields
- lattice gauge theory
- gauge transformations
- ultracold atoms
- local symmetries
- tutorial

date: 2017-09-28
summary: Dynamical gauge fields are a fundamental concept of high-energy physics. However, learning about them typically takes enormous amounts of time and effort. As such, they are typically a bit mystical to students (including me) of other fields of physics like condensed-matter or AMO. Here, we will give a simple introduction into some of the concepts that might allow for the quantum simulation of these theories with ultracold atomic gases.The reader should know about second quantization and the basics of quantum mechanics as the arguments are based on this formalism.

draft: false

bibFile: content/post/2017-intro-dynamical/biblio.json
projects:
- sopa
- nali
- lattice-gauge
---
# Motivation

Dynamical gauge fields are a carrot that the AMO rabbit would like to
understand. However they are typically formulated in the context of QCD
or QED, whose only effect on me is profound sadness. Here, we will
discuss a naive derivation of some of the concepts that might allow for
the simulation of these dynamical gauge fields with ultracold atomic
gases. We will start out the discussion, with a few basic principles of gauge
transformations in quantum mechanics in Sec [2](#2-gauge-transformations-in-quantum-mechanics).

In Sec. [3](#3-non-relativistic-motion-in-an-electric-and-magnetic-field) we will see that these gauge transformations, especially the U(1)
transformations, have a deep relationship with the dynamics for
non-relativistic particles in a magnetic and an electric field. Then we
will get an effective Hamiltonian on a lattice.

After this step, we can discuss a bit physics of dynamical gauge fields
as they were originially introduced by Wilson in Sec. [4](#4-the-wilson-approach-to-dynamical-gauge-fields).

And finally, we will discuss in Sec. [5](#5-the-quantum-link-approach-to-dynamical-gauge-fields) the formalism of Quantum Link models, which seems currently most promising for experimental set-ups. Actual experimental
proposals will not be discussed here, as they typically involved the
discretization of the Dirac equation.

We will exclusively discuss non-relativistic particles in 1D. This very
simple system actually is so simplified, that it does not contain any
interesting dynamics [^1]. However, it teaches us the most fundamental
ingredients to design dynamical gauge fields on lattices. For further
reading, I will guide the reader to the specialized literature, which
will discuss such exciting problems like *Schwinger pair production*
{{< cite "Kasper_2017" >}} or *Coleman's phase transition*.

# 2. Gauge transformations in quantum mechanics

We will start out our discussion of dynamical gauge fields with a short
review of gauge transformations in quantum mechanics. This is slightly
unusual to the high-energy physicist, who will typcially start out with
some Lagrangien and some symmetries as discussed for example in the [PhD
by Valentin
Kasper](http://archiv.ub.uni-heidelberg.de/volltextserver/20372/1/Thesis.pdf).
However, the AMO community used the gauge transformations very
successfully to implement **static** gauge fields as very nicely
reviewed in Ref. {{< cite "Goldman_2014" >}} or the phantastic [lecture by Jean
Dalibard](http://www.college-de-france.fr/site/en-jean-dalibard/course-2013-2014.htm)
at the College de France [^2].

Given a certain Hamiltonian, we can describe the time evolution of the
wave function in terms of the Schrödinger equation:

$$
i\left|\dot{\psi}\right\rangle = \hat{H}\left|\psi\right\rangle
$$
However, the choice of the reference frame is arbitrary and we could
decide to look at the system in a different frame. Think about the
rotating earth for example. We can try to understand it by rotating with
it or by looking at it from the outside, where we see its rotation. Both
are perfectly valid choices and should give the same predictions for
observables. In quantum mechanics such a gauge transformation is
expressed by an operator, which changes the wave function:

$$
\left|\tilde{\psi}\right\rangle = U\left|\psi\right\rangle
$$
We can now directly see that it should be unitary from the condition
that the normalization of the wave function should not change :
$$
\left\langle \tilde{\psi}|\tilde{\psi}\right\rangle  \equiv \left\langle \psi|\psi\right\rangle\\\\
 =\left\langle\psi\right|U^\dagger U\left|\psi\right\rangle\\\\
\Rightarrow U^\dagger U  = 1
$$

Any such unitary operators can also be written as a complex exponential with a hermitian *generator*
$G = G^\dagger$:

$$\begin{aligned}
U &= e^{i \hat{G}}\\\\
UU^\dagger &= e^{i \hat{G}}e^{-i \hat{G}^\dagger} = 1\end{aligned}$$ These
generators will later play the role of local conservation laws.

As we would like to use such gauge transformations to engineer our
Hamiltonians, we better also understand the connection between the
Schrödinger equations in the different reference frames. In the standard frame, we can simply write:
$$
i\left|\dot{\psi}\right\rangle = \hat{H}\left|\psi\right\rangle
$$
Let us now solve the Schrödinger equation for $\tilde{\psi}$, to see how see how we can connect the two frames.
$$\begin{aligned}
\label{eq:GaugeTransformation}
i\left|\dot{\tilde{\psi}}\right\rangle &= \hat{H}\left|\tilde{\psi}\right\rangle\\\\
&=  Ui\left|\dot{\psi}\right\rangle + i \dot{U}\left|\psi\right\rangle\\\\
&= \left(UH + i\dot{U}\right)\left|\psi\right\rangle\\\\
&= \left(UH + i\dot{U}\right)U^\dagger \left|\tilde{\psi}\right\rangle\\\\
\Rightarrow \tilde{H} &= UHU^\dagger + i\dot{U}U^\dagger
\end{aligned}$$

So as we change the reference frame, the Hamiltonian contains different
terms. A typical example from the classical world is the Coriolis force
experienced by a person on the earth.

Finally, we would also like to understand how observables are
transforming under a gauge transformation. We will always measure an
observable given a certain state, so we should use:

$$\begin{aligned}
\langle A \rangle &= \left\langle\psi\right|A\left|\psi\right\rangle\\\\
&=\left\langle\tilde{\psi}\right|UAU^\dagger\left|\tilde{\psi}\right\rangle\\\\
&= \left\langle\tilde{\psi}\right|\tilde{A}\left|\tilde{\psi}\right\rangle\\\\
\Rightarrow\tilde{A} &=  UAU^\dagger
\end{aligned}$$
Most of the time we are actually only interested in the time evolution of certain operators in
the Heisenberg picture:

$$i\dot{A}_H = [H,A_H]$$

A few calculations show that we obtain again as expected:
$$i \frac{d\tilde{A}}{dt} =[\tilde{H},\tilde{A}]$$

## U(1) gauge transformations

As a first important example for gauge transformation, we will study the
multiplication of the wavefunction with a phase, i.e. U(1) gauge
transformations. If the phase is constant in space and time, it leads to
global number conservation. For a phase that is varying, the Hamiltonian
emulates the motion of a charged particle in an EM field.

The U(1) transformation is then defined through:

$$\begin{aligned}
U_1 &= e^{i\varphi(\hat{x},t)}\\\\
\left|\tilde{\psi}\right\rangle &= e^{i\varphi(\hat{x},t)}\left|\psi\right\rangle
\end{aligned}$$

Given that we work in the lab with non-relativistic particles we use the
normal single particle Hamiltonian:

$$\begin{aligned}
\hat{H}_0 &= \frac{\hat{p}^2}{2m}+V(\hat{x})\\\\
[\hat{x}_i,\hat{p}_j] &= i\delta\_{ij}
\end{aligned}$$

So to understand how the Hamiltonian transforms, we can now analyze how $U_1$ transfroms
$\hat{p}$ and $\hat{x}$. As $U$ is a function of $\hat{x}$ and $t$ it
commutes with $\hat{x}$ and leaves it unchanged

$$\begin{aligned}
U\hat{x}U^\dagger = \hat{x}\end{aligned}$$ For the momentum we have on the
other hand:
$$\begin{aligned}
U\hat{p}U^\dagger &\approx (1+i\varphi(\hat{x},t)) \hat{p}(1-i\varphi(\hat{x},t))\\\\
&= \hat{p} +i[\varphi(\hat{x},t),\hat{p}]\\\\
 &= \hat{p}-\nabla_x \varphi(\hat{x},t)
\end{aligned}$$

And for the time derivative we have:

$$i \dot{U}U^\dagger = -\dot{\varphi}(\hat{x},t)$$ In this frame the
Hamiltonian has therefore the following form:

$$
\tag{1}
\label{Eq:HunderU1}
H_1 = \frac{\left(p+\nabla \varphi(\hat{x},t)\right)^2}{2m}+V(\hat{x})-\dot{\varphi}(\hat{x},t)
$$

To summarize:

-   If the externally imprinted phase of the wavefunction is changing
    over, the time derivative looks like a scalar potential or just some
    kind of energy shift.

-   If the gauge transformation has a position dependence, the
    derivative of the phase looks like a vector potential.

To get a better understanding of the relationship to electrodynamics we
can just look at the classical equation of motion that comes out of this
Hamiltonian. But before we get into this connection, let us finish the
discussion here with the relationship between gauge symmetry and
particle conservation, which the reader might skip in a first read.

## 3. Non-relativistic motion in an electric and magnetic field

We have seen that Eq. (\ref{Eq:HunderU1}) looks a lot like a Hamiltonian of a charged
electron that we know from EM, namely: $$\begin{aligned}
H_1 &= \frac{(\mathbf{p}+eA(\mathbf{r},t))^2}{2m}+e\phi(\mathbf{r},t)\end{aligned}$$
$eA(\mathbf{r},t)$ is then the vectore potential and
$e\phi(\mathbf{r},t)$ the scalar potential.

Let us clarify this connection a bit more. In Hamiltonian mechanics we
have to solve the equations of motion: $$\begin{aligned}
\frac{dp_i}{dt}&=-\frac{\partial H}{\partial r_i}\\
\frac{dr_i}{dt}&=\frac{\partial H}{\partial p_i}\end{aligned}$$ We can
now rewrite the Hamiltonian (\ref{Eq:HunderU1}) as:

$$\begin{aligned}
H_1 &= \frac{(\mathbf{p}+eA(\mathbf{r},t))^2}{2m}+e\phi(\mathbf{r},t)\\\\
&= \frac{\mathbf{p}^2 +2e\mathbf{A}(\mathbf{r})\mathbf{p}+e^2\mathbf{A}^2(\mathbf{r})}{2m}+e\phi(\mathbf{r},t)\\\\
\text{with }\mathbf{A}(\mathbf{r},t) &=\frac{\nabla \varphi(\mathbf{r},t)}{e}\text{ and } \phi(\mathbf{r},t) =\frac{ V(\mathbf{r})-\dot{\varphi}(\mathbf{r},t) }{e}\end{aligned}$$

We actually find:

$$\begin{aligned}
v_i &= \frac{dr_i}{dt}= \frac{p_i+eA_i(\mathbf{r})}{m}\\\\
\frac{dp_i}{dt}&= -\left[e\frac{\partial\phi(\mathbf{r},t)}{\partial r_i}+e\sum_j \frac{p_j}{m} \frac{\partial A_j(\mathbf{r})}{\partial r_i}+e^2\sum_j \frac{A_j(\mathbf{r})}{m}\frac{\partial A_j(\mathbf{r})}{\partial r_i}\right]\\\\
\frac{dp_i}{dt}&= -e\left[\frac{\partial\phi(\mathbf{r},t)}{\partial r_i}+\sum_j v_j \frac{\partial A_j(\mathbf{r},t)}{\partial r_i}\right]\end{aligned}$$
For the time dynamics we finally obtain:
$$\begin{aligned}
F_i &= m \dot{v}_i = \dot{p}_i+\dot{A}_i(\mathbf{r})\\\\
&= -e\left[\frac{\partial\phi(\mathbf{r},t)}{\partial r_i}+\sum_j v_j \frac{\partial A_j(\mathbf{r},t)}{\partial r_i}\right]+e\dot{A}_i(\mathbf{r})
\end{aligned}$$
In three dimensions we can now make the identification with the Lorentz
force: $$\begin{aligned}
\mathbf{F} &= e\left(\mathbf{E} + \mathbf{v}\times\mathbf{B}\right)\end{aligned}$$
And we obtain:
$$\label{Eq:DefElectricField}\tag{2}
\mathbf{E} = -\nabla \phi(\mathbf{r},t) + \partial_t \mathbf{A}(\mathbf{r},t)
$$
and for the magnetic field $$\mathbf{B} = \nabla \times \mathbf{A}$$

So we can obtain the equations of motion in a static electric or
magnetic field by doing position and time-dependent U(1)
transformations. [^3] We have seen a first indication the a change in
reference frame and electrodynamics are strongly linked. However, in
this approach the external fields are static and not at all correlated
with the dynamics of the matter field. To create a more complete picture
of electro**dynamics** we should also include this dynamic degree of
freedom. We will see later on that this is done conveniently on a
lattice.

## Discretization in 1D

While we typically think about electromagnetism in continuous space, it
is actually quite common to do most calculations on a lattice. As most
AMO experiments and proposals work on a lattice, we will therefore just
derive the formulation of electromagnetism on a lattice here [^4].
Again, if you know static synthetic gauge fields on a lattice, you might
skip this section.

The Hamiltonian in the continuum limit was: $$\begin{aligned}
H = \int dx \; \psi^\dagger(x) \frac{\left[p-eA(x)\right]^2}{2m} \psi(x) = \frac{1}{2m} \int dx \; \left|\left[\partial_x + ie A(x) \right]\psi(x)\right|^2\; .\end{aligned}$$
Now we discretize with lattice spacing $a$, $$\begin{aligned}
\left[\partial_x + ie A(x) \right]\psi(x) \rightarrow \frac{1}{a}\left(\psi_{n+1} - \psi_n\right)  + ie A_n \psi_n = \frac{1}{a} \left(\psi_{n+1} - \psi_n +iea A_n \psi_n\right) \; .\end{aligned}$$
Thus we find with $A_n = A_n^\dagger$ , $$\begin{aligned}
H \rightarrow \frac{1}{2m a} \sum_n \left(\psi_{n+1}^\dagger - \psi_n^\dagger - iea \psi_n^\dagger A_n\right) \left(\psi_{n+1} - \psi_n +iea A_n \psi_n\right) \equiv H_a \; .\end{aligned}$$
Shifting the index of terms involving
$\psi_{n+1}^\dagger \rightarrow \psi_n^\dagger$, the summand becomes
$$\begin{aligned}
\psi_n^\dagger \left\lbrace\left(\psi_n -\psi_{n-1} +ie A_{n-1} \psi_{n-1}\right) - \left(\psi_{n+1} - \psi_n +iea A_n \psi_n\right) -ie A_n \left(\psi_{n+1} - \psi_n +iea A_n \psi_n\right)\right\rbrace \; .\end{aligned}$$
Rearranging the terms, we find $$\begin{aligned}
2ma H_a = \sum_n \left\lbrace -\psi_n^\dagger \left(1 + iea A_n\right) \psi_{n+1} + 2\psi_n^\dagger \psi_n - \psi_n^\dagger \left(1-ieaA_{n-1}\right)\psi_{n-1} +e^2 a^2 \psi_n^\dagger A_n^2 \psi_n\right\rbrace \end{aligned}$$
The lattice theory is not unique, in particular we can add any term
$\propto a$ because they will vanish in the continuum limit, where
($a\rightarrow 0, N -> \infty$ and $aN = const.$). For example a
derivative term like $$\begin{aligned}
a\sum_n \psi_n^\dagger A_n^2  \cdot \left(\psi_{n+1} - \psi_n\right) \approx \int dx \; \psi^\dagger(x) A^2(x) \cdot  a \partial_x \psi(x)\end{aligned}$$
should not contribute in the end. We thus consider the equivalent
Hamiltonian $$\begin{aligned}
H_a \simeq H_a + \frac{1}{2ma} \sum_n \left(\frac{a^2 e^2}{2}\right) \left\lbrace\psi_n^\dagger A_n^2 \left(\psi_{n+1} - \psi_n\right) + \left(\psi_{n+1}^\dagger - \psi_n^\dagger\right)A_n^2 \psi_n\right\rbrace \; ,\end{aligned}$$
such that all terms involving $A^2$ combine to $$\begin{aligned}
\frac{ae^2}{2} \left(\psi_n^\dagger A_n^2 \psi_{n+1} + \psi_{n+1}^\dagger A_n^2 \psi_n\right)\end{aligned}$$
Shifting everything to $\psi_{n+1}^\dagger$ as before, we arrive at
$$\begin{aligned}
2ma H_a = &-\sum_n \left\lbrace \psi_n^\dagger \left(1 + iea A_n -\frac{1}{2} e^2 a^2 A_n^2\right) \psi_{n+1} + \psi_n^\dagger \left(1-ieaA_{n-1} - \frac{1}{2}e^2 a^2 A_{n-1}^2\right)\psi_{n-1} \right\rbrace \nonumber\\
&+ \sum_n 2\psi_n^\dagger \psi_n\end{aligned}$$ Now we can define
$U_n \equiv \exp \left(iea A_n\right) = 1 + iea A_n - \frac{1}{2}e^2 a^2 A_n^2 + \cdots$
and find the expected form $$\begin{aligned}
H_a \simeq -\frac{1}{2ma}\sum_n  \psi_n^\dagger \left(U_n \psi_{n+1} - 2\psi_n + U_{n-1}^\dagger \psi_{n-1} \right) \; ,\end{aligned}$$
where we have again used that terms of order $\mathcal{O}(a)$ don't
contribute to the continuum limit. For convenience, we may redefine
$\psi_n \rightarrow \sqrt{a} \psi_n$, which makes the fields
dimensionless and we end up with $$\begin{aligned}
H_a = -\frac{1}{2ma^2}\sum_n  \psi_n^\dagger\left(U_n \psi_{n+1} + 2\psi_n + U_{n+1}^\dagger \psi_{n-1}\right)\; .\end{aligned}$$

We will typically obtain on a lattice only the effective tunneling
element, which we identify therefore as: $$\begin{aligned}
J \equiv \frac{1}{2m a_L^2}\end{aligned}$$

## U(1) gauge transformations on a lattice

For clarity, we will now reperform the U(1) gauge transformations  on a lattice.
This will greatly simplify the identification with an electric field etc. Skip it if you know it already.

We will employ the formalism of second quantization in the tight binding
approximation:

$$\begin{aligned}
\hat{H} = - J \sum_i \left(a_i^\dagger a_{i+1} +a_{i+1}^\dagger a_i \right)
\end{aligned}$$

The wave function is now formulated in terms of the field operator:
$$\begin{aligned}
\left|\psi\right\rangle = \sum_j \hat{a}_j w_j(x)
\end{aligned}$$

The operators are defined to operate on the vacuum with the following
commutation relationship:
$$\begin{aligned}
a_j \left|n_j\right\rangle = \sqrt{n_j}\left|n_j-1\right\rangle\\\\
a_j^\dagger \left|n_j\right\rangle = \sqrt{n_j+1}\left|n_j+1\right\rangle\\\\
~[a_i,a_j^\dagger] = \delta_{ij}
\end{aligned}$$

A transformation of the phase corresponds therefore too:
$$\begin{aligned}
\tilde{a}_j = e^{i\varphi_j(t)}\hat{a}_j\end{aligned}$$

Now we have to find the unitary operator that does the necessary transformation. We
typically obtain the relation for the for small case $\varphi_j$of smal
$$\begin{aligned}
\tilde{a}_j &= U_j a_j U_j^\dagger\\\\
U_j &= e^{i\varphi_j(t)\hat{G}_j}\\\\
(1+i\varphi_j)a_j &= (1+i\varphi_j G_j)a_j (1-i\varphi_j G_j)\\\\
a_j +i\varphi_ja_j &= a_j + i\varphi_j (Ga_j - a_jG)\\\\
 a_j &= [G_j,a_j]
 \end{aligned}$$

This last equation is solved by:

$$\hat{G}\_j = -\hat{N}\_j =-a^\dagger_j a_j$$

As each component commutes we can therefore write now:

$$\begin{aligned}
U_1 = e^{i\sum_j \varphi_j(t) \hat{N}_j}
\end{aligned}$$

Therefore we obtain:
$$\begin{aligned}
U_1HU_1^\dagger &= -J\sum_i \left[a_i^\dagger a_{i+1} e^{-i\delta \varphi_i} +a_{i+1}^\dagger a_i e^{i\delta \varphi_i} \right]\\\\
\delta \varphi &= \varphi_i-\varphi_{i+1}
\end{aligned}$$

For the time dependence we have:

$$\begin{aligned}
i\dot{U}U^\dagger = -\sum_j \hat{N}_j \dot{\varphi}_j
\end{aligned}$$

So the transformed Hamiltonian reads:
$$
\tag{3}
\label{Eq:LatticeWithMagField}
 \tilde{H} = -J\sum_i \left[a_i^\dagger a_{i+1} e^{-i\delta \varphi_i} +a_{i+1}^\dagger a_i e^{i\delta \varphi_i} - \dot{\varphi}_i \hat{N}_i\right]
$$
  We can now identify the derivative of the phase with
the vector potential and the time derivative with the scalar potential:
$$\begin{aligned}
 \delta \varphi_i &= eA_i a_L\\
 \dot{\varphi}_i &=  e\phi_i
 \end{aligned}$$

We can now summarize these findings in the figure below. The
identification with the magnetic field and the electric field are then
again like in Eq.(\ref{Eq:DefElectricField})[^5].


{{< figure src="SimpleHoppingv2.png" title="Hopping in the lattice after a U(1) gauge transformation. At each hopping event to right, the particle acquires a phase $e\ A_i\ a$, which is proportional to the vector potential. Hopping to the left leads to the accumulation of the inverse phase $-e\ A_ia$." numbered="true">}}

## From the gauge symmetry to particle conservation

We have seen that the equations of motion remain the same if the wave
function is multiplied by a phase that is constant in space and time. We
can see this directly from Eq. (\ref{Eq:LatticeWithMagField}) with $\varphi_j(t) = \varphi$. So we
obtain:

$$\begin{aligned}
 U_C &= e^{i\varphi\sum_j\hat{N}_j }\\\\
 \tilde{H} &= UHU^\dagger  = H\\\\
 \Rightarrow UH &= HU\\\\
 \Rightarrow [H,U] &= 0
\end{aligned}$$

If the unitary operator commutes with the Hamiltonian,
we also now that its generator $\hat{N} = \sum_j\hat{N}_j$ commutes:
$$\begin{aligned}
~[H, N]=0
\end{aligned}$$
And as the number generator does not depend explicitly
on time we obtain from the Heisenberg equation that the total number of
atoms is conserved.

# 4. The Wilson approach to dynamical gauge fields

Until now we seen that there is an intimate relation between the
existance of electric and magnetic fields and $U(1)$ gauge
transformations that depend on time and position. However, the gauge
fields are not changing in any way as we are moving a charge. This is in
direct constrast to electrodynamics where the motion of the charge
implies directly the change of the electric field, see Figure below. This relationship
is captured by Gauss' Law:
$$\tag{4}
\label{Eq:GaussLaw}
 \mathbf{div} \mathbf{E} = \rho
 $$

Further the time evolution of the vector potential is not at all
captured in the previous section. In electrodynamics we actually have to
fulfill the relation:
$$\tag{5}
\label{Eq:MaxwellTime}
 \partial_t \mathbf{A} = \mathbf{E}
 $$


{{< figure src="gauss_law.gif" title="Gauss law of electrodynamics. As the charge (blue) is displaced, the electric field is also modified. This perfect correlation between electric field and matter field, is one of the cornerstones of any realization of dynamical gauge fields in synthetic systems.">}}

To implement these two constraint, we will have to modify the underlying
Hamiltonian. So we look once again at the Hamiltonian (\ref{Eq:LatticeWithMagField}) and rewrite it in a more suggestive
way:

$$\label{eq:LatticeWithLink}
 \tilde{H} = -J\sum_i \left[a_i^\dagger L^*\_i a_{i+1} +a_{i+1}^\dagger L_i a_i - \dot{\varphi}_j \hat{N}_j\right]
$$

If the $L_i$ was an operator it would actually have a very similiar
structure to the Gauss law. As the particle hops from site to site it
would change the operator $L_i$. We will call them in the following the
**link operators**. In the next section, we
adapt the Hamiltonian with dynamical links such that the system now
fulfills Gauss' Law. Then we will also add an additional term to the
Hamiltonian to obtain the appropiate time dynamics of ED afterwards.

## Gauss law

Eq. (\ref{Eq:GaussLaw}) describes a local conservation law combining
the matter field and the electric field. So we will be able to obtain
such a relation by enforcing local gauge symmetry. To derive the *local*
transformation laws, we will first perform a local gauge transformation
of the matter field:

$$\begin{aligned}
U =& e^{i\varphi_j \hat{N}\_j}\\\\
\tilde{H} =&-J\sum_{i\neq j, j-1}\left[a_i^\dagger \hat{L}^\dagger_i a_{i+1} +a_{i+1}^\dagger \hat{L}_i a_i\right]\\\\
  &- J \left[a_{j-1}^\dagger \hat{L}^\dagger_{j-1} a_{j} e^{i\varphi_j} +a_{j}^\dagger \hat{L}_{j-1}a_{j-1} e^{-i \varphi_j}\right]  \nonumber\\\\
  &- J \left[a_{j}^\dagger \hat{L}^\dagger_{j} a_{j+1} e^{-i\varphi_j} +a_{j+1}^\dagger \hat{L}_{j}a_{j} e^{i \varphi_j} - \dot{\varphi}_{j}\hat{N}_j\right]
\end{aligned}$$

So we would obtain local gauge symmetry if we find a transformation of
the form:
$$\begin{aligned}
 ~\tilde{L}_j &= L_j e^{-i\varphi_j}\\\\
 ~\tilde{L}\_{j-1} &= L\_{j-1} e^{i\varphi_j}
\end{aligned}$$

This gauge transformation enforces the following
conditions on the generator of the gauge transformation:
$$\begin{aligned}
\exp(i\varphi G^L)L \exp(-i\varphi G^L) = \exp(-i\varphi)L
\end{aligned}$$

Let me write it in an infinitisimal way:
$$\begin{aligned}
\exp(i\varphi G^L)L \exp(-i\varphi G^L)  &= (1+i\varphi G^L)L (1-i\varphi G^L) \nonumber\\\\
&= (L+i\varphi G^L L) (1-i\varphi G^L)\nonumber\\\\
&= (L+i\varphi G^L L - i\varphi L G^L)\nonumber\\\\
&= (1-i\varphi )L\nonumber
\end{aligned}$$

We end up with:
$$\tag{6}\label{Eq:CommLinkOps}
[L,G^L] = L
$$

So we can actually now know that the Hamiltonian remains unchanged under a gauge transformation with the generator $$\begin{aligned}
G_j &= \hat{N}\_j + G^L_j - G^L_{j-1}\\\\
 \tilde{H} =& -J\sum_{i}\left[a_i^\dagger \hat{L}^\dagger_i a_{i+1} +a_{i+1}^\dagger \hat{L}_i a_i\right]- J \dot{\varphi}_{j}\hat{G}_j
 \end{aligned}$$

So if we want to have gauge symmetry even for time dependent gauge
transformations we have to fulfill
$$\begin{aligned}
\hat{G}_j\left|\psi\right\rangle = 0
\end{aligned}$$

Additionally we can take a closer look at the structure of the
generator, which can actuall rewrite as something similiar to Gauss'
law:
$$\begin{aligned}
\hat{G}\_j &= \hat{N}\_j + G^L_j - G^L_{j-1} \\\\
&= \hat{N}_j + (\mathbf{div}G^L)_j\\\\
&= \hat{N}_j + \frac{1}{e}(\mathbf{div}E)_j
\end{aligned}$$

So we know that the electric field is basically the generator of the local gauge
transformation of the link operators. Using Eq. (\ref{Eq:CommLinkOps}) we can write down the commutation relation
between link operator and electric field as: $$~[L_i,E_i] = eL_i$$
However, we do not know the value of the charge, nor the commutation
relations of the link operators. We will obtain them from the time
evolution of the gauge field.

## Time dynamics

In analogy with classical mechanics we can introduce the Hamiltonian
dynamics of the electric field via an $E^2$ term. So the full
Hamiltonian reads now:

$$
H = \chi_L \sum_i (G^L_i)^2 - J\sum_i \left[a_i^\dagger L^\dagger_i a_{i+1} +a_{i+1}^\dagger \hat{L}_i a_i \right]
$$
We now have to look at the time dynamics of the link operators. We obtain:
$$i\dot{L}_j = \chi_L [(G^L_j)^2,L_j] - J\sum_i \left[a_i^\dagger [L^\dagger_i,L_j] a_{i+1} +a_{i+1}^\dagger [\hat{L}_i,L_j] a_i \right]\nonumber$$
Comparing to Eq. (\ref{Eq:MaxwellTime}) we see that the commutators between the
links should disappear. So we should enforce:
$$\begin{aligned}
~[L\_i^\dagger,L_j] &= 0\\\\
 ~[L_i,L_j]  &= 0\\\\
 ~[L^\dagger_i,L^\dagger_j]  &= 0
\end{aligned}$$

At this stage we know that
the link operators are unitary:

$$\begin{aligned}
L_i^\dagger L_i = L_i L_i^\dagger
\end{aligned}$$

So in analogy with the classical case we will identify its phase with the vector potential as:
$$\begin{aligned}
L_i = e^{ieA_i a_L}
\end{aligned}$$

Let us now continue to look into the time evolution.

$$\begin{aligned}
i\dot{L}_j &= \chi_L [(G^L_j)^2,L_j] \\\\
&=\chi_L \left(G^L_j[G^L_j,L_j]+[G^L_j,L_j]G^L_j\right)\\\\
&= -\chi_L \left(G^L_jL_j+L_jG^L_j\right)
\end{aligned}$$

And in the classical limit we find now:

$$-ea_L\dot{A}_j = -2\chi_L  \frac{E_j}{e}$$

So we know now that:
$$\begin{aligned}
 \chi_L= \frac{e^2 a_L}{2}
\end{aligned}$$

Our Hamiltonian reads therefore:
$$H = \frac{a_L}{2} \sum_i E_i^2 + \frac{1}{2m a_L^2}\sum_i \left[a_i^\dagger L^\dagger_i a_{i+1} +a_{i+1}^\dagger \hat{L}_i a_i \right]$$
End then we can identify :
$$\begin{aligned}
\chi_L= \frac{e^2 a_L}{2}\\
J= \frac{1}{2ma_L^2}\end{aligned}$$

# 5. The quantum link approach to dynamical gauge fields

The previous approach relies on unitary link operatores, which are
extremely hard to implement with ultracold atomic gases. The idea of QLM
is relax the constraints on the link operators a bit, while keeping
exactly the local gauge invariance. This is also the only formalism for
which proposals of analog quantum simulation exist as discussed in Ref.
{{< cite "Zohar2016" >}} , {{< cite "Kasper_2016" >}} , {{< cite "Wiese2013" >}}  and citations
therein. The discussion on the Gauss' law remains the same as in the
previous section, so we would like to have:

$$\tag{7}\label{eq:CommutRelLinks}
[L_i,G^L_i] = L_i ~~[L^\dagger_i,G^L_i] = -L^\dagger_i
$$

## Using spins as links

A nice way out of the problems with finding a unitary link operator was
suggested by [@Chandrasekharan1997; @Horn1981; @Orland1990]. Actually,
we can decompose the link into its real and imaginary part:
$$\label{Eq:LatticeWithLink}
 L_i = e^{ieA_i a_L} =\cos(eA_i a_L) + i\sin(eA_i a_L)
$$
Instead of using a cosine function we now simply set the real and imaginary part as
operators:
$$\begin{aligned}
 \hat{L}_i = \hat{C}_i + i\hat{S}_i\\
 \hat{L}_i^\dagger = \hat{C}_i - i\hat{S}_i
\end{aligned}$$

We can now plug in these definitions into equation (\ref{eq:CommutRelLinks}) and obtain:
$$\begin{aligned}
~[C+iS, G]&= C + iS \\\\
~[C,G] + i [S,G] &= C + iS \\\\
~[C,G] &= iS \label{Eq:CommSpinLinks}
\end{aligned}$$

In a similiar fashion we have:

$$\begin{aligned}
~[C-iS, G]&= -(C - iS)\\\\
~[C,G] - i [S,G] &= iS -C\\\\
~[G,S] &= iC
\end{aligned}$$

The last line sets the commutation relationship of the links. These can be directly
identified with the commutation relationships of a spin. So we directly
find that we will be able to represent the link operator by composition
of spins:

$$\begin{aligned}
C = J_x\\\\
S = J_y\\\\
G = -J_z
\end{aligned}$$

And we can also write down the link operator as:
$$\begin{aligned}
L &= J_x + iJ_y = J_+\\\\
L^\dagger &=J_x - iJ_y = J_-
\end{aligned}$$

Let us write down explicitly
once more the commutation relationships that we have in the QLM:
$$
[L_i, G_i^L]=[J_+, -J_z] =J_+\label{eq:CommLinkQLM}\tag{8}
$$

So while we keep local gauge invariance, we have now non-commutating
link operators. This means that we implement properly the Gauss' law.
However, the time evolution will only correspond in certain limits to
the time evolution of QED. As reminder each operator acts in the
following way on an eigenstate:

$$\begin{aligned}
J^2 \left|m,\ell\right\rangle &= \ell(\ell+1)\left|m,\ell\right\rangle\\\\
J_z \left|m,\ell\right\rangle &= m\left|m,\ell\right\rangle\\\\
J_+\left|m,\ell\right\rangle &= \sqrt{\ell(\ell+1)-m(m+1)}\left|m+1,\ell\right\rangle\\\\
J_-\left|m,\ell\right\rangle &= \sqrt{\ell(\ell+1)-m(m-1)}\left|m-1,\ell\right\rangle
\end{aligned}$$

# Identification with QED

We can once again write down our microscopic Hamiltonian:
$$H_{QL} = \chi_L \sum_i (J_z^i)^2-J\sum_i \left[a_i^\dagger \hat{J}^+_i a_{i+1} +a_{i+1}^\dagger \hat{J}^-_i a_i \right]$$
We would now like to make the connection to QED. For that we need the
commutators in equation \ref{eq:CommLinkQLM} to become negligable. We actually know that
this will typically happen in the limit of large occupation numbers for
the spin. In this case we can write [(PhD by Christian
Gross)](http://www.kip.uni-heidelberg.de/Veroeffentlichungen/details.php?id=2160):
$$\begin{aligned}
\hat{J}_x &\approx \ell \cos(\hat{\varphi})~~\hat{J}_y \approx \ell \sin(\hat{\varphi})\\
\Rightarrow J_+ &\approx \ell e^{i\hat{\varphi}}~~ J_- \approx \ell e^{-i\hat{\varphi}}\end{aligned}$$
So we definitely want to take the prefactor $\ell$ out of hopping
element and define: $$\begin{aligned}
L_i^\dagger = \frac{J_i^+}{\ell}~~L_i = \frac{J_i^-}{\ell}\end{aligned}$$
So the Hamiltonian should now be written as:
$$H_{QL} = \chi_L \sum_i (J_z^i)^2+\frac{\ell}{m^* a_L^2}\sum_i \left[a_i^\dagger \hat{L}^\dagger_i a_{i+1} +a_{i+1}^\dagger \hat{L}_i a_i \right]$$

In the next step, we have to verify that the equations of motion are the
appropiate ones. We obtain:

$$\begin{aligned}
i\dot{J}^+\_i &= \chi\_L [(J_z^i)^2, J_i^+]-Ja_{i+1}^\dagger a_i [J_i^-,J_i^+]\\\\
&=-\chi_L (J_i^zJ_i^++J_i^+J_z^i)+2Ja_{i+1}^\dagger a_i J^z_i
\end{aligned}$$

In the classical limit we obtain now:

$$\begin{aligned}
-\ell e\dot{A}\_i a_L=  \left(\frac{-2\chi_L \ell}{e}+2Ja_{i+1}^\dagger a_i\right)E_i\\\\
\dot{A}_i=  \left(\frac{2\chi_L }{e^2a_L}-\frac{2Ja_{i+1}^\dagger a_i}{e\ell a_L}\right)E_i
\end{aligned}$$

So the coherence could now be driving the dynamics as in the usual spin
changing collision. However, let us simply assume that it is in the
order of one. Then obtain the condition for finding the QED limit that:
$$\begin{aligned}
\frac{2\chi_L }{e^2a_L}&\gg\frac{2J}{e\ell a_L}\\
\ell&\gg\frac{Je}{\chi_L}\end{aligned}$$ If we have this condition we
can actually write down once again the previous equation of motion,
where we found that: $$\begin{aligned}
\chi_L=\frac{e^2}{2a_L}\end{aligned}$$

# From theory towards experiments

The theoretical concepts of dynamical gauge fields in ultracold atomic
systems have been relatively well established in the last few years and studied in several theory groups. However, the experimental
efforts are still way behind the theoretical framework. The gap is
actually so strong that only a single experiment has been performed with
ultracold ions  {{< cite "Martinez_2016" >}}, which performed a digital quantum
simulation with *four* qubits. With ultracold atomic gases,up to the
groups to decide on the specific experimental implementation, which best
implements the:

-   Gauss law, which connects the matter field dynamics to the gauge
    field dynamics.

-   Time dynamics, which connects the vector potential dynamics to the
    electric field dynamics

And this is exactly, what we are working on in our group.


# Updates

Since we first wrote this article there has been substantial progress on the experimental side.

- In trapped ions there was an experiment with a much larger number of ions {{< cite "Kokail2018" >}}
- In cold atoms there have been a number of experiments. See {{< cite "Goerg2019" >}}, {{< cite "Schweizer2019" >}}, {{< cite "Mil2020" >}}, {{< cite "Bing2020" >}} .
- Concerning non-abelian gauge theories we wrote a paper of similiar style as this tutorial {{< cite "Kasper2020-jaynes" >}}.

Feel free to comment and or write us if you would like to know more and have specific requests.

[^1]: If I am wrong about this part, please tell me.

[^2]: If you do not speak french, this lecture series might be a good
    motivation to change this.

[^3]: While we obtained here the right equations of motion for the
    particle we are still missing the equation of motion for the
    electric field.

[^4]: Kudos to Torsten Zache for this part.

[^5]: **Attention:** From Eq. (\ref{Eq:LatticeWithMagField}) it becomes immediatly clear that
    it is different to hop to the left then hopping to the right. So the
    left-right symmetry is explicitly broken by external factors. This
    is an important point to remember when we discuss dynamical gauge
    fields in the following sections.
