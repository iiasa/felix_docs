---
title: "8. Climate"
layout: default
parent: Global FeliX
nav_order: 8
math: katex
description: the climate section of felix
---

# 8. Climate
The climate module in FeliX is based on the C-ROADS model (Sterman et al., 2012), which in turn refers to FREE model (Fiddaman, 2002) and DICE model (Nordhaus, 1994, 1992). The Earth's radiation budget is constrained to the temperature change due to carbon dioxide ($$CO_2$$), methane ($$CH_4$$), nitrous oxide ($$N_2O$$), halocarbons and other forcings (e.g., aerosols, $$O_3$$, etc.) $$CO_2$$ emissions are endogenous variables as described in [7. Carbon cycle](7_carbon_cycle.md). The rest of forcings are generated exogenously based on historical data and the future projections from Representative Concentration Pathways (RCPs) (Byers et al., 2022). The temperature change is governed by radiative forcings, feedback cooling due to outbound longwave radiation, and heat transfer from the atmosphere and upper ocean to deep ocean layers.

## 8.1 Radiative forcing
Total radiative forcing consists of $$CO_2$$ radiative forcing due to increasing concentration of carbon in atmosphere, and other forcings which includes variables representing forcings from $$CH_4$$, $$N_2O$$, halocarbons and other gases and aerosols.

## 8.2 Feedback cooling
Feedback cooling due to outbound longwave radiation governs feedback mechanism of the atmosphere and the upper ocean. The rate of cooling is determined by the climate sensitivity—a metric used to characterize the response of the global climate system to a given forcing. It is broadly defined as the equilibrium global mean surface temperature change following a doubling of atmospheric $$CO_2$$.

## 8.3 Heat transfer
The heat transfer into deeper layers of the ocean is modeled as a function of the eddy diffusion, which controls the movement of carbon through the deep ocean. FeliX considers four different layers of deep ocean.

## References
- Byers, E., Krey, V., Kriegler, E., Riahi, K., Schaeffer, R., Kikstra, J., Lamboll, R., Nicholls, Z., Sanstad, M., Smith, C., van der Wijst, K.-I., Khourdajie, A.A., Lecocq, F., Portugal-Pereira, J., Saheb, Y., Strømann, A., Winkler, H., Auer, C., Brutschin, E., Gidden, M., Hackstock, P., Harmsen, M., Huppmann, D., Kolp, P., Lepault, C., Lewis, J., Marangoni, G., Müller-Casseres, E., Skeie, R., Werning, M., Calvin, K., Forster, P., Guivarch, C., Hasegawa, T., Meinshausen, M., Peters, G., Rogelj, J., Samset, B., Steinberger, J., Tavoni, M., van Vuuren, D., 2022. AR6 Scenarios Database hosted by IIASA. https://doi.org/doi: 10.5281/zenodo.5886911
- Fiddaman, T.S., 2002. Exploring policy options with a behavioral climate–economy model. System Dynamics Review 18, 243–267. https://doi.org/10.1002/sdr.241
- Nordhaus, W.D., 1994. Managing the global commons. The Economics of Climate Change. MA: MIT Press.
- Nordhaus, W.D., 1992. The ”Dice“ Model: Background and Structure of a Dynamic Integrated Climate-Economy Model of the Economics of Global Warming. Cowles Foundation Discussion Papers 1252.
- Sterman, J., Fiddaman, T., Franck, T., Jones, A., McCauley, S., Rice, P., Sawin, E., Siegel, L., 2012. Climate interactive: the C‐ROADS climate policy model. System Dynamics Review 28, 295–305. https://doi.org/10.1002/sdr.1474

