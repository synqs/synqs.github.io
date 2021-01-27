---
# created through pandoc -s full_article.tex -o test.md
# the bib gets created through pandoc-citeproc --bib2json biblio.bib > biblio.json

title: 'Can we run quantum circuits on ultra-cold atom devices?'
summary: 'In this blog-post, we present our path and thoughts towards using
  ultra-cold atom experiments for quantum computation. They are the
  result of a two month internship where we studied the feasibility of
  such an undertaking in our group. Many associate only universal
  devices, especially qubit devices, to be valid quantum computers. We
  show how we think of our ultra-cold atoms in terms of quantum circuits
  and implement first steps in the software framework [PennyLane](https://pennylane.ai/).'
authors:
- jendrzejewski
- manrud
tags:
- quantum information
- quantum computing
- ultracold atoms
- pennylane
- quantum simulation
- machine learning

categories: []
date: 2020-05-25
lastmod: 2021-01-04T17:18:00+01:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false


projects:
- pennylane-ls

bibFile: content/post/2020-atomic-quantum-circuits/biblio.json

---

# Motivation


Over recent years, interest in quantum information processing has
increased tremendously. This rise was fueled by activities of massive
commercial players like [IBM](https://www.ibm.com/quantum-computing/),
[Google](https://research.google/teams/applied-science/quantum/),
[Microsoft](https://www.microsoft.com/en-us/quantum) and large
investments in startups like [D-Wave](https://www.dwavesys.com/),
[Rigetti](https://rigetti.com/), [Xanadu](https://www.xanadu.ai/),
[Zapata](https://www.zapatacomputing.com/) and [Cambridge Quantum
Computing](https://cambridgequantum.com/). The work of these companies
typically focuses on **universal quantum computers**, which hold the
premise of exponential speed-up for a variety of NP-hard problems.
However, this **universality usually comes at the price** of algorithmic
overhead for a wide range of tasks which generally leads to worse
overall fidelity. If we give up the constraint of a universal quantum
computer, we can build **specialized quantum hardware** for the problems
of interest. Such systems are called **quantum simulators**. 

**Ultra-cold atoms have become** **a leading platform of such quantum
simulators at a large scale**. Most importantly for us, they are the
experimental platform our research group is working on. Already
demonstrated applications involve an enormous variety of
condensed-matter problems like e.g. the Hubbard model {{< cite "Bloch_2008" >}},
topological systems {{< cite "Goldman_2014" >}}, superfluidity {{< cite "Regal_2007" >}} and
disorder {{< cite "Lagendijk_2009" >}}. More recently, cold atoms started to find
applications to Ising models {{< cite "Bernien2017" >}} and high-energy physics
{{< cite "Zohar2016" >}}.  

However, **quantum simulators are** **currently** **limited to an
academic environment** because of 

1.  the **complexity of constructing the experimental hardware**, which
    involves substantial technical know-how and funding.

2.  the **specificity of knowledge and language required** to
    understand/communicate the experiment.

3.  the need to **formulate the target problem as a Hamiltonian**.

4.  the **manual** **compilation of programs** on this hardware class. 

A **circuit-based approach to ultra-cold atom quantum simulators** would
alleviate points 2) and 3) as we could agree on the quantum circuit,
given the hardware-specific operations, and run it on the experiment.
Integrating the system with a software stack
like [PennyLane ](https://pennylane.ai/)would additionally allow to
address and run the experiment on a higher level and **substantially
lower the barrier of entry for users outside of the cold-atom and
quantum physics community**.  

These points motivated our research group to have a look how our
experimental hardware, which is controlled by the [Labscript
Suite](http://labscriptsuite.org/), can be integrated into PennyLane to
run quantum circuits on ultra-cold atom devices.  Our group is part of
[SynQS](http://www.kip.uni-heidelberg.de/synqs/), working on two
ultra-cold atom experiments, the NaLi and SoPa (named after the two
atomic species used in the lab).

# Why use ultra-cold atoms as a quantum information platform ?

For ultra-cold atoms, the **processing unit is not a qubit** and as
such, the **natural operations are not** generally **the commonly used
and widely known qubit operations** such as $X,Y,Z$ rotations,
Hadamard $H$ gates, entangling $CNOT$ or $XX$ gates with oberservables
like $\sigma^z$ expectations. Instead, our NaLi experiment implements
a $X(\theta)$ **rotation on a long spin** of many bosons on one optical
lattice site. Additionally, the system naturally evolves under a
many-body Hamiltonian $H_{mb}$, coupling the the atomic species.

What is the qubit equivalent of those operations? The relation is pretty
complex - and that is the nice thing! **Cold atoms are different**.
Given their success in the quantum simulation of many-body problems,
they could make for an exciting quantum information processor that
is **complementary to universal devices.** So as a general rule of
thumb, it could be argued that cold atom machines often give up some
control over individual particles, leading to much bigger systems.
Additionally, because we work with a large number of atoms, we can
measure obtain rather precise estimates of expectation values **with
a single state preparation and one measurement**. 

# A concrete example from our group

Before we go into more detailed discussion of our implementation, we
will present a **concrete example of our device**, where **we study
lattice gauge theories**. These theories have become a popular benchmark
for quantum simulators {{< cite "Kokail_2019" >}} and quantum
computers {{< cite "Martinez_2016" >}} or {{< cite "tavernelli2020" >}} in recent years. On our NaLi
machine, we recently performed experiments on the building block for
certain quantum simulators that would be suited for theories from
high-energy physics {{< cite "Mil2020" >}}.  These experiments are performed with
two atomic species, sodium and lithium, that can be prepared in two
internal spin states. 

**Re-thinking our analog quantum simulation** for the purpose of quantum
circuits, we can **represent the sodium atoms as a very long spin**
state $\left|\psi_N\right\rangle$. The observable outcomes
are $L_z=-\frac{N}{2},\cdots,\frac{N}{2}$, where $N\sim10^5$ is the
number of sodium atoms. On a quantum computer this should be compared to
a qubit, for which we can only measure two
outcomes $L_z=\pm\frac{1}{2}$.

The **lithium atoms** on the other hand can be **described by the states on two independent sites**
$\left|\psi_p\right\rangle$
and $|\psi_v\rangle$. For each site we can observe that number of atoms
that sit on it. The observable outcomes are then $n_{p/v} = 0, \dots, n$
where $n\sim 10^4$ is the number of lithium atoms. 

In this formulation and **analogous to other circuit-based quantum
computing devices**, the NaLi experiment then consists of three main
stages:

1.  The atoms are prepared in some initial state...

2.  controlled through a set of operations/gates...

3.  and then measured to evaluate the operators $L_z$ and $N_{p,v}$

Without having to dig through all the physical details to understand the
publication {{< cite "Mil2020" >}}, the figures in it intuitively open themselves up
to **readers with varying backgrounds** when plotting the
**corresponding circuits** next to them as shown below.

{{< figure src="mil_with_circuits.png" title="Sketched quantum circuits that correspond to selected figures from Mil et al. The results gain a clear intuitive meaning through the quantum circuits even though the system that is being simulated is not known. The color blue signifies the Sodium atoms and the orange color Lithium." numbered="true">}}


**Additional benefits of using the circuit language** include

-   a **more uniform definition of** *fidelity* for ultra-cold atom
    experiments relative to fidelity in qubit devices where each
    operation and the final result can be quantified.

-   **improved communication** with **and feedback** of theorists
    involved in the project by working on the same level of resolution.

-   more easily **generalizing the capabilities of the device** to work
    on **other problems.**

-   general accessibility and a **path towards using ultra-cold atoms
    experiments in the quantum computing community.**

# Choice of framework software for our quantum circuits

The choice of which framework software to use for our circuit-based
approach was not a particularly hard one for us. We have our own
experiment in the lab which implements a non-standard device for quantum
simulation and thus some of our requirements are (roughly in order of
importance):

1.  Can we **integrate our own experimental hardware** into the
    framework and potentially run it from there?

2.  How strong of an **assumption** is made **about the computational
    unit** of the hardware? Does it have to be strictly qubits/photons
    etc.?

3.  Is the framework **open-source** and shows **openness to the
    academic community**?

4.  Can also **integrate classical simulators** that are based on our
    hardware?

5.  Does it provide some sort of **user management and safety measures**
    to avoid unqualified users from killing the system?

Lets give a brief overview of how we answered those questions with
regard to PennyLane. **PennyLane is designed for users to write and use their own** *plugin*, which is what they call the integration of
quantum computing devices into the framework. Officially, it only
supports *qubit* and *continuous variable* devices and not more general
approaches but we may be able to **integrate bosonic and fermionic atoms flexibly** as the code itself is not very restricted. Other big platorms like [Qiskit](https://qiskit.org/), [Forest](http://docs.rigetti.com/en/stable/)
and [Strawberry
Fields](https://strawberryfields.readthedocs.io/en/stable/) focus
exclusively on their own quantum computing hardware or simulator without
the possibility to integrate your own. PennyLane is **open-source and
Python-based,** which is perfect as the *Labscript Suite* controlling
our experiment is so, too. Additionally, the company behind
PennyLane, [Xanadu](https://www.xanadu.ai/), is a partly academic player
who is very open in their publications and **supports a great community** around the software. The framework allows to add simulators
to the framework device which mirror the functionality of the hardware.
It performs various parameter range checks for the system and the
operations used. Not built-in is user a system for management which
allows only registered users to run the experiment from a queue. We
would have to implement this ourselves.

All-in-all, **PennyLane seems to be the best and likely only fit** for
our endeavors. Let's talk about it in more detail.

# Pennylane

> *A cross-platform Python library for quantum machine learning,
> automatic differentiation, and optimization of hybrid
> quantum-classical computations.*

{{< figure src="PennyLane_puzzle.png" title="PennyLane as the connecting puzzle piece." numbered="true">}}

[PennyLane](https://pennylane.ai/) is
created by [Xanadu ](https://www.xanadu.ai/) and presents itself as
the **connecting puzzle piece between powerful established python libraries for machine learning, and quantum computing platforms**. It provides readily implemented quantum algorithms for quantum machine
learning, quantum chemistry and optimization. A particular algorithm
provided in PennyLane is automatic differentiation of quantum circuits
which allows to perform shot-efficient application of classical-quantum
algorithms such as the *Variational Quantum Eigensolver* (VQE).   

Existing popular quantum computing platforms such as
[Qiskit](https://qiskit.org/) for qubits and [Strawberry
Fields](https://strawberryfields.readthedocs.io/en/stable/#) (also
created by *Xanadu*) for photons have written plugins for PennyLane
which make their **quantum simulators or quantum hardware accessible
through it** and with that PennyLane's quantum algorithms and automatic
differentiation feature. 

In fact, **any quantum lab can adapt the** [plugin
template](https://github.com/XanaduAI/pennylane-plugin-template) **for
their own experiment and simulators** to assimilate their own specific
workflow with PennyLane where users are generally able to use the same
workflow accross platforms and know what to expect.
Fig. 3 below shows a
typical way of using PennyLane in a classical-quantum hybrid algorithm.
Here, the default qubit simulator by PennyLane is used. After writing
our own plugin, we can call that device, change the quantum circuit to
contain the supported operations and the workflow is otherwise the same.
All-in-all, **the interface is very robust towards changing up the
quantum backend** (especially when they support the same operations).

{{< figure src="PennyLane_use.png" title="Typical simple way of using PennyLane by instantiating the device, defining the parametrized quantum circuit and the cost, and calculating the gradient for the classical parameters." numbered="true">}}

# Our workflow and connecting PennyLane to our hardware

The current state of our ***pennylane\_ls*** **plugin for ultra-cold
atom experiments** can be viewed in [**this public github
repository**](https://github.com/synqs/pennylane-ls). It provides
examples from our labs and can guide you to adapting it to your own
experiment and needs.

Our group uses the [**Labscript suite**](http://labscriptsuite.org/)
**to coordinate and execute experimental sequences** with cold atoms.  

>  *The labscript suite is a collection of programs, which work together
> to form a control system for autonomous, hardware timed experiments*.
>  

On the deepest level it is very nuts and bolts with plenty of commands
in the style of Fig. 4 below.

{{< figure src="Labscript_NaLi_code.png" title="The Experiment.py (left) defines the experimental sequence of a Labscript-controlled lab experiment, here by calling functions from NaLiFunctions.py at given times. The function UMPUMP (right) shows the exact low level hardware instructions that are to be executed." numbered="true">}}

The *Experiment.py*  **file determines the exact sequence of hardware controls** that is executed during the measurement. It contains Labscript syntax and is fed into the Labscript Python
compiler **Runmanager**. 

Our approach for **combining Labscript with PennyLane** is sumarized in
Fig. 5.

With the help of the plugin functions *pre\_apply()*,
*apply()* and *post\_apply()*, we generate a
new *Experiment.py* on the fly depending on the quantum
circuit programmed through the PennyLane interface.

{{< figure src="pre_post_apply.png" title="The functions pre_apply(), apply() and post_apply() are used to generate a  new Experiment.py on the fly for each quantum circuit in PennyLane. apply() loops through the operations in the circuit while  the other functions always write the same necessary code for the compilation." numbered="true">}}


In other words, **our PennyLane plugin translates a quantum circuit to
an** *Experiment.py* which our control system can interpret.

The *expval()* method from the plugin is then used to send the
newly generated file to the **Runmanager** and engage the sequence.
The output shots are then evaluated and the method returns an
expectation.

A detailled discussion of the technical details can be found in the
README.md of the [public
repository](https://github.com/synqs/pennylane_ls).  The **features of
our plugin** currently include:

-   **Proposing a higher-level control of experiments** that are run
    controlled by the Labscript Suite through PennyLane.

-   A **framework device that provides a template for labs with
    Labscript** to quickly adapt code for their own setup.

-   Including **two devices of the SynQS group at the
    Kirchhoff-Institute** **for Physics** of Prof. Fred Jendrzejewski.

The framework device in *SynQSDevice.py* is written such that **a group
which uses the Labscript Suite** to run their experiment **can** **adapt
the module easily to their own setup**.

Finishing up this project, we have **succeed in providing first circuit control to our experiments** through PennyLane and extract the results.
However, much **further automation will be needed** to fully leverage
the possibilities of the quantum circuits that we can run on our
ultra-cold atom devices.

# Future steps

To get the project **towards** **a full Pennylane plugin**, we have to:

1.  Give ***wires*** a meaning.

2.  **Operations need to be restricted to certain wires**, especially
    when different atomic species are involved.

3.  Implement **true remote control** of the lab through the
    *pennylane\_ls* module.

4.  Implement **full result post-processing** that is currently used in
    the lab.

5.  Implement some kind of **user management**.

While it seems quite clear how we can implement points 1 - 4, it seems
to be a whole new problem to implement some kind of user management for
our systems. 

In any case the **first steps are remarkably promising** and we will see
how the quantum circuits can be efficiently employed in ultra-cold atom
experiments.
