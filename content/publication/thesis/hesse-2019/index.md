---
# Documentation: https://wowchemy.com/docs/managing-content/

title: A NV center based magnetic field stabilization for atomic physics experiments
subtitle: ''
summary: ''
authors:
- hesse
tags:
- NV
- Cold atoms
- Magnetometry
categories: []
date: '2019-11-19'
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
projects: ['nali', 'sopa']
publishDate: '2019-11-19'
publication_types:
- '7'
abstract: 'In atomic physics experiments, setting the magnetic field strength allows one to
create spin dynamics between atoms, or to tune the interaction between them.
This makes stable magnetic fields desirable, but unfortunately no commercially
available sensor can measure magnetic fields past 20 Gauss with high enough
precision to be used in a feedback loop. In this thesis, I present a magnetic field stabilization based on NV centers as a
sensor. The setup is kept compact by moving the data treatment to a RedPitaya’s
FPGA, and few components are needed to build the setup for performing
spectroscopy on the NV center’s Zeeman shift.
The measured magnetic field noise in our setup can be regulated down to 1.1mG
over the control loop bandwidth of 1 kHz, which is about 2.5 times above the
shot noise limit of our sensors. Using a precise frequency source the long term
stability reaches 300 ppb on average over 30 minutes.'
publication: ''
---
