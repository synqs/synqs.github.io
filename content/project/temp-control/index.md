---
title: 'Temperature control'
summary: "Getting all the ovens etc stable."
authors:
- jendrzejewski
- bhatt
- hoecker
- kilinc

lastmod: "2020-12-29T00:00:00Z"
featured: false
draft: false
tags:
- component
- temp control
- flask
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
    url: https://github.com/synqs/DeviceControlServer
---

A flask server that should simplify the logging of our experimental components. Most of the time the components are Arduinos. The website assumes that the Arduinos are connected via ethernet. For the moment we have to following abilities:

- Add a few arduinos.
- Give setpoint and live temperature in overview.
- It shows data in a long list for the moment.
- The setpoint can be changed in the config page.
- The data can be exported to csv.
- PID values can be set from the interface.
