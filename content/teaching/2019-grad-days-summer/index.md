---
title: 'Computational approaches to quantum many-body systems'
subtitle: 'Summer 2019'
summary: "Lecture series given at the Graduate Days of the HGSFP in the summer term 2019"
authors:
- gaerttner


date: "2019-10-01"
lastmod: "2020-12-30"
featured: false
draft: false
tags:
 - lecture
# - quantum

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 2
  caption: 'Caption'
  focal_point: ""
  preview_only: false

links:
#  - icon_pack: fas
#    icon: arrow-circle-right
#    name: Homepage
#    url: 'https://uebungen.physik.uni-heidelberg.de/v/1123'
#  - icon_pack: fas
#    icon: arrow-circle-right
#    name: LSF
#    url: https://lsf.uni-heidelberg.de/qisserver/rds?state=verpublish&status=init&vmfile=no&publishid=286580&moduleCall=webInfo&publishConfFile=webInfo&publishSubDir=veranstaltung&noDBAction=y&init=y


# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Quantum spin models are the simplest quantum many-body problems, in some cases even allowing for analytical solutions. For this reason their study has led to many fundamental insights about emergent phenomena in quantum many-body physics. Still, in general non-integrable cases, the complexity of spin models, as measured by the Hilbert space dimension, increases exponentially with system size, rendering large spin systems intractable for numerical simulation. Therefore, in order to efficiently treat these problems numerically, and exploring large numbers of spins, methods for reducing this complexity are needed. 

In this lecture series, I will give an introduction to some of these methods. This covers exploiting symmetries for restricting the relevant Hilbert space (LMG models), over semiclassical methods (truncated Wigner approximation), to tensor network states, which restrict the amount of entanglement in the system. Each session will consist of a presentation followed be a programming exercise in which the learned methods are applied and explored further.
