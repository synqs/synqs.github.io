---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Spiking neuromorphic chip learns entangled quantum states
subtitle: ''
summary: ''
authors:
- S. Czischek
- A. Baumbach
- S. Billaudelle
- B. Cramer
- L. Kades
- J. M. Pawlowski
- M. K. Oberthaler
- J. Schemmel
- M. A. Petrovici
- T. Gasenzer
- gaerttner
tags: ['neuromorphic hardware', 'machine learning']
categories: []
date: 2020-08-05
lastmod: 2021-01-21T20:50:11.942193Z
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ''
  focal_point: ''
  preview_only: false



# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
publishDate: 2020-08-05T07:20:09.942193Z
publication_types:
- '2'
projects:
- quantum-ann
abstract: Neuromorphic systems are designed to emulate certain structural and dynamical properties of biological neuronal networks, with the aim of inheriting the brain's functional performance and energy efficiency in artificial-intelligence applications. Among the platforms existing today, the spike-based BrainScaleS system stands out by realizing fast analog dynamics which can boost computationally expensive tasks. Here we use the latest BrainScaleS generation for the algorithm-free simulation of quantum systems, thereby opening up an entirely new application space for these devices. This requires an appropriate spike-based representation of quantum states and an associated training method for imprinting a desired target state onto the network. We employ a representation of quantum states using probability distributions, enabling the use of a Bayesian sampling framework for spiking neurons. For training, we developed a Hebbian learning scheme that explicitly exploits the inherent speed of the substrate, which enables us to realize a variety of network topologies. We encoded maximally entangled states of up to four qubits and observed fidelities that imply genuine N-partite entanglement. In particular, the encoding of entangled pure and mixed two-qubit states reaches a quality that allows the observation of Bell correlations, thus demonstrating that non-classical features of quantum systems can be captured by spiking neural dynamics. Our work establishes an intriguing connection between quantum systems and classical spiking networks, and demonstrates the feasibility of simulating quantum systems with neuromorphic hardware.
publication: 'ArXiv Preprint'
url_pdf: https://arxiv.org/pdf/2008.01039
doi: 
---
