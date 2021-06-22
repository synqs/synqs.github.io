---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Dynamics of open quantum systems in artificial neural networks
event: APS March Meeting 2021
event_url: https://march.aps.org/
# subtitle: 
summary: We showcase the Time Dependent Variational Principle for Neural Network encoded density matrices & other results that were obtained in close collaboration with Markus Schmitt from Universitity of Cologne.
authors:
- reh
- gaerttner
tags: ['Talk', 'ANN']
categories: ['Talk', 'ANN']
date: '2021-03-15'
featured: false
draft: false

# Display author profile cards at the end of the page
profile: true
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
projects:
 - quantum-ann

# Enable math on this page?
math: true
---
Artificial Neural Networks (ANNs) have proven to be powerful function approximators in many realms of physics. Among many other achievements, they present a competetive approach to the solution of the quantum many-body problem, utilizing state of the art network-designs that represent inherent physical properties of the system under scrutiny, e.g. translational symmetry in convolutional networks. While promising results have been obtained for the time evolution in the case of closed quantum systems in which the ANN serves as a variational wave function, the more general case of the dynamics of open quantum systems has not received as much attention. Here, we encode the density matrix by its corresponding POVM probability distribution which is represented through the parameters of an ANN for which we explicitly construct updates corresponding to dissipative Lindbladian dynamics. This is achieved using a Time Dependent Variational Principle, allowing us to accurately recreate the Lindbladian dynamics on the variational manifold.
