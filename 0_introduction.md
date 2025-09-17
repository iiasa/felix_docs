---
title: Introduction
layout: default
nav_order: 2
description: Introduction page for FeliX - Full of Economic-Environment Linkages and Integration dX/dt (FeliX)
math: katex
---

# Introduction

Full of Economic-Environment Linkages and Integration dX/dt (FeliX) is a system dynamics-based integrated assessment model (IAM) that simulates complex interactions among global systems, including population, education, economy, energy, water, land, food, carbon cycle, climate, and biodiversity. FeliX was originally developed for projecting socio-environmental impacts in human-natural systems (Rydzak et al., 2013) and later advanced for exploring emissions pathways (Walsh et al., 2017) and evaluating sustainable diet shifts  (Eker et al., 2019). FeliX is one of the very few models that model human behavior in the human-natural systems considering comprehensive dynamic interactions of socio-economic and environmental sectors. It well addresses the main shortcoming of conventional IAMs  (neglecting feedback perspectives and nonlinear interactions among systems) and covers the breadth of social, economic, and environmental aspects (and their feedback interactions) in one integrated framework. The model operates at an annual timescale and is designed to project global-scale future socioeconomic development and environmental conditions over the long term to 2100. 

This is the full-version documentation of FeliX, including both the global version and a recently regionalized version. This documentation stands alone as a technical documentation of FeliX, and also supports the [scientific publication](https://doi.org/10.1016/j.envsoft.2024.106121) of FeliX.

## Basic information about System Dynamics (SD)
System dynamics (SD) is an interdisciplinary approach to understanding the dynamic behavior of complex systems over time (Meadows and Wright, 2008; Sterman, 2000). Models such as the World3 (Meadows et al., 1972), the Integrated Sustainable Development Goals (Millennium Institute, 2021), and the Earth4All (Dixson-Declève et al., 2022) are all based on SD to simulate how different policies to affect human wellbeing, societies and ecosystems in the short and long term. SD considers the interactions and feedback loops among various components to model and simulate the system's behavior (Figure 1). Feedback loops are a fundamental concept in system dynamics, representing the cause-and-effect relationships within a system. There are two types of feedback loops: reinforcing loops (marked as "+"), which amplify changes and lead to exponential growth or decline, and balancing loops (marked as "-"), which counteract changes and maintain equilibrium.


|[![](images/0_sd_info.png)](images/0_sd_info.png)
|:--|
|Figure 1. Interactions and feedback loops in a simple population system.|

In SD models, four key elements are commonly used: stocks, flows, auxiliary variables, and arrows (Figure 2). 
- Stocks represent accumulations or reserves within the system, such as **Population** in Figure 2. 
- Flows depict the rates of change or transfer between stocks, reflecting processes like *Birth* and *Death* in Figure 2. 
- Auxiliary variables are used to represent various computations, constants, or expressions within the model, like *Birth Fraction* and *Death Fraction* in Figure 2.
- Arrows illustrate the causal connections and feedback loops between stocks, flows and auxiliary variables, aiding in the visualization of the system's structure and dynamics. 

By incorporating these elements, system dynamics provides a powerful tool for analyzing and improving the behavior of complex systems in diverse fields such as business, ecology, and public policy.

|[![](images/0_stocks_flows.png)](images/0_stocks_flows.png)
|:--|
|Figure 2. Key elements used in SD models.|



## FeliX structure and module descriptions
FeliX is a system dynamics model that simulates complex interactions among different global systems: 

1. [Population and education](1_1_1_population_education.md)
2. [Economy](1_1_2_economy.md)
3. [Energy](1_1_3_energy.md)
4. [Water](1_1_4_water.md)
5. [Land use and fertilizer use](1_1_5_land_use_and_fertilizer_use.md)
6. [Diet change](1_1_6_diet_change.md)
7. [Carbon cycle](1_1_7_carbon_cycle.md)
8. [Climate](1_1_8_climate.md)
9. [Biodiversity](1_1_9_biodiversity.md)

The model is developed using the simulation software Vensim. The full functionality of FeliX requires the licensed DSS version of Vensim, whereas it can be displayed freely by using Vensim Model Reader. The user interface of FeliX on Vensim DSS is shown in Figure 3.

|[![](images/vensim_user_interface.png)](images/vensim_user_interface.png)
|:--|
|Figure 3. The user interface of Vensim DSS software.|

The model outcomes are determined by many interacting feedback loops within and between these systems as shown in Figure 4.

|[![](images/overall_structure_felix.png)](images/overall_structure_felix.png)
|:--|
|Figure 4. Overview of the FeliX model. Education shows as a separate component from the population module. The trade module is only for the regionalized version of FeliX. Source: [Moallemi et al. (2022)](https://linkinghub.elsevier.com/retrieve/pii/S2590332222003244).|





## References
- Dixson-Declève, S., Gaffney, O., Ghosh, J., Randers, J., Rockström, J., Stoknes, P.E., 2022. Earth for all: a survival guide for humanity: a report to the Club of Rome (2022), fifty years after The limits to growth (1972). New Society Publishers, Gabriola Island, British Columbia, Canada.
- Eker, S., Reese, G., Obersteiner, M., 2019. Modelling the drivers of a widespread shift to sustainable diets. Nat Sustain 2, 725–735. https://doi.org/10.1038/s41893-019-0331-1
- Meadows, D.H., Meadows, D.L., Randers, J., Behrens III, W.W. (Eds.), 1972. The Limits to growth: a report for the Club of Rome’s project on the predicament of mankind. Universe Books, New York.
- Meadows, D.H., Wright, D., 2008. Thinking in systems: a primer. Chelsea Green Pub, White River Junction, Vt.
- Millennium Institute, 2021. iSDG: Documentation.
- Rydzak, F., Obersteiner, M., Kraxner, F., Fritz, S., McCallum, I., 2013. FeliX3–Impact Assessment Model: Systemic View across Societal Benefit Areas beyond Global Earth Observation. International Institute for Applied Systems Analysis (IIASA), Laxenburg.
- Sterman, J., 2000. Business dynamics: systems thinking and modeling for a complex world. Irwin/McGraw-Hill, Boston.
- Walsh, B., Ciais, P., Janssens, I.A., Peñuelas, J., Riahi, K., Rydzak, F., Van Vuuren, D.P., Obersteiner, M., 2017. Pathways for balancing CO2 emissions and sinks. Nat Commun 8, 14856. https://doi.org/10.1038/ncomms14856
