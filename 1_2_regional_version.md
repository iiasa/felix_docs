---
title: "FeliX—R5"
layout: default
parent: Model Overview
nav_order: 2
has_children: true
math: katex
description: the regionalized version of felix
---

# The Regionalized Version of FeliX

A regionalized version of FeliX is highly requested. We break down the world into five regions according to United Nations’ regional classifications (UN, 2024), that is, African States (Africa), Asia-Pacific States (AsiaPacific), Eastern European States (EastEu), Latin American and Caribbean States (LAC), and Western European and other States including the United States, Canada, Australia, and New Zealand (WestEu_Dev). The country list of each region can be found in Appendix [Geographical Classification](2_2_appendix_regional_classification.md). The motivation for choosing five regions was to capture main geographic and socioeconomic differences without extending to the detail of geographically more heterogeneous models. 

The first step is to create a subscript variable (index) Regions with five values according to the regional classification, representing the regional dimension of the FeliX model. As such, key variables, such as population, gross domestic production (GDP) per capita, oil demand, etc., will have an extra dimension after the regionalization. Five modules (Table 1) are fully regionalized in this first version of regionalized FeliX, including population, education, economy, energy, and biodiversity. The water module and land use module are partly regionalized with regionalized water demand by three sectors, and land categories by different purposes, respectively. Others are kept globally. The following sub-sections describe the detailed regionalization procedures according to the aforementioned three main challenges.

{: .note }
>  **The geographical scales of key variables in the regionalized FeliX modules**
>  
|Module |Global|Inter-regional|Intra-regional
|:---|:---|:---|:---|
|Population|||Population dynamics across age and gender; Life expectancy|
|Education|||Enrollment and graduation rates; Labour force|
|Economy|||Capital accumulation; Gross domestic product (GDP)|
|Energy||Trade of fossil fuels|Fossil fuel extraction; Investment; Technology advancements; Energy production; Market shares; Energy demands|
|Diet Change|Diet population shifts; Caloric demand change|||
|Fertilizer Use|Nitrogen and phosphorus cycles; Fertilizer consumption; Yields|||
|Land Use|Land use change; Land demand; Food demand; Agricultural yield||Land supply|
|Biodiversity|||Species abundance dynamics|
|Water|Water balance||Water demand|
|Carbon Cycle|Carbon accumulation and transfer rate in deep ocean||Emissions from fossil fuels|
|Climate|Heat transfer in atmosphere, upper and deep ocean|||

## References
- UN (2024) Regional groups of Member States of United Nations (UN). Accessed in October 2024.