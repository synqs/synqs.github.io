---
title: Neural quantum states
summary: Using neural networks as efficient quantum state representations

# Short title used in page links (if not set, defaults to title)
title_short: ANN

authors:
- gaerttner
- syrkowski
- reh
- klassert
- epping
- schmale

# Determines ordering of projects
weight: 4

# Optional external URL for project (replaces project detail page).
external_link: ""

tags:
- topics
- ultracold atoms
- quantum mechanics

image:
  caption: ""
  focal_point: Smart

# links:
# - icon: twitter
#   icon_pack: fab
#   name: Follow
#   url: https://twitter.com
# url_code: ""
# url_pdf: ""
# url_slides: ""
# url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

math: true
---

Artificial neural networks have proven extremely successful for machine learning tasks such as computer vision and speech recognition. Specifically, generative models can be trained to approximate probability distributions based on data samples. Quantum states are represented by high-dimensional probability distributions, inviting the use of generative models for finding efficient state representations. We use this approach to develop numerical tools for calculating the time evolution of quantum many-body states and to do quantum state tomography. Furthermore, we exploit, the power of neuromorphic hardware chips which allow the physical emulation of neural networks and thus provide a tool for fast and energy efficient generation of samples from the encoded probability distributions.

