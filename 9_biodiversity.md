---
title: "9. Biodiversity"
layout: default
parent: Model Overview
nav_order: 9
math: katex
description: the biodiversity section of felix
---

# 9. Biodiversity
The biodiversity module is a simple structure representing population carrying capacity. The population is represented by global and encompassing all biomes mean species abundance (MSA). MSA is increased by species regeneration rate (Spec_Regen) and decreased by species extinction rate (Spec_Extn). In addition, MSA approaching species carrying capacity (Spec_Capa) limits Spec_Regen and intensifies Spec_Extn. This process is quantified as logistic functions and based on the ratio between MSA and Spec_Capa, and the regeneration factor and the extinction factor, respectively.