---
title: 'Pennylane-ls'
subtitle: ''
summary: "Pennylane plugin for labscript."
authors:
- jendrzejewski
# tags:
# - Teaching
lastmod: "2020-12-29T00:00:00Z"
featured: false
draft: false
tags:
- software
- quantum information
- quantum computing
- ultracold atoms
- pennylane
- labscript
- technology
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
  - icon: github
    icon_pack: fab
    name: Code
    url: https://github.com/synqs/pennylane-ls
---

The [pennylane_ls](https://github.com/synqs/pennylane-ls) plugin allows to run experiments that are controlled by the Labscript Suite through the interface and with the features that Pennylane offers. Our general approach is to generate Experiment.py scripts with the Labscript syntax on the fly depending on the circuit provided through PennyLane. This experimental sequence is sent remotely to Labscripts Runmanager and the results are evaluated inside the pennylane_ls plugin.

This repo is based on the plugin template provided by pennylane. An example Pennylane plugin is of ProjectQ. It is well-designed and written by C. Gogolin.

## Features

- Proposes a higher-level control of experiment that are run controlled by the Labscript Suite through PennyLane.
- A framework device that provides a template for labs with Labscript to quickly adapt code for their own setup.
- Includes two devices for the SynQS group at the Kirchhoff-Institute for Physics of Prof. Fred Jendrzejewski.
